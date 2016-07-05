+++
categories = ["", ""]
date = "2016-07-05T13:27:45+01:00"
description = "Installation instructions for get_iplayer on openSUSE."
draft = false
pageimage = ""
pagesubtitle = "COMPREHENSIVE GUIDES TO GET YOU STARTED QUICKLY"
pagetitle = "get_iplayer installation guides"
slug = "opensuse"
title = "get_iplayer openSUSE installation guide"
Type = "downloads"
+++

**Before you begin**: Linux/Unix packages are maintained by volunteers and may not be updated for some time after a new release of get_iplayer, thus the version of get_iplayer packaged for your system may be obsolete. You can find the version number of the latest get_iplayer release [here](https://github.com/get-iplayer/get_iplayer/releases). If the version packaged for your system is older than the latest release, it is likely that some functionality is broken. After following the instructions below, you may wish to uninstall the get_iplayer package and use the [manual installation instructions](/wiki/unix) to install the latest get_iplayer CLI and Web PVR Manager. 

## openSUSE

These instructions are for openSUSE Leap 42.1.

### Command-line Interface (CLI)

1. Install restricted formats support according to the instructions here:

    <http://opensuse-community.org/Restricted_formats>
    
    The Packman repository should now be added to your system.  The ffmpeg utility also will have been installed.

    NOTE: Do not install the ffmpeg build provided in the openSUSE repositories. It does not provide the necessary codec support for get_iplayer. If you already installed the openSUSE-supplied ffmpeg, you must upgrade and change vendor for the ffmpeg package and all its subpackages. You cannot upgrade just the ffmpeg package - all must be installed from Packman.

2. Update package database

    	sudo zypper refresh

3. Install get_iplayer package and dependencies

    The get_iplayer package in the [Packman](http://packman.links2linux.org/package/get_iplayer) repository is no longer maintained and should not be used.  You can find a package supplied through the openSUSE Build Service: 

    <http://software.opensuse.org/package/get_iplayer>

    Although labelled as unstable, the package should be safe to install. You may opt for one-click installation, or you may download the RPM file and install it manually (use current version and rpm):

    	sudo zypper install get_iplayer-2.94-3.1.noarch.rpm

4. Install components not installed with get_iplayer package

    	sudo zypper install perl-MP3-Info perl-MP3-Tag perl-Net-SMTP-SSL perl-Authen-SASL id3v2

5. Install additional Perl modules

    The official openSUSE repositories do not provide packages for Perl support for TLS secure email.  You can find a third-party package supplied through the openSUSE Build Service: 

    <http://software.opensuse.org/package/perl-Net-SMTP-TLS>

    Although labelled as unstable, this package should be safe to install. You may opt for one-click installation, or you may download the RPM file and install it manually (amend file name as needed):

    	sudo zypper install perl-Net-SMTP-TLS-0.12-6.1.noarch.rpm

6. Install AtomicParsley

    The official openSUSE repositories do not provide a package for AtomicParsley.  You can find a third-party package supplied through the openSUSE Build Service: 

    <http://software.opensuse.org/package/AtomicParsley>

    Although labelled as unstable, the package should be safe to install. You may opt for one-click installation, or you may download the RPM file and install it manually (amend file name as needed):

    	sudo zypper install AtomicParsley-0.9.6-2.1.x86_64.rpm

    NOTE: Download the correct AtomicParsley RPM for your system architecture.

7. Run CLI with:

    	get_iplayer [...]


### Web PVR Manager (WPM)

1. Install CLI as described above

2. Install WPM package and dependencies

    The get_iplayer-pvr package in the [Packman](http://packman.links2linux.org/package/get_iplayer) repository has not been updated to 2.83+ and thus should not be used.  You can find an updated package supplied through the openSUSE Build Service: 

    <http://software.opensuse.org/package/get_iplayer-pvr>

    Although labelled as unstable, the package should be safe to install. You may opt for one-click installation, or you may download the RPM file and install it manually  (use current version and rpm):

    	sudo zypper install get_iplayer-pvr-2.94-1.1.noarch.rpm

3. Launch the WPM in a terminal window with this command:

    	get_iplayer_pvr
    
    The WPM will open in a new xterm and your default browser will open to this URL:
    
    <http://127.0.0.1:1935>

    **NOTE:** As of get_iplayer v2.83, WPM startup is broken in the openSUSE package.  You will see a message saying "The web pvr was unable to start." and your browser will not open.  However, the WPM actually will have started.  You can connect to it in your browser by clicking the URL above or entering the address in your web browser.

4. After the WPM has opened in your browser, click the `Refresh Cache` button.  A new tab or window will open that shows the cache being refreshed.  Leave that tab or window open to have the cache refreshed automatically every hour.  You can also manually refresh the cache at any time.

5. Stop the WPM by typing Ctrl-C in the small xterm window where it is running.