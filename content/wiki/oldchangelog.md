get_iplayer changelog (OLD)
---------------------------
**(document from original developer)**

**NOTE**: This change log ends at the point get_iplayer was abandoned by its original developer.
It is made available solely for historical reference.

Version 2.75 - 20100307
* Fixed bug where symlinks could be created when streaming-only.

Version 2.74 - 20100307
* Fixed regression from 2.74 in failing to make dir for non-existant output dir.

Version 2.73 - 20100307
* Fix typo in --refreshfuture option.
* Only create output and/or subdir when actually required - fixes bug where subdir was created when streaming-only.
* Removed incorrect entity decoding of iPlayer RDF.
* Remove some deprecated options and tidied help a little.
* Removed support for flvstreamer prior to v1.8.

Version 2.72 - 20100226
* Skip subtitles download if the file already exists.
* Only rename the partial subtitle file after the whole stream is recorded  successfully.

Version 2.71 - 20100225
* Added modeshort substitution parameter which is the same as mode but without the trailing digit.
* Make sure that any fileprefix that specifies mode doesn't use the trailing digit to prevent duplicate recordings in some cases.
* Sort by connection priority in mode numbering.
* Improve user agent function.

Version 2.70 - 20100225
* Added a new XML connection media detection for audio/mp3 for flashaudio mode.

Version 2.69 - 20100225
* Added BBC Radio Sussex into local radio lists.
* Fixed regression bug where URLs would not get recorded if XML::Simple was available.
* Improved error detection for bad rdf URLs.

Version 2.68 - 20100222
* Added ability to filter which PVR searches get run by '--pvr [<regex>]'
* Added ability to exclude matching PVR searches by name using --pvr-exclude=<regex>
* Fixed listing of embedded pids in a brand page that don't have a series.

Version 2.67 - 20100219
* Fixed iphone mode since BBC have recently removed the stream data from the public mediaselector XML metadata.
* If --pid is used with series or brand pids/urls will now list record all contained episodes.
* if --pid-recursive is used with the above it will record all the contained brand/series episodes.
* The above feature requires XML::Simple perl module
* Search now applies to the concatenated fields as opposed to each field individually,

Version 2.66 - 20100123
* Added episodenum and seriesnum to history.
* Fixed a bug where if an invalid option was detected, output would revert to STDERR.

Version 2.65 - 20100121
* Fixed -V to display version even when --nocopyright or --silent is set.
* Added ability to get iPlayer programme metadata and thumbs even if a programme is unavailable.
* The use of --metadataonly, --subsonly or --thumbonly options will now prevent a recording when used with --pid.
* Overhauled the method of getting metadata, subs and thumbnails for existing programmes in the history.
* It will now create metadata files, subs and thumbs matching the prefix of the originally recorded file.
* e.g. 'get_iplayer --history --metadataonly --subsonly --metadata=generic --thumbonly <search of history>'
* Or, 'get_iplayer --history --metadataonly --subsonly --metadata=generic --thumbonly --pid <pid in history>'
* Added --skipdeleted to skip matches if the media file has been deleted when in --history mode.
* Metadata/thumbs/subs for previously recorded programmes will now use the historical fileprefix, dir and ext (use with --history).

Version 2.64 - 20100119
* Added ability to negate boolean options by prefixing with 'no-' e.g. --no-raw
* Fixed buglet where invalid options resulted in an empty option being created.

Version 2.63 - 20100118
* Fixed --exclude option so that it now applies to all search fields specified using --fields (or --long).
* Bad options in the options files will now no longer result in an error but only a warning.
* Added -V to display version and exit.
* Tidied up help and usage text.

Version 2.62 - 20100117
* Added the --subdir-format option to specify the format to be used for the subdirectory naming (--subdir) using substitution fields e.g. '<nameshort>/<seriesnum>'
* If there is no series and episode number detected, make the <senum> field empty.
* Fixed podcast and localfiles plugins to match rest of code clean-up done in 2.61.

Version 2.61 - 20100115
* Fixed bug where history was not checked when a BBC /programmes/ URL was used resulting in recording for multiple modes.
* More code cleanup, less use of %hashes for readability.
* Remove undefined tags in --fileprefix substitutions.
* Added fields <nameshort> and <episodeshort> which are the same as <name> and <episode> but with the Series and Episode numbers stripped out.
* Added field <senum> to contain s##n## format for Boxee, MythTV and XBMC series and episode number parsing.
* e.g. use option --fileprefix='<nameshort> - <episodeshort>.<senum>.<pid>'
* Added fields <descshort> and <descmedium> which are descriptions limited to 255 and 1024 chars respectively.
* Improved metadata tagging of year for mp3 and qt files.

Version 2.60 - 20100114
* Fixed PVR mode bug from 2.59 where only the first search worked.
* Cleaned up code lots and fixed almost all perl warnings.
* Fixed bug in quicktime metadata atom insertion.

Version 2.59 - 20100113
* Added --future option to allow searching of future programme schedules / EPG for BBC Radio and TV (if indexed).
* Added --refresh-future option to allow indexing of future programme schedules / EPG for BBC Radio and TV when refreshing the caches.
* Running the PVR is now much faster due to caching the cache and history files in memory between PVR searches.
* Updated list of available radio channels.
* Improved display of help where options can be used in more than one context e.g. --long.
* Prevent repeated metadata requests when the metadata retrieval fails.
* Renamed --ignorechannels to --refresh-exclude.
* Added --refresh-include option so that only matching channels are indexed when refreshed.
* Fixed --multimode where existing file check was incorrectly failing.

Version 2.58 - 20100109
* More programme name and episode parsing improvements.

Version 2.57 - 20100108
* In freevo metadata format, do not use full path to media file.
* Updated credits for --email options to Network Ned, andy <AT SIGN> networkned.co.uk, http://networkned.co.uk
* Added --limit-matches so that this can be used as a safety-net incase a pvr search inadvertently has too many matches.
* Updated help a little.

Version 2.56 - 20100107
* Fix flvstreamer/rtmpdump version detection.
* Improved episode name extraction from meta-data to include episode number where appropriate.
* Added episode and series numbers to caches.
* Added freevo as a metadata format.
* Added --email options to allow for scheduled html search results to be sent by email (Credit: Stroller). 

Version 2.55 - 20100102
* Fixed lockfile for --pvrscheduler option.

Version 2.54 - 20100102
* Added --pvrscheduler option to run the PVR at regular intervals.
* Fixed buglet where stat was called on a non-existent cache file in debug mode.
* Improve series/episode number extraction from meta-data.
* Added workaround where abs_path does not work in win32.
* Bumped copyright years.

Version 2.53 - 20091231
* Auto-detect http:// or <type>:http:// URLs in a search term and set it as if it were a --url option.
* Revert change from 2.21 and read system-wide options additionally from /etc/get_iplayer/ as /var/lib/get_iplayer/ violates the FHS and Debian policy.
* Display warning that /var/lib/get_iplayer/ will be deprecated in future.
* Get extended metadata if --fileprefix is used.
* Added support for extended / alternate programme versions that have no version name set.
* Added support for multiple programme versions with the same name.
* Added --show-cache-age option to display age of selected programme caches.
* Removed a bunch of deprecated options.
* Display only the mode names without the numerical suffix in help messages.
* Added --ignorechannels option so that matching channels are not even indexed when refreshed.

Version 2.52 - 20091226
* Parse embedded mp3 flashaudio programmes that do not have the encoding attribute set.

Version 2.51 - 20091221
* Fix bug where essential stream metadata lookup was skipped if only iphone mode was specified.
* URL encode the url passed to a prepend type proxy request.

Version 2.50 - 20091220
* Fixed iphone mode after BBC changed things earlier this week.
* Improved and fixed mms and rtsp url parsing from asx and ram playlists which now parses new wma radio stream metadata.
* Added new pattern to connection metadata parsing for aac audio which fixes world service.
* Changed option --itvnothread to --mmsnothread.

Version 2.49 - 20091118
* Remove purchaseDate tag from mp4/AtomicParsley/iTunes tagging as this causes problems with iTunes.
* Strip out unsubstituted tags in metadata files

