## get_iplayer 2.92 Release Notes

## New/Changed

### 1. Live Radio

The BBC has dropped WMA (Windows Media) and Shoutcast AAC live radio streams and replaced them with HLS (HTTP Live Streaming) AAC and Shoutcast MP3 streams.  get_iplayer has been updated to use the new streams.

#### a. HLS

All national, regional and local stations (except World Service) have 4 UK HLS streams: 320k, 128k, 96k, 48k.  These correspond to the `--liveradiomode` values `hlsaachigh`, `hlsaacstd`, `hlsaacmed`, `hlsaaclow`.  All stations (except World Service) have 2 international HLS streams: 96k and 48k, corresponding to the `--liveradiomode` values `hlsaacmed` and `hlsaaclow`. The streams for all stations escept World Service are available from 2 CDNs.  The World Service has 1 64k stream for UK and international, corresponding to the `--liveradiomode` value `hlsaaclow`.  With no mode setting, get_iplayer will use the best quality available.

The BBC will not publish the HLS stream locations, so get_iplayer must generate at least some of them. In essence, those streams are hard-coded within get_iplayer, so the BBC could change and break them at any time.  get_iplayer normally relies on BBC services to determine your geographic location and provide the appropriate streams.  However, this process becomes more indirect when generating the HLS stream locations.  If you are in the UK and get_iplayer doesn't provide the UK streams, use `--liveradio-uk` to force them to be generated.  This option will not defeat the geo-blocking used with the HLS radio streams.  Conversely, if you are not in the UK and get_iplayer doesn't provide the international streams, use `--liveradio-intl` to force them to be generated.

#### b. Shoutcast

All national, regional and local stations have 1 international Shoutcast stream: 128k, corresponding to the `--liveradiomode` value `shoutcastmp3std`.  The streams are available from 2 CDNs.  Note that these are international streams, so some programmes, e.g., sporting events on 5 Live Sports Extra, are not available.  The BBC have claimed that they will provide a complete set of UK Shoutcast streams, but they have not provided any further information on when or how those streams will be implemented.

The BBC has also temporarily restored the 320k Shoutcast AAC stream for Radio 3.  They claim it will remain in operation at least through the 2015 Proms.  This stream corresponds to the `--liveradiomode` value `shoutcastaachigh`.  The stream is available from 2 CDNs.

Shoutcast streams are not used by default.  If you wish to use Shoutcast streams in preference to the HLS streams, use `--liveradiomode=shoutcast`.  The Radio 3 AAC stream will be used in preference to the MP3 stream.  If you wish to use only MP3 streams, use `--liveradiomode=shoutcastmp3`.

### 2. Live TV

All live TV streams, including HD/SD, are now generated automatically.  As a result, the `--hds-livetv` option is ignored and related code was removed in get_iplayer 2.92.  The option will be removed in 2.93.

At least some live TV streams must be generated internally by get_iplayer, so as with the live radio streams there is a small chance that you may not be presented with the available streams even though you are in the UK.  If that occurs, use `--livetv-uk` to force them to be generated.  This option will not defeat the geo-blocking used with the HLS TV streams.

### 3. On-demand Radio

The BBC has removed WMA streams for on-demand radio programmes.  That should affect few, if any, users.  The BBC also has announced that RTMP streams for on-demand radio programmes will disappear in the future, though no timetable has been given.  For the present, RTMP (i.e., flashaac recording modes) is the default format used by get_iplayer, though the default format will switch to HLS in a future version.

get_iplayer now supports the direct download AAC files that are available for a subset of on-demand radio programmes.  They are .m4a files, but you can use `--aactomp3` to convert them if desired.  Where these files are available, they can be downloaded using `--radiomode=ddlaac`.  These files are not available for many programmes, and may be disappearing, so are not included in the default modes for radio.

The BBC has removed (or hidden) the 320k HLS AAC streams for Radio 3 on-demand programmes.  320k RTMP (Flash AAC) streams are still available.

The `flashaudio` mode (Flash MP3) has been removed.  The BBC no longer uses it for regional and local radio.

### 4. On-demand TV

The BBC is operating a new(ish) CDN for HLS on-demand TV streams.  This CDN is not yet supported by get_iplayer.  As a result, if you are using HLS recording modes for TV programmes, you may find that only one stream is available for each mode rather than the usual two.

### 5. Other

