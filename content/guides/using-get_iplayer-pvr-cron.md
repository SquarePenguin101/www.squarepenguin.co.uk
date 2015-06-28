+++
categories = ["", ""]
date = "2015-06-27T01:42:06+01:00"
description = ""
draft = true
pageimage = ""
pagesubtitle = "COMPREHENSIVE GUIDES TO GET YOU STARTED QUICKLY"
pagetitle = "get_iplayer Guides and Tutorials"
slug = "using-get_iplayer-pvr-cron"
title = "Using the get_iplayer PVR with cron"
type = "page"

+++

# Using the get_iplayer PVR with cron

## Don't Want to Miss that Programme on iPlayer over Christmas?

You know how it gets over the Christmas period; busy visiting relatives and friends, drinking and partying.

The last thing you remember to do is to watch that crucial episode on iPlayer within the minute window of seven days the BBC has kindly granted you.

Now is the time to set up get_iplayer to act as a PVR (you know Sky+, TiVo, series-link, etc, etc)!

get_iplayer can be easily configured to automatically download your favourite BBC TV programmes just like any other PVR except that there are no limits on how many programmes you can 'record' simultaneously (OK, except your broadband speed maybe).

You even get seven days grace when you've forgotten to set up the PVR.

Here is a quick guide to setting it up. I'm assuming you have downloaded and installed get\_iplayer as described [here](installation/).

### Setting up a PVR Search

Use get_iplayer to search for the programme you wish to have downloaded. You can search based on the programme name (and can also limit to specific channels and categories etc). In my example I want to get the upcoming TV episodes of *Doctor Who* so I just type this:

    get_iplayer 'Doctor Who' --type=tv

This results in:

    Matches:
     184:    Doctor Who Confidential: Series 4 – A Noble Return, 'BBC Three', Factual,Arts,Culture & the Media,TV, default
     185:    Doctor Who Confidential: Series 4 – The Italian Job, 'BBC Three', Factual,Arts,Culture & the Media,TV, default
     186:    Doctor Who Confidential – At Christmas, 'BBC Three', Factual,Arts,Culture & the Media,TV, default
     187:    Doctor Who: Series 4 – Partners in Crime, 'BBC One', Drama,SciFi & Fantasy,TV, default
     188:    Doctor Who: Series 4 – The Fires of Pompeii, 'BBC One', Drama,SciFi & Fantasy,TV, default
     189:    Doctor Who – Voyage of the Damned, 'BBC One', Drama,SciFi & Fantasy,TV, default

OK, so I don't want those extra programmes on BBC Three, so I limit my search to BBC One only:

    get_iplayer 'Doctor Who' --type=tv --channel='BBC One'

Now I just get these matches:

    Matches:
     187:    Doctor Who: Series 4 – Partners in Crime, 'BBC One', Drama,SciFi & Fantasy,TV, default
     188:    Doctor Who: Series 4 – The Fires of Pompeii, 'BBC One', Drama,SciFi & Fantasy,TV, default
     189:    Doctor Who – Voyage of the Damned, 'BBC One', Drama,SciFi & Fantasy,TV, default

Now I have the search I want, I can save this to the PVR search list by simply appending the --pvradd option:

    get_iplayer 'Doctor Who' -–type=tv –channel='BBC One' --pvradd='Dr Who'

If you want to list all the searches that you have saved just run:

    get_iplayer --pvrlist

If you want to do some more advanced searches you might want to read [this guide](/wiki/documentation/) for examples.

### Getting the PVR to run Automatically

There is one more thing you need to do to get the downloads to happen automatically. You only need to set this up once. You must ensure that this command runs on your PC on a regular basis:

    /path/to/get_iplayer --pvr

In Unix/Linux/OSX systems this can simply be achieved by adding the following lines to your crontab (run 'crontab -e'). Also, if you have local email delivery capability then you will also receive an email when a programme is downloaded (set MAILTO below accordingly):

    MAILTO=”myemail@mydomain.com”
    0 * * * * /path/to/get_iplayer --pvr  2>/dev/null

This will ensure that the PVR checks for new matching programmes every hour, on the hour.

It might also be prudent to add these options as defaults on your system so that you don't get the Audio Described or Sign Language versions by mistake and also so that you know where the downloaded files will be saved:

    get_iplayer --output='/home/jbloggs/videos/' --version-list=default --prefs-add

And finally, remember that this will only work when your computer is booted up and connected to the Internet!

*Source: linuxcentre.net*<!--more-->
