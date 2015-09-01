## get_iplayer 2.93-2.94  Release Notes

## Read this first

get_iplayer 2.94 was released shortly after 2.93 to fix a bug that broke live streaming for BBC News, BBC 6 Music and BBC 1Xtra. There were no other changes in 2.94. If you already installed 2.93 and do not require live streaming for the above stations, updating to 2.94 is not necessarily required.  However, all users are strongly advised to do so.

## New/Changed

### 1. TV listing feeds

On 02/06/2015 the BBC removed the listing feeds used by get_iplayer to populate the TV programme data cache used to support searching.  get_iplayer has now switched to using BBC schedule data instead.  This is what you need to know:

- If you added `--refresh-feeds-tv=schedule` to your preferences as a temporary measure to support the web pvr, remove it now from the command line with:
    
        get_iplayer --prefs-del --refresh-feeds-tv=schedule

- Refreshing your TV data cache will be **MUCH** slower than before.  Remember this especially if you use `--refresh-future`, which doubles the indexing time. The schedule parsing is based on old code inherited from the original version of get_iplayer, but hopefully it should improve a bit in future releases.
- Programmes unique to local BBC One variants are not indexed by default.  This reduces the indexing time by about half at the expense of a handful of programmes, many of which are local news cut-outs.  If you wish to index the BBC One local variants, use `--refresh-exclude-groups-tv=none`.
- You may find some TV programmes in search results that are older than 7 days.  This is because the schedule data used for indexing goes back to the beginning of the previous calendar week.
- You may find some TV programmes in search results that are older than 7 days and no longer available (e.g., films). You may also find some future programmes that are not yet available.  This hopefully should be improved in a future release.
- Fewer TV programmes will be indexed.  The TV schedule data does not contain old archive programmes lurking in the iPlayer site.  It also does not contain programmes broadcast exclusively on red button streams, some of which formerly may have been available.  It also does not include web-only programmes ("BBC iPlayer Exclusives").  Only programmes in the broadcast channel schedule listings will be indexed.
- You can no longer search TV programmes for signed or audio described versions. Those flags are are not included in the schedule data. That facility is unlikely ever to return. However, you should still be able to download those versions where available.
- You can no longer search TV programmes by category. Category information is not included in the schedule data. That facility is unlikely ever to return. Category information will not appear in search results (for the present a blank space will be displayed).
- Programmes broadcast exclusively on red button streams that were formerly available to get_iplayer will no longer be available.

**REMEMBER**: Any programme not in your data caches (and thus not found in your search results) should still be available with `--pid <PID>` or `--url <URL>`.

### 2. Live TV and radio streaming

On 02/06/2015 the BBC removed some metadata resources used by get_iplayer to locate live streams.  get_iplayer has been repaired to work around this problem.  Live streaming should work as before, though not all streams have been tested.

### 3. XML::Simple Perl module now required

On 02/06/2015 the BBC removed some metadata resources (XML playlists) formerly used by get_iplayer to extract media stream identifiers for on-demand programmes.  From 2.91, those resources were only used as a backup in the event that you did not have the XML::Simple Perl module installed.  That backup mechanism no longer works, so now you must have the XML::Simple module installed. Without the module you will see this error:

    WARNING: Please download and run latest installer or install the XML::Simple Perl module for more accurate programme metadata.
    ERROR: Failed to get version pid metadata from iplayer site

The XML::Simple module is provided by the Windows installer and is part of the system Perl in OS X.  Linux/Unix users should consult the installation instructions (see below). 

### 4. Other changes

- Added support for BBC One/Two Northern Ireland/Scotland/Wales live streams.  HD streams are available for BBC One variants, but BBC Two variants are SD only. To access those streams with a search string, you must full spell out which region you want, e.g., `get_iplayer --get --type=livetv "BBC One Scotland"`.
- Added support for HD TV programmes available via HLS (`--mode=hlshd`).
- The `--playlist-metadata` option is now ignored and will be removed in the next release.

