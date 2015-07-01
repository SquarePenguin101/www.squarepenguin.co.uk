**Before you begin**: Linux/Unix packages are maintained by volunteers and may not be updated for some time after a new release of get_iplayer, thus the version of get_iplayer packaged for your system may be obsolete. You can find the version number of the latest get_iplayer release [here](https://github.com/get-iplayer/get_iplayer/releases). If the version packaged for your system is older than the latest release, it is likely that some functionality is broken. After following the instructions below, you may wish to uninstall the get_iplayer package and use the [manual installation instructions](/wiki/manual) to install the latest get_iplayer CLI and Web PVR Manager. 

## Slackware / Salix

These instructions are for Slackware / Salix 14.1. Differences between the two are noted where appropriate. The instructions assume you have a done a full install of Slackware / Salix.  If not, you may need to install additional packages. The instructions below assume you are logged in as root on Slackware and you are using `sudo` on Salix.

### Command-line Interface (CLI)

1. Before You Begin

	These instructions show how to install get_iplayer using **sbopkg** to download, build and install the required [SlackBuilds](http://slackbuilds.org/).  If you prefer to use a different installation method, use the instructions below to guide you.  Information on installing and configuring sbopkg can be found at:

	<http://www.sbopkg.org>

	<http://docs.slackware.com/howtos:slackware_admin:building_packages_with_sbopkg>

	Below are instructions for creating a custom sbopkg queuefile to install get_iplayer and dependencies in a single operation.  If you have used sbopkg before, do not be tempted to use any of the queuefiles from:

	<https://gitorious.org/sbopkg-slackware-queues>

	Some of the required queuefiles are broken and will cause the installation to fail.  Also, there are a few additional components not included in those queuefiles that are useful for full support of get_iplayer functionality.

2. Install Packaged Dependencies

	#### Slackware
	MPlayer is part of the XAP package set and should be part of a full install.  Install it from your Slackware distribution or a Slackware repository if necessary.

	#### Salix

	If you have performed a Salix basic installation, download the multimedia codecs installer (already available in a full install):

		sudo slapt-get -i salix-codecs-installer

	Run the multimedia codecs installer:
	
		sudo salix-codecs-installer

	Select all items for installation.  When the installation is complete, ffmpeg and rtmpdump will have been installed.

	Install mplayer:

		sudo slapt-get -i MPlayer

	
2. Create sbopkg queuefile

    These instructions assume you have configured sbopkg to read queuefiles from the default location `/var/lib/sbopkg/queues`.

	#### Slackware
	
	As root, create a sbopkg queuefile at this location:

	`/var/lib/sbopkg/queues/get_iplayer-full.sqf`

	The file contents should be **exactly** as shown below (the order is important):

		rtmpdump
		libmp4v2
		faac 
		xvidcore
		lame
		x264
		ffmpeg | RTMP=yes FAAC=yes XVID=yes
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

	If you require additional options for ffmpeg, adjust the queuefile options accordingly.  See:

	<http://slackbuilds.org/repository/14.1/multimedia/ffmpeg/>

	#### Salix
	
	As root, create a sbopkg queuefile at this location:

	`/var/lib/sbopkg/queues/get_iplayer-salix.sqf`

	The file contents should be **exactly** as shown below (the order is important):

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

3. Install get_iplayer and dependencies with queuefile

	#### Slackware

	Run this command:

        sbopkg -i get_iplayer-full

	When prompted to confirm the queuefile options for ffmpeg (RTMP=yes FAAC=yes XVID=yes), enter **q** to accept.  All packages will then be downloaded, built and installed.

	#### Salix

	Run this command:

        sudo sbopkg -i get_iplayer-salix

	The principal difference between the Slackware and Salix installations is that the Salix build of ffmpeg will be linked with  more external libraries but will not be linked with the FAAC codec library.  As mentioned above, you can change the options for building ffmpeg in Slackware  Either build will support all the formats necessary for get_iplayer.

4. Install AtomicParsley

    Use the following procedure to download and build the latest version:

        curl -kLO https://bitbucket.org/wez/atomicparsley/get/tip.zip
        unzip tip.zip
        cd wez*
        ./autogen.sh
        ./configure
        make
        make install (sudo make install on Salix)
      
5. Install additional Perl modules

    If you wish to use the MP3::Tag module for better MP3 tagging, or you require the Net::SMTP::TLS::ButMaintained module for TLS email, additional Perl modules may be installed using the [local::lib method](/wiki/manual#manual-perl-locallib).	
6. Run CLI with:

    	get_iplayer [...]

### Web PVR Manager (WPM)

1. The WPM is installed with the CLI, but no launcher script is provided.  Launch the WPM in a terminal window with this command:

        perl /usr/share/get_iplayer/webcgi/get_iplayer.cgi -l 127.0.0.1 -p 1935

2. Once the WPM is running, connect to it by opening this URL in your browser:

    <http://127.0.0.1:1935>

3. After the WPM has opened in your browser, click the `Refresh Cache` button.  A new tab or window will open that shows the cache being refreshed.  Leave that tab or window open to have the cache refreshed automatically every hour.  You can also manually refresh the cache at any time.

4. Stop the WPM by typing Ctrl-C.