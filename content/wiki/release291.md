## get_iplayer 2.91 Release Notes

## Read This First

Some changes in 2.91 make use of the `XML::Simple` Perl module, used for parsing XML data from the BBC. The module is not yet a hard requirement, so if it is not installed, get_iplayer will print a warning and skip the related sections of code. To reiterate: **the XML::Simple module is NOT required for get_iplayer to function**, though it may be required in a future release.  

The XML::Simple module is installed by the Windows installer.  If you have followed the Linux/Unix/OSX installation instructions in the GitHub wiki, you will have installed the module.  To check if you have the module installed, run the following at a command prompt:

    perl -MXML::Simple -e 1
    
If the command returns without printing an error message, you have the module installed.  If not, use the link below to navigate to the installation instructions for your system.  

## Installation/Upgrade

Installation information for all platforms can be found here:

<https://github.com/get-iplayer/get_iplayer/wiki/installation>

#### Linux/Unix

It may take some time for get_iplayer 2.91 to be packaged for your system.  Until then, use the manual installation instructions at the link above.  

#### Windows

Windows users should use the most recent installer to update:

<http://www.infradead.org/get_iplayer_win/get_iplayer_setup_latest.exe>

From get_iplayer 2.90, the installer will update the following components to the indicated versions:

|Component|Version|  
|---------|-------|  
|get_iplayer main script|2.91|  

## Changes in get_iplayer 2.91

### 1. Metadata changes

The extraction of programme metadata for tagging has been re-implemented to replace the loss of BBC data feeds.  The new implementation relies on the `XML::Simple` Perl module (see above).  If the module is not installed, get_iplayer will fall back to the stopgap metadata implementation introduced in 2.89.  If you wish to revert to the 2.89 metadata implementation explicitly, use `--playlist-metadata`.  

**NOTE:** The 2.89 metadata implementation is likely to be removed in a future release.  At that time, `XML::Simple` and `JSON` modules will become a hard requirement for get_iplayer.  Any such future changes will be announced in advance.

NOTE: You cannot set `--playlist-metadata` in the Web PVR.

#### Brand and series parsing
iPlayer programmes have an associated brand name - a top-level name - and an optional series title that varies from series to series, along with an episode title.  get_iplayer now parses the brand and series titles separately, and there are now `<brand>` and `<series>` substitution parameters for use with `--fileprefix` and `--subdir-format`. The `<brand>` and `<series>` parameters are concatenated as the `<name>` parameter.  Note that `<series>` is not always available. A few examples are shown below:

|brand|series|name|nameshort|episode|episodeshort|  
|-----|------|----|---------|-------|------------|  
|15 Minute Drama|Carol|15 Minute Drama: Carol|15 Minute Drama|1. Episode 1|Episode 1|
|The Archers||The Archers|The Archers|17524. 30/11/2014|30/11/2014|
|Doctor Who|Series 8|Doctor Who: Series 8|Doctor Who|12. Death in Heaven|Death in Heaven|
|Horizon|2000-2001|Horizon: 2000-2001|Horizon|Vanished: The Plane That Disappeared|Vanished: The Plane That Disappeared|

#### Subdirectory naming

If you use `--subdir`, you may find that the subdirectory names in your output directory for anthology series like "15 Minute Drama" become noticeably longer with the brand/series parsing described above, e.g. `15_Minute_Drama_Heinrich_Boll_-_The_Lost_Honour_of_Katharina_Blum`. If you don't like that, use `--subdir-format="<nameshort>"` or `--subdir-format="<brand>"` for shorter subdirectory names.

NOTE: You cannot set `--subdir-format` in the Web PVR Manager.

#### Short episode title used for tagging

get_iplayer is now better able to determine episode numbers for programmes.  This means that episode number prefixes are much more likely to appear in the `episode` field.  As a result, get_iplayer now uses the `episodeshort` field by default for track titles.  Since the episode numbers will be saved in a separate tag, the assumption is that you do not require the episode number in track titles. To change that behaviour, see the new tagging options below.

### 2. New tagging options

Several new tagging options have been introduced to allow more flexibility in populating album/show titles and track titles.  Examples of the new options are shown below using this metadata:

