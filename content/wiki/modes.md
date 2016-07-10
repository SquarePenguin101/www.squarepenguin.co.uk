## get_iplayer Recording Modes

### Modes

BBC iPlayer makes programmes available in different streaming formats at multiple levels of video and audio quality. get_iplayer represents each combination of format and quality with an alphanumeric code, referred to as a "mode".  The mode value is a combination of a stream type prefix and bitrate/resolution suffix. You may have seen references to these: "hls" + "hd" = "hlshd", "dash" + "high" = "dashhigh", etc. You can find details of available recording modes [below](#mode-details), though in general you will not need to use them directly. Use shortcuts instead.

### Shortcuts

get_iplayer uses a system of recording mode shortcuts that should work for most users. A shortcut can be a stream type prefix, a quality level, or a combination of the two. A shortcut is expanded into a list of recording modes for get_iplayer to use in selecting which media stream to download. See [below](#shortcut-expansions) for details of how shortcuts are expanded into mode lists.

#### Stream type prefixes

|Prefix|Description|Availability
|------|-----------|-----
|**hls**|Apple HTTP Live Streaming (for mobile devices)|on-demand TV (default), on-demand radio, live radio (default)
|**hvf**|Apple HTTP Live Streaming (for connected TVs)|on-demand TV, live TV (default)
|**dash**|MPEG Dynamic Adaptive Streaming over HTTP|on-demand radio
|**radio**|Combined HLS and DASH|on-demand radio (default)
|**flash** **[DEPRECATED]**|RTMP (Real-Time Messaging Protocol)|on-demand TV and radio
|**shoutcast**  **[DEPRECATED]**|Shoutcast MP3 streaming (cannot be combined with quality levels)|live radio

#### Quality levels

Quality level can be one of five possible values (in order of decreasing bitrate and resolution):

- best
- better
- good
- worse
- worst

The stream type prefixes and quality levels can be combined, e.g. `hlsgood`, `hvfbest`, `dashworst`, but there is rarely any reason to do so. If you specify only a stream type prefix for one of the mode options (e.g., `--tvmode=hvf`), you will download the best available quality for that stream type.  If you specify only a quality level for the value of one of the mode options (e.g., `--tvmode=good`), you will download the best available quality - up to the level specified - in the default format for the given programme type.

The quality level is treated as a maximum. If a stream at the specified level is not available, the best available lower-quality version is used. If you wish to target a specific media stream, use the appropriate mode directly rather than a shortcut value

The mode shortcuts are used for the `--modes`, `--tvmode` and `--radiomode` options of the get_iplayer CLI (command-line interface), the **modes**, **tvmode** and **radiomode** options in your preferences or the **Recording Modes** field in the get_iplayer WPM (Web PVR Manager). Multiple shortcuts can be specified as a comma-delimited list, though that is rarely necessary. Multiple values are processed from left to right.

### Choosing Your Shortcut or Mode

In general, you do not need to specify a shortcut or recording mode. get_iplayer will download the best quality available for the default format for the given programme type. This is usually what you want. If you are using the Web PVR Manager, you should remove any previous setting in the **Recording Modes** field in order to record with the default modes.

There are a few circumstances in which you may need to specify recording modes or shortcuts. Some examples are listed below.

You wish to only record HD video:

    get_iplayer --tvmode=hlshd [...]

You wish to use **hvf** streams in order to record 50 fps HD video when available:

    get_iplayer --tvmode=hvf [...]

You wish to record only the best available 50 fps video:

    get_iplayer --tvmode=hvfhd,hvfsd [...]

You wish to record medium-quality TV, e.g., to save disk storage or if you have poor internet connection:

    get_iplayer --tvmode=good [...]

You wish to revert to the pre-2.95 default for TV programmes **[DEPRECATED]**:

    get_iplayer --tvmode=flashbetter [...]

You wish to always record the worst quality TV streams, e.g., you only want audiodescribed versions and do not need good video resolution:

    get_iplayer --prefs-add --tvmode=worst

This saves the `--tvmode` option in preferences so that it does not need to be specified for each invocation of get_iplayer.

You wish to record medium-quality radio, e.g., for speech programmes:

    get_iplayer --radiomode=good --type=radio [...]

You are using the Web PVR Manager and you wish to record medium-quality TV programmes, but you also wish to record the best quality radio programmes:

> The WPM effectively uses `--modes` behind the scenes, so you will need two shortcuts, one that applies only to radio and one that applies to TV. Enter `radiobest,good` - **the order is important, with radio modes going before TV modes** - in the *Recording Modes* field and click *Apply Settings*, then record your programmes. If you want that to be your new default setting, click *Save As Default* after updating the *Recording Modes* field.

You are using the Web PVR Manager and you wish to record medium-quality radio programmes, but you also wish to record the best quality TV programmes:

> The WPM effectively uses `--modes` behind the scenes, so you will need two shortcuts, one that applies only to radio and one that applies to TV. Enter `radiobetter,best` - **the order is important, with radio modes going before TV modes** - in the *Recording Modes* field and click *Apply Settings*, then record your programmes. If you want that to be your new default setting, click *Save As Default* after updating the *Recording Modes* field.

<a name="mode-options"></a>
## Recording Mode Options

The recording quality for programmes is set by one of the mode options shown in the following table.  Note that you can set separate modes for radio and TV. If no type-specific mode (`--tvmode`, `--radiomode`) is defined, the `--modes` option (if supplied) will be used.  If you use the `--modes` option, take care to supply recording modes appropriate to the  type(s) of programmes you are downloading.  For example, using `--modes=hlshd` in a command to download a radio programme will prevent the download from succeeding.

Mode values are supplied as a comma-separated list of values which get_iplayer processes from left to right, e.g., `--tvmode=hlshigh,hlsstd,hlslow`. The first mode found that matches an available media stream will be used for the download. If the download for the first mode fails, subsequent modes will be tried.

#### Mode Options

Recording modes are configured using the options below. The `--modes` options is applied to all programme types, but is overridden by type-specific options (if specified).

|Options file|Command line|Description
|------------|------------|-----------
|modes|--modes &lt;mode&gt;,&lt;mode&gt;,...| Recording modes.  See --tvmode and --radiomode (with --long-help) for available modes and defaults. Shortcuts: worst,worse,good,better,best
|radiomode|--radiomode &lt;mode&gt;,&lt;mode&gt;,...|Radio recording modes (overrides --modes): dashhigh,dashstd,dashmed,dashlow,flashhigh,flashstd,flashlow,hlshigh,hlsstd,hlsmed,hlslow. Shortcuts: worst,worse,good,better,best,dash,flash,hls. (default=hlshigh,dashhigh,hlsstd,dashstd,hlsmed,dashmed,hlslow,dashlow)
|tvmode|--tvmode &lt;mode&gt;,&lt;mode&gt;,...|TV recording modes (overrides --modes): flashhd,flashvhigh,flashhigh,flashstd,flashnormal,flashlow,hlshd,hlsvhigh,hlshigh,hlsstd,hlslow,flashlow,hvfhd,hvfsd,hvfvhigh,hvfhigh,hvfstd,hvflow. Shortcuts: worst,worse,good,better,best,flash,hls,hvf. (default=hlshd,hlsvhigh,hlshigh,hlsstd,hlslow)
|liveradiomode|--liveradiomode &lt;mode&gt;,&lt;mode&gt;,...|**[DEPRECATED]** Live Radio recording modes (overrides --modes): hlshigh,hlsstd,hlsmed,hlslow,shoutcastmp3std,shoutcastaachigh (R3 only, UK only). Shortcuts: worst,worse,good,better,best,hls,shoutcast. (default=hlshigh,hlsstd,hlsmed,hlslow)
|livetvmode|--livetvmode &lt;mode&gt;,&lt;mode&gt;,...|**[DEPRECATED]** Live TV recording modes (overrides --modes): hvfhd,hvfsd,hvfvhigh,hvfhigh,hvfstd,hvflow. Shortcuts: worst,worse,good,better,best,hvf. (default=hvfhd,hvfsd,hvfvhigh,hvfhigh,hvfstd,hvflow)

<a name="mode-details"></a>
## Recording Mode Details

The characteristics for all recording modes are shown below for reference: [TV Modes](#tv-modes), [Radio Modes](#radio-modes)

<a name="tv-modes"></a>
### TV Modes

Below are representative values for recordings made with each of the TV recording modes.

|Recording Mode|Stream Format|Video Codec|Video Resolution|Video Bitrate|Audio Codec|Audio Bitrate|Overall Bitrate
|--------------|-------------|-----------|----------------|-------------|-----------|-------------|---------------
|**hlshd**|HLS|H.264|1280 x 720|2280 kbps|AAC|96 kbps|2379 kbps
|**hlsvhigh**|HLS|H.264|832 x 468|1404 kbps|AAC|96 kbps|1496 kbps
|**hlshigh**|HLS|H.264|640 x 360|700 kbps|AAC|96 kbps|801 kbps
|**hlsstd**|HLS|H.264|640 x 360|416 kbps|AAC|96 kbps|516 kbps
|**hlslow**|HLS|H.264|512 x 288|304 kbps|AAC|96 kbps|404 kbps
|**hvfhd**|HLS **(50fps)**|H.264|1280 x 720|4780 kbps|AAC|128 kbps|4919 kbps
|**hvfsd**|HLS **(50fps)**|H.264|960 x 540|2719 kbps|AAC|128 kbps|2859 kbps
|**hvfvhigh**|HLS|H.264|960 x 540|1759 kbps|AAC|96 kbps|1496 kbps
|**hlshigh**|HLS|H.264|704 x 396|956 kbps|AAC|96 kbps|801 kbps
|**hvfstd**|HLS|H.264|512 x 288|551 kbps|AAC|96 kbps|516 kbps
|**hvflow**|HLS|H.264|385 x 216|390 kbps|AAC|96 kbps|404 kbps
|**flashhd** **[DEPRECATED]**|RTMP|H.264|1280 x 720|2301 kbps|AAC|96 kbps|2400 kbps
|**flashvhigh** **[DEPRECATED]**|RTMP|H.264|832 x 468|1404 kbps|AAC|96 kbps|1505 kbps
|**flashhigh** **[DEPRECATED]**|RTMP|H.264|640 x 360|700 kbps|AAC|96 kbps|801 kbps
|**flashstd** **[DEPRECATED]**|RTMP|H.264|640 x 360|416 kbps|AAC|96 kbps|516 kbps
|**flashlow** **[DEPRECATED]**|RTMP|H.264|512 x 288|304 kbps|AAC|96 kbps|404 kbps

<a name="radio-modes"></a>
### Radio Modes

Below are representative values for recordings made with each of the radio recording modes.

|Recording Mode|Stream Format|Audio Codec|Audio Bitrate|Notes
|--------------|-------------|-----------|-------------|-----
|**dashhigh**|MPEG-DASH|AAC|320 kbps|UK only
|**dashstd**|MPEG-DASH|AAC|128 kbps|UK only
|**dashmed**|MPEG-DASH|AAC|96 kbps|UK and Intl
|**dashlow**|MPEG-DASH|AAC|48 kbps|UK and Intl
|**hlshigh**|HLS|AAC|320 kbps|live radio only, UK only
|**hlsstd**|HLS|AAC|128 kbps|UK only
|**hlsmed**|HLS|AAC|96 kbps|live radio only, UK and Intl
|**hlshlow**|HLS|AAC|48 kbps|UK and Intl
|**flashhigh** **[DEPRECATED]**|RTMP|AAC|320 kbps|Radio 3 only, UK only
|**flashstd** **[DEPRECATED]**|RTMP|AAC|128 kbps|UK only
|**flashlow** **[DEPRECATED]**|RTMP|AAC|48 kbps|UK and Intl
|**shoutcastmp3** **[DEPRECATED]**|Shoutcast|MP3|128 kbps|live radio only, UK and Intl
|**shoutcastaac** **[DEPRECATED]**|Shoutcast|AAC|320 kbps|live radio only, UK only, Radio 3 only

<a name="shortcut-expansions"></a>
## Shortcut Expansions

The tables below detail how recording mode shortcuts are expanded into lists of mode values.

### TV Shortcuts

|Shortcut|Modes
|--------|-----
|**worst**|synonym for **hlsworst**
|**worse**|synonym for **hlsworse**
|**good**|synonym for **hlsgood**
|**better**|synonym for **hlsbetter**
|**best**|synonym for **hlsbest**
|**hlsworst**|hlslow
|**hlsworse**|hlsstd,hlslow
|**hlsgood**|hlshigh,hlsstd,hlslow
|**hlsbetter**|hlsvhigh,hlshigh,hlsstd,hlslow
|**hlsbest**|hlshd,hlsvhigh,hlshigh,hlsstd,hlslow
|**hls**|synonym for **hlsbest**
|**hvfworst**|hvflow
|**hvfworse**|hvfstd,hvflow
|**hvfgood**|hvfhigh,hvfstd,hvflow
|**hvfbetter**|hvfvhigh,hvfhigh,hvfstd,hvflow
|**hvfbest**|hvfhd,hvfsd,hvfvhigh,hvfhigh,hvfstd,hvflow
|**hvf**|synonym for **hvfbest**
|**flashworst** **[DEPRECATED]**|flashlow
|**flashworse** **[DEPRECATED]**|flashstd,flashlow
|**flashgood** **[DEPRECATED]**|flashhigh,flashstd,flashlow
|**flashbetter** **[DEPRECATED]**|flashvhigh,flashhigh,flashstd,flashlow
|**flashbest** **[DEPRECATED]**|flashhd,flashvhigh,flashhigh,flashstd,flashlow
|**flash** **[DEPRECATED]**|synonym for **flashbest**

### Live TV Shortcuts

|Shortcut|Modes
|--------|-----
|**worst**|synonym for **hvfworst**
|**worse**|synonym for **hvfworse**
|**good**|synonym for **hvfgood**
|**better**|synonym for **hvfbetter**
|**best**|synonym for **hvfbest**
|**hvfworst**|hvflow
|**hvfworse**|hvfstd,hvflow
|**hvfgood**|hvfhigh,hvfstd,hvflow
|**hvfbetter**|hvfvhigh,hvfhigh,hvfstd,hvflow
|**hvfbest**|hvfhd,hvfsd,hvfvhigh,hvfhigh,hvfstd,hvflow
|**hvf**|synonym for **hvfbest**

### Radio Shortcuts

|Shortcut|Modes
|--------|-----
|**worst**|hlslow,dashlow
|**worse**|hlslow,dashlow
|**good**|hlsmed,dashmed,hlslow,dashlow
|**better**|hlsstd,dashstd,hlsmed,dashmed,hlslow,dashlow
|**best**|hlshigh,dashhigh,hlsstd,dashstd,hlsmed,dashmed,hlslow,dashlow
|**radioworst**|synonym for **worst** applied only to radio
|**radioworse**|synonym for **worse** applied only to radio
|**radiogood**|synonym for **good** applied only to radio
|**radiobetter**|synonym for **better** applied only to radio
|**radiobest**|synonym for **best** applied only to radio
|**dashworst**|dashlow
|**dashworse**|dashlow
|**dashgood**|dashmed,dashlow
|**dashbetter**|dashstd,dashmed,dashlow
|**dashbest**|dashhigh,dashstd,dashmed,dashlow
|**dash**|synonym for **dashbest**
|**hlsworst**|hlslow
|**hlsworse**|hlslow
|**hlsgood**|hlsmed,hlslow
|**hlsbetter**|hlsstd,hlsmed,hlslow
|**hlsbest**|hlshigh,hlsstd,hlsmed,hlslow
|**hls**|synonym for **hlsbest**
|**flashworst** **[DEPRECATED]**|flashlow
|**flashworse** **[DEPRECATED]**|flashlow
|**flashgood** **[DEPRECATED]**|flashlow
|**flashbetter** **[DEPRECATED]**|flashstd,flashlow
|**flashbest** **[DEPRECATED]**|flashhigh,flashstd,flashlow
|**flash** **[DEPRECATED]**|synonym for **flashbest**

### Live Radio Shortcuts

|Shortcut|Modes
|--------|-----
|**worst**|synonym for **hlsworst**
|**worse**|synonym for **hlsworse**
|**good**|synonym for **hlsgood**
|**better**|synonym for **hlsbetter**
|**best**|synonym for **hlsbest**
|**hlsworst**|hlslow
|**hlsworse**|hlslow
|**hlsgood**|hlsmed,hlslow
|**hlsbetter**|hlsstd,hlsmed,hlslow
|**hlsbest**|hlshigh,hlsstd,hlsmed,hlslow
|**hls**|synonym for **hlsbest**
|**shoutcast** **[DEPRECATED]**|shoutcastaac,shoutcastmp3

## Modes and CDNs

BBC iPlayer programmes may be available from more than one content distribution network (CDN).  A CDN is an external provider of media streaming services and infrastructure.  get_iplayer internally differentiates between available CDNs with a number appended to recording modes.  The metadata for a radio programme might show the following:

	modes:    original: dashhigh1,dashhigh2,dashstd1,dashstd2,dashmed1,dashmed2,dashlow1,dashlow2

This indicates that the dash* streams are available from two CDNs. Some programmes are only available from a single CDN:

	modes:    original: hlsstd1,hlslow1

The CDNs that correspond to the "1" and "2" may be different for each invocation of get_iplayer.  It is not possible to predict which CDN will be be used for a given recording.  In general it is not necessary to specifically designate a CDN when recording a programme.  If, for example, get_iplayer cannot download the dashhigh1 stream, it will roll over to the dashhigh2 stream and retry the download.

**NOTE:** get_iplayer does not roll over to another CDN when recording live streams.

There may be times when the #1 CDN is not responding properly or rejecting connections.  You can force the use of the #2 CDN by explicitly setting your recording modes with the "2" appended.  An example:

	get_iplayer --get 123 --tvmode=hvfhd2,hvfvhigh2

Be aware that the #2 CDN in your second attempt may correspond to the problematic #1 CDN from the previous download attempt, so a few retries may be required to get a connection to the working CDN.

<a name="external-programs"></a>
## External Programs

The table below shows the external programmes required to download and - if applicable - convert and tag files produced from each combination of recording mode and output format used by get_iplayer.

|Type|Mode|Format|rtmpdump|ffmpeg|atomicparsley|id3v2/MP3::Tag
|----|----|------|--------|------|-------------|--------------
|TV|hlshd, hlsvhigh, hlshigh, hlsstd, hlslow|mp4 (h264/aac)|---|X|X|---
|TV|hlshd, hlsvhigh, hlshigh, hlsstd, hlslow (with --raw)|mpegts (h264/aac)|--|---|---|---
|TV|hlshd, hlsvhigh, hlshigh, hlsstd, hlslow (with --mkv)|mkv (h264/aac)|---|X|---|---
|TV|hvfhd, hvfsd, hvfvhigh, hvfhigh, hvfstd, hvflow|mp4 (h264/aac)|---|X|X|---
|TV|hvfhd, hvfsd, hvfvhigh, hvfhigh, hvfstd, hvflow (with --raw)|mpegts (h264/aac)|--|---|---|---
|TV|hvfhd, hvfsd, hvfvhigh, hvfhigh, hvfstd, hvflow (with --mkv)|mkv (h264/aac)|---|X|---|---
|TV|flashhd, flashvhigh, flashhigh, flashstd, flashlow|mp4 (h264/aac)|X|X|X|---
|TV|flashhd, flashvhigh, flashhigh, flashstd, flashlow (with --raw)|flv (h264/aac)|X|---|---|---
|TV|flashhd, flashvhigh, flashhigh, flashstd, flashlow (with --mkv)|mkv (h264/aac)|X|X|---|---
|Radio|dashhigh, dashstd, dashmed, dashlow|m4a (aac)|---|X|X|---
|Radio|dashhigh, dashstd, dashmed, dashlow (with --raw)|mpegts (aac)|---|X|---|---
|Radio|dashhigh, dashstd, dashmed, dashlow (with --aactomp3)|mp3|---|X|---|X
|Radio|hlsstd, hlslow|m4a (aac)|---|X|X|---
|Radio|hlsstd, hlslow (with --raw)|mpegts (aac)|---|X|---|---
|Radio|hlsstd, hlslow (with --aactomp3)|mp3|---|X|---|X
|Radio|flashhigh, flashstd, flashlow|m4a (aac)|X|X|X|---
|Radio|flashhigh, flashstd, flashlow (with --raw)|flv (aac)|X|---|---|---
|Radio|flashhigh, flashstd, flashlow (with --aactomp3)|mp3|X|X|---|X
|Podcast|podcast|mp3|---|---|---|---
