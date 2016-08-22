+++
categories = ["", ""]
date = "2016-07-05T13:27:45+01:00"
description = "Installation instructions for get_iplayer on Debian."
draft = false
pageimage = ""
pagesubtitle = "COMPREHENSIVE GUIDES TO GET YOU STARTED QUICKLY"
pagetitle = "get_iplayer installation guides"
slug = "debian"
title = "get_iplayer Debian installation guide"
Type = "downloads"
+++

**Before you begin**: Linux/Unix packages are maintained by volunteers and may not be updated for some time after a new release of get_iplayer, thus the version of get_iplayer packaged for your system may be obsolete. You can find the version number of the latest get_iplayer release [here](https://github.com/get-iplayer/get_iplayer/releases). If the version packaged for your system is older than the latest release, it is likely that some functionality is broken. After following the instructions below, you may wish to uninstall the get_iplayer package and use the [manual installation instructions](https://github.com/get-iplayer/get_iplayer/wiki/unix) to install the latest get_iplayer CLI and Web PVR Manager. 

## Debian

These instructions are for Debian 8 (jessie). The instructions assume that you are logged in as root, but the installation commands may also be performed with `sudo`.

**NOTE**: As of Debian 8 (jessie), get_iplayer is no longer available in the stable repository. Use the instructions below to combine dependencies from stable and backports repositories with the get-iplayer package from the testing repository. The example below is for get_iplayer 2.94.  Adjust file names accordingly for later versions. Information for the get-iplayer package in the testing repository can be found at:

https://packages.debian.org/testing/get-iplayer

### Command-line Interface (CLI)

1. Install dependencies (except ffmpeg) from stable repository

        apt-get install libwww-perl libxml-simple-perl libmp3-tag-perl libmp3-info-perl libnet-smtp-ssl-perl libauthen-sasl-perl libnet-smtp-tls-butmaintained-perl rtmpdump atomicparsley
 
2. Install ffmpeg from backports repository

    If you previously installed the libav-tools package from the stable repository, you may wish to remove it first:

        apt-get autoremove libav-tools

    You can also remove it after installing ffmpeg. The libav-tools package is upgraded during ffmpeg installation so that its utilities are linked to the ffmpeg equivalents (e.g., avconv -> ffmpeg), so you do not need libav-tools for get_iplayer.

    To access the backports repository, add this line to `/etc/apt/sources.list`:

        deb http://ftp.uk.debian.org/debian jessie-backports main

    Update package database and install:

        apt-get update
        apt-get -t jessie-backports install ffmpeg

    For further information see:

    http://backports.debian.org/Instructions/

    For a list of backports mirrors see:

    https://www.debian.org/mirror/list

3. Install get_iplayer package from testing repository

    Download DEB package (do not install with `apt-get`, `aptitude`, `Synaptic`, etc.)
        
        wget http://ftp.uk.debian.org/debian/pool/main/g/get-iplayer/get-iplayer_2.94-1_all.deb

    For a list of download links from other mirrors see:

        https://packages.debian.org/testing/all/get-iplayer/download

    Remove any existing get-iplayer package:

        dpkg -r get-iplayer
    
    Install new get-iplayer package:

        dpkg -i get-iplayer_2.94-1_all.deb

4. Run CLI with:

		get_iplayer [...]

### Web PVR Manager (WPM)

The WPM is installed along with the CLI.

1. Launch the WPM in a terminal window with this command:

        get_iplayer_web_pvr

2. Once the WPM is running, connect to it by opening this URL in your browser:

    <http://127.0.0.1:1935>

3. After the WPM has opened in your browser, click the `Refresh Cache` button.  A new tab or window will open that shows the cache being refreshed.  Leave that tab or window open to have the cache refreshed automatically every hour.  You can also manually refresh the cache at any time.

4. Stop the WPM by typing Ctrl-C.