|brand|series|name|nameshort|episode|episodeshort|  
|-----|------|----|---------|-------|------------|  
|15 Minute Drama|Carol|15 Minute Drama: Carol|15 Minute Drama|1.&#160;Episode&#160;1|Episode&#160;1|

Default:

|album/show title|track title|  
|---------------|-----------|
|15 Minute Drama: Carol|Episode 1|


With `--tag-longepisode`: Use `episode` instead of `episodeshort` for track title

|album/show title|track title|  
|---------------|-----------|
|15 Minute Drama: Carol|1. Episode 1|

With `--tag-longtitle`: Prepend `series` (if available) to track title

|album/show title|track title|  
|---------------|-----------|
|15 Minute Drama: Carol|Carol: Episode 1|

Combine `--tag-longtitle` with `--tag-shortname`: Use `nameshort` instead of `name` for album/show title

|album/show title|track title|  
|---------------|-----------|
|15 Minute Drama|Carol: Episode 1|

Another new option has been introduced to allow reformatting dates in track titles.  An example is shown below using this metadata:

|brand|series|name|nameshort|episode|episodeshort|  
|-----|------|----|---------|-------|------------|  
|The Archers||The Archers|The Archers|17524. 30/11/2014|30/11/2014|

Default:

|album/show title|track title|  
|---------------|-----------|
|The Archers|30/11/2014|


With `--tag-isodate`: Use ISO8601 dates (YYYY-MM-DD) in album/show names and track titles


|album/show title|track title|  
|---------------|-----------|
|The Archers|2014-11-30|


NOTE: You cannot set any tagging options in the Web PVR Manager.

### 3. Cache changes

#### Prevent cache file writes if errors encountered in data download

If the new `--refresh-abortonerror` option is set, no changes will be made to a cache file if any of the associated feeds fail to download.  Each feed gets 3 download attempts, and the full URL of the feed is printed on failure. You can use `--refresh-exclude` to temporarily exclude problem feeds, though no programmes for the associated channel will be saved in the cache.

NOTE: You cannot set `--refresh-abortonerror` in the Web PVR Manager.

#### Brand and series parsing

get_iplayer now parses the brand and series titles separately for a programme when populating its cache, similar to the scheme described above for programme metadata.  The brand and series (if present) titles are concatenated to populate the `name` field in the cache. It should now be easier to search for programmes with different brand and series titles without using `--fields=name,episode` or `--long`.  An example:

||name|episode|
|---|----|-------|
|pre-2.91|15 Minute Drama|Carol: Episode 1|
|2.91+|15 Minute Drama: Carol|1. Episode 1|

#### Category information for radio programmes

You can now use `--refresh-feeds-radio=ion` to populate the cache with category information for radio programmes, thus allowing search by category.  However, this comes at a price: The ION feeds are **MUCH** slower that the default radio feeds, many repeats will be missing for Radio 3, Radio 4 and World Service, and virtually all recent programmes from Radio Nan Gaidheal/Cymru/Wales/Foyle/Ulster/2/6Music (and possible others) will be missing.  There may be other yet-to-be-discovered lacunae in the cache data. These alternate feeds were implemented for testing purposes, but use them if you want to do category searches and can live with the limitations. Also keep in mind that the BBC are likely to kill the ION feeds at any time without warning.

You can use `--refresh-feeds-tv=ion`, but it is completely redundant: the ION feeds are already the default for TV.

NOTE: You cannot set `--refresh-feeds{-radio,-tv}` in the Web PVR Manager.

#### Exclude channel groups from cache

As mentioned above, the ION feeds for radio are slow.  If you find them to be particularly slow on your system, you may be able to speed up cache refreshes a bit by excluding groups of channels using the new  `--refresh-exclude-groups-radio` option.  The option accepts a comma-delimited list that may contain any of three values: `national`, `regional`, `local`.  The groups are defined as:

Radio groups

	national: Radio 1-5, World Service, digital-only stations
	regional: Radio Wales/Cymru/Ulster/Foyle/Scotland/Nan Gaidheal
	local   : All other radio

TV groups

	national: BBC One/Two/Three/Four/CBBC/CBeebies/News/Parliament
	regional: BBC Alba, S4C
	local   : All other TV (none at present)

Although you can use `--refresh-exclude-groups-tv`, it will have little effect given the above groupings (unless you actually want to exclude the national channels).

