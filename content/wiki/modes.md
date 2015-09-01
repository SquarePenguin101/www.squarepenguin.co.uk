## get_iplayer Recording Modes

BBC iPlayer makes programmes available at several levels of video and audio quality.  get_iplayer represents each video/audio quality level with an alphanumeric code, referred to as a "mode".  You may have seen references to these: "flashvhigh", "flashaudio". etc.  Each mode corresponds to a set of media streams available from the BBC.  You can find details of recording modes later in this document.  

get_iplayer 2.83 and higher use a simplified system of recording mode shortcuts that should be sufficient for most users.  You are encouraged to use the mode shortcuts if at all possible.  You may still specify your own custom mode settings if you wish.

## Shortcuts 

Recording mode shortcuts use a simple system with four possible values: "good", "better", "best" and "default" (synonym for "better").  The mode shortcuts are used as values for the `--modes` parameter of the get_iplayer CLI (command-line interface), the **modes** option in your preferences or the **Recording Modes** field in the get_iplayer WPM (Web PVR Manager).

### You Need to Know This

If you are upgrading from get_iplayer 2.82 or earlier, be aware that the *default* recording mode - the mode used if you do not supply a value - has changed.  Beginning with get_iplayer 2.83, the default recording mode is set to download the best available SD video for TV programmes (flashvhigh).  get_iplayer 2.82 and earlier download lower-quality video (flashhigh) by default.  In practical terms, that means that after you upgrade from 2.82 or earlier your downloads will be nearly twice as large and take nearly twice as long (given constant bandwidth) as with the previous default mode setting.  See the next section for instructions on restoring the pre-2.83 behaviour.

WPM users:  If you saved a previous value of the **Recording Modes** field as your default it will still be honoured after upgrade.  However, after you upgrade to WPM 2.83 or higher you are strongly encouraged to set the **Recording Modes** field to one of the mode shortcuts as described in the next section and set the new value as your default.

### Choosing Your Mode

The easiest way to decide which shortcut to use is to answer a few simple questions:

- Do you want the default behaviour, which is to download the best available SD video for a single TV programme?

	CLI: `get_iplayer --modes=default [...]`

	NOTE: `--modes=default` can be omitted for the CLI since it is, well, the default.

	WPM: Enter "default" (without quotes) in **Recording Modes** field and click **Apply Settings**, then record programme.

	NOTE: **Recording Modes** may not be left blank.
	
- Do you *always* want the default behaviour, which is to download the best available SD video for all TV programmes?

	CLI: `get_iplayer --prefs-add --modes=default`

	NOTE: It is not necessary to set this preference for the CLI  since it is, well, the default.

	WPM: Enter "default" (without quotes) in **Recording Modes** field and click **Save As Default**

	NOTE: **Recording Modes** may not be left blank.

- Do you want to download HD video (if available) for a single programme?

	CLI: `get_iplayer --modes=best [...]`

	WPM: Enter "best" (without quotes) in **Recording Modes** field and click **Apply Settings**, then record programme.

	NOTE: Best available SD video will be downloaded if HD video not available.

- Do you *always* want to download HD video (if available) for all TV programmes?

	CLI: `get_iplayer --prefs-add --modes=best`

	WPM: Enter "best" (without quotes) in **Recording Modes** field and click **Save As Default**

	NOTE: Best available SD video will be downloaded if HD video not available.
	
- Do you want to revert to pre-2.83 default behaviour and download lower-quality video for a single programme?

	CLI: `get_iplayer --modes=good [...]`

	WPM: Enter "good" (without quotes) in **Recording Modes** field and click **Apply Settings**, then record programme.

- Do you *always* want to revert to pre-2.83 default behaviour and download lower-quality video for all TV programmes?

	CLI: `get_iplayer --prefs-add --modes=good`
	 
	WPM: Enter "good" (without quotes) in **Recording Modes** field and click **Save As Default**

#### What About Radio?

get_iplayer downloads the best available quality for all radio programmes regardless of the mode shortcut used.  You can override this behaviour by using specific mode values (see below).

#### Show Me the Modes

