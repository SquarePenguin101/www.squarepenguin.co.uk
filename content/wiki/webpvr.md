# get_iplayer Web PVR Manager

## About

The Web PVR Manager (WPM) is a Web-based search front-end to get_iplayer which allows you, through a web browser, to manage the get_iplayer PVR and start recordings. You are able to search all of the programmes indexed by get_iplayer. It also has a built-in streaming proxy server so you can play get_iplayer content from the web browser or using simple HTTP URLs. It automatically generates OPML and M3U playlists for any programme type so that media players can use the streams.

**THIS IS BETA CODE!!! DO NOT RUN THIS ON AN UNTRUSTED NETWORK**

## Installation

See the [get_iplayer installation page](/wiki/installation) for instructions on how to install and run WPM.  Bear in mind that WPM is a front end for the get_iplayer command-line interface (CLI), so you must install the CLI, its related Perl modules and the necessary external applications along with WPM.  In particular, note that [ffmpeg](http://ffmpeg.org) and [rtmpdump](http://rtmpdump.mplayerhq.hu/) are required for streaming or recording of the Flash streams that comprise the bulk of BBC iPlayer content.

Windows users should download and run the latest [get_iplayer installer](https://github.com/get-iplayer/get_iplayer_win32/releases/latest), which will set up everything you need.  You can launch the WPM from `All Programs -> get_iplayer -> Web PVR Manager` on the Start Menu (`All Apps -> get_iplayer -> Web PVR Manager` on Windows 10) or the `Web PVR Manager` tile in the Windows 8 Start screen.

It is also recommended to install [VLC Media Player](http://www.videolan.org/vlc/) to use with the **Play** links (see below).

## Usage

### DO THIS EVERY TIME YOU RUN THE WEB PVR MANAGER

1. Select the programme types you wish to search by ticking the appropriate **Programme type** boxes in the **Search** tab. Only BBC TV programmes are indexed and searched by default, so you MUST select additional types for them to be included in your search results.

2. Click the **Refresh Cache** button to open a new browser window/tab where the programme data cache will be updated. You MUST do this in order to find the latest programmes in your search results. Leave that window open to automatically refresh the cache at periodic intervals.

### Page Tabs

There are several different tabs along the top of the page:

- **Search** - Shows you a list of all **available** programmes that match your default options. Use any of the search criteria presented, enter a search term then click the **Search** button below (select the **Advanced Search** tab to get more search options).
- **Recordings** - Shows you a list of all **recorded** programmes that match your default options. Use any of the search criteria presented, enter a search term then click the **Search** button below (click **Advanced Search** to get more search options).
- **PVR List** - Shows you a list of currently saved PVR searches or queued recordings (you can delete them from here also)
- **Run PVR** - Runs the PVR immediately in a new tab - make sure you wait for it to fully complete before closing the browser screen. If you do not close the tab it will automatically run the PVR every 4 hours.
- **Update Software** - Updates to the latest PVR Manager script (if it is writable) - make sure you restart the service after doing so. This feature is unavailable in Windows - use the installer and re-install the get_iplayer component to get the latest Web PVR Manager.
- **Help** - Sends you here.

### Action Buttons

There are several different action buttons along the top and bottom of the search results:

- **Search** - Enter your search term in the *Search* field and click this button to execute the search.  You and target your search at a field other than *Name* by changing the value of *Search in*.  Additional search options may found in the **Advanced Search** tab. You can search the PVR recordings history instead of the available programmes by selecting *Search History* in the search panel

> **HEY!** - With the default settings WPM will only search TV programmes.  Select the *BBC Radio* checkbox to add radio programmes to the search results.

- **Record** - Select the checkbox next to the programme(s) you want to record and click this for immediate recording in a separate browser tab.

>**HEY!** - In Linux/Unix/OSX recordings are saved by default in the directory where you started the WPM service. With the Windows installer version of WPM recordings are saved by default in the `iPlayer Recordings` folder on your desktop. You can override this in your get_iplayer preferences, or you may enter a new location in the *Override Recordings Folder* field in the **Recording** settings tab.

- **Play** - Select the checkbox next to the programme(s) you want to playback and click this to download an m3u playlist (you should associate m3u playlists with VLC in your browser for immediate playback).

- **Queue** - Select the checkbox next to the programme(s) you want to record and click this to queue them for when the PVR next runs (i.e.by clicking 'Run PVR').

- **Add Search to PVR** - Once you have added the search terms to get the list of programmes you wish to regularly record, click this button.

>**HEY!** - The queued recordings and PVR searches that you add will only actually be recorded when you click the **Run PVR** button at the top of the page.

- **Refresh Cache** - You must regularly refresh the programme cache to see new programmes. Clicking this button opens another tab or window that refreshes the list of programmes from the online feeds of the selected programme types. If you leave it open it will auto-refresh every hour unless you override the settings.

    **NOTE:** It may take a while to reload page when refreshing caches.

>**HEY!** - Like the man says: Don't forget to refresh your cache before doing a search.

- **Quick URL** - To record or play a BBC iPlayer audio or video URL, paste the programme episode page URL into the *Quick URL* box and click **Play** or **Record**. The correct programme type (BBC TV or BBC Radio) must also be selected.

### Programme Links

#### Actions

- **Play** - Play back a programme by clicking its *Play* link. The *Play* link generates an m3u playlist with a single programme in it. You can associate m3u playlists with VLC for immediate playback.

- **Queue** - Queue a programme for recording by clicking its *Queue*.

- **Record** - Immediately record a programme (opens a new tab) by clicking its *Record* link.

	**NOTE:** Only two recording tabs can work at any one time.

- **Add Series** - Add a programme's whole series (including future episodes) to the PVR by click its *Add Series*.

#### Information

- Click the description text to retrieve full metadata for a programme

- Click any underlined text to search only for that clicked text, e.g., a series name or content category.

- Click a thumbnail image to go to the associated episode web site

- Sort columns by clicking the headings

- Add or remove columns in the search results by selecting checkboxes in the Columns settings tab

## Settings

Settings are grouped into 5 tabs: Advanced Search, Display, Columns, Recording and Streaming.  Hover over any form field with your mouse to see a tooltip with a brief description of its purpose.

>**HEY!** - WPM does not download HD TV (where available) by default out of consideration for users with limited internet bandwidth.  If you wish to download HD TV, change the value of *Recording Modes* in the **Recording** tab to "best" (without quotes).  Use the **Save As Default** button to make the setting permanent (see below).

The settings correspond to options for the get_iplayer CLI.  See [this page](/wiki/manpage) for a full list.  Not all get_iplayer options are available to the WPM.  For those options, get_iplayer uses either its default values or values that have been saved to its user options file with `get_iplayer --prefs-add` (examples [here](/wiki/documentation#saving-settings)).

When you change settings, use the buttons beneath the settings tabs to apply them:

- **Apply Settings** applies the options in settings tabs to the current search.

- **Save As Default** saves the options in settings tabs and a few of the standard settings such as Programme Type. The settings are saved as browser cookies.

- **NOTE:** When using the stream, playlist or play links directly, cookies are not sent and the settings are not applied.

## Streaming

### Direct Streaming URLs

Web PVR Manager allows you to stream audio and video to media player

software such as VLC, mplayer, ffplay and hardware streamers such as the

Logitech Squeezebox by creating URLs for the following:

- Stream BBC iPlayer programmes directly from the Internet as FLV streams

- Stream pre-recorded programmes losslessly or by transcoding on-the-fly

- Stream mp3 files using the localfiles get_iplayer plugin

The [original README](webpvrold) gives examples.

### Automatic Playlist URLs

Web PVR Manager allows you to create M3U playlists on-the-fly from searches to enable you to stream audio and video to media player software such as VLC, mplayer, ffplay and hardware streamers such as the Logitech Squeezebox. These playlist URLs can:

- Create playlists of currently available programmes based on user defined search criteria

- Create playlists of pre-recorded programmes based on user defined search criteria

- Create OPML playlists which can be used to selectively navigate on devices like the Logitech Squeezebox

The [original README](webpvrold) gives examples.

## CGI Deployment

The [original README](webpvrold) contains instructions.

## Relationship to CLI

When you invoke an action in the WPM such as "Search", "Record" or "Add to PVR", behind the scenes the WPM constructs a command string and runs the get_iplayer CLI just as if you typed the equivalent command at a prompt.  However, the WPM was designed as a standalone, simpler - and more limited - interface to get_iplayer, and thus lacks a number of  options available to the CLI.  The WPM also was designed to maintain its own configuration settings separate from preferences set with the CLI using `--prefs-add`.   It is strongly recommended that if you are a WPM user you do all your configuration in the WPM.  However, there are some very particular cases where CLI preferences may be required.  Below is list of considerations to keep in mind if you attempt to use CLI preferences from the WPM.

1. The WPM cannot load, display, or change the values of CLI preferences.  Any settings you save in the WPM are saved for the WPM only.  In order to view or change the values of your preferences, you must use the CLI with `--prefs-show`, `--prefs-add` and `--prefs-del`.

2. Any WPM setting with a non-empty value will override the equivalent CLI preference value.  This is the same as if you override a preference value by adding the equivalent option to the CLI command line.

3. Any WPM setting with a text string value (e.g., "Exclude Channels Containing") will **not** override the equivalent CLI preference if the string value is empty, so it is technically possible (though not advisable) to use the equivalent CLI preference.

4. Any WPM setting with a boolean (on/off) value (e.g., "Refresh Future Schedule") will **always** override the equivalent CLI preference since it always has a value (on or off).  These settings must **always** be made in the WPM.

5. Any WPM setting with a fixed set of possible values (e.g., "Download Metadata") will **always** override the equivalent CLI preference since it always has a value (one of the set). These settings must **always** be made in the WPM.

6. Any CLI preference that does not have an equivalent WPM setting (e.g., "aactomp3") will **always** be used by the CLI when it is invoked from the WPM.

Examples:

1. You may wish to permanently exclude BBC Three from your search results.  To do that, set the necessary preference with the CLI:

		get_iplayer --prefs-add --exclude-channel "BBC Three"

	However, if you enter any value in the "Exclude Channels Containing" setting in the WPM, it will override your CLI preference.  It will **not** be added to it.  It is strongly recommended that you make this and similar settings in the WPM.

2. You may always wish to pull in the following week's listings whenever you refresh your programme cache.  To do that with the CLI, you set the necessary preference:

		get_iplayer --prefs-add --refresh-future

	This preference will **always** be overridden by the WPM.  Instead, you must set "Refresh Future Schedule" = On in the WPM.

3. You may wish to convert all your radio downloads to MP3 automatically.  To do that, set the necessary preference with the CLI:

		get_iplayer --prefs-add --aactomp3

	Since the WPM does not support a "aactomp3" setting - and thus cannot override it - this preference will be used for all radio downloads.

*Source: linuxcentre.net*
