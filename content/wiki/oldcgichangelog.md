get_iplayer.cgi changelog (OLD)
-------------------------------
**(document from original developer)**

**NOTE**: This change log ends at the point get_iplayer was abandoned by its original developer.
It is made available solely for historical reference.

Version 0.70 - 20100226
* Added Back buttons on recordings delete page.
* Made delete page less verbose.
* Changed 'Record' button and links to perform immediate recording in a new browser tab.
* Added 'Queue' button and links to queue programme for PVR recording.

Version 0.69 - 20100130
* Added basic edit support for PVR List entries.

Version 0.68 - 20100129
* Fixed tab logic based on posted options as well as next page.

Version 0.67 - 20100128
* Set the pageno variable to 1 when we do a series/category/channel click otherwise results may be empty.

Version 0.66 - 20100128
* Disable update for win32 due to vista/win7 UAC VirtualStore problems.

Version 0.65 - 20100125
* Lots of cosmetic and layout changes.

Version 0.64 - 20100124
* Fixed problems with html entity encoding with passed search params.
* Added Freevo FXD format into metadata formats.
* Added PVR Hold off period option.
* Currently displayed options tab is no longer saved as default.
* Simplified the tab selection code.
* Fixed a few CSS errors when hiding the options tabs.

Version 0.63 - 20100122
* Added Series, Category and Channel hyperlinks.
* Moved column selectors to options panel.
* Column selections are now saved with settings.
* Added support for future programme schedule searches.
* Delete button now removes thumbnail, subs and metadata files.

Version 0.62 - 20100121
* Integrated improvements in get_iplayer v2.65 using --skipdeleted option.
* Guess URLs of missing thumbnails.

Version 0.61 - 20100120
* Added action bar after programme listings for ease of navigation.

Version 0.60 - 20100107
* Added Series/Episode Numbers to headings.

Version 0.59 - 20091108
* Check for get_iplayer script at start-up.
* Added --before option to GUI

Version 0.58 - 20091107
* Fixed bug where multiple prog types werer being specified when record was clicked.

Version 0.57 - 20091024
* When multi-select Play is used in Search mode, if there is no mode associated with the programme, use the users modes list.
* Force livetv mode to not transcode for stream modes.

Version 0.56 - 20091023
* Updated default modes lists to allow for new flashaachigh, flashaacstd and flashaaclow modes.

Version 0.55 - 20091021
* opml top-level menu mode added for new Squeezecenter plugin.

Version 0.54 - 20091002
* Fixed bug where refresh page didn't correctly set the selected prog types when reloading or forced refresh.

Version 0.53 - 20090924
* Minor UI tweaks to page titles and fixed a few typos.

Version 0.52 - 20090922
* Fixed bug where form.target value was set incorrectly after a pvr run.
* Made bitrate, frame rate and video size options apply to all streaming playback methods except file based playlists.
* 'Refresh Cache' and 'PVR Run' now open sepearate tabs and auto-run according to interval set in preferences.
* Todo: Use of async web requests to refresh caches and run PVR.
* Normal use of the Web interface no longer refreshes the cache - this must now be triggered manually or on a PVR Run

Version 0.51 - 20090920
* Fixed bug when form values are set and submit() is called and upon 'Back' the field is still set - created a js function to backup and restore form in a global hash.
* Made Remote Stream Type into a popup box.
* Fixed 'Play' link on recorded files to create a playlist to play the file streamed from the get_iplayer server.
* Fixed libfaac bitrate to 160k - the maximum supported.
* Fixed bug where apostrophies in prog names or pids caused js errors.

Version 0.50 - 20090919
* Fixed squeezebox wav streaming for liveradio which broke in 0.49.
* Improved and fixed auto-detection for audio flv streaming.

Version 0.49 - 20090918
* Fixed bug where 'Play' links in search mode were not inheriting the modes option.
* Added a Remote Stream Type option to allow user to control what media format gets sent to the media player.
* If Remote Stream Type is set to 'none' then all transcoding is disabled.
* Issue: Play links are causing stream_prog to remux get_iplayer flv output to flv, unavoidable unless we can get the mode in advance of streaming.
* Issue: URL based pids like http://news.bbc.co.uk/1/hi/uk/7875336.stm which have different content at different times need to have a unique id added to pid.

Version 0.48 - 20090918
* Improved Options tabs navigation.
* Simplified a few button labels.
* 'Update Software' now updated get_iplayer also.
* Todo: Read-only mode - i.e. start-up or ENV option to remove all write or PVR changes
* Todo: Add a 'Run' action to each item in the PVR List to allow it to be recorded right away.

Version 0.47 - 20090917
* All recorded or localfiles media can now be streamed remotely - access PVR from anywhere.
* Re-mux mp4/avi/mov files to flv when direct streaming recordings from the web server, this allows remote streaming into a media player.
* Added Reverse Sort preference.
* Added stream transcoding audio bitrate, video size and framerate options for 'Remote Play' streaming.
* Added new Display/Search/Output/Streaming preferences tabs.

Version 0.46 - 20090916
* Rework playlist URLs
* Added support for PlayFile action on pids that are files
* Moved paging and sortng of search results into get_iplayer for better efficiency
* Created functions to build the playlist and stream URLs
* Forced ffmpeg to output stereo regardless of mono source - fixes problems with Squeezebox.
* Added 'Quick URL' box to allow user to either record play any supported iPlayer or BBC video/audio page.
* Known Bug: 'Play' link for Quick URL recordings where the pid is a URL doesn't work
* Todo: Add a way of getting opml URLs (footer link?)