Version 2.48 - 20091110
* Added episode and season numbers and aired date to metadata files and nfo files.
* Added --fatfilename option for those DOS users. Submitted by David Pottage.

Version 2.47 - 20091108
* Tweaked tagging some more.

Version 2.46 - 20091108
* Fixed using full datespec for year tag in AtomicParsley tagging.
* Improved metadata tagging format with AtomicParsley.

Version 2.45 - 20091106
* Fix bug with authstring typo in level3/iplayertok CDN rtmp parameters which caused iPlayer HD to often fail.

Version 2.44 - 20091102
* windows7 or Vista can set the HOME environment variable so check for USERPROFILE first to determine if this is a win system.
* Added --before option to limit search results to programmes added before a specified number of hours.
* Fixed bug where --atomicparsley path override was ignored.
* Added advisory and genre tags to AtomicParsley tagging.
* Use full datespec for year tag in AtomicParsley tagging.
* Set AtomicParsley mp4 'stik' tag to 'Film' or 'TV Show' depending on programme category.

Version 2.43 - 20091024
* Added support for new flashvhigh, flashhigh, flashstd and flashnormal BBC Live TV modes.
* Added --livetvmode option.
* Updated iPlayer EMP swf revision.
* Fixed bug where --exclude comma separated values were not split into different terms to exclude.
* Added AtomicParsley support for tagging mp4 files - submitted by Jimmy Aitken.
* Added detection for different audio rtmp AAC stream bitrates.
* flashaac is now expanded into flashaachigh, flashaacstd and flashaaclow.

Version 2.42 - 20091015
* Fixed bug where external binary options got added to command line multiple times.

Version 2.41 - 20091002
* No longer make episode == title if the episode isn't defined as this makes the filename too long.
* For user commands, escape characters that have a special meaning in bash double quotes.
* Implemented workaround where mplayer cannot understand drive letters preceeding file paths for pcm output.
* Check for generated filename paths longer than 255 characters and generate error.

Version 2.40 - 20090926
* Fixed bug introduced in 2.32 where using the info option with --get would result in a file extension of EXT.

Version 2.39 - 20090924
* Fixed bug where named pipe filename was not quoted in command strings causing problems where the user profile dir contained whitespace.

Version 2.38 - 20090922
* Fixed bug where --expiry option was being ignored.
* localfiles plugin no longer uses unix find command so will work under win32.

Version 2.37 - 20090921
* Fixed name and episode extraction from URL title metadata.
* Do thumbnail download before running user commands.

Version 2.36 - 20090915
* Fixed bug where options were not bound when refreshing cache for external plugins
* Added Programme class method to set per-type expiry.
* Added new experimental localfiles mp3 plugin - requires MP3::Info - only in SVN
* Added new Streamer::filestreamonly class for localfiles plugin
* Added --page, --pagesize, --sort=<field>, --sortreverse to control output of displayed matches
* Sort mode disables tree mode
* When getting index feeds for a programme type, don't delete the old cache file if it fails.
* If name is not defined after getting metadata then set the name to longname - helps with naming of url recordings.
* If the pid is a URL then set the metadata web field to this URL.
* Removed old itv plugin because it no longer works.
* Known bug: localfiles plugin does not work for win32 yet.

Version 2.35 - 20090914
* Save absolute paths in history instead of relative ones.

Version 2.34 - 20090913
* When loading history, if there is a duplicate pid append the mode and filename fields with the existing record.
* Fixed bug where --pvrqueue ignored a default or preset --type value.
* Made thumbsize support more intuitive, --thumbsize now affects thumb downloads and metadata files, --thumbsizecache only affects the caches upon refresh.

Version 2.33 - 20090911
* Added detection for bbc streaming urls with mediaselector params in them.

Version 2.32 - 20090910
* --info now shows fileprefix and filenames, EXT is used if the file extension is not yet known.
* Added much more metadata to the history file to allow history search support.
* History entries can now be listed and searched by adding --history .
* The --info, --thumbonly, --metadataonly and --subsonly options can now be used with --history to get metadata after recording.

Version 2.31 - 20090909
* Added --thumbonly option to download the thumbnail without recording the programme
* The --thumbonly option implies that the --thumbnail option is set.
* Options --subsonly, --thumbonly, --metadataonly and --streaminfo are now done outside of the usual programme recording loop.
* Corrected file open bug for subtitles and thumbnails which failed in nowrite mode.
* Cleaned up stray newlines in logging.
* Fixed versions list population for prog types that have no verpids.

Version 2.30 - 20090909
* Fixed bug where iplayer name and episode was parsed incorrectly if there was no ':' in the title.
* Added 832x468 thumbnails to the list for --thumbsize.

Version 2.29 - 20090908
* Fixed bug: webrequest processing incorrectly used '-' as a delimiter.
* Fixed bug: incorrectly interpreted error return codes from open3 external commands.
* Send increasingly destructive signals to spawned commands if a SIGTERM/PIPE/INT is received.

Version 2.28 - 20090907
* Backed out change to use http://feeds.bbc.co.uk/iplayer/[channel]/list/limit/400 instead of http://feeds.bbc.co.uk/iplayer/[channel]/list as this results in more programmes.
* Added in a SIGTERM handler for the external program calls - if get_iplayer gets a SIGTERM then send one to the external program.

Version 2.27 - 20090905
* Thumbnail size support.
* Use --thumbsize=N to select the size of the thumbnails in the cache (use --info to see available thumbnail sizes).
* Use --thumbsizemeta=N to select the size of the thumbnails used in the metadata (use --info to see available thumbnail sizes).
* --thumbsize option requires the cacahe to be refreshed to update the default sizes.
* Tweaked debug for exit code display in debug mode.
* Added --help-basic for simplistic help page.
* --debug now switches on --verbose.
* Added new --series option which lists only series names with number of episodes and categories.
* Remove commas from source category names otherwise the comma spearated list of categories gets confusing.
* Improved accuracy of bbc iplayer programme feed name and episode parsing.
* Fixed bug where streaming-only mode would fail if the recorded file already existed.

Version 2.26 - 20090904
* Dropped support for rtmpdump versions older than v1.5
* Improved flvstreamer, id3v2, vlc, ffmpeg and mplayer invocation to avoid using shell
* Fixed bug where unlink was called as a command when purging old recordings
* Fixed --wav and --raw modes on non-Unix platforms for realaudio modes

Version 2.25 - 20090901
* Popular and Highlights tv and radio programmes are now tagged as categories.
* e.g. To list most popular tv programmes use --category=popular
* e.g. To list tv highlights use --category=highlights

Version 2.24 - 20090901
* Extract even longer description from BBC programmes site metadata for info and metadata files.

Version 2.23 - 20090831
* Extract longer description from BBC iPlayer metadata for info and metadata files.
* Abort with an error if the download_hostory file is not writable in append mode.

Version 2.22 - 20090827
* Fixed small bug where number of matches was not displayed in non-pvr mode.
* Added "Audio Described" category search to tv mode.
* Changed method of merging the list of programme versions for tv/radio modes.
* Made "Misc" options visible in advanced/long help mode.

Version 2.21 - 20090826
* Added --packagemanager=disable option for externally managed get_iplayer pkgs.
* Changed /etc/get_iplayer/options to /var/lib/get_iplayer/options as a default system-wide options file for *nix to comply with Linux FHS.
* Give a warning if options exist in /etc/get_iplayer/options

Version 2.20 - 20090825
* Added --metadataonly option to retrieve programme metadata without streaming or recording the programme.
* Thumbnails can also be retrieved alone by using --thumbnail option with --metadataonly.
* Added/improved --metadata=xbmc_movie format.

Version 2.19 - 20090824
* If --multimode is used record all modes in one invocation of get_iplayer.

Version 2.18 - 20090822
* If --multimode is used, --hide has no effect. Without this PVR mode will fail to work with multimode

Version 2.17 - 20090822
* If an unknown new CDN connection is found for an iPlayer programme, do not add it to the mode list
* Added --multimode option to allow the recording of multiple modes of the same programme
* WARNING: --multimode will record *all* specified/default modes for each programme
* If multimode option is used, put the mode name in the default filename prefix

