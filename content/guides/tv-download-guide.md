+++
categories = ["", ""]
date = "2015-06-27T01:27:06+01:00"
description = "A simple beginners guide to get_iplayer, with examples commands & other useful references to help you get started quickly & easily."
draft = false
pageimage = ""
pagesubtitle = "COMPREHENSIVE GUIDES TO GET YOU STARTED QUICKLY"
pagetitle = "get_iplayer Guides and Tutorials"
slug = "tv-download-guide"
title = "TV download guide • get_iplayer"
Type = "guides"
breadcrumb = "get_iplayer TV download guide"
+++

# get_iplayer TV Download Guide

This guide has been written in a step by step manner for beginners. If this is your first time here you really must go through the guide in this fashion if you are to understand and get the most out of get_iplayer.

However, if you are coming back here to use this guide as a reference or just have a specific question, feel free to click on any of the links in the contents below to jump to the relevant section you need.

**NOTE** - Need the full get_iplayer documentation? Find it in the [Wiki Documentation](https://github.com/get-iplayer/get_iplayer/wiki/documentation/) page.

## Guide Contents

1. [How do I search for programmes using get_iplayer?](#how-do-i-search-for-programmes-using-get-iplayer)
2. [How do I record a programme with get_iplayer?](#how-do-i-record-a-programme-with-get-iplayer)
3. [Where does get_iplayer save downloaded programmes?](#where-does-get-iplayer-save-downloaded-programmes)
4. [How do I specify or change the quality level of programmes downloaded in get_iplayer?](#how-do-i-specify-or-change-the-quality-level-of-programmes-downloaded-in-get-iplayer)
5. [How do I make sure get_iplayer downloads a TV show and not a Radio programme?](#how-do-i-make-sure-get-iplayer-downloads-a-tv-show-and-not-a-radio-programme)
6. [How do I make sure get_iplayer downloads from the correct channel?](#how-do-i-make-sure-get-iplayer-downloads-from-the-correct-channel)
7. [How do I make get_iplayer automatically rename downloaded programmes?](#how-do-i-make-get-iplayer-automatically-rename-downloaded-programmes)
8. [How do I make get_iplayer automatically rename downloaded programmes for use with XBMC and Plex?](#how-do-i-make-get-iplayer-automatically-rename-downloaded-programmes-for-use-with-xbmc-and-plex)
9. [How do I change or specify where get_iplayer saves downloaded programmes?](#how-do-i-change-or-specify-where-get-iplayer-saves-downloaded-programmes)
10. [How do I permanently change where get_ipayer saves downloaded TV programmes?](#how-do-i-permanently-change-where-get-ipayer-saves-downloaded-tv-programmes)

## How do I search for programmes using get_iplayer?

See the [Searching section](https://github.com/get-iplayer/get_iplayer/wiki/search) of the wiki documentation for information on get_iplayer search limitations before searching for any programmes.

To begin using get_iplayer, we should first search for the programme we want to watch. Once you have the programme in mind that you would like to see, we simply search for a programme using get_iplayer by typing the following:

```bash
get_iplayer "Programme Name"
```
It is crucial that you use the " " marks when performing a search containing more than one word. If you don't, you'll either get an error or results will only be relevant to the first word you type.

Get in the habit of using " quotation " marks for each and every search you do. In this case, the above command will search for...

```bash
Programme Name
```

...and will return a set of results corresponding to that search. In the screenshot below you can see that there are "0 matching programmes". Not surprising!

![get_iplayer-_Programme-Search_](/img/2015/06/get_iplayer-_Programme-Search_.png)

**HINT** - "0 matching programmes" is written on the second from bottom line of the terminal window, the text you see above is a read out of all the TV programmes that BBC iPlayer is currently making available for download.

get_iplayer has to update its list of these before it can match your search query to them. You can effectively ignore this text.

![get_iplayer-_Programme-Search_](/img/2015/06/get_iplayer-_Programme-Search_.png)

To search for something more useful, we could type:

```bash
get_iplayer "Top Gear"
```
This returns the following...

![get_iplayer-_Top-Gear_-search](/img/2015/06/get_iplayer-_Top-Gear_-search.png)

**HINT** - Notice how get_iplayer doesn't have to refresh the available streams? This is because it did it in the last command. get_iplayer will remember the list for 4 hours, and then update the list if a new search is performed after this 4 hour time limit.

That's is all there is to performing a basic search. I've not needed to use any of the more advanced options, but feel free to leave a comment if you need help with narrowing down your searches and I'll be happy to help you out.

Anyway, as you can see, a lot of additional information is returned about each individual programme. We can use this information in the upcoming examples to narrow our recording to specific channels and types of broadcast (radio/TV etc).

## How do I record a programme with get_iplayer?

There are three basic ways to download programmes with get_iplayer, one uses the search string, one uses the index number and one uses the PID.

### The Search String

In the example above, we used "Top Gear" as the search string. We can use this search string in combination with the "get" command to download all programmes that match this search string. This makes more sense when we type it out:

```bash
get_iplayer --get "Top Gear"
```

Once we execute this command, get_iplayer will begin to download all programmes that match this search string.

### The Index Number

The second method is to use the index number. Notice in the screen shot above that each programme comes with a three or four digit number? I've highlighted this in the screenshot below:

![get_iplayer-Top-Gear-index](/img/2015/06/get_iplayer-Top-Gear-index.png)

We can use this number to tell get_iplayer to download specific programmes and nothing else. We do so using the following command:

```bash
get_iplayer --get 962
```

...where 962 is the index number of the programme you want to download. If you want to download more than one specific programme at a time, you can type the index numbers one after the other like so:

```bash
get_iplayer --get 962 123 1234
```

### The PID method

To find the PID you'll need to go to the programme page on the BBC iPlayer website and identify it in the URL (web address) that can be seen in your browsers address bar. Lets look at an example URL:

```bash
http://www.bbc.co.uk/iplayer/episode/b04n9p9c/the-missing-episode-1
```

The PID in the example above is the seemingly random string of characters`b04n9p9c`.

In fact, many (possibly all) PIDs start with b0, so you can usually identify the PID pretty easily. To download the programme using the PID we use the `--pid` command.

An example of the above episode being downloaded in this fashion would be:

```bash
get_iplayer --pid=b04n9p9c
```

### Downloading multiple PIDs

You can download multiple PIDs in a single command.

You can enter multiple PIDs in two ways:

#### Comma-separated list

```bash
get_iplayer --pid PID1,PID2,PID3
```

#### Multiple `--pid` options

```bash
get_iplayer --pid PID1 --pid PID2 --pid PID3
```

*(Remember to include `--type=radio` with `--pid` when downloading radio programmes.)*

#### Multiple `--url` options

You can also do the same thing with episode page URLs:

```bash
get_iplayer --url URL1,URL2,URL3
```

or alternatively...

```bash
get_iplayer --url URL1 --url URL2 --url URL3
```

*(Remember to include `--type=radio` with `--url` when downloading radio programmes.)*

Prefer `--pid` to `--url` where possible - it is slightly quicker and more reliable. And no, you can't download multiple PIDs or multiple URLs with the Web PVR Manager.

You can use all the other commands throughout this guide along with the `--pid` command to specify the output directory and naming structure etc, just substitute it and the PID in place of `--get` and the search string/index number.

That is all there is to it, nothing too hard as long as you search first and then use the simple commands above to download the programme you want. We'll get on to saving these searches.

## Where does get_iplayer save downloaded programmes?

get_iplayer saves files to your current working directory as a default on both Mac OS X and Linux, whereas it saves programmes to the folder you specified when first installing if you're using Windows.

I will show you how to download programmes to a directory (folder) of your choice in the [How do I change or specify where get_iplayer saves downloaded programmes?](#how-do-i-change-or-specify-where-get-iplayer-saves-downloaded-programmes) section.

Click the link to jump there now if you need to, or if this is your first time using this guide simply read on and we'll get to that shortly.

Personally, I do not recommend simply using the default location as it makes organising programmes much more difficult and you might end up with programmes in several different locations.

This is especially true if you use the PVR function (which I will explain later in the guide).

## How do I specify or change the quality level of programmes downloaded in get_iplayer?

For a full explanation of get_iplayer recording quality, check out the [Recording Quality](https://github.com/get-iplayer/get_iplayer/wiki/modes/) wiki entry.

As a default, get_iplayer will download the highest quality version of each TV programme, so you DO NOT need to change anything or use any of the commands below if you are happy with having the highest quality version. By "highest quality" I mean the version with the largest video size.

If you want to make get_iplayer download a lower quality you should use the "--tvmode" command. The code is written like this

```bash
--tvmode=
```

...followed by the desired quality level. The list of available settings to add to the above command is below:

```bash
best
better
good
worst
```

The default is `--tvmode=best`, so you do not need to specify it. However, for the purposes of this guide I will include it in the example commands. 

Quality levels are treated as **maximum** values. If only lower quality versions are available, get_iplayer will download the best available from those versions.

**NOTE** - Regardless of recording quality, when you download a file it is automatically converted to MP4 format and so is compatible with an entire galaxy of devices, video players and media systems.

### Want get_iplayer to download in HD?

get_iplayer will attempt to download the best available quality by default. If an HD version of a TV programme is available, get_iplayer will download it.

### On a restricted bandwidth connection?

If you are on a restricted bandwidth internet connection with usage limits, use a lower quality level. Try `--tvmode=good` to start. This should help keep your downloads small but still of reasonable quality and help stop you going over your bandwidth allowance.

## How do I make sure get_iplayer downloads a TV show and not a Radio programme?

I've noticed that sometimes, with programmes like 'Click', which shares the same name as its sister radio show, there can be times when the radio show might show up in a search for the TV programme. To make sure that the TV programme is the one downloaded we can specify the "type" of broadcast using the following command:

```bash
--type=tv
```

This tells get_iplayer to download the TV show matching the search string. You can use the following to download the radio programme:

```bash
--type=radio
```

To add this code to the previous examples as we build towards our final example code, it would look like this:

```bash
get_iplayer --get "Top Gear" --tvmode=best --type=tv
```

## How do I make sure get_iplayer downloads from the correct channel?

It can be frustrating when get_iplayer downloads from the wrong channel! Sometimes programmes from different, or even the same, series are shown on different channels at the same time. This can be annoying as you may accidentally download something from a previous series you have already seen on TV.

get_iplayer remembers programmes it has previously downloaded and won't download them again, but it's still useful to be able to specify which channel you would like to download from.

To do this we use the "Channel" command, which looks like this:

```bash
--channel=
```

An example of the command in use would be:

```bash
--channel="BBC Two"
```

**DON'T FORGET THE QUOTATION MARKS!** If we add this to our code so far, we get:

```bash
get_iplayer --get "Top Gear" --tvmode=best --type=tv --channel="BBC Two"
```

## How do I make get_iplayer automatically rename downloaded programmes?

To make get_iplayer rename downloaded programmes to a scheme of our choice, we use the "File Prefix" command coupled with the "Substitution Parameters" of our choice to 'build' the file name we want.

A full list of available Substitution Parameters can be found in the [Substitution Parameters Wiki entry](https://github.com/get-iplayer/get_iplayer/wiki/subparams).

For our purposes, we will be using the following three Substitution Parameters:

```bash
<nameshort> = the programme name with the series number stripped
<senum> = Series and Episode numbers in the s##e## format
<episodeshort> = programme episode name with episode number stripped
```

### How do I make get_iplayer automatically rename downloaded programmes for use with XBMC and Plex?

I use [Plex](http://www.plexapp.com/) as my media system because I find its [Server/Client](http://wiki.plexapp.com/index.php/Frequently_Asked_Questions) philosophy perfect for my needs.

Based on the popular [XBMC](http://xbmc.org/) media system, it retains the same naming conventions, therefore we can tell get_iplayer to rename downloaded programmes automatically.

This means that the filenames will be sure to meet the XBMC and Plex naming conventions, allowing each system to pull down programme info from the web automatically.

**NOTE** - If you don't use Plex/XBMC, this naming convention is still useful for correctly naming programmes and episodes as you will see in the example below, so you can still use it or modify it as you see fit.

To tell get_iplayer to rename files to the relevant naming convention, we use the following command:

```bash
--file-prefix="<nameshort><-senum><-episodeshort>"
```

**YOU MUST REMEMBER TO USE THE QUOTATION MARKS!**

**NOTE** - See those "-" dashes inside the Substitution Parameters? Check out the [Output File Naming Guide](https://github.com/get-iplayer/get_iplayer/wiki/filenames) for an explanation as to why they are added INSIDE the parameter and not in between.

This tells get_iplayer to name the file like the example below...

```bash
Jonathan_Creek-s01e01-The_Clue_of_the_Savants_Thumb
```

...which is just how XBMC and Plex require you to name your files. Adding the command to our earlier examples gives us:

```bash
get_iplayer --get "Top Gear" --tvmode=best --type=tv --channel="BBC Two" --file-prefix="<nameshort><-senum><-episodeshort>"
```

## How do I change or specify where get_iplayer saves downloaded programmes?

We can set the output path of programmes get_iplayer downloads on a case by case basis. You _can_ do this globally, but it makes more sense to do this on a programme by programme basis, particularly if you are trying to ensure the relevant XBMC and Plex folder structure conventions are met.

To specify the directory/folder get_iplayer outputs downloaded files to, we use the "output" command which looks like this:

```bash
--output
```

...to which we simply add the folder path:

```bash
--output "/path/to/output/folder/goes/here/" [...]
```

**DON'T FORGET THE QUOTATION MARKS!**

The file path should go within the quotation marks. You are free to type out the location and get_iplayer will create it for you if it doesn't exist already, or it will simply add files to the directory if it already exists.

If you are unsure of the exact folder path to use, you can use the Graphical User Interface file explorer to navigate to the folder where you want the programmes to be downloaded and simply press "ctrl+L".

On Ubuntu at least, this will reveal the folder path at the top of the explorer window, as shown in the example below, and you can just copy and paste this into the terminal window.

![get_iplayer-_How-to-find-directory_-example](/img/2015/06/get_iplayer-_How-to-find-directory_-example.png)

To find out the full path of a folder on Windows, use this handy guide:

[http://technet.microsoft.com/en-us/magazine/ff678296.aspx](http://technet.microsoft.com/en-us/magazine/ff678296.aspx)

To find the full path of a folder on Mac OS X, use this handy guide:

[How to find the location of a Folder in Mac OS X](http://josharcher.uk/code/find-path-to-folder-on-mac/ "Find the Path to a Folder in Mac OS X").

So, adding the output folder path to our code so far gives us our final command:

```bash
get_iplayer --get "Top Gear" --type=tv --channel="BBC Two" --file-prefix="<nameshort><-senum><-episodeshort>" --output "/media/TV Shows 1/2 - TV Shows/Top Gear/Season 19"
```

This complete code will be made available again in the Example Section, but you can use it from here to download, rename and output the file to a directory of your choice. Just make sure to replace the relevant search string, channel and output destination to suit you.

## How do I permanently change where get_ipayer saves downloaded tv programmes?

It's quite common to want to permanently change the location get_iplayer saves its downloaded files. For a complete overview of all output options take a look at the [Output Options](https://github.com/get-iplayer/get_iplayer/wiki/options/#output-options) in the wiki, but lets take a look at a few simple and common options you can use.

### Change download location for all files

Firstly, to save a download location for all files, use the `--prefs-add` command like so:

```bash
get_iplayer --prefs-add --output "/media/TV Shows 1/2 - TV Shows/"
```

This will have get_iplayer save all downloaded shows in the "2 - TV Shows" directory in the "TV Shows 1" disc. On Windows, the exact path will look a little different but I don't have a Windows install to show you directly.

### Change download location for just TV shows

Instead of downloading everything to one location, you might only want TV shows to go to a particular directory. It that's the case you can use the `--outputtv` command like so:

```bash
get_iplayer --prefs-add --outputtv "/media/TV Shows 1/2 - TV Shows/"
```

This will have get_iplayer save **ONLY** TV shows in the "2 - TV Shows" directory in the "TV Shows 1" disc.

The `--outputtv` option overrides the `--output` command, which means if you set the `--output` command, all downloads *apart from tv shows* will go to that location and all TV shows will go wherever `--outputtv` is set.

You can set specific locations for the different types of files with the following options. Each one will override the `--output` command for their specific file type, so you have some flexibility in where you can save files:

```
--outputradio
--outputtv
```

Full info in the [Output Options section](https://github.com/get-iplayer/get_iplayer/wiki/options/#output-options) of the Options wiki page.

If you have skipped down to this section, go back up to the [How do I search for programmes using get_iplayer?](#how-do-i-search-for-programmes-using-get-iplayer) section learn how to perform a simple search.
