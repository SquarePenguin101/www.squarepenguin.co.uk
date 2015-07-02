+++
categories = ["", ""]
date = "2015-06-27T01:32:12+01:00"
description = "A complete beginners guide to downloading radio shows with get_iplayer - includes example commands to help you get started quickly & easily."
draft = false
pageimage = ""
pagesubtitle = "COMPREHENSIVE GUIDES TO GET YOU STARTED QUICKLY"
pagetitle = "get_iplayer Guides and Tutorials"
slug = "radio-download-guide"
title = "Beginners guide to downloading radio shows • get_iplayer"
type = "page"

+++

# get\_iplayer Radio Download Guide

This guide has been written in a step by step manner for beginners. If this is your first time here you really must go through the guide in this fashion if you are to understand and get the most out of get\_iplayer.

However, if you are coming back here to use this guide as a reference or just have a specific question, feel free to click on any of the links in the contents below to jump to the relevant section you need.

**NOTE** - Need the full get\_iplayer documentation? Find it in the [Wiki Documentation](/wiki/documentation/).

## Guide Contents

1. [How do I search for radio programmes using get\_iplayer?](#how-do-i-search-for-radio-programmes-using-get-iplayer)
1. [How do I record a radio programme with get\_iplayer?](#how-do-i-record-a-radio-programme-with-get-iplayer)
1. [Where does get\_iplayer save downloaded radio programmes?](#where-does-get-iplayer-save-downloaded-radio-programmes)
1. [How do I specify or change the quality level of radio programmes downloaded in get\_iplayer?](#how-do-i-specify-or-change-the-quality-level-of-radio-programmes-downloaded-in-get-iplayer)
1. [How do I make get\_iplayer automatically convert radio programmes to MP3?](#how-do-i-make-get-iplayer-automatically-convert-radio-programmes-to-mp3)
1. [How do I change or specify where get\_iplayer saves downloaded radio programmes?](#how-do-i-change-or-specify-where-get-iplayer-saves-downloaded-radio-programmes)
2. [How do I permanently change where get_ipayer saves downloaded radio programmes?](#how-do-i-permanently-change-where-get-ipayer-saves-downloaded-radio-programmes)

## How do I search for radio programmes using get\_iplayer?

See: [get\_iplayer v2.90 release notes](/wiki/release289// "get\_iplayer 2.89-2.90 Release Notes") to see how recent changes have impacted get\_iplayer before searching for any programmes.

If you don't know the name of the show your would like to download I would recommend using the BBC iPlayer website to browse for programmes you might enjoy. When you know the name of the show you'd like, we can begin searching.

To have get\_iplayer search for the show we use the following command:

```bash
get\_iplayer --type=radio "Programme Name"
```

It is crucial that you use the " " marks when performing a search containing more than one word. If you don't, you'll either get an error or results will only be relevant to the first word you type.

Get in the habit of using " quotation " marks for each and every search you do. In this case, the above command will search for...

```bash
Programme Name
```

That's is all there is to performing a basic search. I've not needed to use any of the more advanced options, but feel free to leave a comment in the forum if you need help with narrowing down your searches and I'll be happy to help you out.

## How do I record a radio programme with get\_iplayer?

### Using a search string

There are two basic says to download radio programmes with get\_iplayer, one uses the search string and one uses the index number. We can use this search string in combination with the "get" command to download all programmes that match this search string.

This makes more sense when we type it out:

```bash
get\_iplayer --type=radio --get "Programme Name"
```

Once we execute this command, get\_iplayer will begin to download all radio programmes that match this search string. Technically, the search term is a regular expression and acts as a sub-string, so if a programme is called:

```
This is a long programme name for a show
```

Then the above command would download this show, because "programme name" exists in the show name.

This behaviour is useful because it allows you to set up a PVR (explained in the [get\_iplayer PVR Guide](/guides/get\_iplayer-pvr-guide/)) for a programme and it doesn't matter if the name changes slightly over time, such as "Programme Name Series 1" to "Programme Name Series 2" because the search string will still match and the download still run as "Programme Name" is still there.

### Using the Index Number

The second method is to use the index number. We can use this number to tell get\_iplayer to download specific programmes and nothing else. We do so using the following command:

```bash
get\_iplayer --type=radio --get 1234
```

...where 1234 is the index number of the number you want to download. If you want to download more than one specific programme at a time, you can type the index numbers one after the other like so:

```bash
get\_iplayer --type=radio --get 123 1234 12345
```

### The PID

The PID functions very similarly to the index number. To find it you'll need to go to the page on the iplayer website and identify it in the URL (web address) that can be seen in your browsers address bar.

Lets look at an example URL:

```bash
http://www.bbc.co.uk/programmes/b04mctvz
```

The PID in the example above is the seemingly random string of characters `b04mctvz`. In fact, many (possibly all) PIDs start with b0, so you can usually identify the PID pretty easily.

To download the programme using the PID we use the `--pid` command.

An example of the above episode being downloaded in this fashion would be:

```bash
get\_iplayer --pid=b04mctvz --type=radio
```

Don't forget to add `--type=radio` when downloading a radio programme.

### Downloading multiple PIDs

From get\_iplayer v2.90 you can now download multiple PIDs in a single command.

You can now enter multiple PIDs in two ways:

#### Comma-separated list

```bash
get\_iplayer --pid PID1,PID2,PID3
```

#### Multiple `--pid` options

```bash
get\_iplayer --pid PID1 --pid PID2 --pid PID3
```

*(Remember to include `--type=radio` with `--pid` when downloading radio programmes.)*

#### Multiple `--url` options

You can also do the same thing with episode page URLs:

```bash
get\_iplayer --url URL1,URL2,URL3
```

or alternatively...

```bash
get\_iplayer --url URL1 --url URL2 --url URL3
```

*(Remember to include `--type=radio` with `--url` when downloading radio programmes.)*

Prefer `--pid` to `--url` where possible - it is slightly quicker and more reliable. And no, you can't download multiple PIDs or multiple URLs with the Web PVR Manager.

You can use all the other commands throughout this guide along with the `--pid` command to specify the output directory and naming structure etc, just substitute it and the PID in place of `--get` and the search string/index number.

That is all there is to it, nothing too hard as long as you search first and then use the simple commands above to download the programme you want.

So when using the PID method you can still use all the other commands throughout this guide along with the to specify the output directory and naming structure etc.

## Where does get\_iplayer save downloaded radio programmes?

get\_iplayer saves files to your current working directory as a default on both Mac OS X and Linux, whereas it saves programmes to the folder you specified when first installing on Windows.

You can see how to download programmes to a directory (folder) of your choice in the [How do I change or specify where get\_iplayer saves downloaded radio programmes?](#how-do-i-change-or-specify-where-get-iplayer-saves-downloaded-programmes) section.

Click the link to jump there now if you need to, or if this is your first time using this guide simply read on and we'll get to that shortly.

## How do I specify or change the quality level of radio programmes downloaded in get\_iplayer?

As a default, get\_iplayer will download the highest quality version of each radio programme, so you DO NOT need to change anything or use any of the commands below if you are happy with having the highest quality version.

If you want to make get\_iplayer download a lower quality you should use the "--radiomode" command. The code is written like this

```bash
--radiomode=
```

...followed by the desired quality level. The full list of available settings to add to the above command is below:

```bash
default
best
better
good
flashaachigh
flashaacstd
flashaudio
flashaaclow
wma
```

**NOTE** - don't be concerned that the word 'flash' is used. This is purely for technical purposes to differentiate between the streams BBC iPlayer offers. When you download an file, it is automatically converted to AAC format.

The top four options are known as 'mode shortcuts'. You can read a full explanation of these recording modes and their associated quality levels in the [Recording Modes](/wiki/modes/) wiki.

The explanation is beyond the scope of this beginners guide and I recommend you simply use the default settings where you are not required to specify the quality level.

## How do I make get\_iplayer automatically convert radio programmes to MP3?

You can have get\_iplayer automatically convert downloaded radio programmes to .mp3 format by adding the following command when you download a show:

```bash
--aactomp3
```

If you don't want have to add this every time you do a download, you can set it as a global preference that will auto convert every download automatically by simply entering the command below into the command line:

```bash
get\_iplayer --prefs-add --aactomp3
```

This is adding the command to your preferences so it will remember to always perform the conversion, automatically, for every radio download you make.

## How do I change or specify where get\_iplayer saves downloaded radio programmes?

We can set the output path of programmes get\_iplayer downloads on a case by case basis. You _can_ do this globally, but it makes more sense to do this on a programme by programme basis, particularly if you are trying to ensure the relevant XBMC and Plex folder structure conventions are met.

To specify the directory/folder get\_iplayer outputs downloaded files to, we use the "output" command which looks like this:

```bash
--output
```

...to which we simply add the folder path:

```bash
--output "/path/to/output/folder/goes/here/"
```

**DON'T FORGET THE QUOTATION MARKS!**

The file path should go within the quotation marks. You are free to type out the location and get\_iplayer will create it for you if it doesn't exist already, or it will simply add files to the directory if it already exists.

## How do I permanently change where get_ipayer saves downloaded radio programmes?

It's quite common to want to permanently change the location get\_iplayer saves its downloaded files. For a complete overview of all output options take a look at the [Output Options](/wiki/options/#output-options) in the wiki, but lets take a look at a few simple and common options you can use.

### Change download location for all files

Firstly, to save a download location for all files, use the `--prefs-add` command like so:

```bash
--prefs-add --output "/media/Radio Shows 1/2 - Radio Shows/"
```

This will have get\_iplayer save all downloaded shows in the "2 - Radio Shows" directory in the "Radio Shows 1" disc. On Windows, the exact path will look a little different but I don't have a Windows install to show you directly.

### Change download location for just Radio shows

Instead of downloading everything to one location, you might only want radio shows to go to a particular directory. It that's the case you can use the `--outputradio` command like so:

```bash
--prefs-add --outputradio "/media/Radio Shows 1/2 - Radio Shows/"
```

This will have get\_iplayer save **ONLY** radio shows in the "2 - Radio Shows" directory in the "Radio Shows 1" disc.

The `--outputradio` option overrides the `--output` command, which means if you set the `--output` command, all downloads *apart from radio shows* will go to that location and all radio shows will go wherever `--outputtv` is set.

You can set specific locations for the different types of files with the following commands. Each one will override the `--output` command for their specific file type, so you have a lot of flexibility in where you can save files:

```
--output
--outputliveradio
--outputlivetv
--outputlocalfiles
--outputpodcast
--outputradio
--outputtv
```

Full info in the [Output Options section](/wiki/options/#output-options) of the Options wiki page.