Version 2.16 - 20090815
* Added new flashstd iPlayer TV mode (480kbps H.264 640x360)
* Changed default tv modes to: iphone,flashhigh,flashstd,flashnormal
* Tweaked PVR text output
* Fixed thumbnails and web urls for liveradio and livetv

Version 2.15 - 20090804
* Remove nocopyright option from pvr save options
* Move --itvnothread option to main script as it is not actually used in itv plugin and causes problems for installer.

Version 2.14 - 20090801
* Run command even after streaming to stdout.
* Allow --hash option to affect flvstreamer command if it supports this feature.
* Made flvstreamer exit code handling better when streaming

Version 2.13 - 20090729
* With rtmp recordings, retry when any non-zero exitcode is returned from flvstreamer.

Version 2.12 - 20090726
* --force now overrides --hide. This allows force to have the desired effect in pvr mode.

Version 2.11 - 20090724
* --list now takes account of search parameters when counting and creating unique list

Version 2.10 - 20090719
* Updated PVR Manager script with latest options changes.
* PVR Manager now runs better under Win32.
* Renamed --rtmpstop & --rtmpstart to --stop & --start.
* The --stop and --start can now be used with both realaudio and rtmp streams.
* Improved partial proxy support.
* Skip mediaselector stream lookup if only iphone mode is specified.

Version 2.09 - 20090712
* Ensure rtmpdump option is still recognised after warning.

Version 2.08 - 20090709
* Fixed bug in options and preset parsing.

Version 2.07 - 20090708
* Added new sislive realaudio CDN.
* Run the init method before checking download history so that live streams ignore history.
* min_download_size is now defined on a per programme type basis.
* Added support for flvstreamer stop/start offsets using --rtmpstart and --rtmpstop options.
* Use --rtmpstop to limit length of live rtmp recordings which have timestamped streams.
* Allow --url to specify BBC iPlayer tv/radio short URLs like 'http://www.bbc.co.uk/i/lbtbg/'
* iPlayer urls can optionally have a start offset appended like '?t=16m51s' (must use flvstreamer 1.8c or later).
* Fixed download retry loop bug where a different mode for a programme was tried where the next programme should have been tried.
* Prevent thumbnail download, id3tagging, command and download history logging if streaming only.
* All option names, not just the internal names, are allowed in option and preset files.
* Added patch by Steven Luo to make different speakers appear on different lines in subtitles.
* mp3/aac mode auto-detect for audio EMP urls.

Version 2.06 - 20090706
* Improved and simplified CDN parser for iPlayer mediaselector data
* New iPlayer CDN streams will now mostly be automatically found when added by the BBC.
* Added checks for invalid and deprecated options in options files and presets.
* Recognise iPlayer tv pids starting with p0.
* iPhone redirect URL no longer looked up if iphone is not a selected mode.
* Added BBC Radio 4 Long-Wave into liveradio channel list.
* Added --rtmplivetvopts and --rtmpliveradioopts options.
* flvstreamer v1.8b recommended for better reliability.
* Reduced flvstreamer timeout to 10 secs because I'm impatient.

Version 2.05 - 20090701
* Fallback to allow xml BBC EMP playlist urls to be directly specified for --pid/--url requests.
* Allow specification of a BBC Programmes page with an embedded player when using --url.
* Allow spaces in path for external binaries.
* Bumped player version for iPlayer.
* Fixed flashaac1 mode to append authstring in playpath.

Version 2.04 - 20090626
* Simplified live BBC streaming support.
* Added --type=livetv and --type=liveradio which simplifies searching/streaming/recording live BBC tv and radio channels.
* Added --stream option which is an alias of --nowrite and --stdout.
* Added --player option which will pipe all output to the specified command for direct streaming.
* Added --attempts option to set the number of attempts to make or resume a failed connection.
* Example usage: get_iplayer 'BBC Four' --type=livetv --stream --player='mplayer -cache 128 -'
* Added --modes option - a general set of default modes for all programme types.
* Changed --amode to --radiomode and added --liveradiomode options.
* Changed --vmode to --tvmode.
* Commandline search arguments now get added to presets and options if specified.
* The id3tag tool can be used instead of id3v2 - use the --id3tag option to specify it.
* Assume that ITV stream is successful if file is > 10MB even if there is a reported error to stdout.
* The Chnagelog since the previous version is displayed after updatng get_iplayer.
* rtsp and mms streamers now cope better with nested asx playlists.
* Force --raw when --stream is used with radio or live radio to prevent lame or ffmpeg transcoding.
* Fixed bug where tee function was not correctly referenced in rtsp streamer.
* Fixed flashaac2 mode for mp3 streams.
* Don't check download history when live streams are being streamed or recorded.
* Fixed lwp timeout invocation bug.
* Fixed get method return codes for iphone and mms streamers.
* Error if stdout is requred for mms streams.
* Check that external programs are also executable in exists_in_path function.
* Deprecated --usertmpdumpexit option which is now always assumed to be true.
* Caveats: --player and --stdout streaming does not work properly on windows.

Version 2.03 - 20090620
* Added in debug level options to control verbose output from flvstreamer

Version 2.02 - 20090619
* Added support for BBC world service Live and bulletin AAC streams from the worldservice page
* Much more reliable Live streaming with new flvstreamer v1.8
* Fixed bug where raw audio flv files were id3 tagged
* Removed incorrect -auth parameter from flvstreamer
* Bumped BBC iPlayer swf version

Version 2.01 - 20090618
* Fixed bug where cmdline options were being overridden by default options

Version 2.00 - 20090617
* Tag substitution now uses version-specific metadata about the recorded programme.
* Caveat: if --pid is used to record a programme less metadata will be obtained
* Added <dldate> and <dltime> tags to allow for these download timestamp tags in filenames etc.
* Options presets can be applied so that you can have a saved set of options and invoke them using --preset or -z
* User options and Presets can now be edited as follows
* Option --prefs-show displays all options in the user options or preset if specified
* Options --prefs-add and --prefs-del adds/deletes specified options from the user options file or preset if specified
* Option --prefs-clear removes *all* options from the current preset or user options
* Option --preset selects predefined sets of options
* Option --preset-list lists all saved options presets
* Using --save option now reports an error telling user to use --pref options
* Option --pvr-single runs a specifically named PVR search
* User profile direcotry can now be overridden using --profile-dir

Version 1.99 - 20090613
* Fixed Win32 file move and rename bug.
* Added --metadata=<type> option which creates a file with programme metadata after download.
* --metadata=xbmc creates a .nfo file (not verified in XBMC yet) and --metadata=generic creates an .xml file.
* Improved the programme versions searching using version substring matches.
* e.g. --versions=def,sign  will match and try to record default and signed programmes in that order.
* Get full info metadata before any download so that full substitution works for --metadata and --command options
* Only get verpid metadata if we dont have it already.
* The various search options can now use a comma delimiter as an implied OR.

Version 1.98 - 20090611
* Bugfixes to prevent some metadata lookups for BBC EMP and Live iPlayer content
* Set flvstreamer timeout down to 20 seconds
* Fix id3 tagging where quotes were not properly escaped
* Fix radio pid parsing for live URLs

Version 1.97 - 20090610
* supports many more BBC web pages with embedded media such as Learning Zone
* Updated with new BBC iPlayer swfUrl
* Prevent checking for iPhone stream for BBC EMP and Live requests
* Improved BBC iPlayer pid parsing
* Limit filename to 256 chars max

Version 1.96 - 20090610
* Added support for BBC Embedded Media Player Live Channels and Videos
* To stream or record embedded BBC video use option --pid tv:<URL>
* Use of flvstreamer or rtmpdump 1.6 is recommended - older versions are flakey.
* Live Radio streams are AAC 128-192kbps
* Human readble timeadded output in --info
* Cleaned up a few perl warnings

