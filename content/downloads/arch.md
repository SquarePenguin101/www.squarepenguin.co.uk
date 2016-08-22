+++
categories = ["", ""]
date = "2016-07-05T13:27:45+01:00"
description = "Installation instructions for get_iplayer on Arch Linux."
draft = false
pageimage = ""
pagesubtitle = "COMPREHENSIVE GUIDES TO GET YOU STARTED QUICKLY"
pagetitle = "get_iplayer installation guides"
slug = "arch"
title = "get_iplayer Arch Linux installation guide"
Type = "downloads"
+++

**Before you begin**: Linux/Unix packages are maintained by volunteers and may not be updated for some time after a new release of get_iplayer, thus the version of get_iplayer packaged for your system may be obsolete. You can find the version number of the latest get_iplayer release [here](https://github.com/get-iplayer/get_iplayer/releases). If the version packaged for your system is older than the latest release, it is likely that some functionality is broken. After following the instructions below, you may wish to uninstall the get_iplayer package and use the [manual installation instructions](https://github.com/get-iplayer/get_iplayer/wiki/unix) to install the latest get_iplayer CLI and Web PVR Manager. 

## Arch Linux

These instructions are for Arch Linux

### Command-line Interface (CLI)

1. Install packages available in official repositories

		sudo pacman -S rtmpdump ffmpeg id3v2 atomicparsley perl-xml-simple perl-mp3-info perl-net-smtp-ssl perl-authen-sasl

2. Prepare to build packages from Arch User Repository (AUR)

	Although not covered here, you may also be able to install the AUR packages with an AUR helper, for example, [Yaourt](https://wiki.archlinux.org/index.php/Yaourt).

	Install required development tools:

		sudo pacman -S --needed base-devel

	Make a base directory for the package builds:

		mkdir ~/abs

	Download, build and install each package in turn, as shown below.

3. Install Perl modules

	Install additional Perl modules:

		cd ~/abs
		curl -kLO https://aur.archlinux.org/cgit/aur.git/snapshot/perl-mp3-tag.tar.gz
		tar xzf perl-mp3-tag.tar.gz
		cd perl-mp3-tag
		makepkg -s
		sudo pacman -U perl-mp3-tag*.tar.xz
	
		cd ~/abs
		curl -kLO https://aur.archlinux.org/cgit/aur.git/snapshot/perl-net-smtp-tls.tar.gz
		tar xzf perl-net-smtp-tls.tar.gz
		cd perl-net-smtp-tls
		makepkg -s
		sudo pacman -U perl-net-smtp-tls*.tar.xz

4. Install get_iplayer

	There are 2 AUR packages for get_iplayer. The *get_iplayer* package installs a release version of get_iplayer. The *get_iplayer-git* package may install a later development snapshot of get_iplayer, so it may contain new features or changes not incorporated in the current release version. However, the *get_iplayer-git* package requires installation of the *git* revision control system in order to retrieve the get_iplayer code. If in doubt, install the *get_iplayer* package.

		cd ~/abs
		curl -kLO https://aur.archlinux.org/cgit/aur.git/snapshot/get_iplayer.tar.gz
		tar xzf get_iplayer.tar.gz
		cd get_iplayer
		makepkg -s
		sudo pacman -U get_iplayer*.tar.xz

	OR

		cd ~/abs
		curl -kLO https://aur.archlinux.org/cgit/aur.git/snapshot/get_iplayer-git.tar.gz
		tar xzf get_iplayer-git.tar.gz
		cd get_iplayer-git
		makepkg -s
		sudo pacman -U get_iplayer-git*.tar.xz

5. Run CLI with:

		get_iplayer [...]

### Web PVR Manager (WPM)

The WPM is installed along with the CLI.

1. Launch the WPM in a terminal window with this command:

        get_iplayer.cgi --listen 127.0.0.1 --port 1935

2. Once the WPM is running, connect to it by opening this URL in your browser:

    <http://127.0.0.1:1935>

3. After the WPM has opened in your browser, click the `Refresh Cache` button.  A new tab or window will open that shows the cache being refreshed.  Leave that tab or window open to have the cache refreshed automatically every hour.  You can also manually refresh the cache at any time.

4. Stop the WPM by typing Ctrl-C.