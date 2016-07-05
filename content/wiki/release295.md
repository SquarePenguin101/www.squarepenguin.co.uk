## get_iplayer 2.95 Release Notes

## Read First

### Unix packagers

- If you don't already do so, use the get_iplayer source tarball from the GitHub repo. See <https://github.com/get-iplayer/get_iplayer/releases/latest> for the link. If you pull from Git, use the [GitHub repo](https://github.com/get-iplayer/get_iplayer) `master` branch. The infradead.org locations are no longer being used.
- get_iplayer no longer references LAME, MPlayer and VLC. You may remove those applications from your package dependencies, if applicable.
- The `packagemanager` option is no longer used and a warning is issued if it is found in options files. You should remove it from the system options file you install with your package. You can omit the system options file altogether if it only contains the `packagemanager` option.
- Several tagging-related options may vary between distros  due to different versions of AtomicParsley available. Those are now automatically determined at runtime and have been deprecated, and thus no tagging options should be included in a system options file.
- See the [options documentation](options) for the list of deprecated options.  Remove any deprecated options from your system options file to avoid warnings being presented to users.
- In general, you should no longer need to deploy a system options file unless you wish to configure AtomicParsley/ffmpeg/rtmpdump binaries that are not installed in $PATH.
- get_iplayer no longer uses any plugin files. You should not install a system `plugins` directory or the `podcast` and `localfiles` plugin files (both now removed from source). You may remove those files from existing installations if you wish, though it is harmless to leave them in place.
- Some obsolete documents have been removed from the get_iplayer source distribution. Please check your package specs and remove any files that are no longer distributed with get_iplayer.
- get_iplayer 2.95 introduces a soft dependency on the XML::LibXML Perl module (for HTML parsing in the event the BBC remove the current XML data sources). Use of XML::LibXML will likely expand in future releases, so please add it to your package dependencies if it is not already pulled in with other Perl XML modules.

### Self-updaters

- The `--update` option is no longer supported and has been removed from get_iplayer. You will need to download and install get_iplayer 2.95+ manually.

## New/Changed

### 1. 30-day cache

get_iplayer now retains programme data in its index cache for up to 30 days.

- **get_iplayer does NOT index 30 days of programme listings every time the cache is updated** - it indexes no further back than the beginning of the previous calendar week. This means that you must update your cache each calendar week for a month after installation in order to build up a full 30 days of programme data. From then on, the 30-day buffer should be maintained as long as you update the cache at least once per calendar week.
- No programme is retained in the cache for longer than 30 days, regardless of how long it is available from the iPlayer site.
- Some programmes will expire from the cache in less than 30 days. For example, TV news bulletins generally expire after 1 day and week-ahead weather forecasts expire after 7 days. Films also generally expire in less than 30 days.
- Whenever a cache file is updated, the previous version is now saved in your profile directory with `.old` appended to the file name. If you encounter any problems, you can restore the previous cache file by copying the `.old` backup over the current version.
- Local BBC One variants are once again indexed by default. If you wish to reduce indexing time, you can exclude them with `--refresh-exclude-groups-tv=local`
- BBC schedule data is now also used for indexing radio programmes, which means that updating the radio cache will be noticeably slower. If you wish to reduce indexing time and you don't require local radio programmes, you can exclude them with `--refresh-exclude-groups-radio=local`
- Search results with `--long` show relative expiry date
- Added `--available-since=N` and `--expires-before=N` (where N is in hours) to search for recently available or soon-to-expire programmes.
- The get_iplayer cache now contains an additional `expires` field containing the programme expiration time in epoch format.
- BBC schedule data is still used for indexing TV programmes, which means:
    - You still cannot search for programmes by category
    - You still cannot search for audio described or signed programmes
    - You still cannot search for web-only or red button programmes
    - Indexing still only covers programmes scheduled for broadcast on BBC linear services. BBC Three, iPlayer exclusives and red button programmes are not indexed.

One caveat: For some reason, the necessary schedule data for BBC Radio Solent is not available. This means that only the previous 7 days of Radio Solent programmes will be indexed, and all of those programmes will be assumed to expire in 30 days. If the schedule data for any other radio stations should disappear, get_iplayer will fall back to the same mechanism for indexing.

### 2. HD now default for TV programmes

You no longer need to use `--tvmode=best` or `--modes=best` to get HD video for TV programmes - it is now the default. If you normally use default options, this means that your TV downloads will roughly double in size, with approximately 1GB required for each hour of HD video. If you wish to return to the previous behaviour and download lower-quality video by default, use `--tvmode=better`.

### 3. New default streaming formats

#### TV