Version 1.95 - 20090609
* Added live BBC iPlayer radio and tv support
* Live TV Streams are either 512x288 or 640x360 VP6 500-800 kbps
* For live TV use options: --pid tv:<Channel URL/ChannelID> --vmode flashnormal
* For live Radio use options: --pid radio:<Channel URL/ChannelID> --vmode flashaac,wma,realaudio
* ChannelID can be found in the URL for the channel on the BBC iPlayer web page
* Note that not all Radio channels have AAC streams
* To stream add: --nowrite --stdout | mplayer -cache 128 -
* Live flash streaming requires flvstreamer or rtmpdump v1.5 or newer.
* Added validity checking to date and time calculations.

Version 1.94 - 20090609
* Fixed $_ bug

Version 1.93 - 20090609
* Fixed time function overflow - year must be limited to max 2038

Version 1.92 - 20090608
* Decoded entities for longname attribute for iplayer programmes.
* Added Estimates of file sizes for each mode in --info output.
* Now read the Version PID rdf metadata to display first and last broadcast times in --info.

Version 1.91 - 20090606
* Fixed bug with using webrequest and search options with pvradd

Version 1.90 - 20090525
* Fixed bbc tv subtitle ttxt to srt conversion bug

Version 1.89 - 20090525
* Fixed bbc tv subtitle ttxt to srt conversion bug

Version 1.88 - 20090523
* Fixed stdout streaming support when using flvstreamer tool

Version 1.87 - 20090522
* Added support for flvstreamer tool

Version 1.86 - 20090519
* Overhauled the get_iplayer updater
* Plugins will now only be updated if they are all writable
* Plugins in the system and user plugins dirs will all be updated
* Added hidden --packagemanager option to allow packages to disable script based updates
* Added --plugins-update option to force get_iplayer to download or update all the latest plugins
* plugins update will run if no installed plugins are found

Version 1.85 - 20090511
* Moved more web requests to use common request_url_retry method
* Added prepend url support for proxy option

Version 1.84 - 20090507
* Added STDOUT Streaming support for rtmp streams - only works with both --stdout and --nowrite
* Moved itv get_url method to itv plugin
* Make updater retry failed web updates

Version 1.83 - 20090506
* Drop support for Hulu, Channel4 4oD and Demand Five plugins.
* Added new option to allow custom options to be added to rtmpdump invocation for BBC iPlayer --rtmp-tv-opts and --rtmp-radio-opts.
* Modified help to reflect recording nature of PVR
* Added --listplugins option to list the currently found programme type plug-ins or built-ins.

Version 1.82 - 20090505
* Full metadata is now obtained from cache if it exists before every get so that --command works properly with --pid.
* Added --rtmpport option to allow users to override the rtmp port - allows use of port 443.

Version 1.81 - 20090505
* Force the updater to run if there is no plugins dir detected - required to make old versions obtain the plugins.
* Full metadata is now obtained before every get so that --command works properly.
* Converted itv type into a plugin.
* Moved more global vars into respective methods.
* Changed user-agent for updater.
* Improved ua string selection.
* Updated swf versions for iplayer.
* Fixed guidance parsing in itv plugin

Version 1.80 - 20090505
* Tweaked updater to fix plugin copy bug

Version 1.79 - 20090505
* Tweaked updater

Version 1.78 - 20090505
* Tweaked updater
* New plugin based distribution.
* The --force option can now be used with --update to disable version checking.

Version 1.77 - 20090504
 to make get_iplayer appear to be more like a conventional web browser to the server.

Version 1.76 - 20090503
* Bugfixed user agent setting and for scraping.

Version 1.75 - 20090501
* Fix ch4 scraping

Version 1.74 - 20090501
* Fix ch4 scraping

Version 1.73 - 20090429
* Switch off cookies when scraping five site otherwise downloads fail.

Version 1.72 - 20090429
* Remove LWP debug - oops

Version 1.71 - 20090429
* Demand Five - Channel 5 flash content now searchable and downloadable.
* Demand Five requires rtmpdump v1.5.
* Demand Five type is --type=five.
* New Automated Installer released.

Version 1.70 - 20090428
* Channel4 4oD Catch-up indexing and search support.
* Channel4 type is '--type=ch4'.

Version 1.69 - 20090427
* Initial Channel4 4oD Catch-up download support - requires rtmpdump v1.5.
* Channel4 support should use options: --pid ch4:<PLAYurl> --vmode=flashnormal.
* Indexing of Channel4 programmes to follow.

Version 1.68 - 20090426
* Added --hash option to output basic progress hashes instead of detailed progress.
* Fixed bug where pvr name was not sanitized.
* Removed colons and parentheses from PVR queue names - breaks some platforms.

Version 1.67 - 20090423
* Minor mods to webrequest option parsing.
* Removed <br> tags in description of BBC iPlayer progs.
* Validation of prog type before creating an object.

Version 1.66 - 20090422
* Programme type detection fixed for --pid downloads which are not in cache.
* No more history file read warnings unless in verbose mode.

Version 1.65 - 20090420
* Added --nocopyright option to make the startup quieter.
* Added --webrequest option to allow options to be specified as a single urlencoded string.
* Added automatic manpage generation using --manpage option.
* Help sections are now ordered more logically.

Version 1.64 - 20090419
* Fixed bug where a succesful download was not exiting the mode loop thus downloading all specified versions.

Version 1.63 - 20090419
* Fixed itv default vmode bug

Version 1.62 - 20090418
* Added new akamai CDN for BBC iPlayer flashhigh vmode to make it work again.
* Only modes that exist for a programme are now attempted to be downloaded.
* All selected modes are tried for each prog version bofre falling back to next version.
* Programme stream data is now downloaded only once per download attempt.
* stream data is now an attribute of the prog object.
* In verbose mode unknown streams or CDNs are now reported.
* Added flashlow2 vmode for new reported CDN

Version 1.61 - 20090416
* Added 1280x720 3200kbps HD download support for BBC iPlayer. Use --vmode=flashhd

Version 1.60 - 20090416
* Added --nothreaditv option to force ITV programme parts to download one after another.
* --nothreaditv option works around bugs in Windows ActivePerl or Strawberry Perl with Vista.
* Fixed bug to decode html entities in ITV programmes name, episode and guidance text.
* Removed html entities from radio channel names
* Added patch to insert programme type and index number into mythtv xml output

Version 1.59 - 20090409
* Modified --pvrlist output to make it easier to parse
* Guidance is now correctly detected for BBC iPlayer tv
* Fixed a small scoping bug in iPlayer get_links method
* Added programme web url to metadata listing for --info

Version 1.58 - 20090408
* Added --subsraw to allow saving of the raw subtitles file.
* Fixed bug where iphone mode sometimes had no streaming class defined
* Detect iphone mode 403 responses

Version 1.57 - 20090407
* Fixed bug where a // in a path resulted in a 2 being added to the path when --subdir was used.
* Fixed bug when using --command the command string was being over-sanitized.

Version 1.56 - 20090405
* Added in wmvdrm vmode and renamed mobile vmode to mobile_wmvdrm.
* New ability to download wmv drm streams - cannot decode them though.
* Changed name of class Streamer::podcast to Streamer::http.
* get_stream_data method now sets streamer class and filename ext.
* iPlayer radio and tv classes now share a common download method.
* Radio modes are now attempted to be downloaded based on stream metadata rather than blindly trying them.
* realaudio mode now creates symlink when beginning to download if required

Version 1.55 - 20090404
* If downloaded programmes of over 30 days old still exist the user is prompted to delete them.
* This fair-use behaviour can be disabled by using the --nopurge option.
* Filenames are now added to download history
* VLC now quits correctly after a download for n95_mobile and n95_wifi vmodes

Version 1.54 - 20090403
* New Hulu programme feed indexing method
* Minor code cleanup

Version 1.53 - 20090403
* Fixed small $_ scoping bug

Version 1.52 - 20090402
* Rewrote BBC iPlayer stream metadata parser
* flashaac, flashhigh and flashvhigh modes are now expanded to try all CDNs modes in turn if one fails
* Fixed flashvhigh stream detection - wrongly parsed flashhigh stream as flashhigh
* limelight CDN rtmp vmodes now working with rtmpdump v1.4

Version 1.51 - 20090401
* Added support for experimental 1500kbps 832x468 resolution BBC iPlayer streams as flashvhigh vmode