Version 0.45 - 20090914
* Where the recordings history has relative paths, try to convert to absolute paths so that playlists work
* Added 'Create File Playlist' action button to 'Recordings' tab

Version 0.44 - 20090913
* Added 'Delete Selected Recordings' button
* Hide deleted recordings option
* In ACTION=direct mode, use PID=<pid>|<mode> because there may be >1 mode per pid
* Added a preferences page/tab.

Version 0.43 - 20090913
* Added thumbnail, metadata and subtitle download support
* Recording options now get applied with 'Queue'
* 'Recordings' tab now works in non-search pages
* Added filename and mode columns for Recordings list

Version 0.42 - 20090912
* Support https protocol under apache.

Version 0.41 - 20090911
* Added 'Recordings' Tab as a quick way of accessing history, clears a number of search items to make all history show in most recent order.
* History setting is no longer saved as a cookie (please remove this cookie if you have it saved)

Version 0.40 - 20090911
* 'PVR Run' now opens a new tab.
* Added direct streaming/playback of recorded files in the history.

Version 0.39 - 20090911
* Fixed Apache CGI support
* Changed all stream URLs from http://127.0.0.1/METHOD?options to http://127.0.0.1/iplayer?ACTION=METHOD&options - see README-get_iplayer.cgi.txt
* Old stream URLs should still work with embedded web server in addition to new form above.
* Made Output directory override option apply to 'Queued for Recording' and 'Queue'

Version 0.38 - 20090910
* popup a warning if no programmes are selected for some actions.
* Made the info page prettier, made URLs into hyperlinks and display a thumbnail, added Play and Queue buttons
* Added ability to search PVR history of recordings.
* Added tooltips for all options.
* No display of broken thumbnails.

Version 0.37 - 20090909
* Fixed empty modes list for create playlist button.
* Added flashstd mode to default modes list.

Version 0.36 - 20090908
* Added back buttons.
* All PVR manipulation pages now re-list the PVR searches after performing the PVR add/queue/del.
* Improved signal handling.

Version 0.35 - 20090907
* Remove SINCE option from Series link.

Version 0.34 - 20090907
* Created win32 specific command forking subroutings cos windows is rubbish with forking in perl.

Version 0.33 - 20090905
* Added 'Series' link to each listed programme to allow the creation of a PVR record for that series.

Version 0.32 - 20090905
* Improved external command invocation to use IPC::open3 and non-shell where possible
* Latest automated installer 2.2 required for non-Unix platforms

Version 0.31 - 20090813
* Added tooltip help to buttons

Version 0.30 - 20090813
* Modified the items per page list. Now defaults to 10
* Display the Programme Types in a multi-row table for better readability.

Version 0.29 - 20090805
* URL encode all user definable fields that are sent to get_iplayer to improve security
* Changed versionlist to versions for sort and search fields
* Added --listen option for listen address - defaults to 0.0.0.0
* Warn user of insecure remote access capability if 127.0.0.1 is not used for a listen address
* Added script update feature
* Added Queue option for each programme

Version 0.28 - 20090730
* Tweaked Run PVR so that output gets rendered in browser.
* Updated mouse pointers over links and buttons.
* Added iphone and realaudio to the mode list for 'Play' generated playlists.
* New Logo

Version 0.27 - 20090729
* Added a new 'P' link to each programme. Clicking on it opens a player to play the contained M3U playlist.

Version 0.26 - 20090728
* Added ability to create playlist from selected programmes in GUI

Version 0.25 - 20090727
* Added --port, --getiplayer, --debug and --ffmpeg options to replace old cmdline args
* get_iplayer is now searched for in cwd and /usr/bin if not specified using --getiplayer
* Fixed bug where get_iplayer command was not correctly called for plugin evaluation

Version 0.24 - 20090724
* Squeezebox Browseable OPML playlist support
* Add a favourite to Squeezebox e.g. http://<SERVER_IP>:1935/opml?PROGTYPES=radio&MODES=flash,iphone&LIST=channel
* Or for AAC liveradio: http://<SERVER_IP>:1935/opml?PROGTYPES=liveradio&OUTTYPE=wav
* Requires get_iplayer 2.11 or later

Version 0.23 - 20090723
* Playlist generation support - point vlc or mplayer at "http://127.0.0.1:1935/playlist?TYPE=<progtype>"
* Playlist URLs can use the SEARCH='<regex>' syntax to limit the playlist to names of programmes.
* e.g. "http://127.0.0.1:1935/playlist?PROGTYPES=liveradio&SEARCH=' \d '" to limit to liveradio with single digits in names.
* Syntax change for streaming proxy support: 
* e.g. FLAC stream for liveradio: http://localhost:1935/stream?PID=liveradio:bbc_radio_one&MODES=flashaac&OUTTYPE=flac"
* ffmpeg needs to be in the system PATH of the shell that invokes it.

Version 0.22 - 20090722
* Vastly improved streaming proxy support.
* e.g. FLAC stream for liveradio: http://localhost:1935/stream?SEARCH=liveradio:bbc_radio_one&MODES=flashaac&OUTTYPE=flac"
* Can now get high quality WAV streams of flashaac radio and liveradio on a Squeezebox.

Version 0.21 - 20090719
* Updated PVR Manager script with latest options changes.
* PVR Manager now runs better under Win32 - still no streaming.