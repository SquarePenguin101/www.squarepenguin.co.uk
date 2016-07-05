## get_iplayer Options

# Table of Contents

* [Search Options](#search-options)

* [Display Options](#display-options)

* [Recording Options](#recording-options)

* [Output Options](#output-options)

* [PVR Options](#pvr-options)

* [Config Options](#config-options)

* [External Program Options](#external-program-options)

* [Tagging Options](#tagging-options)

* [Misc Options](#misc-options)

* [Deprecated Options](#deprecated-options)

<a id="search-options"></a>

## Search Options

|Options file|Command line|Description
|------------|------------|-----------
|availablesince|--available-since &lt;hours&gt;|Limit search to programmes that have become available in the last N hours
|before|--before &lt;hours&gt;|Limit search to programmes added to the cache before N hours ago
|channel|--channel &lt;string&gt;|Narrow search to matched channel(s) (regex or comma separated values)
|exclude|--exclude &lt;string&gt;|Narrow search to exclude matched programme names (regex or comma separated values)
|excludechannel|--exclude-channel &lt;string&gt;|Narrow search to exclude matched channel(s) (regex or comma separated values)
|expiresbefore|--expires-before &lt;hours&gt;|Limit search to programmes that will expire in the next N hours
|fields|--fields &lt;field1&gt;,&lt;field2&gt;,...|Searches only in the specified comma separated fields
|future|--future|Additionally search future programme schedule if it has been indexed (refresh cache with: --refresh --refresh-future).
|history|--history|Search/show recordings history
|long|--long, -l|Additionally search in programme descriptions and episode names (same as --fields=name,episode,desc )
|search|--search &lt;search term&gt;|GetOpt compliant way of specifying search args
|since|--since &lt;hours&gt;|Limit search to programmes added to the cache in the last N hours
|type|--type &lt;type&gt;|Only search in these types of programmes: liveradio,livetv,localfiles,podcast,radio,tv,all (tv is default)

<a id="display-options"></a>

## Display Options

|Options file|Command line|Description
|------------|------------|-----------
|conditions|--conditions|Shows GPLv3 conditions
|debug|--debug|Debug output
|dumpoptions|--dump-options|Dumps all options with their internal option key names
|help|--help, -h|Intermediate help text
|helpbasic|--helpbasic, --usage|Basic help text
|helplong|--helplong|Advanced help text
|hide|--hide|Hide previously recorded programmes
|info|--info, -i|Show full programme metadata and availability of modes and subtitles (max 40 matches)
|listformat|--listformat &lt;format&gt;|Display programme data based on a user-defined format string (such as &lt;pid&gt;, &lt;name&gt; etc)
|long|--long, -l|Show long programme info
|manpage|--manpage &lt;file&gt;|Create man page based on current help text
|nocopyright|--nocopyright|Don&#39;t display copyright header
|page|--page &lt;number&gt;|Page number to display for multipage output
|pagesize|--pagesize &lt;number&gt;|Number of matches displayed on a page for multipage output
|quiet|--quiet, -q|Reduce logging output
|showcacheage|--show-cache-age|Displays the age of the selected programme caches then exit
|showoptions|--show-options|Shows options which are set and where they are defined
|showver|-V|Show get_iplayer version and exit.
|silent|--silent|No logging output except PVR download report.  Cannot be saved in preferences or PVR searches.
|sortmatches|--sort &lt;fieldname&gt;|Field to use to sort displayed matches
|sortreverse|--sortreverse|Reverse order of sorted matches
|streaminfo|--streaminfo|Returns all of the media stream urls of the programme(s)
|verbose|--verbose, -v|Verbose
|warranty|--warranty|Displays warranty section of GPLv3

<a id="recording-options"></a>

## Recording Options

|Options file|Command line|Description
|------------|------------|-----------
|attempts|--attempts &lt;number&gt;|Number of attempts to make or resume a failed connection.  --attempts is applied per-stream, per-mode.  TV modes typically have two streams available.
|excludesupplier|--exclude-supplier &lt;suppliers&gt;|Comma-delimited list of media stream suppliers to skip.  Possible values: level3,akamai,limelight,bidi
|force|--force|Ignore programme history (unsets --hide option also). Forces a script update if used with -u
|get|--get, -g|Start recording matching programmes. Search terms required unless --pid specified. Use  --search=.* to force download of all available programmes.
|hash|--hash|Show recording progress as hashes
|includesupplier|--include-supplier &lt;suppliers&gt;|Comma-delimited list of media stream suppliers to use if not included by default.  Possible values: level3,akamai,limelight,bidi
|metadataonly|--metadata-only|Create specified metadata info file without any recording or streaming (can also be used with thumbnail option).
|modes|--modes &lt;mode&gt;,&lt;mode&gt;,...|Recording modes.  See --tvmode and --radiomode (with --long-help) for available modes and defaults. Shortcuts: worst,worse,good,better,best
|noproxy|--no-proxy|Ignore --proxy setting in preferences
|overwrite|--overwrite|Overwrite recordings if they already exist
|partialproxy|--partial-proxy|Only uses web proxy where absolutely required (try this extra option if your proxy fails). If specified, value of http_proxy environment variable (if any) in parent process is retained and passed to child processes.
|pid|--pid &lt;pid&gt;|Record an arbitrary PID that does not necessarily appear in the index.
|pidrecursive|--pid-recursive|Record all related episodes if value of --pid is a series or brand PID. Requires --pid.
|pidrecursivenoclips|--pid-recursive-noclips|When used with --pid and --pid-recursive, skip all associated programme clips if the value of --pid is a brand PID. Requires --pid and --pid-recursive.
|proxy|--proxy, -p &lt;url&gt;|Web proxy URL e.g. &#39;http://USERNAME:PASSWORD@SERVER:PORT&#39; or &#39;http://SERVER:PORT&#39;. Sets http_proxy environment variable for child processes (e.g., ffmpeg) unless --partial-proxy is specified.
|radiomode|--radiomode &lt;mode&gt;,&lt;mode&gt;,...|Radio recording modes (overrides --modes): dashhigh,dashstd,dashmed,dashlow,flashhigh,flashstd,flashlow,hlshigh,hlsstd,hlsmed,hlslow. Shortcuts: worst,worse,good,better,best,dash,flash,hls. (default=hlshigh,dashhigh,hlsstd,dashstd,hlsmed,dashmed,hlslow,dashlow)
|raw|--raw|Don&#39;t transcode or change the recording/stream in any way (i.e. RTMP-&gt;FLV, HLS-&gt;MPEG-TS)
|start|--start &lt;secs&#124;hh:mm:ss&gt;|Recording/streaming start offset
|stop|--stop &lt;secs&#124;hh:mm:ss&gt;|Recording/streaming stop offset
|suboffset|--suboffset &lt;offset&gt;|Offset the subtitle timestamps by the specified number of milliseconds
|subsfmt|--subsfmt &lt;format&gt;|Subtitles format.  One of: default, compact.  Default: &#39;default&#39;
|subsonly|--subtitles-only|Only download the subtitles, not the programme
|subsraw|--subsraw|Additionally save the raw subtitles file
|subsrequired|--subtitles-required|Do not download TV programme if subtitles are not available.
|subtitles|--subtitles|Download subtitles into srt/SubRip format if available and supported
|tagonly|--tag-only|Only update the programme metadata tag and not download the programme (can also be used with --history)
|tagonlyfilename|--tag-only-filename &lt;filename&gt;|Add metadata tags to specified file (ignored unless used with --tag-only)
|test|--test, -t|Test only - no recording (will show programme type)
|thumb|--thumb|Download Thumbnail image if available
|thumbonly|--thumbnail-only|Only Download Thumbnail image if available, not the programme
|tvmode|--tvmode &lt;mode&gt;,&lt;mode&gt;,...|TV recording modes (overrides --modes): flashhd,flashvhigh,flashhigh,flashstd,flashnormal,flashlow,hlshd,hlsvhigh,hlshigh,hlsstd,hlslow,flashlow,hvfhd,hvfsd,hvfvhigh,hvfhigh,hvfstd,hvflow. Shortcuts: worst,worse,good,better,best,flash,hls,hvf. (default=hlshd,hlsvhigh,hlshigh,hlsstd,hlslow)
|url|--url &quot;&lt;url&gt;&quot;|Record the embedded media player in the specified URL. Use with --type=&lt;type&gt;.
|versionlist|--versions &lt;versions&gt;|Version of programme to record. List is processed from left to right and first version found is downloaded. Example: &#39;--versions=audiodescribed,default&#39; will prefer audiodescribed programmes if available.

<a id="output-options"></a>

## Output Options

|Options file|Command line|Description
|------------|------------|-----------
|command|--command, -c &lt;command&gt;|Run user command after successful recording using args such as &lt;pid&gt;, &lt;name&gt; etc
|fileprefix|--file-prefix &lt;format&gt;|The filename prefix (excluding dir and extension) using formatting fields. e.g. &#39;&lt;name&gt;-&lt;episode&gt;-&lt;pid&gt;&#39;
|metadata|--metadata &lt;type&gt;|Create metadata info file after recording. Valid types are: xbmc (or kodi), xbmc_movie (or kodi_movie), freevo, generic
|output|--output, -o &lt;dir&gt;|Recording output directory
|outputradio|--outputradio &lt;dir&gt;|Output directory for radio recordings (overrides --output)
|outputtv|--outputtv &lt;dir&gt;|Output directory for tv recordings (overrides --output)
|subdir|--subdir, -s|Put Recorded files into Programme name subdirectory
|subdirformat|--subdir-format &lt;format&gt;|The format to be used for the subdirectory naming using formatting fields. e.g. &#39;&lt;nameshort&gt;-&lt;seriesnum&gt;&#39;
|thumbsize|--thumbsize &lt;index&#124;width&gt;|Default thumbnail size/index to use for the current recording and metadata. index: 1-11 or width: 86,150,178,512,528,640,832,1024,1280,1600,1920
|thumbsizecache|--thumbsizecache &lt;index&#124;width&gt;|Default thumbnail size/index to use when building cache. index: 1-11 or width: 86,150,178,512,528,640,832,1024,1280,1600,1920
|whitespace|--whitespace, -w|Keep whitespace in file and directory names. Default behaviour is to replace whitespace with underscores.

<a id="pvr-options"></a>

## PVR Options

|Options file|Command line|Description
|------------|------------|-----------
|comment|--comment &lt;string&gt;|Adds a comment to a PVR search
|pvr|--pvr [pvr search name]|Runs the PVR using all saved PVR searches (intended to be run every hour from cron etc). The list can be limited by adding a regex to the command. Synonyms: --pvrrun, --pvr-run
|pvradd|--pvr-add &lt;search name&gt;|Save the named PVR search with the specified search terms.  Search terms required. Use --search=.* to force download of all available programmes. Synonyms: --pvradd
|pvrdel|--pvr-del &lt;search name&gt;|Remove the named search from the PVR searches. Synonyms: --pvrdel
|pvrdisable|--pvr-disable &lt;search name&gt;|Disable (not delete) a named PVR search. Synonyms: --pvrdisable
|pvrenable|--pvr-enable &lt;search name&gt;|Enable a previously disabled named PVR search. Synonyms: --pvrenable
|pvrexclude|--pvr-exclude &lt;string&gt;|Exclude the PVR searches to run by search name (regex or comma separated values). Synonyms: --pvrexclude
|pvrlist|--pvr-list|Show the PVR search list. Synonyms: --pvrlist
|pvrqueue|--pvr-queue|Add currently matched programmes to queue for later one-off recording using the --pvr option. Search terms required unless --pid specified. Synonyms: --pvrqueue
|pvrscheduler|--pvr-scheduler &lt;seconds&gt;|Runs the PVR using all saved PVR searches every &lt;seconds&gt;. Synonyms: --pvrscheduler
|pvrsingle|--pvr-single &lt;search name&gt;|Runs a named PVR search. Synonyms: --pvrsingle

<a id="config-options"></a>

## Config Options

|Options file|Command line|Description
|------------|------------|-----------
|cachereset|--cache-reset|Reset cache to retain only latest update and discard previous contents.
|expiry|--expiry, -e &lt;secs&gt;|Cache expiry in seconds (default 4hrs)
|limitmatches|--limit-matches &lt;number&gt;|Limits the number of matching results for any search (and for every PVR search)
|nopurge|--nopurge|Don&#39;t ask to delete programmes recorded over 30 days ago
|prefsadd|--prefs-add|Add/Change specified saved user or preset options
|prefsclear|--prefs-clear|Remove *ALL* saved user or preset options
|prefsdel|--prefs-del|Remove specified saved user or preset options
|prefsshow|--prefs-show|Show saved user or preset options
|preset|--preset, -z &lt;name&gt;|Use specified user options preset
|presetlist|--preset-list|Show all valid presets
|profiledir|--profile-dir &lt;dir&gt;|Override the user profile directory/folder
|refresh|--refresh, --flush, -f|Refresh cache
|refreshexclude|--refresh-exclude &lt;string&gt;|Exclude matched channel(s) when refreshing cache (regex or comma separated values). Overrides --refresh-include-groups[-{tv,radio}] status for specified channel(s)
|refreshexcludegroups|--refresh-exclude-groups|Exclude channel groups when refreshing radio or tv cache (comma-separated values).  Valid values: &#39;national&#39;, &#39;regional&#39;, &#39;local&#39;
|refreshexcludegroupsradio|--refresh-exclude-groups-radio|Exclude channel groups when refreshing radio cache (comma-separated values).  Valid values: &#39;national&#39;, &#39;regional&#39;, &#39;local&#39;
|refreshexcludegroupstv|--refresh-exclude-groups-tv|Exclude channel groups when refreshing tv cache (comma-separated values).  Valid values: &#39;national&#39;, &#39;regional&#39;, &#39;local&#39;
|refreshfuture|--refresh-future|Obtain future programme schedule when refreshing cache
|refreshinclude|--refresh-include &lt;string&gt;|Include matched channel(s) when refreshing cache (regex or comma separated values). Overrides --refresh-exclude-groups[-{tv,radio}] status for specified channel(s)
|refreshincludegroups|--refresh-include-groups|Include channel groups when refreshing radio or tv cache (comma-separated values).  Valid values: &#39;national&#39;, &#39;regional&#39;, &#39;local&#39;
|refreshincludegroupsradio|--refresh-include-groups-radio|Include channel groups when refreshing radio cache (comma-separated values).  Valid values: &#39;national&#39;, &#39;regional&#39;, &#39;local&#39;
|refreshincludegroupstv|--refresh-include-groups-tv|Include channel groups when refreshing tv cache (comma-separated values).  Valid values: &#39;national&#39;, &#39;regional&#39;, &#39;local&#39;
|skipdeleted|--skipdeleted|Skip the download of metadata/thumbs/subs if the media file no longer exists. Use with --history &amp; --metadataonly/subsonly/thumbonly.
|webrequest|--webrequest &lt;urlencoded string&gt;|Specify all options as a urlencoded string of &quot;name=val&amp;name=val&amp;...&quot;

<a id="external-program-options"></a>

## External Program Options

|Options file|Command line|Description
|------------|------------|-----------
|atomicparsley|--atomicparsley &lt;path&gt;|Location of AtomicParsley binary
|ffmpeg|--ffmpeg &lt;path&gt;|Location of ffmpeg or avconv binary. Synonyms: --avconv
|ffmpegobsolete|--ffmpeg-obsolete|Indicates you are using an obsolete version of ffmpeg (&lt;0.7) that does not support the -loglevel option, so  --quiet, --verbose and --debug will not be applied to ffmpeg. Synonym: --avconv-obsolete

<a id="tagging-options"></a>

## Tagging Options

|Options file|Command line|Description
|------------|------------|-----------
|noartwork|--no-artwork|Do not embed thumbnail image in output file. Also removes existing artwork. All other metadata values will be written.
|notag|--no-tag|Do not tag downloaded programmes
|tag_formatshow|--tag-format-show|Format template for programme name in metadata (use substitution parameters). Default: none
|tag_formattitle|--tag-format-title|Format template for episode title in metadata (use substitution parameters). Default: none
|tag_isodate|--tag-isodate|Use ISO8601 dates (YYYY-MM-DD) in album/show names and track titles
|tag_podcast|--tag-podcast|Tag downloaded radio and tv programmes as iTunes podcasts (requires MP3::Tag module for AAC/MP3 files)
|tag_podcast_radio|--tag-podcast-radio|Tag only downloaded radio programmes as iTunes podcasts (requires MP3::Tag module for AAC/MP3 files)
|tag_podcast_tv|--tag-podcast-tv|Tag only downloaded tv programmes as iTunes podcasts
|tag_utf8|--tag-utf8|Use UTF-8 encoding for non-ASCII characters in AtomicParsley parameter values (Linux/Unix/OS X only). Use only if auto-detect fails.

<a id="misc-options"></a>

## Misc Options

|Options file|Command line|Description
|------------|------------|-----------
|encodingconsolein|--encoding-console-in &lt;name&gt;|Character encoding for standard input (currently unused). Encoding name must be known to Perl Encode module. Default (only if auto-detect fails): Linux/Unix/OSX = UTF-8, Windows = cp850
|encodingconsoleout|--encoding-console-out &lt;name&gt;|Character encoding used to encode search results and other output. Encoding name must be known to Perl Encode module. Default (only if auto-detect fails): Linux/Unix/OSX = UTF-8, Windows = cp850
|encodinglocale|--encoding-locale &lt;name&gt;|Character encoding used to decode command-line arguments. Encoding name must be known to Perl Encode module. Default (only if auto-detect fails): Linux/Unix/OSX = UTF-8, Windows = cp1252
|encodinglocalefs|--encoding-locale-fs &lt;name&gt;|Character encoding used to encode file and directory names. Encoding name must be known to Perl Encode module. Default (only if auto-detect fails): Linux/Unix/OSX = UTF-8, Windows = cp1252
|indexconcurrent|--index-concurrent|Perform fork()-based concurrent (i.e., faster) indexing when web scraping TV schedules only. Requires --ybbcy and Parallel::ForkManager Perl module. Not supported on Windows.
|indexmaxconn|--index-maxconn &lt;number&gt;|Maximum number of forks (connections) to use for concurrent indexing. Requires --index-concurrent. Default: 4 Max: 10
|noscrapeversions|--no-scrape-versions|Do not scrape episode web pages as extra measure to find audiodescribed/signed versions.
|trimhistory|--trim-history &lt;# days to retain| Remove download history entries older than number of days specified in option value.  Cannot specify 0 - use &#39;all&#39; to completely delete download history
|ybbcy|--ybbcy|Use alternate programme indexing and metadata retrieval if the BBC removes its XML data sources. TV programme indexing will be extremely slow. Some metadata will be missing or incorrect.

<a id="deprecated-options"></a>

## Deprecated Options

|Options file|Command line|Description
|------------|------------|-----------
|aactomp3|--aactomp3|Transcode AAC audio to MP3 with ffmpeg/avconv (CBR 128k unless --mp3vbr is specified).  Applied only to radio programmes. (Synonyms: --mp3)
|avi|--avi|Output video in AVI container instead of MP4. There is no metadata tagging support for AVI output.
|category|--category &lt;string&gt;|Narrow search to matched categories (regex or comma separated values). Supported only for podcasts (not tv or radio programmes).
|checkduration|--check-duration|Print message showing recorded duration, expected duration and difference between them. Ignored when recording live streams.
|email|--email &lt;address&gt;|Email HTML index of matching programmes to specified address
|emailpassword|--email-password &lt;password&gt;|Email password
|emailport|--email-port &lt;port number&gt;|Email port number (default: appropriate port for --email-security)
|emailsecurity|--email-security &lt;TLS&#124;SSL&gt;|Email security TLS, SSL (default: none)
|emailsender|--email-sender &lt;address&gt;|Optional email sender address
|emailsmtp|--email-smtp &lt;hostname&gt;|SMTP server IP address to use to send email (default: localhost)
|emailuser|--email-user &lt;username&gt;|Email username
|excludecategory|--exclude-category &lt;string&gt;|Narrow search to exclude matched categories (regex or comma separated values). Supported only for podcasts (not tv or radio programmes).
|fatfilename|--fatfilename|Remove FAT forbidden characters in file and directory names.  Always applied on Windows. Overrides --punctuation.
|ffmpegliveradioopts|--ffmpeg-liveradio-opts &lt;options| Add custom options to ffmpeg re-muxing for liveradio
|ffmpeglivetvopts|--ffmpeg-livetv-opts &lt;options&gt;|Add custom options to ffmpeg re-muxing for livetv
|ffmpegradioopts|--ffmpeg-radio-opts &lt;options&gt;|Add custom options to ffmpeg re-muxing for radio
|ffmpegtvopts|--ffmpeg-tv-opts &lt;options&gt;|Add custom options to ffmpeg re-muxing for tv
|fxd|--fxd &lt;file&gt;|Create Freevo FXD XML of matching programmes in specified file
|hfsfilename|--hfsfilename|Remove colons in file and directory names. Prevents OS X Finder displaying colon as forward slash. Always applied on OS X. Overrides --punctuation.
|hlsffmpeg|--hls-ffmpeg|Use ffmpeg/avconv instead of built-in HLS downloader. Ignored for downloading on-demand radio programmes, which use DASH downloader. 320k on-demand radio programmes cannot be streamed with --hls-ffmpeg.
|hlsffmpegencode|--hls-ffmpeg-encode|Make ffmpeg HLS downloader re-encode streams. For avconv and old versions of ffmpeg (&lt;2.5). May record slower than real time and may not be able to stream higher-quality media.
|hlsliveradioopts|--hls-liveradio-opts &lt;options&gt;|Add custom options to ffmpeg HLS download re-muxing for liveradio
|hlslivetvopts|--hls-livetv-opts &lt;options&gt;|Add custom options to ffmpeg HLS download encoding for livetv
|hlsradioopts|--hls-radio-opts &lt;options&gt;|Add custom options to ffmpeg HLS download re-muxing for radio
|hlstvopts|--hls-tv-opts &lt;options&gt;|Add custom options to ffmpeg HLS download re-muxing for tv
|html|--html &lt;file&gt;|Create basic HTML index of matching programmes in specified file
|id3v2|--id3v2 &lt;path&gt;|Location of id3v2 or id3tag binary
|isodate|--isodate|Use ISO8601 dates (YYYY-MM-DD) in filenames and subdirectory paths. Default: true
|keepall|--keep-all|Keep whitespace, all possible punctuation and non-ASCII characters in file and directory names. Shortcut for: --whitespace --non-ascii --punctuation.
|list|--list &lt;categories&#124;channel&gt;|Show a list of available categories/channels for the selected type and exit
|listplugins|--listplugins|Display a list of currently available plugins or programme types
|liveradiointl|--liveradio-intl|Force use of hard-coded international streams for HLS live radio.  Ignored for World Service
|liveradiomode|--liveradiomode &lt;mode&gt;,&lt;mode&gt;,...|Live Radio recording modes (overrides --modes): hlshigh,hlsstd,hlsmed,hlslow,shoutcastmp3std,shoutcastaachigh (R3 only, UK only). Shortcuts: worst,worse,good,better,best,hls,shoutcast. (default=hlshigh,hlsstd,hlsmed,hlslow)
|liveradiouk|--liveradio-uk|Force use of hard-coded UK streams for HLS live radio (overrides --liveradio-intl). Ignored for World Service
|livetvmode|--livetvmode &lt;mode&gt;,&lt;mode&gt;,...|Live TV recording modes (overrides --modes): hvfhd,hvfsd,hvfvhigh,hvfhigh,hvfstd,hvflow. Shortcuts: worst,worse,good,better,best,hvf. (default=hvfhd,hvfsd,hvfvhigh,hvfhigh,hvfstd,hvflow)
|localfilesdirs|--localfilesdirs &lt;dir&gt;[,dir,]|Directories/Folders to scan for new files
|mediaselector|--mediaselector &lt;identifier&gt;|Identifier of mediaselector API to use when searching for media streams. One of: 4,5 Default: 5
|mkv|--mkv|Output video in MKV container instead of MP4. There is no metadata tagging support for MKV output.
|mp3vbr|--mp3vbr|Set LAME VBR mode to N (0 to 9) for AAC transcoding. 0 = target bitrate 245 Kbit/s, 9 = target bitrate 65 Kbit/s (requires --aactomp3). Applied only to radio programmes.
|multimode|--multimode|Allow the recording of more than one mode for the same programme - WARNING: will record all specified/default modes!!
|mythtv|--mythtv &lt;file&gt;|Create Mythtv streams XML of matching programmes in specified file
|nonascii|--non-ascii, --na|Keep non-ASCII characters in file and directory names. Default behaviour is to remove all non-ASCII characters.
|nowrite|--nowrite, -n|No writing of file to disk (use with -x to prevent a copy being stored on disk)
|outputliveradio|--outputliveradio &lt;dir&gt;|Output directory for live radio recordings (overrides --output)
|outputlivetv|--outputlivetv &lt;dir&gt;|Output directory for live tv recordings (overrides --output)
|outputlocalfiles|--outputlocalfiles &lt;dir&gt;|Output directory for localfiles recordings (overrides --output)
|outputpodcast|--outputpodcast &lt;dir&gt;|Output directory for podcast recordings (overrides --output)
|player|--player &#39;&lt;command&gt; &lt;options&gt;&#39;|Use specified command to directly play the stream
|punctuation|--punctuation, --pu|Keep punctuation characters and symbols in file and directory names, with ellipsis always replaced by underscore. Default behaviour is to remove all punctuation and symbols except underscore, hyphen and full stop. Overridden by --fatfilename and --hfsfilename.
|refreshabortonerror|--refresh-abortonerror|Abort cache refresh for programme type if data for any channel fails to download. Use --refresh-exclude to temporarily skip failing channels.
|refreshlimit|--refresh-limit &lt;days&gt;|Minimum number of days of programmes to cache (max: 30)
|refreshlimitradio|--refresh-limit-radio &lt;integer&gt;|Number of days of radio programmes to cache. Makes cache updates VERY slow. Default: 7 Min: 1 Max: 30
|refreshlimittv|--refresh-limit-tv &lt;days&gt;|Number of days of TV programmes to cache. Makes cache updates VERY slow. Default: 7 Min: 1 Max: 30
|rtmpdump|--rtmpdump &lt;path&gt;|Location of rtmpdump binary. Synonyms: --flvstreamer
|rtmpport|--rtmpport &lt;port&gt;|Override the RTMP port (e.g. 443)
|rtmpradioopts|--rtmp-radio-opts &lt;options&gt;|Add custom options to rtmpdump for radio
|rtmptvopts|--rtmp-tv-opts &lt;options&gt;|Add custom options to rtmpdump for tv
|series|--series|Display programme series names only with number of episodes
|shoutcastliveradioopts|--shoutcast-liveradio-opts &lt;opti|ns&gt; Add custom options to ffmpeg Shoutcast download re-muxing for liveradio
|stdout|--stdout, -x|Additionally stream to STDOUT (so you can pipe output to a player)
|stream|--stream|Stream to STDOUT (so you can pipe output to a player)
|swfurl|--swfurl &lt;URL&gt;|URL of Flash player used by rtmpdump for verification.  Only use if default Flash player URL is not working.
|symlink|--symlink &lt;file&gt;|Create symlink to &lt;file&gt; once we have the header of the recording
|tag_cnid|--tag-cnid|Use AtomicParsley --cnID argument (if supported) to add catalog ID used for combining HD and SD versions in iTunes
|tag_fulltitle|--tag-fulltitle|Prepend album/show title to track title
|tag_hdvideo|--tag-hdvideo|AtomicParsley accepts --hdvideo argument for HD video flag
|tag_id3sync|--tag-id3sync|Save ID3 tags for MP3 files in synchronised form. Provides workaround for corruption of thumbnail images in Windows. Has no effect unless using MP3::Tag Perl module.
|tag_longdesc|--tag-longdesc|AtomicParsley accepts --longdesc argument for long description text
|tag_longdescription|--tag-longdescription|AtomicParsley accepts --longDescription argument for long description text
|tag_longepisode|--tag-longepisode|Use &lt;episode&gt; (incl. episode number) instead of &lt;episodeshort&gt; for track title
|tag_longtitle|--tag-longtitle|Prepend &lt;series&gt; (if available) to track title. Ignored with --tag-fulltitle.
|tag_shortname|--tag-shortname|Use &lt;nameshort&gt; instead of &lt;name&gt; for album/show title
|terse|--terse|Only show terse programme info (does not affect searching)
|thumbext|--thumb-ext &lt;ext&gt;|Thumbnail filename extension to use
|tree|--tree|Display Programme listings in a tree view
|xmlalpha|--xml-alpha|Create freevo/Mythtv menu sorted alphabetically by programme name
|xmlchannels|--xml-channels|Create freevo/Mythtv menu of channels -&gt; programme names -&gt; episodes
|xmlnames|--xml-names|Create freevo/Mythtv menu of programme names -&gt; episodes