Version 1.50 - 20090331
* Now supports rtmpdump-1.4 for Hulu using current --hulu-decrypt-pid method
* Removed unusable RTMPE streams from Hulu stream data parsing
* Specified --protocol and --port when invoking rtmpdump 1.4 to stop it complaining

Version 1.49 - 20090322
* The list of available download vmodes/amodes for a programme are now shown when you use --info
* Work around divide-by-zero error in average download speed calculation
* --info option now works for all programme types

Version 1.48 - 20090321
* Worked around bug where perl move can delete a file if src and dest are the same file in strawberry perl.

Version 1.47 - 20090319
* If an rtmpdump download fails try to resume and get new streamdata again so that it isn't stale.
* Use a different number of retries for above depending on the mode of download - more for rtmp modes.
* Removed patch from 1.44 which was broken.
* Changed flashhd to flashvhigh as this isnt really HD quality.

Version 1.46 - 20090317
* Improved BBC HD iPlayer 720x404 RTMP support - alpha.
* rtmpdump can now download HD streams better if using Level3 CDN.
* Added rtmpdump version detection - needed for Level3 HD downloads
* Known issue: content is not playable beyond first part.
* Changed calling params to Streamer::rtmp::get

Version 1.45 - 20090317
* BBC HD iPlayer 720x404 RTMP support - alpha. The BBC haven't actually launched this service yet so it is subject to change.
* Added flashhd mode for BBC iPlayer high-definition TV support
* Known issue: I suspect that rtmpdump currently has problems downloading the full hd stream without timeouts
* Fixed flashhigh parsing due to BBC iPlayer changes

Version 1.44 - 20090314
* If rtmp downloads timeout with exitcode 2 then try to resume them automatically up to 6 times to workaround bug/issue where audio downloads hang after approx 40-60MB.
* You must still wait a few minutes for the download to timeout but at least it is hands-off.
* Based on a batch submitted by Simon Quinn.

Version 1.43 - 20090309
* The --hulu-decrypt-pid option now requires both the decrypted pid and the auth string to be returned, separated by a space from the external program.
* Changed the smil URL for hulu

Version 1.42 - 20090305
* Updated support for BBC Radio AAC/AAC+ audio streams after they changed their content delivery provider
* Added the --isodate option to change the date in the filename to ISO8601 format: YYYY-MM-DD
* Fixed a buglet where the lwp http proxy was being set unnecessarily
* Added advanced option --use-rtmpdump-exitcode to use the rtmpdump exit code to decide whether a stream downloaded OK

Version 1.41 - 20090226
* Fixed bug in subtitle sanitizing
* Added --overwrite option to allow previously downloaded files to be overwritten

Version 1.40 - 20090224
* Added --thumb and --thumb-ext options to automatically download thumbnail image and set extension fo the file
* Use --thumb --thumb-ext=tbn options to have XBMC pick up thumbnails automatically
* Fixed bug: make all valid options usable as pvr options
* Added --hulu-decrypt-pid option to specify the exernal program that returns the decrypted hulu pid given the encrypted one as the first argument
* Use environment variables GETIPLAYERUSERPREFS and GETIPLAYERSYSPREFS if they are set to override the get_iplayer user and systems prefs directories

Version 1.39 - 20090217
* BBC iPlayer get_metadata method now doesnt assume that every prog has an episode name
* --info now displays all collected metadata
* iphone download now uses 12 digit random number - probably not significant though
* Cleaned up XML output for Freevo and MythTV and fixed some matching bugs

Version 1.38 - 20090216
* Automatically fetch programme metadata if required - useful with --pid mode
* Fix get_hex method call in debug mode
* BBC iPlayer get_metadata method now obtains more data

Version 1.37 - 20090215
* Code cleanup for metadata extraction
* Added --hulu-pages, --hulu-sort, --hulu-types options for controlling the indexing hulu.com
* Fixed bug where first line of cache files was assumed to be a cache-order definition
* Simplified channel hashes
* Added --subtitles-only option to allow only the downloading of subtitles (also sets the --subtitles option)
* Worked around a Programme/Streamer class instantiation bug where options instance would not get bound to the class unless there was a single instance

Version 1.36 - 20090214
* Added new audio download mode for AAC audio "flashaac" for BBC iPlayer Radio (requires rtmpdump)
* id3v2 also tags AAC audio files

Version 1.35 - 20090211
* Failure to download subtitles now no longer results in an empty file in hulu
* The hulu vmode classification is now based on bitrate ranges 

Version 1.34 - 20090211
* Fixed small bug in Hulu closed-captions / subtitles SMI format parsing

Version 1.33 - 20090208
* Now downloads Hulu closed-captions / subtitles in SMIL format and converts into SubRip / srt format

Version 1.32 - 20090207
* Improved Hulu indexing and stream download support
* Rewritten Hulu indexing method to use page scraping which is more controlled and sometimes faster
* Now using category-based channels from Hulu site and limiting the number of pages per channel (10) to speed up scraping
* All Hulu movies now added to index
* Fixed subtitles TT to SubRip conversion. The BBC decided to add new html tags which broke it.

Version 1.31 - 20090206
* Changes tv vmode flashwii to flashlow for consistency between iPlayer and Hulu
* Renamed hulu vmodes flash1/2/3 to flashhigh/flashnormal/flashlow for consistency
* Bugfix: parse the H264(flashhigh) hulu stream url which was accidentally skipped
* Changed default vmode list for hulu to be flashnormal,flashlow because flashhigh requires encrypted rtmp support
* Sort the hulu vmodes based on reported bitrate in the metadata
 
Version 1.30 - 20090206
* Added beta Hulu TV indexing and download support (US only) with the support of rtmpdump
* Used the Hulu download method by Andrej Stepanchuk, author of rtmpdump
* URLs containing PIDs can be specified with --pid together with a single --type
* If a pid and single type are specified, no indexing is performed

Version 1.29 - 20090205
* Added --fields option to allow user to customise which programme fields to search using a comma-separated list
* if ".get_iplayer/" exists in current working directory, use its options file to override any user/system options
* Added --pvrqueue option to allow matching programmes to be added to the pvr download queue on a one-off basis
* Fixed bug: Only skip the current programme download, and not exit, if file already exists
* Added benign --comment option to allow annotation of pvr searches

Version 1.28 - 20090131
* Changed behaviour - all ITV progs now get downloaded under directory specified with --outputitv and not from --outputtv
* Made global type hash local
* Removed global download_dir hash and put functionality into generate_file_prefix method
* Added detection of bad request url for iphone download method
* Detect lack of programmes in iplayer playlists and report unavailability
* Allow --streminfo in --pid mode

Version 1.27 - 20090126
* Fixed bug where the programme type leaked between PVR entries

Version 1.26 - 20090126
* Fixed tv vmode parsing bug
* Rewrote retry/fallback mode loop code
* Added StreamImage thumbnail element to xmlchannels output for mythtv
* Fixed Stream element locations in xmlchannels xml output for mythtv

Version 1.25 - 20090126
* Fixed bug where >1 search index numbers on the commandline would be ignored if the type was not specified in --type
* Made the cache type loading more intelligent - now only loads specified --type caches if absolutely required

Version 1.24 - 20090125
* Fixed broken podcast downloading

Version 1.23 - 20090123
* Fix bug where symlink in itv mode was not created unless --raw was specified
* Fix bug where symlink fields were not substituted for several modes
* itv symlink target is now the multi-part dir if there is more than one part
* itv prog parts now have zero-padded part number to ensure they are played back in the right order
* By default, only simple options are shown under --help.
* Added --help-long option to show all options.
* Fix bug where subdirs were not created correctly in itv mode using --subdir option

Version 1.22 - 20090123
* Fix bug where license/version info was sent to stdout in pvr mode
* Added --showoptions option to display all set options and where they were defined

Version 1.21 - 20090123
* More OO refactoring
* Added GPL text at runtime as per GPLv3
* Added --conditions and --warrany options for GPLv3

