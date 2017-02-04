+++
categories = ["Updates"]
date = "2017-02-03T00:01:45"
description = "get_iplayer updated to release v2.98."
draft = false
pageimage = ""
title = "get_iplayer v2.98 released"
+++
get_iplayer has been updated to version v2.98. 

This release removes a number of deprecated features. As it's likely the release notes will go unseen, here's a quick rundown of what has been removed :-)

## But first - there is new stuff too!

I don't want it to sound to depressing right off the bat, so there is new stuff too so go and check it out:

[https://github.com/get-iplayer/get_iplayer/wiki/release298#newchanged](https://github.com/get-iplayer/get_iplayer/wiki/release298#newchanged)

## And on to the stuff that's been removed...
<!--more-->
The features below were deprecated in get_iplayer 2.95 and have now been removed in get_iplayer v2.98.

- Any remaining support for news/sport videos, other embedded media, archive sites, special collections, educational material, programme clips or any content other than whole episodes of programmes broadcast on BBC linear services within the previous 30 days, plus episodes of BBC Three programmes posted within the same period (though BBC Three programmes are not searchable).
	- Some excluded content will still be downloadable via PID or URL, but such use is no longer supported. If downloading those items via PID or URL should stop working in the future, get_iplayer will not be modified to restore access.
	- Recursive downloading is still supported, but if for some reason any episodes older than 30 days can no longer be downloaded, get_iplayer will not be modified to restore access.
	- Programme clips are no longer included in recursive downloading. Although many will still be downloadable via PID or URL, such use is no longer supported. If downloading clips via PID or URL should stop working in the future, get_iplayer will not be modified to restore access.
	- For content not supported by get_iplayer try [youtube-dl](https://rg3.github.io/youtube-dl/).
- The `podcast` programme type
	- You can use a web browser or podcatcher application for BBC podcasts
	- BBC podcasts are found at <http://www.bbc.co.uk/podcasts>
	- A full OPML directory is at <http://www.bbc.co.uk/podcasts.opml>
	- If you prefer the podcast edit of a radio programme, use `--version=podcast` with get_iplayer
- The `localfiles` programme type
- Streaming and recording of live programmes
	- If you don't like the BBC/Radioplayer streaming service, live radio stream links can be found at: <http://www.radiofeeds.co.uk/query.asp?feedme=BBC> 
	- If you know of a similar resource for live TV stream links (FilmOn doesn't count), post it in the [support forums](https://squarepenguin.co.uk/forums).
	- If you have a DIY bent and you speak Perl, the test harness for HLS streams in [this gist](https://gist.github.com/dinkypumpkin/7dd022d20838dd4a840b32dd919ead9c) will show you how to retrieve and/or construct live stream links.
- Streaming of on-demand programmes
	- Includes removal of "Play" links in Web PVR search results
	- Web PVR can still stream downloaded programmes
- ID3 metadata tagging
- Built-in support for alternative media output formats or containers (MP3/AVI/MKV)
	- See custom command examples in documentation for some alternatives
	- There are many applications available that can convert get_iplayer output files to MP3/AVI/MKV
	- CLI converters can be used with `--command`
- Built-in support for alternative metadata formats (Kodi/Freevo/MythTV)
	- See custom command examples in documentation for alternative method to create Kodi .nfo files
- Built-in support for alternative search results formats (HTML/Freevo/MythTV)
- Multimode recording
- Symbolic linking of output files
- Option to use ffmpeg for downloads
- Customisation of ffmpeg options for remux
	- You can still do custom remuxing with `--command`
- Email functions
- Some obsolete tagging options (replaced by auto-configuration) - see `--tag-*` options in list below
	- Use the `--tag-format-show` and `--tag-format-title` options to customise programme/episode names in tags.
- File name sanitisation options (replaced by uniform naming scheme)
	- All file names are now ASCII-only, with most punctuation removed.
	- All dates in episode titles are now converted to YYYY-MM-DD format for use in file names

#### Options removed

With the removal of deprecated features, the following options have been removed. An error will be generated if you attempt to use these on the command line. A warning will be printed if any of these are found in saved preferences.

```
--aactomp3
--avi
--email
--email-password
--email-port
--email-security
--email-sender
--email-smtp
--email-user
--fatfilename
--ffmpeg-liveradio-opts
--ffmpeg-livetv-opts
--ffmpeg-radio-opts
--ffmpeg-tv-opts
--fxd
--hfsfilename
--hls-ffmpeg
--hls-ffmpeg-encode
--hls-liveradio-opts
--hls-livetv-opts
--hls-radio-opts
--hls-tv-opts
--html
--id3v2
--isodate
--keep-all
--listplugins
--liveradio-intl
--liveradio-uk
--liveradiomode
--livetvmode
--localfilesdirs
--mediaselector
--mkv
--mp3vbr
--multimode
--mythtv
--non-ascii
--nowrite
--outputliveradio
--outputlivetv
--outputlocalfiles
--outputpodcast
--pid-recursive-noclips
--player
--punctuation
--shoutcast-liveradio-opts
--stdout
--stream
--symlink
--tag-cnid
--tag-fulltitle
--tag-hdvideo
--tag-id3sync
--tag-longdesc
--tag-longdescription
--tag-longepisode
--tag-longtitle
--tag-shortname
--xml-alpha
--xml-channels
```

## Full release notes

As this is going to be a pretty big change in get_iplayer land, I recommend really actually reading the release notes this time. 

Really, some stuff you've been using just might stop working (maybe) because certain things have been removed. So here they are:

[https://github.com/get-iplayer/get_iplayer/wiki/release298](https://github.com/get-iplayer/get_iplayer/wiki/release298)

As ever, if you are running into difficulties and can't work out how to get something working, you are welcome over in the [forums](/forums/). Just remember to read up on [How to Submit a Support Request](https://squarepenguin.co.uk/forums/thread-706.html).