- Restored ability to search for audio described programmes using `--versionlist=audiodescribed` (with default ION data feeds).
- Implemented numbering scheme for programmes with episodes split over multiple broadcasts. A letter is appended to the episode number in `<senum>` (e.g., s18e05a), and the letter is available in `<episodepart>` substitution parameter.  You will probably never encounter this unless you download Silent Witness.
- Added `--exclude-supplier` option.  This has only one potential use: When the Level3 CDN (used only for HD TV streams) is causing problems by dropping connections or truncating downloads (as was the case for most of February), use `--exclude-supplier=level3` to bypass it and use the alternate CDN.
- The `rtsp` recording modes have been removed. The streams are no longer available.
- Programme clips now have full metadata applied.
- Did some minor cleanup of Kodi .nfo metadata output.  See [issue #139](https://github.com/get-iplayer/get_iplayer/issues/139) for details.

## Fixed

- Fixed a problem which caused "No programme versions found" error even though default versions were available.
- Fixed a problem which caused audiodescribed or signed versions of some programmes to be downloaded even though default versions were available.
- Fixed programme runtime value in Kodi/Freevo XML metadata files (now in minutes rather than seconds).  Added `<runtime>` substitution parameter for new value.
- Fixed a Web PVR problem where some Unicode punctation characters caused recording and PVR queuing to fail.
- Fixed a problem that prevented downloading of BBC archive programmes. Archive programmes require the old mediaselector/4 API to locate media streams.  get_iplayer now attempts to do this automatically, but if any archive downloads fail, try again with `get_iplayer --url=<archive page> --mediaselector=4`.
- Fixed a problem where self-update would needlessly fail when get_iplayer script was read-only.
- Fixed missing episode titles for some programmes with `--playlist-metadata`.

## Details

[Issues closed in get_iplayer 2.92](https://github.com/get-iplayer/get_iplayer/issues?q=is%3Aclosed+milestone%3A2.92+sort%3Acreated-asc+)

[Commit log for get_iplayer 2.92](https://github.com/get-iplayer/get_iplayer/compare/v2.91...v2.92)

## Notes

### On `--playlist-metadata`

The `--playlist-metadata` option was implemented as a fallback mechanism to locate stream information and programme metadata in case the new method implemented in 2.91 had any problems.  For a handful of programmes, a bug in 2.91 prevented the stream information from being located ("No programme versions found" error), so `--playlist-metadata` was required to download those programmes.  That problem should be fixed now.  If you use `--playlist-metadata` for every download, don't.  If you have `--playlist-metadata` saved in your preferences, remove it.  If no further related bugs are reported, the `--playlist-metadata` option will be removed in the next release.

### On "default" programme versions

In the BBC metadata, programme versions may have numerous labels: "technical", "original", "shortened", "editorial", etc.  get_iplayer attempts to find the longest one and use it as the "default" version, i.e., the non-signed, non-audiodescribed version of a programme downloaded by default.  The BBC metadata doesn't always support finding the longest version, in which case the first non-signed, non-audiodescribed version found is used as default.  If there is no default version, the signed or audiodescribed version will be downloaded, if present.  Use `--versionlist=default` to prevent a signed or audiodescribed version from being downloaded.  If for some reason a non-signed, non-audiodescribed version exists, but a default version is not detected, you can download a specific version with, e.g., `--versionlist=original`.  Use `--info` to see the versions available.

## Install/Upgrade

Installation information for all platforms can be found here:

<https://github.com/get-iplayer/get_iplayer/wiki/installation>

#### Linux/Unix

Linux/Unix packages are maintained by volunteers and may not be updated for a short time after a new release of get_iplayer.  Until then, use the manual installation instructions at the link above.

#### Windows

Windows users should use the most recent installer to update:

<https://github.com/get-iplayer/get_iplayer_win32/releases/latest>

The installer will update the following components to the indicated versions:

|Component|Version|Notes
|---------|-------|-----
|get_iplayer main scripts|2.92|includes both CLI and Web PVR Manager

After installing, **immediately** refresh all your tv/radio cache data:

    get_iplayer --refresh --type=tv,radio,livetv,liveradio

For the Web PVR, select the equivalent "Programme type" options and click "Refresh Cache".  After the refresh, de-select the options you don't want to use for searching.

## More Information

See [get_iplayer wiki](https://github.com/get-iplayer/get_iplayer/wiki)