See [below](#shortcut-expansions) for details of how shortcuts are expanded into mode lists.

## Recording Mode Details

The characteristics for all recording modes are shown below for reference: [TV](#tv-modes), [Radio](#radio-modes)

The recording quality for programmes is set by one of the mode options shown in the following table.  Note that you can set separate modes for each get_iplayer programme type. If no type-specific mode is defined, the **modes** option (if supplied) will be used.  If you use the **modes** option, take care to supply recording modes appropriate to the  type(s) of programmes you are downloading.  For example, using `--modes=flashhd` in a command to download a radio programme will prevent the download from succeeding.

Mode values are supplied as a comma-separated list of values which get_iplayer processes from the left to right.  The first mode found that matches an available media stream will be used for the download.  If the  download for the first mode fails, subsequent modes will be used.

A few examples:

- Set all recording modes (TV and Radio) explicitly to download best quality available:

		get_iplayer --get 123 --modes=flashhd,flashvhigh,flashhigh,flashstd,flashnormal,flashlow,flashaachigh,flashaacstd,flashaudio,flashaaclow,wma

- Record a single TV programme at the lowest quality available:

		get_iplayer --get 123 --tvmode=flashlow,flashstd,flashhigh,flashvhigh,flashhd

- Make a live radio recording in WMA format, with fallback to AAC format:

		get_iplayer --type=liveradio --liveradiomode=wma,flashaac "Radio 3"

- Record at a lower bit rate for speech radio programmes:

		get_iplayer --get 123 --type=radio --radiomode=flashaaclow

- Set a preference to *only* record the highest-quality (HD and SD) TV programmes, with no fallback to lower-quality video:

		get_iplayer --prefs-add --tvmode=flashhd,flashvhigh


#### Mode Options

|Options file|Command line|Description|
|------------|------------|-----------|
|modes|--modes &lt;mode&gt;,&lt;mode&gt;,...|Recording modes.  See --tvmode and --radiomode for available modes and defaults. Shortcuts: default,good,better(=default),best. Use --modes=best to select highest quality available (incl. HD TV).|
|tvmode|--tvmode &lt;mode&gt;,&lt;mode&gt;,...|TV recording modes: flashhd,flashvhigh,flashhigh,flashstd,flashnormal,flashlow,hlshd,hlsvhigh,hlshigh,hlsstd,hlslow. Shortcuts: default,good,better(=default),best,rtmp,flash,hlsbest,hls. (Use &#39;best&#39; for HD TV.) (&#39;default&#39;=flashvhigh,flashhigh,flashstd,flashlow)|
|radiomode|--radiomode &lt;mode&gt;,&lt;mode&gt;,...|Radio recording modes: flashaachigh,flashaacstd,flashaaclow,hlsaachigh,hlsaacstd,hlsaaclow. Shortcuts: default,good,better(=default),best,rtmp,flash,flashaac,hls,hlsaac,ddl,ddlaac. (&#39;default&#39;=flashaachigh,flashaacstd,flashaaclow)|
|livetvmode|--livetvmode &lt;mode&gt;,&lt;mode&gt;,...|Live TV recording modes: hlshd,hlssd,hlsvhigh,hlshigh,hlsstd,hlslow. Shortcuts: default,good,better(=default),vbetter,(incl. SD),best. (Use &#39;best&#39; for HD/SD TV.)(&#39;default&#39;=hlsvhigh,hlshigh,hlsstd,hlslow)|
|liveradiomode|--liveradiomode &lt;mode&gt;,&lt;mode&gt;,...|Live Radio recording modes: hlsaachigh,hlsaacstd,hlsaacmed,hlsaaclow,shoutcastaachigh,shoutcastmp3std. Shortcuts: default,good,better(=default),best,hls,hlshaac,shoutcast,shoutcastmp3. (&#39;default&#39;=hlsaachigh,hlsaacstd,hlsaacmed,hlsaaclow)|

<a name="tv-modes"></a>
### TV Modes

Below are representative values for recordings made with each of the TV recording modes.

|Recording Mode|Access Method|Video Codec|Video Resolution|Video Bitrate|Audio Codec|Audio Bitrate|Overall Bitrate|
|--------------|-------------|-----------|----------------|-------------|-----------|-------------|---------------|
|**flashhd**|RTMP streaming|H.264|1280 x 720|2301 kbps|AAC|96 kbps|2400 kbps|  
|**flashvhigh**|RTMP streaming|H.264|832 x 468|1404 kbps|AAC|96 kbps|1505 kbps|  
|**flashhigh**|RTMP streaming|H.264|640 x 360|700 kbps|AAC|96 kbps|801 kbps| 
|**flashstd**|RTMP streaming|H.264|640 x 360|416 kbps|AAC|96 kbps|516 kbps|  
|**flashnormal**|RTMP streaming|H.264|512 x 288|672 kbps|AAC|128 kbps|841 kbps|  
|**flashlow**|RTMP streaming|H.264|512 x 288|304 kbps|AAC|96 kbps|404 kbps|  
|**hlshd**|HLS streaming (live)|H.264|1280 x 720|3500 kbps|AAC|128 kbps|3643 kbps|  
|**hlshd**|HLS streaming|H.264|1280 x 720|2800 kbps|AAC|128 kbps|2128 kbps|  
|**hlssd**|HLS streaming (live)|H.264|1024 x 756|2000 kbps|AAC|128 kbps|2081 kbps|  
|**hlsvhigh**|HLS streaming|H.264|832 x 468|1404 kbps|AAC|96 kbps|1496 kbps|  
|**hlshigh**|HLS streaming|H.264|640 x 360|700 kbps|AAC|96 kbps|801 kbps| 
|**hlsstd**|HLS streaming|H.264|640 x 360|416 kbps|AAC|96 kbps|516 kbps|  
|**hlslow**|HLS streaming|H.264|512 x 288|304 kbps|AAC|96 kbps|404 kbps|  

<a name="radio-modes"></a>
### Radio Modes

Below are representative values for recordings made with each of the radio recording modes.

|Recording Mode|Source|Access Method|Audio Codec|Audio Bitrate|Notes|
|--------------|------|-------------|-----------|-------------|-----|
|**flashaachigh**|Radio 3|RTMP streaming|AAC|320 kbps|Radio 3 only| 
|**flashaacstd**|National Radio|RTMP streaming|AAC|128 kbps||
|**flashaaclow**|National Radio|RTMP streaming|AAC|48 kbps||
|**hlsaacstd**|National Radio|HLS streaming|AAC|128 kbps||
|**hlshaaclow**|National Radio|HLS streaming|AAC|48 kbps||

<a name="shortcut-expansions"></a>
### Shortcut Expansions

The tables below detail how recording mode shortcuts are expanded into lists of mode values.

#### TV Shortcuts

|Shortcut|Modes|Notes|
|--------|-----|-----|
|**good**|flashhigh,flashstd,flashnormal,flashlow||
|**better**|flashvhigh + 'good'||
|**best**|flashhd + 'better'||
|**default**|synonym for 'better'||
|**flash**|same as 'default'|for backwards compatibility|
|**rtmp**|same as 'default'|for backwards compatibility|
|**hlsgood**|hlshigh,hlsstd,hlslow||
|**hlsbetter**|hlsvhigh + 'hlsgood'||
|**hlsbest**|synonym for 'hlsbetter'||
|**hlsdefault**|synonym for 'hlsbetter'||
|**hls**|synonym for 'hlsdefault'||

#### Live TV Shortcuts

|Shortcut|Modes|Notes|
|--------|-----|-----|
|**good**|hlshigh,hlsstd,hlslow||
|**better**|hlsvhigh + 'good'||
|**vbetter**|hlssd + 'better'||
|**best**|hlshd + 'vbetter'||
|**default**|synonym for 'better'||

#### Radio Shortcuts

|Shortcut|Modes|Notes|
|--------|-----|-----|
|**flashaac**|flashaachigh,flashaacstd,flashaaclow||
|**flash**|synonym for 'flashaac'||
|**rtmp**|same as 'flash'|for backwards compatibility|
|**good**|synonym for 'flashaac'||
|**better**|same as 'good'||
|**best**|same as 'good'||
|**default**|synonym for 'better'||
|**hlsaac**|hlshaachigh,hlsaacstd,hlsaaclow||
|**hls**|synonym for 'hlsaac'||
|**ddlaac**|ddlhaachigh,ddlaacstd,ddlaaclow||
|**ddl**|synonym for 'ddlaac'||

#### Live Radio Shortcuts

Same as Radio Shortcuts

## Modes and CDNs

BBC iPlayer programmes may be available from more than one content distribution network (CDN).  A CDN is an external provider of media streaming services and infrastructure.  get_iplayer internally differentiates between available CDNs with a number appended to recording modes.  The metadata for a TV programme might show the following:

	modes:    default: flashhd1,flashhd2,flashhigh1,flashhigh2,flashlow1,flashlow2,flashstd1,flashstd2,flashvhigh1,flashvhigh2,subtitles1

This indicates that the flash* streams are available from two CDNs. Some radio programmes are only available from a single CDN:

	modes:    default: flashaaclow1,flashaacstd1

The CDNs that correspond to the "1" and "2" may be different for each invocation of get_iplayer.  It is not possible to predict which CDN will be be used for a given recording.  In general it is not necessary to specifically designate a CDN when recording a programme.  If, for example, get_iplayer cannot download the flashhd1 stream, it will roll over to the flashhd2 stream and retry the download.  

**NOTE:** get_iplayer does not roll over to another CDN when recording live streams.

There may be times when the #1 CDN is not responding properly or rejecting connections.  You can force the use of the #2 CDN by explicitly setting your recording modes with the "2" appended.  An example:

	get_iplayer --get 123 --tvmode=flashhd2,flashvhigh2

Be aware that the #2 CDN in your second attempt may correspond to the problematic #1 CDN from the previous download attempt, so a few retries may be required to get a connection to the working CDN.

<a name="external-programs"></a>
## External Programs

The table below shows the external programmes required to download and - if applicable - convert and tag files produced from each combination of recording mode and output format used by get_iplayer.

|Type|Mode|Format|rtmpdump|ffmpeg|mplayer|atomicparsley|id3v2/MP3::Tag|
|----|----|------|--------|------|-------|-------------|--------------|
|TV|flashhd, flashvhigh, flashhigh, flashstd, flashnormal, flashlow|mp4 (h264/aac)|X|X|---|X|---|
|TV|flashnormal|avi (h264/aac)|X|X|---|X|---|
|TV|flashhd, flashvhigh, flashhigh, flashstd, flashnormal, flashlow (with --raw)|flv (h264/aac)|X|---|---|---|---|
|TV|flashhd, flashvhigh, flashhigh, flashstd, flashnormal, flashlow (with --mkv)|mkv (h264/aac)|X|X|---|---|---|
|TV|hlshd, hlsvhigh, hlshigh, hlsstd, hlsnormal, hlslow|mp4 (h264/aac)|---|X|---|X|---|
|TV|hlshd, hlsvhigh, hlshigh, hlsstd, hlsnormal, hlslow (with --raw)|mpegts (h264/aac)|--|---|---|---|---|
|TV|hlshd, hlsvhigh, hlshigh, hlsstd, hlsnormal, hlslow (with --mkv)|mkv (h264/aac)|---|X|---|---|---|
|Radio|flashaachigh, flashaacstd, flashaaclow|m4a (aac)|X|X|---|X|---|
|Radio|flashaachigh, flashaacstd, flashaaclow (with --raw)|flv (aac)|X|---|---|---|---|
|Radio|flashaachigh, flashaacstd, flashaaclow (with --aactomp3)|mp3|X|X|---|---|X|
|Radio|hlsaachigh, hlsaacstd, hlsaaclow|m4a (aac)|---|X|---|X|---|
|Radio|hlsaachigh, hlsaacstd, hlsaaclow (with --raw)|mpegts (aac)|---|X|---|---|---|
|Radio|hlsaachigh, hlsaacstd, hlsaaclow (with --aactomp3)|mp3|---|X|---|---|X|
|Podcast|podcast|mp3|---|---|---|---|---|