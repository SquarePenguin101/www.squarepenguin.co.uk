+++
categories = ["", ""]
date = "2015-07-09T22:11:38+01:00"
description = "A quick installation guide to get get_iplayer installed on your Mac in just a few minutes."
draft = false
pageimage = ""
pagesubtitle = "COMPREHENSIVE GUIDES TO GET YOU STARTED QUICKLY"
pagetitle = "get_iplayer Guides and Tutorials"
slug = "mac-os-x-quick-install-guide"
title = "Mac OS X Quick Install Guide • get_iplayer"
Type = "guides"
breadcrumb = "get_iplayer Mac OS X Quick Install Guide"
+++

# Mac OS X Quick Install Guide

## Option 1 - Get iPlayer Automator

There are a couple of options on Mac. The easiest of the two is to use Get iPlayer Automator, a free tool that greatly simplifies the process of downloading content from the BBC (and now ITV) and have it deposited straight into iTunes.

Most Mac users enjoy this 'just works' setup and are not interested in the details underlying the programme. If you fit this description you can [download Get iPlayer Automator](https://github.com/GetiPlayerAutomator/get-iplayer-automator/releases/) or find out more on the [Get iPlayer Automator site](https://github.com/GetiPlayerAutomator/get-iplayer-automator).

I have not used Get iPlayer Automator, so I can't help you with it, but you can visit the [Get iPlayer Automator issue tracker](https://github.com/GetiPlayerAutomator/get-iplayer-automator/issues) if you get stuck.

## Option 2 - Easy manual installation

If you like to see how things work and don't mind using the Terminal, you can install get_iplayer manually in less than 10 steps by using the instructions below.

1.  Create a working folder You will use a temporary working folder to hold all the necessary files before installation.
    *   Navigate to your 'Home' folder (the one with a house next to it in the Finder sidebar).
    *   Create a working folder inside your home folder called "get_iplayer_install" without the quote marks.
2.  Download the latest version of get_iplayer (v2.87 at time of writing) from the link below: [https://github.com/get-iplayer/get_iplayer/archive/latest.zip](https://github.com/get-iplayer/get_iplayer/archive/latest.zip)
3.  Extract get_iplayer
    *   Go to your "Downloads" folder and identify the downloaded get_iplayer file. It should be named "get_iplayer-latest.zip".
    *   The zip file may have been automatically extracted after download. If not, double click on the file and it should be automatically extracted to a folder in your Downloads folder. This new folder will be named "get_iplayer-latest".
    *   Navigate to this new folder and select the 2 files named "get_iplayer" and "get_iplayer.cgi", then press Cmd+C to copy the files.
    *   Navigate to the working folder you created earlier.
    *   Press Cmd+V to paste the files in the new location.
4.  Download external programs get_iplayer requires several utilities in order to record and process programmes. Download a bundle containing the necessary external programs from one of the links below (select the appropriate link for your version of OS X):
    *   OS X 10.6 (Snow Leopard) or higher, 64-bit Intel only: [http://sourceforge.net/projects/get-iplayer/files/osx/utils/x86_64/20141227/get_iplayer-osx-utils-x86_64-20141227.zip](http://sourceforge.net/projects/get-iplayer/files/osx/utils/x86_64/20141227/get_iplayer-osx-utils-x86_64-20141227.zip)
    *   OS X 10.5 (Leopard), 32-bit Intel only: [http://sourceforge.net/projects/get-iplayer/files/osx/utils/i386/20141227/get_iplayer-osx-utils-i386-20141227.zip](http://sourceforge.net/projects/get-iplayer/files/osx/utils/i386/20141227/get_iplayer-osx-utils-i386-20141227.zip) **NOTE:** There is no bundle available for PowerPC machines.
5.  Extract external programs
    *   Go to your "Downloads" folder and identify the downloaded utilities file. It should be named "get_iplayer-osx-utils-x86_64-20141227.zip" or "get_iplayer-osx-utils-i386-20141227.zip".
    *   The zip file may have been automatically extracted after download. If not, double click on the file and it should be automatically extracted to another folder in your Downloads folder. This new folder will be named "get_iplayer-osx-utils-x86_64-20141227" or "get_iplayer-osx-utils-i386-20141227".
    *   Navigate to this new folder and use Cmd+Click to select these 5 files: AtomicParsley, ffmpeg, id3v2, mplayer and rtmpdump. Then press Cmd+C to copy the files.
    *   Navigate to the working folder you created earlier.
    *   Press Cmd+V to paste the files in the new location.
6.  Now open up a terminal window. You can do this by pressing Cmd+Spacebar to activate Spotlight and typing "Terminal" in the search field, then pressing Return. You can also launch Terminal directly from /Applications/Utilities.
7.  Initialise get_iplayer settingsBefore installing get_iplayer you must perform a one-time initialisation of its profile directory (~/.get_iplayer - note the dot in the filename), where settings and plugins are stored. In the terminal window, navigate to the working folder you created earlier:

        cd ~/get_iplayer_install

    Ensure get_iplayer has the correct permissions:

        chmod 755 ./get_iplayer

    Run get_iplayer:

        ./get_iplayer

    The output from this first run should look like:

    <pre>get_iplayer v2.83, Copyright (C) 2008-2010 Phil Lewis
      This program comes with ABSOLUTELY NO WARRANTY; for details use --warranty.
      This is free software, and you are welcome to redistribute it under certain
      conditions; use --conditions for details.

    WARNING: Running the updater again to obtain plugins.
    INFO: Current version is 2.83
    INFO: Checking for latest version from www.infradead.org
    INFO: Found new plugin localfiles.plugin
    INFO: Installing localfiles.plugin in /Users/username/.get_iplayer/plugins
    INFO: Downloaded /Users/username/.get_iplayer/plugins/localfiles.plugin
    INFO: Found new plugin podcast.plugin
    INFO: Installing podcast.plugin in /Users/username/.get_iplayer/plugins
    INFO: Downloaded /Users/username/.get_iplayer/plugins/podcast.plugin</pre>

    where "username" is your OSX username.
8.  Install get_iplayer and utilitiesWhile still in your working folder, run the command below to create the installation directory if it does not already exist:

        sudo mkdir -p /usr/local/bin

    `sudo` indicates you wish to run the the `mkdir` command with administrator privileges, so you may be prompted for your password before proceeding. The `-p` flag instructs `mkdir` to create directories as needed. Run the command below to install get_iplayer and associated utilities in /usr/local/bin:

        sudo install -m 755 get_iplayer get_iplayer.cgi AtomicParsley ffmpeg id3v2 mplayer rtmpdump /usr/local/bin

    `sudo` indicates you wish to run the `install` command with administrator privileges, so you may be prompted for your password before proceeding. The `-m 755` flag instructs `install` to apply the correct permissions to each file. That is followed by the list of 7 files you wish to install and finally by the installation directory (/usr/local/bin).
9.  That's it! You have installed get_iplayer. In the terminal window, navigate to your home directory:

        cd ~

    then test your newly-installed get_iplayer:

        get_iplayer

    You should see the TV cache being populated and the list of available TV programmes scroll past in the terminal window. Perform a few test downloads to ensure everything is working correctly. Once you are sure that is the case, you can delete the working folder you created earlier.

## Post installation steps

### Set get_iplayer output directory

By default, get_iplayer downloads programmes to your current working directory. You will probably want to configure get_iplayer to download programmes to a central location. Use the command below to configure a permanent output directory:

    get_iplayer --prefs-add --output=/path/to/output/directory

Replace "/path/to/output/directory" with your selected path.

If you ever wish to change the output directory, re-run the above command with a different directory path. If you ever wish to completely remove the setting, use the following command:

    get_iplayer --prefs-del --output=/path/to/output/directory

**NOTE:** Do not use a tilde (~) to indicate your home directory when setting the get_iplayer output path. Use $HOME instead:

    get_iplayer --prefs-del --output=$HOME/path/to/output/directory

or use the fully expanded form:

    get_iplayer --prefs-del --output=/Users/username/path/to/output/directory

where "username" is your OSX username.

## Web PVR Manager (WPM)

Create the installation directory if it does not exist:

    sudo mkdir -p /usr/local/bin

then use the WPM [manual installation procedure](/wiki/osxmanual/) described for Linux/Unix.

## Uninstalling get_iplayer

If you should ever wish to remove get_iplayer and utilities installed according to the above instructions, run the command below in a terminal window:

    sudo rm /usr/local/bin/{get_iplayer,get_iplayer.cgi,AtomicParsley,ffmpeg,id3v2,mplayer,rtmpdump}

`sudo` indicates you wish to run the `rm` command with administrator privileges, so you may be prompted for your password before proceeding.

If you also wish to remove your get_iplayer settings, use this command:

    rm -fr ~/.get_iplayer

For further information on installing get_iplayer on OS X, please see the [Installation Guides](/wiki/installation).