Version 1.20 - 20090122
* Changed behaviour, --pid=<pid> now limits download attempts to specified prog types unless --pid=<type>:<pid> form is used
* Changed behaviour, a search term can contain a pid but it must be in the form of 'pid:<pid>' and the correct prog type must be specified using --type
* Major refactoring using OO Perl
* Created Programme, Pvr, Streamer & Options classes
* Allow Programme/Streamer/Pvr subclasses to add thier own options (and usage text)
* Command line options are now dynamically processed
* Added --listformat option to allow a user to specify the search output text format (using usual substitution fields)
* Added %index_prog hash "index => prog instance" (done away with global "index => pid" hash)
* Cache file format is now read from first line of each cache file - this will allow future format changes
* Fixed symlinking of downloaded file when resuming iplayer tv/radio
* Fixed unescaped <Name> data in --xml-channels output.

Version 1.19 - 20090112
Fixed dumb bug where RTMP video was being wrongly demuxed audio-only

Version 1.18 - 20090111
* Now use mplayer to demux the flv stream into mp3, ffmpeg can only seem to retranscode the flv to mp3 with obvious loss in quality.
* Some output message tweaks
* Simplified search result display creation
* Fixed the episode subdir creation when ITV episodes have more than 1 part
* Failed ITV prog parts are retried up to 3 times (mplayer is returning zero even when failed). Use backticks and get the error messages which come out of mplayer
* In ITV mode, if any prpg parts are less than a minimum size then retry the download.
* Added programme web page link to cache to enhance --html output and fix it for ITV and podcasts
* Improved readability of html output

Version 1.17 - 20090109
* Scrape and index ITV player 'TV Classics' programmes (in addition to ITV Catch-Up progs) 
* Added 'guidance' info to caches

Version 1.16 - 20090109
* Restructured code to make various download methods more consistent
* Moved all media stream url resolution into get_media_stream_data()
* Fixed ITV PVR downloading
* Improved the text of lots of messages
* Try to guess if ffmpeg has successfully transcoded an flv file by looking at the resulting file size
* Added the "--exclude <regex>" option so that you can exclude programme names from your search
* The --amode and --vmode options can now specify a comma separated list of audio or video download methods to try in order
* Unified the http user-agent setup
* Added download rate reporting in itv mode
* Record audio/video download mode in download history
* Workaround rtmpdump non-zero exit code even when it appears to succeed

Version 1.15 - 20090107
* Fixed undefined hash ref in get_media_stream_data that was causing some downloads to fail

Version 1.14 - 20090106
* Handle thread waiting more gracefully in parallel download mode
* Display download byte counters for each ITV download thread
* Display download rate/time summary for each ITV download thread

Version 1.13 - 20090106
* Added ITVplayer Catch-up Indexing and Searching support (use --type=itv)
* Fixed bug in --list option - programme names were being incorrectly parsed

Version 1.12 - 20090106
* Added alpha support for ITV Catch-up downloads (--pid itv:<numeric pid from itv site>)
* Added parallel download support for all parts of ITV programmes because they stream in realtime.
* Fixed field length bug in metadata tagging of mov files.

Version 1.11 - 20090104
* Added iPlayer Flash Audio download support via rtmpdump tool / ffmpeg
* The --amode (Audio Mode) option can now be set to 'flashaudio'
* Reworked get_media_stream_data function to return a hash for more flexible usage
* Display --streaminfo data in a much clearer way
* --pvrlist now displays entries sorted alphanumerically
* Allow --partial-proxy to affect subtitle downloading
* Add user meta-data to iPhone/h.264 downloaded video (hopefully helps with iTunes)
* In Quicktime files ftyp atom is now the first one which makes it more mp4 compliant
* Fixed stdout iphone video mode with resumed downloads (broke in v1.06)
* Fixed retry reporting on failed downloads 
* Known issue: flashaudio downloads appear to fail even though they complete with rtmpdump v1.2

Version 1.10 - 20090103
* In rtmp mode, remove pageUrl detection - not required
* Added capability of downloading RTMP Wii Flash video
* Deprecated --mp3audio, --realaudio, --rtmp, --n95 options (they still work for now).
* New options --amode=[mp3|realaudio] (default: mp3 fallback to realaudio)
* New option --vmode=[iphone|rtmp|n95|flashhigh|flashnormal|flashwii] (default: iphone)
* If --vmode is set to "rtmp" then try all rtmp modes (flashhigh/flashnormal/flashwii) until one works
* Fixed typo bug which prevented lame transcoding realaudio to mp3

Version 1.09 - 20090102
* In rtmp mode, use authstring from streaminfo for calling new version of rtmpdump v1.2

Version 1.08 - 20081231
* In rtmp mode, If High Quality Flash RTMP version is used, use mp4 file extension
* In rtmp mode, If High Quality Flash RTMP version is not available then use Normal Quality Flash RTMP version
* In rtmp mode, if Normal Quality Flash is used, an avi file is created (ffmpeg cannot yet demux vp6 flv streams into mp4 containers)

Version 1.07 - 20081230
* --raw option now also prevents ffmpeg converting flv to mp4 format in rtmp mode
* search options now affect the results of --html and --xml output

Version 1.06 - 20081228
* Send all text output to stdout unless --stdout or --pvr modes are being used.

Version 1.05 - 20081228
* Added resume option to rtmpdump invocaton
* Get RTMP application name from BBC media metadata

Version 1.04 - 20081225
* Show thumbnail url for --info
* Added RTMP Flash High Quality video download additions using rtmpdump from Andrej Stepanchuk (--rtmp)

Version 1.03 - 20081221
* Now use the new Coyopa streams for BBC Local Radio.
* Added all BBC local radio stations to the radio channel list

Version 1.02 - 20081220
* Dont get index info from BBC site if were only specifying a pid to download (using --pid)

Version 1.01 - 20081125
* Added proxy workaround for some broken web proxies (--partial-proxy)

Version 1.00 - 20081109
* Added --hide option to remove programmes in listings when they have already been downloaded
* Force the --hide option on when running PVR

Version 0.99 - 20081103
* Added new radio and tv channels: bbc_radio_nan_gaidheal, bbc_radio_cymru, and bbc_alba

Version 0.98 - 20081103
* Added tree-view --tree option for listing programmes

Version 0.97 - 20081103
* streaminfo sub now uses request_url_retry instead of download_block because this caused problems getting the RTSP urls for some strange BBC reason

Version 0.96 - 20081024
* Added streaminfo detection of N95 3G stream (in addition to the N95 wifi stream)
* Fixed streaminfo detection which was somewhat broken - now split the media tags before

Version 0.95 - 20081020
* Added another use of the --raw option to stop the iPhone video downloads having their moov atoms re-arranged for partial download playback capability

Version 0.94 - 20081014
* Changed all references to N96 into N95
* Streaminfo option now displays new Mobile WMV DRM stream data

Version 0.93 - 20081013
* Added id3v2 dependancy to deb and rpm
* Now run tagging on --pid downloads

Version 0.92 - 20081007
* Added writable check for --update option
* More checks around update file permissions

Version 0.91 - 20081005
* Allow cmdline args to override pvr search options

Version 0.90 - 20081004
* Allow user to specify filename prefix format (not pathname or extension) using %prog field names. e.g. --file-prefix='<name>-<episode>-<pid>-<type>'
* Fixed bug where saved options were ignored
 
Version 0.89 - 20081004
* Fixed bug where <profile>/pvr/ dir not get created with --pvr-add
 
Version 0.88 - 20081003
* Fixed update_script function which was downloading the new version twice! (darn, it is half as popular as I thought)
* PVR enable/disable search support allows you to disable a search without deleting it. --pvr-enable=<searchname>, --pvr-disable=<searchname>
* Using the --test option with --pvr no longer uses the lockfile

Version 0.87 - 20081002
* using --test with --pvr allows user to see which programmes will match the PVR downloads
* implemented locking to prevent >1 --pvr process from running (in ~/.get_iplayer/pvr_lock)
* When using --pvr option, a message is sent to STDOUT so that this can be piped to email for new programme downloads,
* Ignore the --flush option with --pvr - use the --expiry option instead (i.e. set to just less than the frequency of the pvr schedule)

Version 0.86 - 20081001
* Improved --symlink option to allow format subtitution from %prog fields
* Symlink option now works for radio and podcasts also

