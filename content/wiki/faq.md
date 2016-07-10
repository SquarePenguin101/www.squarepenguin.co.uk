## get_iplayer FAQ

1. **How do I install get_iplayer on Unix/OS X/Windows?**

    See: [get_iplayer Installation](/wiki/installation)

2. **How do I get help with using get_iplayer?**

    See: [Getting Help for get_iplayer](/wiki/help)

3. **I'm a complete noob. Is there a step-by-step guide to using get_iplayer?**

    See: [Guides](https://squarepenguin.co.uk/guides/)

4. **How do I start get_iplayer on Windows?**

    See: [Windows instructions](/wiki/windows)

5. **How do I enter get_iplayer commands on Windows?**

    See: [Windows instructions](/wiki/windows)

6. **How do I search for TV programmes with get_iplayer?**

    See: [Usage and Examples](/wiki/documentation#searching)

    Also see: [TV Guide](https://squarepenguin.co.uk/guides/tv-download-guide/)

7. **How do I record TV programmes with get_iplayer?**

    See: [Usage and Examples](/wiki/documentation#recording)

    Also see: [TV Guide](https://squarepenguin.co.uk/guides/tv-download-guide/)

8. **How do I search for radio programmes with get_iplayer?**

    See: [Usage and Examples](/wiki/documentation#searching)

    Also see: [Radio Guide](https://squarepenguin.co.uk/guides/radio-download-guide/)

9. **How do I record radio programmes with get_iplayer?**

    See: [Usage and Examples](/wiki/documentation#recording)

    Also see: [Radio Guide](https://squarepenguin.co.uk/guides/radio-download-guide/)

10. **How do I change the output directory for get_iplayer recordings?**

    See: [Usage and Examples](/wiki/documentation#filenames-and-directories)

    Also see: [TV Guide](https://squarepenguin.co.uk/guides/tv-download-guide/), [Radio Guide](https://squarepenguin.co.uk/guides/radio-download-guide/)

11. **How do I record TV programmes with audio description?**

    See: [Usage and Examples](/wiki/documentation#recording-versions)

    Also see: [Audio Described Programmes Guide](https://squarepenguin.co.uk/guides/downloading-audio-described-version-programmes/)

12. **How do I record TV programmes with signing?**

    See: [Usage and Examples](/wiki/documentation#recording-versions)

    Also see: [Signed Programmes Guide](https://squarepenguin.co.uk/guides/download-signed-programmes-get_iplayer/)

13. **How do I record a programme using its episode URL?**

    See: [Usage and Examples](/wiki/documentation#recording-url)

    Also see: [TV Guide](https://squarepenguin.co.uk/guides/tv-download-guide/), [Radio Guide](https://squarepenguin.co.uk/guides/radio-download-guide/)

14. **How do I record a programme using its episode PID?**

    See: [Usage and Examples](/wiki/documentation#recording-pid)

    Also see: [TV Guide](https://squarepenguin.co.uk/guides/tv-download-guide/), [Radio Guide](https://squarepenguin.co.uk/guides/radio-download-guide/)

15. **What is a PID?**

    See: [Usage and Examples](/wiki/documentation#recording-pid)

16. **How do I use the PVR functionality in get_iplayer?**

    See: [Usage and Examples](/wiki/documentation#pvr-usage)

    Also see: [PVR Guide](https://squarepenguin.co.uk/guides/get_iplayer-pvr-guide/)

17. **I am outside the UK and I can't download a programme. What can I do?**

    Use of get_iplayer outside the UK is not supported, with the exception of downloading lower-quality (96k and 48k) radio programmes that are available to international users. Do not ask for help downloading TV programmes or higher-quality (320k and 128k) radio programmes from outside the UK. Do not discuss methods to circumvent BBC geoblocking in get_iplayer forums. It doesn't matter what VPN, VPS, HTTP proxy or DNS proxy you use - you may find yourself blocked by the BBC, and get_iplayer can do nothing about it.

18. **I am in the UK, but I am using a VPN, VPS, HTTP proxy or DNS proxy and I can't download a programme. What can I do?**

    Use of get_iplayer with any VPN, VPS, HTTP proxy or DNS proxy - even if you are in the UK - is not supported. If the BBC has blocked you even though you are in the UK, there is nothing get_iplayer can do about it. If your VPN/VPS/proxy is causing download problems, there is nothing get_iplayer can do to work around them.

19. **How do I download HD video for TV programmes?**

    get_iplayer downloads HD video by default if it is available for a TV programme. See [get_iplayer Recording Modes](/wiki/modes) for examples and more information on recording quality settings.
    
20. **I have a poor internet connection and I can't download HD video. How can I download lower-quality video?**

    Specify lower-quality recording mode(s). See [get_iplayer Recording Modes](/wiki/modes) for examples and more information on recording quality settings.

21. **I can't find a programme with a get_iplayer search.  What am I doing wrong?**

    - Did you correctly spell the programme name (or partial name) in your search string?
    
    - Are you searching for a radio programme? If so, did you use `--type=radio` in your get_iplayer command? It is required for searching radio programmes.
    
    - Are you searching for a TV programme with audio description or signing? That search functionality is no longer available in get_iplayer, though you can still use `--versions=audiodescribed` or `--versions=signed` when downloading to select the desired version (if available).
    
    - Are you searching for programmes by category? That search functionality is no longer available in get_iplayer, though category information is still included in the metadata added to programmes after download.
    
    - Was the programme actually broadcast on a BBC linear service? iPlayer Exclusives, archive programmes, red button programmes and BBC Three programmes are not indexed by get_iplayer and thus cannot be searched.
    
    - Was the programme broadcast within the past 30 days? get_iplayer only caches programme index entries for a maximum of 30 days.
    
    - Is the programme a film, newscast or weather forecast? Such programmes, among others, expire in less than 30 days. Films may expire after 1 week and newscasts may expire after 1 day.
    
    - Is the programme actually available on the iPlayer site? Not every programme will be available, or there may be a delay of several days before a programme is made available.
    
    - Have you just installed get_iplayer for the first time? After your first installation of get_iplayer, you much refresh the programme index cache each calendar week for a month in order to build up 30 days of listings. Once that is done, the 30-day buffer will be maintained as long as you refresh once per calendar week.
    
    - Some programmes lack the metadata get_iplayer needs for indexing. These programmes cannot be searched.
    
    - When in doubt, use the programme PID or URL to download a programme directly.  All available programmes can be downloaded via PID or URL regardless of whether or not they are in the get_iplayer index cache.
    
            get_iplayer --pid=<PID> [...]
            get_iplayer --url=<URL> [...]

22. **I can't record a programme with get_iplayer. What am I doing wrong?**

	- If you are recording programmes individually, did you enter the correct episode URL or episode PID?

	- Is the programme actually available on the iPlayer site? Not every programme will be available, or there may be a delay of several days before a programme is made available.
    
    - Can you actually play the programme on the iPlayer site? Sometimes a programme may be listed on the iPlayer site but cannot be played. If a programme is not playable on the iPlayer site, it is probably also not available to get_iplayer.
    
    - Are you outside the UK? Only lower-quality radio programmes are available to international users. Even if you have a VPS, VPN, HTTP proxy or DNS proxy, you may still be blocked by the BBC.
    
    - Are you downloading an RTMP (Flash) stream with rtmpdump?. This method can be unreliable and has been deprecated. Use the default settings (which utilise HLS streams) instead. See [get_iplayer Recording Modes](/wiki/modes) for information on stream types.
    
23. **What does it mean when I get the message "WARNING: No media streams found for requested programme versions and recording modes."?**

    - Are you outside the UK? get_iplayer attempts to detect when the BBC is blocking you, but it doesn't always work. If not, get_iplayer will see that no streams are available, but it cannot know the reason, so only the above message will be displayed.
    
    - It may also mean that the programme is listed on the iPlayer site, but the media streams used by get_iplayer have not been configured on the partner CDN sites.
    
24. **How do I extract audio from a TV or radio programme into an MP3 file?**

    The best solution is to use a separate media converter utility on your downloaded files. You can also use the deprecated `--aactomp3` option (**radio programmes only** - not recommended) or see [custom command examples](/wiki/documentation#custom-commands) in documentation.

25. **How do I repackage audio and video from a TV programme into an MKV file?**

    The best solution is to use a separate media converter utility on your downloaded files. You can also use the deprecated `--mkv` option (not recommended) or see [custom command examples](/wiki/documentation#custom-commands) in documentation.

26. **How do I repackage audio and video from a TV programme into an AVI file?**

    The best solution is to use a separate media converter utility on your downloaded files. You can also use the deprecated `--avi` option (not recommended) or see [custom command examples](/wiki/documentation#custom-commands) in documentation.

27. **How do I create .nfo files for Kodi?**

    Use the deprecated `--metadata=kodi` option (not recommended) or see [custom command examples](/wiki/documentation#custom-commands) in documentation.
    
28. **How do I record an entire series?**

    If the series is still ongoing and episodes are available in get_iplayer search results, then catch up by downloading episodes normally. You can also use the PVR functionality to record an ongoing series. You can download episodes individually via PID or URL if they do not appear in search results. If the series is still available on iPlayer but a large number of episodes have expired from the get_iplayer index cache, see [recursive recording examples](wiki/documentation#recording-recursive) for information on using `--pid-recursive` to perform recursive downloading of all episodes in a series.

29. **What do I do if my anti-virus software identifies the get_iplayer Windows installer, or one of its components, as being infected?**

    Some anti-virus software may flag the installer itself, the generated uninstaller (`uninstall.exe`) or other components as infected, and thus may quarantine or auto-delete those files. Historically, these have always been false positives, but you must check with your anti-virus vendor to be certain. **Do not install get_iplayer if you are at all unsure about the contents of its Windows installer**.

30. **Why does the download progress display show a percentage complete >100%?**

    The file sizes provided in media stream metadata do not match the actual sizes of the downloaded files. Therefore, the calculated percentage complete will be >100% when the actual size is greater than the size in metadata. You should ignore this. If get_iplayer cannot download part of a programme, you will see an error message. Flash streams are not affected.

31. **Should I be concerned when I see the message `non-existing SPS 0 referenced in buffering period` in get_iplayer output?**

    This message comes from the H.264 video decoder in ffmpeg and is printed when re-muxing MPEG-TS files to MP4. As far as is known, the condition flagged by ffmpeg does not have any effect on get_iplayer re-muxing, so you can ignore this message. It can be suppressed with `--quiet`, but you are strongly recommended not to do so because that may suppress other error messages from ffmpeg.

32. **Why does `sudo apt-get install get-iplayer` install an obsolete version of get_iplayer on Ubuntu/Mint?**

    The get-iplayer packages in Ubuntu/Mint repositories usually include obsolete and partially broken versions of get_iplayer. You must use the [get_iplayer PPA](https://launchpad.net/~jon-hedgerows/+archive/get-iplayer) to install get_iplayer on Ubuntu/Mint. See: [Ubuntu installation guide](https://squarepenguin.co.uk/downloads/ubuntu/).
