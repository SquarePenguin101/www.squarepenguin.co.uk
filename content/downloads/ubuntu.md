+++
categories = ["", ""]
date = "2016-07-05T13:27:45+01:00"
description = "Installation instructions for get_iplayer on Ubuntu / Mint."
draft = false
pageimage = ""
pagesubtitle = "COMPREHENSIVE GUIDES TO GET YOU STARTED QUICKLY"
pagetitle = "get_iplayer installation guides"
slug = "ubuntu"
title = "get_iplayer Ubuntu / Mint installation guide"
Type = "downloads"
+++

## Ubuntu / Mint

These instructions are for Ubuntu (all versions that have not reached end-of-life) and Ubuntu-based Mint 17, but not Mint Debian edition (LMDE). 

The get_iplayer versions incorporated in Ubuntu repositories are all out of date or broken, so Ubuntu/Mint users should install from the get-iplayer PPA.

Ubuntu packages are maintained by volunteers and may not be updated for a short time after a new release of get_iplayer, thus the version of get_iplayer packaged for your system may be obsolete. You can find the version number of the latest get_iplayer release [here](https://github.com/get-iplayer/get_iplayer/releases). If the version packaged for your system is older than the latest release, it is likely that some functionality is broken. You may either wait a short while for a new release, usually less than 24 hours, or use the [manual installation instructions](https://github.com/get-iplayer/get_iplayer/wiki/unix) to install the latest get_iplayer CLI and Web PVR Manager.

Users of Ubuntu/Mint editions that have reached end-of-life ([Ubuntu](https://wiki.ubuntu.com/Releases), [Mint](http://www.linuxmint.com/oldreleases.php)), or that do not have a PPA build available, should use the [manual installation procedure](https://github.com/get-iplayer/get_iplayer/wiki/unix).

### get-iplayer PPA

The [get-iplayer PPA](https://launchpad.net/~jon-hedgerows/+archive/get-iplayer) (Personal Package Archive) is maintained by Jon Davies.  Packages with up-to-date versions of get_iplayer and dependencies are available for supported Ubuntu releases.

### Command-line Interface (CLI)

1. Add the PPA repository

        # If you do not have apt-add-repository on your system, first install python-software-properties
        sudo apt-get install python-software-properties software-properties-common

    	sudo apt-add-repository ppa:jon-hedgerows/get-iplayer

2. Ensure package database is current

    	sudo apt-get update

3. Install get_iplayer and its dependencies from the PPA:

    	sudo apt-get install get-iplayer
    
    You may install from the PPA over an existing get-iplayer installation from the Ubuntu repositories.  Dependencies will be updated automatically.

4. If you install from the PPA over an existing get-iplayer installation from the Ubuntu repositories, you may find that rtmpdump is not automatically updated. To check, run `rtmpdump` without any arguments. If the version string in the output is `RTMPDump v2.4`, you still have the Ubuntu build.  The PPA build will show a version string similar to `RTMPDump v2.4-n87-gita9f353c-ppa8~saucy`.  If you still have the Ubuntu build, you can update rtmpdump separately:

        sudo apt-get install rtmpdump

5. **Ubuntu 12.04 only:** You will need an additional codec to convert radio programmes to MP3

        sudo apt-get install libavcodec-extra-53

6. Run CLI with:

    	get_iplayer [...]

+++
categories = ["", ""]
date = "2016-07-05T13:27:45+01:00"
description = "Installation instructions for get_iplayer on Slackware / Salix."
draft = false
pageimage = ""
pagesubtitle = "COMPREHENSIVE GUIDES TO GET YOU STARTED QUICKLY"
pagetitle = "get_iplayer installation guides"
slug = "slackware"
title = "get_iplayer Slackware / Salix installation guide"
Type = "downloads"
+++

If you wish to remove the PPA packages and roll back any updates:

    # If you do not have ppa-purge on your system, first install it
    sudo apt-get install ppa-purge

    sudo ppa-purge ppa:jon-hedgerows/get-iplayer

### Web PVR Manager (WPM)

The WPM is installed along with the CLI.

1. Launch the WPM in a terminal window with this command:

    	get_iplayer_web_pvr

2. Once the WPM is running, connect to it by opening this URL in your browser:

    <http://127.0.0.1:1935>

3. After the WPM has opened in your browser, click the `Refresh Cache` button.  A new tab or window will open that shows the cache being refreshed.  Leave that tab or window open to have the cache refreshed automatically every hour.  You can also manually refresh the cache at any time.

4. Stop the WPM by typing Ctrl-C.

### Graphical Interface (giPlayer)

Although not officially connected to the get_iplayer project, there is a desktop graphical front end for get_iplayer called giPlayer.  It's a simple Python/GTK program that has a .deb for easy installation on Ubuntu.  It also comes with both Chrome and Firefox browser extensions to let you easily launch the program whilst browsing any TV or Radio entry on the iPlayer web site to let you download what you were viewing in your browser.

See their web site:

<http://sourceforge.net/projects/giplayer/files>

for more information.