Version 0.85 - 20081001
* Fixed --pvr-add so that options derrived from options files are not saved to the PVR search
* Options specified on the cmdline with --pvr option will override those options in the pvr searches
* All PVR searches will, by default, use the options from the saved options files
* Fixed bug where %prog hash was retained between pvr searches making the type option get ignored in some cases

Version 0.84 - 20080929
* New PVR functionality allows you to add a search criteria to a PVR search file for scheduled downloads
* Added --pvr, --pvradd=<searchname>, --pvrdel=<searchname>, --pvrlist options
* e.g. Add the following line to your crontab: '0 * * * * /path/to/get_iplayer --pvr 2>>/tmp/get_iplayer.log'

Version 0.83 - 20080929
* Remove 16MB block downloads for iphone mp3 radio - does not appear to be unnecessary
* Improved and simplified metadata --info collection using new prog feed
* Improved channel feed parser for TV so that Sign Zone progs are correctly detected
* Added --version-list option so that the preferred version(s) of a programme can be specified e.g. --version-list=signed,default
* Added --versions option to narraw search to specific programme versions (e.g. default or signed or any regex)
 
Version 0.82 - 20080929
* Some code simplification
* Remove web bug and cookie whitelisting crud
* No more web scraping to get the version pids - use the iplayer metadata feed 
* Use the media stream metadata to determine if PID is for radio or tv
* Use the media stream metadata to determine subtitles url
* Fixed streaminfo option to also parse world service media stream data
* Added WMA audio into media stream data parser

Version 0.81 - 20080927
* Added get_iplayer user agent while getting podcasts as per request from James Cridland

Version 0.80 - 20080927
* Bugfixed -o option - it was incorrectly assigned to podcasts only

Version 0.79 - 20080927
* Use xml podcast feed - simpler to parse and contains a few additional progs

Version 0.78 - 20080926
* Cleaned up some more perl warnings after turning on this feature - now disabled
* Behave better when a programme is listed but unavailable
* Improve reporting of prgramme name when pid is already in download history

Version 0.77 - 20080926
* Added non-mandatory idv3 tagging support for MP3 files downloaded by new iPhone method using external id3 tools if available
* Added --id3v2 option to specify non-default location of id3v2 binary
* Added <fileprefix>, <ext> and <dir> to %prog so that it can be used in --command option
* Tidied up definition of cache files
* Cache files no longer get deleted upon get_iplayer upgrade

Version 0.76 - 20080924
* A few cosmetic tweaks like the 'number of matches' appearing at the end on the programme listing
* Set the 'type' option according to the index number specified (i.e. 1xxxx => radio, < 10000 => tv and > 19999 => podcast)
* The programme cache is additionally read if an index is specified in its number range

Version 0.75 - 20080924
* If an MP3 version of a radio programme is not available the default is to try to use the realaudio stream
* --realaudio option prevents the downloading of radio MP3 streams
* --mp3audio option ensures that realaudio stream is not used as a fallback for radio
* A few cosmetic bug fixes
* Check for existence of a PID when an index number is specified
* Don't add empty pids to download_history file
* Added --force-download option to override download history
* Report final average download speed / bitrate / duration after successful downloads (not for rtsp streams)
* Remove stdout logs - messes with stdout streaming in too many strange ways
* Does not check download history if nowrite & stdout options are specified

Version 0.74 - 20080924
* Changed --list-categories and --list-channels to use --list <element_name> where element name can be any element name in the %prog hash
* Bugfix --streaminfo doesn't add to download history
* Allow h.264 download subroutines to now also download mp3 audio for iphone radio
* Added --realaudio option for radio downloads where mp3 download is not available

Version 0.73 - 20080922
* Now remembers which PIDs/programmes have already been downloaded and will prevent downloading them after you delete the programme
* The PID download history file is in ~/.get_iplayer/download_history
* Added --outputradio --outputtv --outputpodcast to override --output so that different directories can be used for different programme types respectively
* Added --list-categories and --list-channels support
* Fixed a bug introduced in version 0.72 which --type=all would only result in --type=podcast

Version 0.72 - 20080919
* time stamping of cache entries
* Added --since option to see what was added since a number of hours ago (using above time stamps)
* --flush now refreshes the cache rather than simply deleting it (retains timestamps)

Version 0.71 - 20080916
* Workaround BBC World Service using non-standard PID format (not starting with b0)
* Workaround BBC World Service HTTP redirects which contain extra whitespace and newlines around RTSP urls which mplayer does not like
* Workaround BBC World Service where mediaselector metadata sets XML element kind="" instead of kind="audio"

Version 0.70 - 20080916
* Added BBC World Service to iPlayer radio channels list

Version 0.69 - 20080915
* Remove empty download file if download fails
* Make all program info output go to stdout unless --stdout is specified

Version 0.68 - 20080911
* Added quotes to file= arg of mplayer for post-transcode wav option - breaks if there is a space in the path
* Added rudimentary support for vlc to download/stream N96 iPlayer streams (lower quality 192kbps streams) using --n96 option
* Added --vlc option to specify path to vlc (for N96 streams)

Version 0.67 - 20080910
* streaminfo option now gets Nokia N96 rtsp stream URL (not just the URl that points to it)
* streaminfo option now makes all other functions quiet and sets --get and --test
* Added all audio, subtitles, iphone and wii stream info to streaminfo option
* quiet option can now be overridden by verbose or debug options

Version 0.66 - 20080909
* Changed --rtmp to --streaminfo
* --streaminfo now gets Nokia N96 rtsp stream URL also

