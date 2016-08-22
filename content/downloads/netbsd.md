+++
categories = ["", ""]
date = "2016-07-05T13:27:45+01:00"
description = "Installation instructions for get_iplayer on NetBSD."
draft = false
pageimage = ""
pagesubtitle = "COMPREHENSIVE GUIDES TO GET YOU STARTED QUICKLY"
pagetitle = "get_iplayer installation guides"
slug = "netbsd"
title = "get_iplayer NetBSD installation guide"
Type = "downloads"
+++

**Before you begin**: Linux/Unix packages are maintained by volunteers and may not be updated for some time after a new release of get_iplayer, thus the version of get_iplayer packaged for your system may be obsolete. You can find the version number of the latest get_iplayer release [here](https://github.com/get-iplayer/get_iplayer/releases). If the version packaged for your system is older than the latest release, it is likely that some functionality is broken. After following the instructions below, you may wish to uninstall the get_iplayer package and use the [manual installation instructions](https://github.com/get-iplayer/get_iplayer/wiki/unix/) to install the latest get_iplayer CLI and Web PVR Manager. 

## NetBSD

These instructions are for NetBSD 7.0.  The installation instructions assume that you are logged in as root.

### Command-line Interface (CLI)

1. Install Perl

        pkg_add -v perl

    NOTE: Perl will likely already be installed if you installed a desktop environment.

2. Install get_iplayer package and dependencies from release repository (assumes PKG_PATH configured)

        pkg_add -v get_iplayer

3. Install components not installed with get_iplayer package

        pkg_add -v p5-MP3-Info p3-MP3-Tag p5-Net-SMTP-SSL p5-Authen-SASL

4. Packages for ffmpeg1 and ffmpeg2 are available - install ffmpeg2
        
        pkg_add -v ffmpeg2
        
5. As regular user: configure get_iplayer to use ffmpeg2

        get_iplayer --prefs-add --ffmpeg=ffmpeg2

6. Run CLI with:

    	get_iplayer [...]

### Web PVR Manager (WPM)

The WPM is not installed with the get_iplayer package.  Use the [manual installation procedure](https://github.com/get-iplayer/get_iplayer/wiki/unix/).
