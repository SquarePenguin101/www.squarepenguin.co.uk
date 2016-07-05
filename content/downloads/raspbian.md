+++
categories = ["", ""]
date = "2016-07-05T13:27:45+01:00"
description = "Installation instructions for get_iplayer on Raspbian."
draft = false
pageimage = ""
pagesubtitle = "COMPREHENSIVE GUIDES TO GET YOU STARTED QUICKLY"
pagetitle = "get_iplayer installation guides"
slug = "raspbian"
title = "get_iplayer Raspbian installation guide"
Type = "downloads"
+++

**Before you begin**: Linux/Unix packages are maintained by volunteers and may not be updated for some time after a new release of get_iplayer, thus the version of get_iplayer packaged for your system may be obsolete. You can find the version number of the latest get_iplayer release [here](https://github.com/get-iplayer/get_iplayer/releases). If the version packaged for your system is older than the latest release, it is likely that some functionality is broken. After following the instructions below, you may wish to uninstall the get_iplayer package and use the [manual installation instructions](/wiki/unix) to install the latest get_iplayer CLI and Web PVR Manager. 

## Raspbian / Raspberry Pi

These instructions are for both Raspbian wheezy and Raspbian jessie.

### get-iplayer Package

Raspbian users are recommended to use the get_iplayer repository version (see below), even though the Debian get-iplayer package is incorporated in Raspbian repositories.  If you must use the Debian package, refer to the installation instructions for [Debian](/downloads/debian).  Note that the version of AtomicParsley packaged with Raspbian (but not the version packaged here) frequently fails with files downloaded with get_iplayer.

#### get_iplayer Repository Installation

1. Add the repository

    Paste these lines into a terminal window:

	    echo "deb http://packages.hedgerows.org.uk/raspbian wheezy/" | sudo tee /etc/apt/sources.list.d/packages.hedgerows.org.uk.list
	    echo "deb-src http://packages.hedgerows.org.uk/raspbian wheezy/" | sudo tee -a /etc/apt/sources.list.d/packages.hedgerows.org.uk.list

2. Install the repository signing key, and update the package index:

	    sudo apt-key adv --keyserver keyserver.ubuntu.com --recv 0F5BFDFE
	    sudo apt-get update

3. Install the get-iplayer package

    	sudo apt-get install get-iplayer

That's it!  You are now ready to run the command line interface with:

    	get_iplayer [...]

(There are instructions for removing the repository at [packages.hedgerows.org.uk](http://packages.hedgerows.org.uk/))

### Web PVR Manager (WPM)

The WPM is installed as part of the get-iplayer package.

1. Launch the WPM in a terminal window with this command:

    	get_iplayer_web_pvr

2. Once the WPM is running, connect to it by opening this URL in your browser:

    <http://127.0.0.1:1935>

3. After the WPM has opened in your browser, click the `Refresh Cache` button.  A new tab or window will open that shows the cache being refreshed.  Leave that tab or window open to have the cache refreshed automatically every hour.  You can also manually refresh the cache at any time.

4. Stop the WPM by typing Ctrl-C.