Example: If you were only interested in programmes on national radio stations, you might use: 

	--refresh-exclude-groups-radio="regional,local"

You can also use `--refresh-exclude` to further winnow your cache data selection.  For example, if you were only interested in programmes on national radio stations, but not programmes on the World Service, you could use:

	--refresh-exclude-groups-radio="regional,local" --refresh-exclude="World Service"
	
Note that `--refresh-exclude-groups{-radio,-tv}` are applied **before** `--refresh-include` and `--refresh-exclude`.

NOTE: You cannot set `--refresh-exclude-groups{-radio,-tv}` in the Web PVR Manager.


### 4. HLS recording modes

The BBC have announced that they will be removing WMA and RTMP streams for live and on-demand audio in favour of Apple HLS (HTTP Live Streaming).  They are already using HLS for live/on-demand radio and on-demand TV, and Adobe HDS (HTTP Dynamic Streaming) for live TV, so it's not inconceivable that all RMTP streams may disappear in the near future.  HLS streaming is not yet the default for get_iplayer, except for live TV (see below), but it will be the default - for radio at least - in the near future, so please give it a try so that any problems can be identified. HLS streaming requires `ffmpeg` or `avconv`.

HLS recording modes analogous to the existing Flash modes have been implemented:

	tv     : hlshd hlsvhigh hlshigh hlsstd hlslow 
	radio  : hlsaachigh hlsaacstd hlsaaclow
	aliases: hls hlsdefault hlsbest hlsvbetter hlsbetter hlsgood

The output file formats are the same as for the Flash streams: TV is MP4 with H264 video/AAC audio, radio is M4A with AAC audio.  If you use `--raw` or stop recording manually, you will be left with a `.ts` (MPEG Transport Stream) file in your output directory, not a `.flv` file as with the `flash` modes.

You can use `--aactomp3` with HLS streams. 

#### Caveats

The `hls` modes use the streams employed for mobile devices, so no on-demand HD TV streams are known to be available.  The 320k Radio 3 live stream also is not available. You will need to use the existing `flash` modes to access those streams.

### 5. Live TV

Live TV streaming has been restored.  Before using it, you **must** refresh your livetv cache:

    get_iplayer --refresh --type=livetv

In the Web PVR Manager, select "Live BBC TV" in "Programme types" and click "Refresh Cache".  When the refresh is complete, deselect "Live BBC TV" in "Programme types".

### Live TV with HLS streams

get_iplayer now uses the live TV HLS streams employed for mobile devices.  The same `--modes` aliases (best, default, better, good) can still be used, but there are no longer any `flash` modes for live TV.  Instead, there are equivalent `hls` modes: `hlsvhigh, hlshigh, hlsstd, hlslow`.  Live TV recording produces a `.ts` (MPEG Transport Stream) file in your output directory, not a `.flv` file as with the `flash` modes in earlier releases. The stream formats are still the same: H264 video/AAC audio,

Live TV HD streams via HDS workaround

There are no HD or SD streams available for live TV using the mobile HLS streams described above.  However, it is currently possible to get HD/SD streams for 3 channels (BBC One/Two/Three) by using the `--hds-livetv` option.  Other HD/SD streams may be available in future releases.  The `--hds-livetv` option instructs get_iplayer to use a different data source (HDS manifests - files with stream information) to find the HD/SD streams, which are downloaded via HLS. get_iplayer does not support HDS itself - it merely uses HDS data to find the streams. With `--hds-livetv`, you can use the `hlshd` mode for a HD 1280x720 3500kbps HD stream, and the `hlssd` mode for a 1024x576 2000kbps SD stream. Or simply use the `best` alias. The `--hds-livetv` option requires the `XML::Simple` Perl module described above.  

NOTE: Consider the `--hds-livetv` feature as experimental and subject to removal in a future release. 

NOTE: You cannot set `--hds-livetv` in the Web PVR Manager.

#### Caveats

The live TV streams are re-encoded during download due to problems with timestamp discontinuities in the video stream.  This requires more system resources than merely copying streams over the network.  Although it is now possible to record and stream live TV simultaneously, be aware that you will be encoding 2 streams (1 to disk, 1 to player), which will require yet more system resources.  If your system lacks the necessary horsepower, you may find glitches or gaps in your recording.

