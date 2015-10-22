``` perl
### This template is just a quick example of how to write you own plug-in for get_iplayer
### Once written it can be tested by copying to <profile dir>/plugins/ (e.g. ~/.get_iplayer/plugins/)
### The file must be named as <PROGTYPE>.plugin so that get_iplayer will recognise it (use 'get_iplayer --listplugins' to test it)
### <PROGTYPE> must start with a letter and be lowercase
### All the plugin help text in this file starts with '###'
### This template is just a bunch of example methods stolen from different plugins - it wont work as-is

#    This program is free software: you can redistribute it and/or modify
#    it under the terms of the GNU General Public License as published by
#    the Free Software Foundation, either version 3 of the License, or
#    (at your option) any later version.
#
#    This program is distributed in the hope that it will be useful,
#    but WITHOUT ANY WARRANTY; without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#    GNU General Public License for more details.
#
#    You should have received a copy of the GNU General Public License
#    along with this program.  If not, see <http://www.gnu.org/licenses/>.

################### Podcast class #################
### Substitute PROGTYPE in the rest of this file to be the type of your plugin (e.g. podcast or hulu etc)
package Programme::PROGTYPE;

use Env qw[@PATH];
use Fcntl;
use File::Copy;
use File::Path;
use File::stat;
use HTML::Entities;
use HTTP::Cookies;
use HTTP::Headers;
use IO::Seekable;
use IO::Socket;
use LWP::ConnCache;
use LWP::UserAgent;
use POSIX qw(mkfifo);
use strict;
use Time::Local;
use URI;

# Inherit from Programme class
use base 'Programme';

# Class vars
# Global options
my $opt;


# Constructor
# Usage: $prog{$pid} = Programme->new( 'pid' => $pid, 'name' => $name, <and so on> );
sub new {
	my $type = shift;
	my %params = @_;
	my $self = {};
	for (keys %params) {
		$self->{$_} = $params{$_};
	}
	## Ensure that all instances reference the same class global $optref var
	# $self->{optref} = $Programme::optref;
	# Ensure the subclass $opt var is pointing to the Superclass global optref
	$opt = $Programme::optref;
	bless $self, $type;
}

### Choose a min-max range of programme index numbers currently not used by other plugins
### Required
sub index_min { return 60001 }
sub index_max { return 69999 }

### Keep all you channel listings here if any... (see other plugins for examples)
sub channels { return {}; }


### Add any plugin specific options that you want get_iplayer to display in the help pages in the following format:
### <option name> => [ <1=advance help | 0=normal help>, '<getopt format>', '<Help section>', 'Usage', 'help text'],
### You then refer to the option as $opt->{<option name>}
### The example line below will automatically allow users to specify the output dir for recordings for your PROGTYPE
### Optional
# Class cmdline Options
sub opt_format {
	return {
		outputPROGTYPE	=> [ 1, "outputPROGTYPE=s", 'Output', '--outputPROGTYPE <dir>', "Output directory for PROGTYPE recordings"],
	};
}


# Method to return optional list_entry format
### This defines which programme fields should be displayed AFTER 
### '${prefix}$prog->{index}:\t${prog_type}${name}$prog->{episode}' when 'get_iplayer --type=PROGTYPE' is used
### Optional
sub optional_list_entry_format {
	my $prog = shift;
	return ", $prog->{available}, $prog->{channel}, $prog->{categories}";
}


# Returns the modes to try for this prog type
### Set this to the mode to be used for download - this can be the same as the PROGTYPE if only one type exists
sub modelist {
	return 'podcast';
}


### This method simply (!) gets an XML feed which lists all programme or scrapes a web page that gived overview info for each available programme.
### Once you have the requisite information (you don't need all the fields) then you can create an object which will add it to the cache automatically for you. 
### The example below does 'five' web page scraping but this code will very much depend on how you need to get the info
### Just make sure you use '$progref->{$pid} = Programme::PROGTYPE->new()' to add a new prog object for each programme
### The pid is a unique numeric or alphanumeric identifier used on the website or feed to identify that programme
### The main::request_url_retry method should be used whenever downloading web pages or 
### feeds (search for 'sub request_url_retry ' in the get_iplayer script for usage)
# Usage: Programme::tv->get_links( \%prog, 'five' );
# Uses: %{ channels() }, \%prog
sub get_links {
	shift; # ignore obj ref
	my $progref = shift;
	my $prog_type = shift;
	my %channels = %{ channels() };

	# page scraping here

	my $xml;
	my $feed_data;
	my $res;
	main::logger "INFO: Getting $prog_type Programmes List\n";

	# Setup user agent with redirection enabled and cookie-jar disabled
	# Disable cookie jar (otherwise it saves cookies that prevent further XML downloads for a prog)
	my $ua = main::create_ua( undef, 1 );

	my $baseurl = 'http://demand.five.tv';

	my $url = $baseurl.'/SeriesAZ.aspx';
	$xml = main::request_url_retry($ua, $url, 3, '.', "WARNING: Failed to get series list from from Demand Five site\n");

	# Hash of <name> => <uri>;
	my %names;
	# class="episodeLink" href="Series.aspx?seriesBaseName=HiddenLives">Hidden Lives</a>
	while ( $xml =~ m{class="episodeLink"\s+href="(.+?)">\s*(.+?)</a>}sg ) {
		$names{$2} = "/$1";
		main::logger "DEBUG: Series '$2', URI: /$1\n" if $opt->{debug};
	}

	# Download index feed
	# Sort feeds so that category based feeds are done last - this makes sure that the channels get defined correctly if there are dups
	for my $name ( keys %names ) {

		my $url = $baseurl.$names{$name};
		main::logger "DEBUG: Getting Episodes for $name\n" if $opt->{verbose};
		$xml = main::request_url_retry($ua, $url, 3, '.', "WARNING: Failed to get programme index feed for $_ from Demand Five site\n");
		decode_entities($xml);
		StringUtils::clean_utf8_and_whitespace($xml);

		# <div id="episode4" class="episodesOff">
		# 	<div class="serepisodesdtls">
		# 		<div class="fltlt">
		# 			<a href="javascript:void(0);" class="episodeClose" onclick="toggleEpisode('episode4');">
		# 				<img src="/images/ico_episode_close.gif" alt="View Details" vspace="2" border="0"  title="View Details" />
		# 			</a>
		# 			<a href="javascript:void(0);" class="episodeOpen" onclick="toggleEpisode('episode4');">
		# 				<img src="/images/ico_episode_open.gif" alt="View Details" vspace="2" border="0"  title="View Details" />
		# 			</a>
		# 		</div>
		#		<div class="serepiinfo">
		#			<a href="javascript:void(0);" onclick="toggleEpisode('episode4');">episode 24 :</a> 
		#			<a href="javascript:void(0);" onclick="toggleEpisode('episode4');" class="epititle"> I Want To Cook</a> 
		#			<!-- Parental Guidance REMEMBER TO SET THE ALT AND TITLE FROM DATA -->
		#			<!-- Subtitles image -->
		#			<!-- Schedule -->
		#			<br />
		#			<!-- Ratings image -->
		#			<br />Avg Rating:
		#			<div id="ctl00_MainContent_EpisodeList_EpisodeList_ctl03_AvgRatingStars" class="userRating" itemid="C5116040024">
		#		<img id="ctl00_MainContent_EpisodeList_EpisodeList_ctl03_AvgRatingStars_AvgStars" src="images/avg_star_5.png" style="border-width:0px;" /><span id="ctl00_MainContent_EpisodeList_EpisodeList_ctl03_AvgRatingStars_Count" class="countLabel">(1 vote)</span>
		#	</div>
		#	<!-- FileSize -->
		#	<br />
		#	<div style="float:left;">
		#		11 mins - 60.5 MB
		#	</div>
		#	<!-- Expires image -->
		#	<div id="ctl00_MainContent_EpisodeList_EpisodeList_ctl03_ExpiresVisible" style="float:left;">
		#		<img src="/images/ico_epi_expires.gif" alt="expires" width="14" height="12" hspace="5" />
		#		<span class="expires">Available for another <strong>6</strong> days</span>
		#	</div>
		#</div>
		#</div>
		#<div id="ctl00_MainContent_EpisodeList_EpisodeList_ctl03_divPlayItem">
		#	<div class="serepirent" >
		#	<a href="Episode.aspx?episodeBaseName=C5116040024" class="PlayEpisodeItem" >
		#		<img src="/images/btn_play.gif" alt="rent" border="0" align="top" title="play" />
		#	</a> 
		#</div>
		#</div>
		#<div class="seperator"><img src="/images/seperator.gif" alt="" title="" /></div>
		#<div class="epimoreinfo">
		#	<div class="moreinfort">
		#		<img src="http://content.download.five.tv/bthttp/five/downloadstore/images/LittlePrincess_ESmall.png" alt="episode image"/>	
		#	</div>
		#	<div class="findmore">Little Princess is baking a cake.
		#	<div>
		#		<img src="/images/find_more.gif" alt="find more" width="12" height="12" align="top" title="find more" /> 
		#		<a href="Episode.aspx?episodeBaseName=C5116040024"> find out more</a></div>
		#	</div>
		#</div>
		#</div>

		# Parse XML

		# get list of entries within <entry> </entry> tags
		my @entries = split /<div id="episode\d+"/, $xml;
		# Discard first element == header
		shift @entries;

		main::logger "INFO: Got ".($#entries + 1)." episodes\n" if $opt->{verbose};

		foreach my $entry (@entries) {
			my ( $episode, $desc, $pid, $available, $expiry, $channel, $duration, $thumbnail, $versions, $guidance );

			$entry =~ s/[\r\n]/ /g;
			$entry =~ s/\s+/ /g;

			# main::logger "DEBUG: Entry = $entry\n" if $opt->{debug};

			# PID
			# <a href="Episode.aspx?episodeBaseName=C5116040024">
			$pid = $1 if $entry =~ m{Episode.aspx\?episodeBaseName=(C\d+)"}i;

			# Episode
			## <a href="javascript:void(0);" onclick="toggleEpisode('episode4');">episode 24 :</a>
			# <a href="javascript:void(0);" onclick="toggleEpisode('episode4');" class="epititle"> I Want To Cook</a>
			$episode = $1 if $entry =~ m{class="epititle">\s*(.+?)\s*</a>}i;

			# Available
			# <span class="expires">Available for another <strong>6</strong> days</span>
			$available = $1 if $entry =~ m{<span class="expires">Available for another (.+?)</span>}i;
			$available =~ s|<\/?.+?>||g;

			# Duration
			# <!-- FileSize -->
			# <br />
			# <div style="float:left;">
			#	11 mins - 60.5 MB
			# </div>
			$duration = $1 if $entry =~ m{FileSize\s*-->\s*<b.+?>\s*<div.+?>\s*(.+?)\s*</div>}i;

			# Desc
			# <div class="findmore">Little Princess is baking a cake.
			# <div>
			$desc = $1 if $entry =~ m{<div class="findmore">\s*(.+?)\s*<div>};
			# Remove unwanted html tags and extra whitespace
			$desc =~ s!</?(br|b|i|p|strong)\s*/?>!!gi;
			$desc =~ s/\s+/ /g;

			# <span class="channel">Channel 4</span>
			#$channel =  $1 if $entry =~ m{<span\s+class="channel">\s*(.+?)\s*</span>}i;

			# Merge and Skip if this pid is a duplicate
			if ( defined $progref->{$pid} ) {
				main::logger "WARNING: '$pid, $progref->{$pid}->{name} - $progref->{$pid}->{episode}, $progref->{$pid}->{channel}' already exists (this channel = $channel)\n" if $opt->{verbose};
				next;
			}

			# Thumbnail
			#	<div class="moreinfort">
			#		<img src="http://content.download.five.tv/bthttp/five/downloadstore/images/LittlePrincess_ESmall.png" alt="episode image"/>	
			#	</div>
			$thumbnail = $1 if $entry =~ m{<div class="moreinfort">\s*<img src="(.+?)"};
			main::logger "DEBUG: pid='$pid',name='$name', episode='$episode', duration='$duration', available='${available}'\n" if $opt->{debug};

			# build data structure
			$progref->{$pid} = main::progclass($prog_type)->new(
				'pid'		=> $pid,
				'name'		=> $name,
				'versions'	=> 'default',
				'episode'	=> $episode,
				'desc'		=> $desc,
				'guidance'	=> $guidance,
				'available'	=> $available,
				'duration'	=> $duration,
				'thumbnail'	=> $thumbnail,
				'channel'	=> 'five',
				'categories'	=> 'tv',
				'type'		=> $prog_type,
				'web'		=> "http://demand.five.tv/Episode.aspx?episodeBaseName=${pid}",
			);
		}
	}
	main::logger "\n";
	return 0;
}



### This method is called to get the URL or stream URI to enable get_iplayer to download it. (example from old 'five' plugin)
### The $data{MODE}{streamer} value must refer to one of the Streamer::XXXXX classes in get_iplayer.
### If you need to add a new one best contact the get_iplayer author.
### The stream URL should be in $data{MODE}{streamurl}, other $data{MODE} parameters might need to be set depending on the Stremer class used
### The $data{MODE}{ext} should reflect the filename extension of the finally recorded or streamed file. e.g. 'mp4' or 'mov'
# Gets media streams data for this version pid
sub get_stream_data {
	my ( $prog, undef, $media ) = @_;
	my %data;
	my $entry;

	# Setup user agent with redirection enabled and cookie-jar disabled
	# Disable cookie jar by setting '1' (otherwise it saves cookies that prevent further XML downloads for a prog)
	my $ua = main::create_ua( undef, 1 );
	$opt->{quiet} = 0 if $opt->{streaminfo};

	# Need to add temporary cookie with request of "handlerReferer=<pid>"
	# e.g. Set-Cookie: handlerReferer=C5144920007; path=/; domain=.demand.five.tv;
	$ua->default_header('Cookie' => "handlerReferer=$prog->{pid}; path=/;");
	main::logger "DEBUG: Sending Cookie: Cookie: handlerReferer=$prog->{pid}; path=/;\n" if $opt->{debug};
	# Get XML
	my $prog_metadata_url = 'http://demand.five.tv/Handlers/FlashEpisode.ashx?baseName='; # + <pid>
	$entry = main::request_url_retry($ua, "${prog_metadata_url}$prog->{pid}", 3 );

	decode_entities($entry);
	main::logger "DEBUG: ${prog_metadata_url}$prog->{pid}:\n$entry\n\n" if $opt->{debug};
	# Flatten
	$entry =~ s|[\r\n]||g;

	my $stremuri;

	#   <video>
	#     <![CDATA[rtmpe://streamflv.download.five.tv/a800/o10/mp4:bthttp/five/downloadstore/secure/thegadgetshow/movies/The-Gadget-Show_S11_E7_Episode-7_FLVSTREAM.mp4?e=1241001311&h=62a13cc33a4f88fccbdef4baccc80c41]]>
	# </video>

	$stremuri = $1 if $entry =~ m{\[(rtmpe://.+?)\]};

	# streams
	my $mode = 'flashhigh';
	$data{$mode}{ext} = 'mp4';
	$data{$mode}{streamer} = 'rtmp';

	$data{$mode}{type} = 'Flash RTMPE h264 stream';
	$data{$mode}{streamurl} = $stremuri;
	$data{$mode}{protocol} = 3;
	main::logger "DEBUG: Found $mode: $data{$mode}{type}\n" if $opt->{debug};

	# Return a hash with media => url if '' is specified - otherwise just the specified url
	if ( ! $media ) {
		return %data;
	} else {
		# Make sure this hash exists before we pass it back...
		$data{$media}{exists} = 0 if not defined $data{$media};
		return $data{$media};
	}
}



### Finally, this method is called by get_iplayer when a --get is used (this example is from the old ch4 plugin)
### This is where we check that the required download external progs exist (and fallback to a raw mode if required)
### Get the detailed streamdata using %streamdata = %{ $prog->get_stream_data( undef, '<MODE>') };
### You will need to set the correct $prog->{ext} from $prog->{streams}->{$version}->{$mode}->{ext} (taken from above method)
### The filename generation can be tweaked using the usual <fields> when calling $prog->generate_filenames
### Best keep the test step in there
### Create the streamer instance
### The final return $stream->get( $ua, $prog->{pid}, $prog ) calls the streamer/recorder with all your data
sub download {
	my ( $prog, $ua, $mode, $version, $version_pid ) = ( @_ );
	my %streamdata;

	# if subsonly required then skip
	return 'skip' if $opt->{subsonly};

	# if rtmpdump does not exist
	if ( $mode =~ /^(rtmp|flash)/ && ! main::exists_in_path('rtmpdump')) {
		main::logger "WARNING: Required program rtmpdump does not exist\n";
		return 'next';
	}
	# Force raw mode if ffmpeg is not installed
	if ( $mode =~ /^(flash|rtmp)/ && ! main::exists_in_path('ffmpeg')) {
		main::logger "\nWARNING: ffmpeg does not exist - not converting flv file\n";
		$opt->{raw} = 1;
	}

	%streamdata = %{ $prog->get_stream_data( undef, 'flashnormal') };

	# Get extension from streamdata if defined and raw not specified
	$prog->{ext} = $prog->{streams}->{$version}->{$mode}->{ext};
	$prog->{ext} = 'flv' if $opt->{raw};
	
	my $url = $prog->{streams}->{$version}->{$mode}->{streamurl};

	if ( not $url ) {
		main::logger "WARNING: No programme stream URL was found, skipping\n";
		return 'skip';
	}
	
	# Determine the correct filenames for this recording
	return 'skip' if $prog->generate_filenames( $ua, "<name> <episode> <pid>" );

	# Skip from here if we are only testing recording
	return 'skip' if $opt->{test};

	# Instantiate new streamer from streamdata
	my $class = "Streamer::$prog->{streams}->{$version}->{$mode}->{streamer}";
	my $stream = $class->new;

	# Do the recording
	return $stream->get( $ua, $prog->{streams}->{$version}->{$mode}->{streamurl}, $prog, %{ $prog->{streams}->{$version}->{$mode} } );
}

1;
```