- HLS (HTTP Live Streaming) is now the default format for on-demand TV
- HLS downloads are MPEG-TS (transport stream) files, which can be played by most media players. The files are re-muxed to MP4 by default to make them palatable to AtomicParsley for metadata tagging. Downloading with `--raw` will produce MPEG-TS files.
- RTMP (Flash) format is temporarily still available with `--tvmode=flash`. The previous default setting is available with `--tvmode=flashbetter`.

#### Radio

- A combination of HLS and MPEG-DASH (Dynamic Adaptive Streaming over HTTP) is now the default for on-demand radio. HLS is preferred, but the higher-quality streams for both UK and international users are currently only available in DASH format, so the DASH streams will generally be used.
- 320kbps and 96kbps DASH versions of on-demand radio programmes are now available, in addition to the 128kbps and 48kbps DASH and HLS versions. Non-UK users only have access to 96kbps and 48kbps.
- Some programmes created before the advent of DASH streaming will only be available in HLS format, but this should be transparent to users.
- DASH radio downloads are M4A files, but they are still re-muxed with ffmpeg by default in order to make the files palatable to AtomicParsley for metadata tagging. Downloading with `--raw` will produce M4A files.
- HLS radio downloads are MPEG-TS (transport stream) files, which are by default re-muxed to M4A for tagging. Downloading with `--raw` will produce MPEG-TS files.
- On-demand radio programmes in DASH format are not streamable (`--stream` or `--stdout` options) via ffmpeg. If either of those options is used, get_iplayer will fall back to HLS format. That means that only 128kbps (UK only) and 48kbps versions will be streamed.
- RTMP (Flash) format is temporarily still available with `--radiomode=flash`.

### 4. Video Factory streams

Since the release of get_iplayer 2.94, the BBC has completed the rollout of its Video Factory streams for on-demand TV programmes. These are HLS streams with slightly different bitrates and video resolutions from the default HLS streams (see [recording modes documentation](modes) for details). They are the same as the streams available for live TV. The Video Factory streams are available with the **hvf** prefix (e.g., `--tvmode=hvf`) - think "**H**LS **V**ideo **F**actory".

There are two significant differences to be aware of:

- The Video Factory HD streams are 5Mbps 1280x720 50fps (frames per second), which means downloads are roughly double the size (2 GB per hour of video) of the default 2.5Mbps 1280x720 25fps HD streams. You will have to judge for yourself if **hvf** HD streams are worth the doubled download size and bandwidth usage.
- There is an additional 3Mbps 960x540 50fps stream available, designated as `hvfsd`.

There is one very important limitation: Downloads from Video Factory streams cannot be re-muxed to MP4 by avconv or ffmpeg <2.5. Only ffmpeg 2.5+ appears to work. This is of particular note to users still on old LTS versions of Ubuntu (12.04, 14.04) and Mint (13, 17), and Mageia 5. If you are unable or unwilling to upgrade your system, you will need to acquire a modern version of ffmpeg if you wish create MP4 files from Video Factory streams (you can still download with `--raw`). There may be several alternatives available, but one possible solution is to use a static build of ffmpeg from:

<http://johnvansickle.com/ffmpeg/>

### 5. New Windows installer

The get_iplayer Windows installer has been rewritten and simplified:

- The installer is now self-contained. It does not download additional components, nor does it access the network while running. This should hopefully avoid some problems with anti-virus and anti-spyware packages.
- There are no user-selectable options for installation. The installer performs an "All Users" installation to `C:\Program Files\get_iplayer` [32-bit systems] or `C:\Program Files\get_iplayer (x86)` [64-bit systems]. This should hopefully help to avoid users creating permissions problems when installing under a different user account.
- The installer will append the get_iplayer installation directory to the value of the system PATH environment variable (`%PATH%`). This will allow you to run get_iplayer from any location in a normal command prompt window.
- The path for the embedded Perl distribution (`perl` subdirectory) and the path to the included atomicparsley, ffmpeg and rtmpdump utilities (`utils` subdirectory) are not permanently added to `%PATH%`. They are temporarily added to `%PATH%` only when get_iplayer batch scripts are running.
- The get_iplayer menu shortcut now opens a console window in your home directory (`%HOMEDRIVE%%HOMEPATH%`) rather than in the installation directory.
- The major and minor version of the Windows installation (as shown in control panel) will now track the version of the embedded get_iplayer script.
- The new installer attempts to clean up after flaws in the original installer that could lead to broken installations on multi-user systems, among other things. The cleanup process is described here:

    <https://github.com/get-iplayer/get_iplayer_win32/wiki/cleanup>

