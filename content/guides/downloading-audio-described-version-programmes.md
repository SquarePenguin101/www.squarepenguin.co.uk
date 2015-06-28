+++
categories = ["", ""]
date = "2015-06-26T22:11:53+01:00"
description = ""
draft = false
pageimage = ""
pagesubtitle = "COMPREHENSIVE GUIDES TO GET YOU STARTED QUICKLY"
pagetitle = "get_iplayer Guides and Tutorials"
slug = "downloading-audio-described-version-programmes"
type = "page"
title = "Downloading Audio Described version of programmes"

+++

# Downloading Audio Described version of programmes

* * *

  **UPDATE - 23.06.2015** - It is currently not possible to search for audiodescribed or signed versions of TV programmes using get_iplayer as the BBC has removed that information from their feeds.

You can still download audiodescribed versions, but you'll have to search for them on the iPlayer site to find the PIDs.

For more information, read the [get_iplayer version 2.94 release notes](/wiki/release293/ "get_iplayer 2.89-2.90 Release Notes").

* * *

Downloading an Audio Described programme with get_iplayer is almost identical to downloading a standard show. Make sure you view the TV Download Guide to get an understanding of the basics of downloading a programme.

## Using the `--versions` command

From the [Options Wiki](/wiki/options/) page we see that in order to obtain Audio Described versions of TV programmes we need to use the `--versions` command. get_iplayer doesn't download these versions of the show by default, so we need to manually tell it to do so.

With this command you then use the argument 'audiodescribed' in order to tell get_iplayer to download the signed version of the programme.

It doesn't really matter where in the full download command you place this `--versions` command and its arguments but I usually place it at the end. Lets look at an example:

`get_iplayer --get 123 --versions=audiodescribed`

## Common Errors

If there is no signed version available you will likely see the following error:

```
WARNING: No programmes are available for this pid with version(s): audiodescribed (available versions: default)
```

This is not get_iplayers fault - there simply isn't an Audio Described version of this programme available from the BBC.
