+++
date = "2015-06-24T11:27:34+01:00"
description = "Some of the most commonly asked questions about get_iplayer answered."
draft = false
slug = "faqs"
title = "Frequently Asked Questions • get_iplayer"
type = "page"
pagetitle = "get_iplayer Frequently Asked Questions"
pagesubtitle = "A LIST OF COMMON QUESTIONS..."
+++

## Basic questions

### I'm not in the UK, can I use get_iplayer?

You need a UK IP address to use get_iplayer, just like you would if you used the BBC iPlayer service.

### Does get_iplayer circumvent DRM?

No. get_iplayer does not circumvent any digital rights management security (see the [BBC’s website](http://news.bbc.co.uk/1/hi/technology/6944830.stm) on how to do that with the Windows-only DRM content they provide).

get_iplayer does not circumvent any effective technological measures as the BBC does not implement any such measures.

The BBC uses RTMP, which is a streaming protocol now publicly published by Adobe. Sometimes they use RTMP ‘SWF verification’ which has proven to be ineffective in its current BBC implementation (flvstreamer cannot handle such verification requests so the stream is dropped and is then automatically resumed).

The WMA and RealAudio streams and likewise unprotected. The BBC may at some point choose to effectively protect their streams with DRM or some ‘effective technological measure’ in which case get_iplayer will no longer be a useful tool for those streams.

The BBC do implement DRM on their iPhone and Adobe Air downloadable files and therefore get_iplayer is not useful with those. The BBC iPlayer TV only works in the UK so that they can limit the reach of their output to UK TV Licence fee payers who fund iPlayer (although legally you do not require a licence to watch non-live iPlayer output).

## Installing get_iplayer

1.  [How do I install get_iplayer on Mac OS X?](/guides/mac-os-x-quick-install-guide/)
2.  [How do I install get_iplayer on Windows?](/guides/windowsinstall/)
3.  [How do I install get_iplayer on Ubuntu based Linux?](/wiki/ubuntu/)
4.  [How do I install get_iplayer on other Linux or BSD distros?](/downloads/#more-installation-guides)

## Downloading TV programmes

1. [How do I search for programmes using get_iplayer?](/guides/tv-download-guide/#how-do-i-search-for-programmes-using-get-iplayer)
2. [How do I record a programme with get_iplayer?](/guides/tv-download-guide/#how-do-i-record-a-programme-with-get-iplayer)
3. [Where does get_iplayer save downloaded programmes?](/guides/tv-download-guide/#where-does-get-iplayer-save-downloaded-programmes)
4. [How do I specify or change the quality level of programmes downloaded in get_iplayer?](/guides/tv-download-guide/#how-do-i-specify-or-change-the-quality-level-of-programmes-downloaded-in-get-iplayer)
5. [How do I make sure get_iplayer downloads a TV show and not a Radio programme?](/guides/tv-download-guide/#how-do-i-make-sure-get-iplayer-downloads-a-tv-show-and-not-a-radio-programme)
6. [How do I make sure get_iplayer downloads from the correct channel?](/guides/tv-download-guide/#how-do-i-make-sure-get-iplayer-downloads-from-the-correct-channel)
7. [How do I make get_iplayer automatically rename downloaded programmes?](/guides/tv-download-guide/#how-do-i-make-get-iplayer-automatically-rename-downloaded-programmes)
8. [How do I make get_iplayer automatically rename downloaded programmes for use with XBMC and Plex?](/guides/tv-download-guide/#how-do-i-make-get-iplayer-automatically-rename-downloaded-programmes-for-use-with-xbmc-and-plex)
9. [How do I change or specify where get_iplayer saves downloaded programmes?](/guides/tv-download-guide/#how-do-i-change-or-specify-where-get-iplayer-saves-downloaded-programmes)
10. [How do I permanently change where get_ipayer saves downloaded TV programmes?](/guides/tv-download-guide/#how-do-i-permanently-change-where-get-ipayer-saves-downloaded-tv-programmes)

## Downloading radio programmes

1. [How do I search for radio programmes using get_iplayer?](/guides/radio-download-guide/#how-do-i-search-for-radio-programmes-using-get-iplayer)
1. [How do I record a radio programme with get_iplayer?](/guides/radio-download-guide/#how-do-i-record-a-radio-programme-with-get-iplayer)
1. [Where does get_iplayer save downloaded radio programmes?](/guides/radio-download-guide/#where-does-get-iplayer-save-downloaded-radio-programmes)
1. [How do I specify or change the quality level of radio programmes downloaded in get_iplayer?](/guides/radio-download-guide/#how-do-i-specify-or-change-the-quality-level-of-radio-programmes-downloaded-in-get-iplayer)
1. [How do I make get_iplayer automatically convert radio programmes to MP3?](/guides/radio-download-guide/#how-do-i-make-get-iplayer-automatically-convert-radio-programmes-to-mp3)
1. [How do I change or specify where get_iplayer saves downloaded radio programmes?](/guides/radio-download-guide/#how-do-i-change-or-specify-where-get-iplayer-saves-downloaded-radio-programmes)
1. [How do I permanently change where get_ipayer saves downloaded radio programmes?](/guides/radio-download-guide/#how-do-i-permanently-change-where-get-ipayer-saves-downloaded-radio-programmes)

## Example commands

1.  [get_iplayer Example Commands](/wiki/documentation/)

## <a name="faq1"></a> I see a programme that is available on the iPlayer web site, but I can't find it with a get_iplayer search.  What's wrong?

First ascertain:

1. If you're looking for a radio programme, did you use `--type=radio` in your get_iplayer command?
2. Are you searching for a TV programme with audio description or signing? That functionality is no longer available in get_iplayer, though you can still use `--versions=audiodescribed` or `--versions=signed` when downloading to select the desired version (if available).
3. Are you searching for programmes by category (`--category=...`)? That functionality is no longer available in get_iplayer, though category information is still included in the metadata added to programmes after download.
4. Was the programme actually broadcast on a BBC channel within the last 7 days?  If so, feel free to post a query with the relevant information in the [forums](/forums/).  In the likely event that it was **NOT** actually broadcast on a BBC channel within the last 7 days, read on.

In early October 2014, the BBC made some changes to the iPlayer service and web site that affected get_iplayer.  This is what you need to know:

- If a programme you're looking for does not appear in get_iplayer search results, check it on the iPlayer or iPlayer Radio site **BEFORE** reporting it as an error.
- Web-only and red button programmes are **NOT** available for indexing by get_iplayer and therefore will **NOT** appear in search results. Only programmes scheduled for broadcast on a BBC channel will be indexed.
- Programmes broadcast more than 7 days ago generally are **NOT** available for indexing by get_iplayer and therefore will **NOT** appear in search results.  
- It **DOES NOT MATTER** that a programme is still available on the iPlayer site up to its 30-day expiry.  Once 7 days pass from its last broadcast, it is generally no longer available for indexing by get_iplayer.
- There are a few exceptions to the 7-day rule, such as series like Doctor Who that have a full series catch-up policy. The episodes of those series remain available until the final episode reaches its expiry date.  But again, once 7 days pass from the broadcast of the final episode you should expect those episodes to disappear from the get_iplayer search results.
- From get_iplayer 2.94, some TV programmes > 7 days old and < 14 days old may also appear in search results due to changes in indexing.
- You **MUST** download **ANY** other programme not found in search results directly via PID or URL. If you don't know what that means, it's time to refresh yourself [here](documentation#recording).
- get_iplayer 2.87 or higher is **REQUIRED** to download programmes more than 7 days old via PID or URL.  If you're using your own hacked version of get_iplayer, you'll need to do some more hacking.
- When in doubt, use the programme PID.  All available programmes can be downloaded via PID regardless of whether or not they are in the get_iplayer cache.

        TV: get_iplayer --pid=<PID> ...

        Radio: get_iplayer --pid=<PID> --type=radio ...