If you use `avconv` instead of `ffmpeg`, e.g., on Debian/Ubuntu/Mint, there will be no download progress display during recording of live TV streams by default.  get_iplayer suppresses `ffmpeg/avconv` warning messages related to the above-mentioned timestamp issues. Unlike `ffmpeg`, `avconv` cannot display download progress with those messages suppressed.  You can use `--hls-livetv-opts="-loglevel info"` to see `avconv` progress output, but that will only reveal a continuous stream of warning messages that will swamp the progress display.

As in earlier versions of get_iplayer, recording live TV on Windows is not recommended because the recording won't stop when you close the browser window (Web PVR Manager) or press Ctrl-C (get_iplayer console window).   If you know how to use Task Manager to kill processes, and you know which processes to kill, then you can stop recording that way. This caveat also applies to recording live TV in the Web PVR Manager with `avconv` on other platforms.  You will need to kill the relevant processes from a command prompt.  You will also notice that the Web PVR Manager recording window will fill up with progress messages from `ffmpeg` instead of the more compact display of hash symbols formerly generated by `rtmpdump`.

### 6. Treatment of apostrophes and quotes in `--fileprefix` and `--subdir-format` in options file

Earlier versions of get_iplayer erroneously stripped apostrophes and quotes from `--file-prefix` and `--subdir-format` settings stored in the user options file.  This has been changed in 2.91.  The difference is shown below for this example setting with apostrophes:

        fileprefix '<nameshort> <episodeshort> <pid>'


|version|filename|  
|---------------|-----------|
|pre-2.91| /tmp/BBC_Radio_1s_Essential_Mix_Warp_25_b04t92qd.EXT|
|2.91+| /tmp/'BBC_Radio_1s_Essential_Mix_Warp_25_b04t92qd'.EXT|

The same applies for quotes:

        fileprefix "<nameshort> <episodeshort> <pid>"


|version|filename|  
|---------------|-----------|
|pre-2.91| /tmp/BBC_Radio_1s_Essential_Mix_Warp_25_b04t92qd.EXT|
|2.91+| /tmp/"BBC_Radio_1s_Essential_Mix_Warp_25_b04t92qd".EXT|


Do not use apostrophes or quotes in your options file as shown above.  They are unnecessary, and you almost certainly don't want them in your file or directory names.  Quotes are also illegal in Windows file names and from 2.91 will break get_iplayer downloads if stored in the user options file.  Unfortunately, get_iplayer doesn't prevent you from saving apostrophes or quotes in your options file if you are determined to do so.


### 7. Other changes in get_iplayer 2.91

- Added BBC Sports and S4C programmes to cache data, S4C to live TV
- Added accessibility improvements for Web PVR Manager that make it easier to use with screen readers. The changes are described [here](https://github.com/get-iplayer/get_iplayer/commit/924c54c6e5d0a48bf4de2ab8410f80371f9f2401) and [here](https://github.com/get-iplayer/get_iplayer/commit/6706a3b19a2c7f1096c7615191708a8f8c62743b).  Thanks to J Teh.
- The `<desc>` substitution parameter now contains the brief programme description from the cache.  A new `<desclong>` parameter has been added for the full programme description. Any white space and line breaks are stripped from `<desclong>` in `--info` output, but are retained in the various XML metadata files.
- Added additional thumbnail sizes.  `--thumbsize` can now be in range 1-11 or one of width values in: 86,150,178,512,528,640,832,1024,1280,1600,1920.
- Switched to mediaselector/5 API as default for retrieving stream data.  In the unlikely event you wish to revert to mediaselector/4 API, use `--mediaselector=4`
- get_iplayer now works in Cygwin

## Fixes in get_iplayer 2.91

- Fixed download failures for Strictly Come Dancing and other programmes where main audio/video is preceded by a "competition closed" warning.
- Fixed download failure for Radio 2, 6 Music and regional radio programmes that were removed from the mediaselector/4 API by the BBC.
- Fixed failure to find default version for some archive programmes
- Fixed problem with `--whitespace` being applied to filenames when not configured.
- Fixed incorrect handling of ampersands and semi-colons in Web PVR Manager

## Changelog

The full log of changes since v2.90 can be viewed here:

<https://github.com/get-iplayer/get_iplayer/compare/v2.90...v2.91>