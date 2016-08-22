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

**Before you begin**: Linux/Unix packages are maintained by volunteers and may not be updated for some time after a new release of get_iplayer, thus the version of get_iplayer packaged for your system may be obsolete. You can find the version number of the latest get_iplayer release [here](https://github.com/get-iplayer/get_iplayer/releases). If the version packaged for your system is older than the latest release, it is likely that some functionality is broken. After following the instructions below, you may wish to uninstall the get_iplayer package and use the [manual installation instructions](https://github.com/get-iplayer/get_iplayer/wiki/unix) to install the latest get_iplayer CLI and Web PVR Manager. 

## Slackware / Salix

These instructions are for Slackware / Salix 14.1. Differences between the two are noted where appropriate. The instructions assume you have a done a full install of Slackware / Salix.  If not, you may need to install additional packages. The instructions below assume you are logged in as root on Slackware and you are using `sudo` on Salix.

### Command-line Interface (CLI)

1. Before You Begin

	These instructions show how to install get_iplayer using **sbopkg** to download, build and install the required [SlackBuilds](http://slackbuilds.org/).  If you prefer to use a different installation method, use the instructions below to guide you.  Information on installing and configuring sbopkg can be found at:

	<http://www.sbopkg.org>

	<http://docs.slackware.com/howtos:slackware_admin:building_packages_with_sbopkg>

	Below are instructions for creating a custom sbopkg queuefile to install get_iplayer and dependencies in a single operation.

    #### Salix only

    Do not use the multimedia codecs installer provided with Salix. The included version of ffmpeg is too old for full support of get_iplayer.

2. Create sbopkg queuefile

    These instructions assume you have configured sbopkg to read queuefiles from the default location `/var/lib/sbopkg/queues`. As root, create a sbopkg queuefile at this location:

	`/var/lib/sbopkg/queues/get_iplayer-full.sqf`

    The file contents should be **exactly** as shown below (the order is important):

		rtmpdump
		lame
		x264
		xvidcore
		ffmpeg | LAME=yes X264=yes XVID=yes
		id3lib
		id3v2
		perl-http-date
		perl-file-listing
		perl-IO-HTML
		perl-encode-locale
		perl-html-tagset
		perl-html-parser
		perl-lwp-mediatypes
		perl-http-message
		perl-http-cookies
		perl-http-daemon
		perl-http-negotiate
		perl-net-http
		perl-www-robotrules
		libwww-perl
		perl-digest-sha1
		perl-digest-hmac
		perl-Authen-SASL
		Net-SSLeay
		perl-Net-LibIDN
		perl-IO-Socket-SSL
		perl-Net-SMTP-SSL
		perl-MP3-Info
		get_iplayer

	The above ffmpeg options are the minimum for get_iplayer. If you require additional options for ffmpeg, adjust the queuefile options accordingly.  See:

	<http://slackbuilds.org/repository/14.1/multimedia/ffmpeg/>

3. Install Build Dependencies

    #### Salix only

    Install some ffmpeg build dependencies that are already installed by default with Slackware:

        sudo slapt-get --install yasm libssh tetex
        # load $PATH changes before running sbopkg
        source /etc/profile
	
3. Install get_iplayer and dependencies with queuefile

	Run this command:

        # Slackware
        sbopkg -i get_iplayer-full
        # Salix
        sudo sbopkg -i get_iplayer-full

	When prompted to confirm the queuefile options for ffmpeg (LAME=yes X264=yes XVID=yes), enter **q** to accept.  All packages will then be downloaded, built and installed.

4. Install AtomicParsley

    Use the following procedure to download and build the latest version:

        curl -kLO https://bitbucket.org/wez/atomicparsley/get/tip.zip
        unzip tip.zip
        cd wez*
        ./autogen.sh
        ./configure
        make
        # Slackware
        make install
        # Salix
        sudo make install
      
5. Install additional Perl modules

    If you wish to use the MP3::Tag module for better MP3 tagging, or you require the Net::SMTP::TLS::ButMaintained module for TLS email, additional Perl modules may be installed using the [local::lib method](https://github.com/get-iplayer/get_iplayer/wiki/unix#perl-locallib).	

6. Run CLI with:

    	get_iplayer [...]

### Web PVR Manager (WPM)

1. The WPM is installed with the CLI, but no launcher script is provided.  Launch the WPM in a terminal window with this command:

        perl /usr/share/get_iplayer/webcgi/get_iplayer.cgi -l 127.0.0.1 -p 1935

2. Once the WPM is running, connect to it by opening this URL in your browser:

    <http://127.0.0.1:1935>

3. After the WPM has opened in your browser, click the `Refresh Cache` button.  A new tab or window will open that shows the cache being refreshed.  Leave that tab or window open to have the cache refreshed automatically every hour.  You can also manually refresh the cache at any time.

4. Stop the WPM by typing Ctrl-C.
