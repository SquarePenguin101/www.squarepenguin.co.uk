+++
categories = ["", ""]
date = "2016-07-05T13:27:45+01:00"
description = "Installation instructions for get_iplayer on Fedora."
draft = false
pageimage = ""
pagesubtitle = "COMPREHENSIVE GUIDES TO GET YOU STARTED QUICKLY"
pagetitle = "get_iplayer installation guides"
slug = "fedora"
title = "get_iplayer Fedora installation guide"
Type = "downloads"
+++

**Before you begin**: Linux/Unix packages are maintained by volunteers and may not be updated for some time after a new release of get_iplayer, thus the version of get_iplayer packaged for your system may be obsolete. You can find the version number of the latest get_iplayer release [here](https://github.com/get-iplayer/get_iplayer/releases). If the version packaged for your system is older than the latest release, it is likely that some functionality is broken. After following the instructions below, you may wish to uninstall the get_iplayer package and use the [manual installation instructions](/wiki/unix) to install the latest get_iplayer CLI and Web PVR Manager. 

## Fedora

These instructions are for Fedora 23.

### Command-line Interface (CLI)

1. Configure the RPM Fusion repositories as described here:

    <http://rpmfusion.org/Configuration>

2. Install get_iplayer and dependencies

        sudo dnf install get_iplayer

3. Install additional Perl modules

        sudo dnf install perl-MP3-Info perl-Authen-SASL perl-Net-SMTP-SSL

    If you wish to use the MP3::Tag module for better MP3 tagging, or you require support for TLS email, additional Perl modules may be installed using the [local::lib method](/wiki/manual#manual-perl-locallib).	

4. Run CLI with:

    	get_iplayer [...]

### Web PVR Manager (WPM)

The WPM is not installed with the get_iplayer package.  Use the [manual installation procedure](/wiki/unix).