- The installer will attempt to preserve any custom output directory configured by a previous installer, but this may not always be possible. Be sure to check any custom output directory after installation with `get_iplayer --show-options` and re-configure if necessary.

### 6. Fallback indexing: For when the BBC plays with matches

Several times in 2016, the BBC has removed the data sources used by get_iplayer. It must be assumed that those outages presage the eventual permanent removal of those data sources, as the BBC have been promising for some time. If/when the data sources disappear again:

- Wait several days before using get_iplayer. **Seriously - just wait**. Earlier outages have lasted less than 3 days, so save yourself some trouble and wait to see if the outage is permanent. Monitor the [support forums](https://squarepenguin.co.uk/forums/) for information.
- Once you are certain the outage is permanent, add the `--ybbcy` option to your preferences at the command line (you cannot do this in the Web PVR Manager):

        get_iplayer --prefs-add --ybbcy

    This is a stopgap measure until a new release of get_iplayer becomes available. If the data resources return, remove the `--ybbcy` option from your preferences:

        get_iplayer --prefs-del --ybbcy

The `--ybbcy` option triggers a fallback mode for indexing programme data and populating the get_iplayer cache. This fallback indexing is intended to keep get_iplayer limping along until a more permanent solution can be found, so it has significant limitations:

- TV indexing will be very, very, very slow (ca. 10 mins or more) because it is based on web scraping of BBC schedule pages. A high-speed connection won't help much because most of the delay lies in page rendering at the BBC end. However, the TV indexing will only run once per calendar week.
- The fallback TV indexing is more prone to errors due to server rendering failures, so you should expect that there may be some gaps in the programme data in your cache.
- Radio indexing will be relatively quick since it reverts to the method used in get_iplayer 2.94. However, that means that radio indexing must be run at least once every 7 days to avoid gaps in the cache.
- If you are indexing both radio and TV, you need to update your cache at least once every seven days. The TV indexing will still only run once per calendar week.
- Local BBC One variants are excluded from TV indexing (as in get_iplayer 2.94)
- The `--refresh-future` option is ignored, so searching of future schedules will not work.
- All programmes will be retained in the cache for 30 days even if they should expire sooner (availability information is not available via web scraping of schedule pages). This means that false positives will appear in search results. Many of these are ephemeral programmes such as newscasts and weather forecasts, but some unavailable entertainment programmes and films will also be returned in search results.

**NOTE: Fallback indexing is NOT SUPPORTED unless and until the BBC permanently removes the data sources used by get_iplayer, and there is no guarantee it will still work when the time comes.**

Experimental: If you use Unix/OS X, you can speed up the fallback TV indexing a bit by installing the `Parallel::ForkManager` Perl module and using the `--index-concurrent` option in conjunction with `--ybbcy`. This implements a crude fork()-based method of indexing multiple channels at one time. Since the necessary Perl module is unlikely to be packaged for your system, concurrent indexing is only suitable for users who manage their own Perl installation and libraries. Even for those users, it is of dubious worth since it will only save you a few minutes once a week. This feature was implemented purely as an experiment and will be removed in a future release. To reiterate: **this is not supported on Windows**.

### 7. Other changes

- HLS and DASH on-demand programmes are now recorded with a built-in downloader rather than ffmpeg. If you encounter a problem with the built-in downloader with HLS streams, you can temporarily revert to using ffmpeg by employing the `--hls-ffmpeg` option (does not apply to DASH).
- BBC Three programmes are now online-only and thus are not indexed by get_iplayer. You can still download BBC Three programmes with `--pid` or Quick URL in the web pvr manager.
- The web pvr manager has had a minor visual makeover (thanks to James Ross for CSS improvements)
- In most cases, it is no longer necessary to use `--type=radio` when downloading on-demand radio programmes with `--pid`. However, an unnecessary search of the TV cache is still performed. If you have any problems, revert to using `--type=radio`. 
- Metadata tags are no longer added to podcasts. The BBC already tags them.
- The `<version>` substitution parameter (used in default file prefix) now always includes the actual programme version downloaded, rather than sometimes using "default" as a catch-all value. This will make it easier to determine if you have downloaded an edited version of a programme.
- No more plugins will be distributed with get_iplayer. The podcast and localfiles plugins have been incorporated into the main get_iplayer script.
- The `--iso-date` option is now set by default. If you wish to revert to the previous behaviour, use `--no-iso-date`.
- Empty `<category>` and `<version>` fields have been removed from default search results. The `<pid>` field is displayed instead.
- BBC One and BBC Two variants are combined under main channel name in cache
- Broadcast versions of radio programmes now selected in preference to podcast versions when default settings are in force
- Added `--tag-only-filename` option to designate target file for `--tag-only`. In general, the simplest way to re-tag a file is:

        get_iplayer --pid=<pid> --tag-only --tag-only-filename="<filename>"

- Added `--pid-recursive-noclips` option to skip programme clips when downloading with `--pid-recursive`.
- Added `--tag-format-show` and `--tag-format-title` options to enable custom formats (using [substitution parameters](documentation#substitution-parameters)) for programme name and episode title, respectively, in tag metadata.
- Quality levels ("worst", "worse", "good", "better", "best") are now utilised in recording mode shortcuts for radio programmes as well as TV programmes. Previously, the highest-quality radio stream was downloaded regardless of level specified. This means you should specify `--tvmode` and `--radiomode` separately if you wish to use different quality levels.
- The `--update` option has been removed. Self-update is no longer supported.
- Removed deprecated `--playlist-metadata` option
- The now-unused options below have been removed. The presence of any of these options in options files will trigger a warning.

        bandwidth
        ddlradioopts
        lame
        livetvuk
        mmsnothread
        mplayer
        packagemanager
        refreshfeeds
        refreshfeedsradio
        refreshfeedstv
        rtmpliveradioopts
        rtmplivetvopts
        vlc
        wav

## Fixed

- Restored support for news and sport sites video clips
- Restored HD live TV streams
- Restored support for live TV URLs
- Fixed problem that caused incorrect subtitles to be downloaded when more than one version was available
- Fixed error caused by multiple series in RDF file (thanks to Alexey Tourbin)
- Fixed problems with encoded entities and relative URLs in HLS playlists
- Fixed podcast feed parsing broken by multi-paragraph item descriptions
- Fixed web pvr manager "Add Search to PVR" failure when search string contained apostrophe

## Details

[Issues closed in get_iplayer 2.95](https://github.com/get-iplayer/get_iplayer/issues?q=is%3Aclosed+milestone%3A2.95+sort%3Acreated-asc+)

[Commit log for get_iplayer 2.95](https://github.com/get-iplayer/get_iplayer/compare/v2.94...v2.95)

## Install/Upgrade

Installation information can be found here:

<https://github.com/get-iplayer/get_iplayer/wiki/installation>

The Windows installer is now available from:

<https://github.com/get-iplayer/get_iplayer_win32/releases/latest>

The previous infradead.org location is no longer used.

## Support Notes

### Windows XP/Vista no longer supported

As far as is known, get_iplayer, its dependencies and the Windows installer still work on XP and Vista. However, if any of those components stop working on XP or Vista, no effort will be made to fix them. Those platforms can no longer be supported by the maintainer.

### Installation documentation reduced

The wiki pages describing package installation for Unix distros have been removed. That documentation can no longer be supported by the maintainer. Similar pages for for MacPorts and Cygwin have also been removed. get_iplayer was never packaged for those platforms.

There is now a summary page listing the available Unix packages, with links to package and repo sites. If you wish to maintain installation documentation on your own site for a Unix distro feel free to insert a link to it at an appropriate place in:

<https://github.com/get-iplayer/get_iplayer/wiki/unixpkg>

## Deprecations

The features below have been deprecated by the maintainer because they are obsolete, unreliable, impede future development or can no longer be supported. They will be removed in a future release of get_iplayer.

- Any remaining support for news and sport site video clips, archived sites, special collections and any other content that is outside the iPlayer catch-up service for programmes broadcast on BBC linear services. In general, you should still be able to access programmes for which you have a PID.
- RTMP (Flash) format media streams. RTMP support will be removed even if it is still offered by the BBC.
- Searching by category and/or version (has been unavailable for a while - this just makes deprecation and removal official)
- The `podcast` programme type
- The `localfiles` programme type
- Streaming and recording of live programmes
- Streaming of on-demand programmes
- ID3 metadata tagging
- Built-in support for alternative media output formats or containers (MP3/AVI/MKV)
- Built-in support for alternative metadata formats (Kodi/Freevo/MythTV)
- Built-in support for alternative search results formats (HTML/Freevo/MythTV/series/terse/tree)
- Multimode recording
- Symbolic linking of output files
- Option to use ffmpeg for on-demand downloads
- Customisation of ffmpeg options for download or remux
- Email functions
- Some obsolete indexing options
- Some obsolete tagging options (replaced by auto-configuration)
- Some file name sanitisation options (replaced by uniform naming scheme)

See the [options documentation](options) for a list of deprecated options. The presence of any deprecated options in saved preferences will trigger a warning when get_iplayer starts. The warnings can safely be ignored - they are simply reminders.

## More Information

See: [get_iplayer wiki](https://github.com/get-iplayer/get_iplayer/wiki)