Version 0.65 - 20080909
* Created ability to have system-wide default configs for options (/etc/get_iplayer/ and '<allusersprofile>\get_iplayer\' on Win32)
* Moved windows system/personal config dirs to <allusersprofile>\get_iplayer\ and <profile>\.get_iplayer\
* System-wide options can be overridden by the personal options and cmdline options

Version 0.64 - 20080909
* Tweaked to get home directory (USERPROFILE) in ActivePerl
* Renamed --freevo as --symlink (still backwards compatable)
* Added ability for ActivePerl/Windows to transcode radio programmes to mp3 after downloading (thanks Simon Dible)

Version 0.63 - 20080908
* Added code to resolve rtmp url for future use (--rtmp returns the urls)

Version 0.62 - 20080902
* Added ID3 tagging for radio downloads (uses lame)

Version 0.61 - 20080901
* Subtitles can now be downloaded if available using --subtitles option and are converted automatically into SubRip (.srt) format
* Subtitles can be offset by a number of milliseconds using --suboffset <ms> (the H.264 streams seem to start a little earlier than the flash video versions)

Version 0.60 - 20080824
* Now can create MythTV streams XML file aswell as Freevo fxd XML (thanks to ear9mrn)
* Added --bandwidth option for rtsp streams (thanks to nrq)
* Removed world writable perms on cache files
* quiet option now works properly with radio downloads

Version 0.59 - 20080813
* de-duplication of search/match results

Version 0.58 - 20080813
* quote filenames in helper apps to allow whitespace in filenames for mp3 transcoding
* provide better debug output for radio downloading
* Known issue: mplayer bug means that it cannot accept whitespace in filenames when dumping to wav/pcm files

Version 0.57 - 20080805
* Now use an OPML feed from BBC to get a list of all podcast RSS feeds - no more web scraping
* Fixed thumbnail parsing for podcasts
* Removed obsolete and broken --scrape option
* Fixed category parsing for changed iplayer XML feed format
* Show Categories in --info display

Version 0.56 - 20080804
* Added raw realaudio stream saving support (--raw) which does not require lame (thanks to nrq)
* Added new BBC channel 'BBC HD'
* Improved efficiency of stco atom searching to make slow machines start streaming faster
* Known issue: stdout support for radio wav and raw support can be problematic due to named pipe closing

Version 0.55 - 20080718
* Detect and report lack fo realaudio format for radio programmes

Version 0.54 - 20080717
* Fix rename radio file bug under Activeperl
* Do not catch sigchld, quits prog after first download

Version 0.53 - 20080717
* Fix mkfifo quit under Activeperl

Version 0.52 - 20080716
* Fix inverted logic bug in --wav option
* Fix already exists bug for partially downloaded radio progs
* Use dynamic fifo file so simultaneous downloads can occur for radio
* Use signal handler to clean up temp named pipe file

Version 0.51 - 20080716
* Fallback to wav mod for type=radio if platform doesn't support fifos (e.g. ActivePerl/Windows)
* Added --wav option for radio (i.e. don't transcode to mp3)

Version 0.50 - 20080714
* Removed available time of tv/radio programmes because it was misleading and wrong, --info option should be used instead
* Changed progress calc using file pointer instead of file stat - better for cygwin
* Allow option to specify location of mplayer and lame binaries if not in path (--mplayer and --lame)

Version 0.49 - 20080713
* Re-corrected bad display of download rate calcs (I had a hangover yesterday)

Version 0.48 - 20080713
* changed shell escaping from --command option

Version 0.47 - 20080712
* Corrected bad display of download rate and time remaining calcs => now uses less cpu
* --command option allows user to run a custom command after every successful download using substitution variables (see README.txt)
* Improved --info metadata

Version 0.46 - 20080712
* Can now Index and Download BBC podcast mp3/aac streams using --type=podcast
* Check external programme dependancies
* Use non-shell mknod (POSIX mkfifo)

Version 0.45 - 20080710
* Use HTTP pipelined requests for feeds
* Added info option (--info/-i) to get full programme metadata on searches below 40 matches

Version 0.44 - 20080709
* Add radio one into channels list - sorry!

Version 0.43 - 20080709
* Bugfixed stdout support for radio

Version 0.42 - 20080709
* Now uses channel specific atom feeds from iplayer site by default - scrape is still optional for TV index
* Relocated all cache, cookies, config and namedpipe files into $HOME/.get_iplayer/
* Indexes iplayer Radio programmes
* Added --type to limit search to radio, tv or all (tv is default)
* Radio RTSP stream now transcoded on the fly to mp3 using named pipes
* Added stdout support for radio - still only creates small mp3 file when stdout used?!
* TV and Radio now use separate index cache files that are populated independantly
* Added retry loop for bad cookie detection - dont just fail
* Added --exclude-channel/--exclude-category support
* Added channel name to html output
* Known issue: BBC has an error in their atom feeds which says that the programme has been available longer than it has.
* Known issue: stdout support for radio only creates small mp3 file, lame stalls
 
Version 0.41 - 20080708
* Fixed cookie deletion bug

Version 0.40 - 20080707
* Fixed saving of thumbnail url in cache
* Added audio pid download/convert support (downloads rtsp and converts to mp3)

Version 0.39 - 20080707
* Download File name fixed in scrape mode - episode appeared twice
* Image thumbnail url was wrong in scrape mode
* html option never looked for a filename

Version 0.38 - 20080707
* Updates to allow downloading after the BBC updated their website - kludged for now using scrape method until I can work out the atom feed again
* Category/channel searching (and fxd channel menus) and duration listing will be broken until atom feeds get fixed.
* Programme version is broken - different URL now used for signed versions etc. Only Original versions are listed for now.
* Added --terse listing mode
* Don't display version, duration, channel and categories if we use scrape mode

Version 0.37 - 20080703
* Made fxd and html output formats optional with ability to specify output filenames
* --fxd output now has 3 menu modes channel->progname->episode (--fxd-channels), progname->episode (--fxd-names), alpha->progname-episode (--fxd-alpha)
* removed type=video attribute from fxd container tags
* Now encode/decode xml entities for output
* --stdout option now implies --get

Version 0.36 - 20080701
* Now use the --get/-g option to get the selected files, without this we only list matches
* Re-use cookie for faster connections (no need to get web bugs every time)
* Fixed download rate calc on 32M block downloads
* Increased LWP timeouts to 20 seconds
* Checks for when we get a duff moov atom length (i.e. an XORed file) then deletes the cookie and quits
* Removed XML::Twig parser - use perl regex instead
* Now reports how long ago rather than date made available...

Version 0.35 - 20080630
* Restructured downloading code
* Now handles different versions better (i.e. Original, Signed) - tries to download next avaiable version type if one fails
* Freevo FXD now has programmes sorted by channel

Version 0.34 - 20080629
* Fixed duplicate listing bug when using --long
* Added --quiet option
* Added freevo symlink creation option --freevo
* FXD file for freevo now uses standard Video plugin with a player wrapper script
* Use logger function instead of print

Version 0.33 - 20080627
* Now gets programme categories and channel from Atom feed
* Only write the fxd and html files when writing cache
* Channel and category search (regex) --channel --category
* Fixed options saving/reading
* Added download progress for Atom feed and movie header

Version 0.32 - 20080626
* Now uses Atom feed rather than scraping website for programme info (much more reliable availability info)
* Now requires Perl XML::Twig
* Reduced cache expiry to 4 hrs (atom feed is now quicker to download and is more up to date)
* version pid (pid) is no longer used for reference - only programme pid (urlpid) == $pid
* Index now contains duration and start of availability date/time (Atom method only)
* Allow fallback to scraping website for programme index
* Removed deprecated XOR decoding

Version 0.31 - 20080624
* Allow user to save options and specify default options in $HOME/.iplayerrc
* Now uses long options also

Version 0.30 - 20080622
* Generate FXD file for Freevo iplayer streaming plugin
* Now can resume downloads and strema to STDOUT simultaneously (streaming always starts from beginning of programme)
* Retry loop for getting index pages incase BBC site breaks like it just did
 
Version 0.29 - 20080619:
* Fixed streaming + file download mode
* Added random numbers after some requests more like iphone
* Added interrim checking of reported mp4 stream availability
* Reduced index cacahe default to 12 hours

Version 0.28 - 20080619:
* Update get_iplayer option (-u)

Version 0.27 - 20080619:
* New option to allow streaming while downloading AND writing file to disk (allows you to watch while downloading while keeping a copy for later)
* Sanity check to ensure we don't stream partially downloaded content

Version 0.26 - 20080618:
* Fixed partial download resuming
* Changed file suffix for partially downloaded files to <prog>.partial.mov to ease playback of partially downloaded movies 

Version 0.25 - 20080618:
* Automatically re-arrange the atoms so that file can be streamed and start faster (used method from qt-faststart.c, v0.1 by Mike Melanson, melanson@pcisys.net)
* Option -x allows STDOUT streaming during download (see usage)
* All messages now go to STDERR

Version 0.24 - 20080618:
* Now supports downloading of *unencrypted* streams from BBC Iplayer site - no more XOR nonsense
* Downloads web bugs to whitelist our cookies on BBC servers
* Downloads the file in blocks to avoid XOR

Version 0.23 - 20080617:
* added binmode for decode sub also for windows to work properly

Version 0.22 - 20080616:
* Detect null Content-Length header upon download - doesn't replace a partially d/loaded file if there is a failure

Version 0.21 - 20080616:
* Added binmode for Windows file writing - fixes bug where windows would not decode properly

Version 0.20 - 20080615:
* Remaining time reported in hrs/mins/secs
* Added sort-into-subdirectories option to create subdirectories for programmes

Version 0.19 - 20080614:
* Fixed PID searching
* Now supports restarting downloads of incomplete files
* Fixed swap detection bug where moov atom started on even byte offset
* Remaining time added
* Fixed kbps (not misreported kBps anymore)

Version 0.18 - 20080613:
* Auto detection of byte-swapping
* Auto detection of XOR sequence

Version 0.17 - 20080612:
* Non-UK error detection
* Not available error detection

Version 0.16 - 20080612:
* Fixed HTML output links 
* Sanitized data structures
* Now parses days/hours left
* Fixed XOR % completion calculation
* Reads IPLAYER_OUTDIR environment

Version 0.15 - 20080611:
* Fixed duplicate programme removal
* Now supports different programme type downloads (i.e. Original, Signed, etc)
* Changes hashes to give more meaningful names
* Test option (-t) will now determine the programme type
* Increased speed of XOR decoder by reading in 1024 blocks at a time

Version 0.14 - 20080611:
* Not using curl anymore - seems to fail through some firewalls mysteriously and will not work on Ubuntu
* Using LWP for all http requests
* Fixed indexing sort bug

Version 0.01 - 20080312
* Initial Release