## Fixed

- Fixed "Not a SCALAR reference at get_iplayer.pl line 7099" errors. There should no longer be any need to use `--exclude-supplier=akamai` or `--exclude-supplier=limelight` to work around those errors.
- Fixed problem with future repeat overwriting previous broadcast of same programme in cache data.
- Fixed problem with downloading "open subtitles" programme versions with embedded subtitles (e.g., opera broadcasts).

## Details

[Issues closed in get_iplayer 2.93](https://github.com/get-iplayer/get_iplayer/issues?q=is%3Aclosed+milestone%3A2.93+sort%3Acreated-asc+)

[Commit log for get_iplayer 2.93](https://github.com/get-iplayer/get_iplayer/compare/v2.92...v2.93)

[Issues closed in get_iplayer 2.94](https://github.com/get-iplayer/get_iplayer/issues?q=is%3Aclosed+milestone%3A2.94+sort%3Acreated-asc+)

[Commit log for get_iplayer 2.94](https://github.com/get-iplayer/get_iplayer/compare/v2.93...v2.94)

## Notes

### What about radio?

For the moment, radio listing feeds are unaffected.  Your radio programme data cache should be populated the same as before, with the previous 7 days of programmes only. But also as before, you still cannot search radio programmes by category. That facility is unlikely ever to return.

### So what next?

The next release of get_iplayer will switch to using BBC schedule feeds for both TV and radio programme data.  This will be used to provide full 30-day programme data caches. To compensate for the slower indexing time, you will have some additional flexibility in specifying which channels to index.

Given the potential size of 30-day caches, both the CLI and web PVR will, if possible, be changed to only display search results if an explicit search string is entered, i.e., no more display of the entire TV data cache by default.

Hopefully, BBC schedule data will remain available for the foreseeable future.  But given the BBC's propensity for information arson, that can't be taken for granted. Moreover, the BBC will be making further changes to iPlayer this year, so at least some parts of get_iplayer could be rendered inoperable at any time.

#### Nitro: If you build it but then bar the door, will they still come?

You may have read about Nitro, the BBC's newish all-singing, all-dancing programme metadata API.  The latest Nitro announcement, which also announced the imminent death of the TV listing feeds (Dynamite):

http://www.bbc.co.uk/blogs/internet/entries/bc82562e-ea9d-4655-982d-e6219b2c877b

After nearly two years, Nitro has still not been opened to outside developers, though it may be opened up later this year.  Even so, Nitro is not an option for get_iplayer, at least not directly.  The terms and conditions (and the BBC) prevent direct access to Nitro services by get_iplayer. 

In its present form, get_iplayer must rely on the BBC schedule data or, if it should come to the worst, rely on scraping the iPlayer site. Scraping is one possible way to return category information and signed/audiodescribed flags to the programme data caches, but there are no plans to implement it.

## Install/Upgrade

Installation information for all platforms can be found here:

<https://github.com/get-iplayer/get_iplayer/wiki/installation>

#### Linux/Unix

Linux/Unix packages are maintained by volunteers and may not be updated for a short time after a new release of get_iplayer.  Until then, use the manual installation instructions at the link above.  

#### Windows

Windows users should use the most recent installer to update:

<http://www.infradead.org/get_iplayer_win/get_iplayer_setup_latest.exe>

The installer will update the following components to the indicated versions:

|Component|Version|Notes|
|---------|-------|-----|
|get_iplayer main scripts|2.94|includes both CLI and Web PVR Manager|

**After installing, you must immediately refresh all your cache data:**

    get_iplayer --refresh --type=tv,radio,livetv,liveradio

For the Web PVR, select the equivalent "Programme type" options and click "Refresh Cache".  After the refresh, de-select the options you don't want to use for searching.

## More Information

See [get_iplayer wiki](https://github.com/get-iplayer/get_iplayer/wiki)