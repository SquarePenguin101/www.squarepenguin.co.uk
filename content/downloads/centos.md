+++
categories = ["", ""]
date = "2016-07-05T13:27:45+01:00"
description = "Installation instructions for get_iplayer on CentOS and RHEL."
draft = false
pageimage = ""
pagesubtitle = "COMPREHENSIVE GUIDES TO GET YOU STARTED QUICKLY"
pagetitle = "get_iplayer installation guides"
slug = "centos"
title = "get_iplayer CentOS / RHEL installation guide"
Type = "downloads"
+++

**Before you begin**: Linux/Unix packages are maintained by volunteers and may not be updated for some time after a new release of get_iplayer, thus the version of get_iplayer packaged for your system may be obsolete. You can find the version number of the latest get_iplayer release [here](https://github.com/get-iplayer/get_iplayer/releases). If the version packaged for your system is older than the latest release, it is likely that some functionality is broken. After following the instructions below, you may wish to uninstall the get_iplayer package and use the [manual installation instructions](/wiki/unix) to install the latest get_iplayer CLI and Web PVR Manager. 

## CentOS / RHEL

These instructions are for CentOS / RHEL 7.

### Command-line Interface (CLI)

The instructions below assume you are logged in as root.

1. Configure nux-dextop repository

	Instructions to configure the nux-dextop repo can be found at:

	<http://li.nux.ro/repos.html> 

	Note that nux-dextop requires the EPEL (Extra Packages for Enterprise Linux) repo. The nux-dextop configuration process installs EPEL as well.

2. Install get_iplayer and dependencies (accept repo keys as required):

        yum install get_iplayer

3. Install additional Perl modules if desired

        yum install perl-Authen-SASL perl-Net-SMTP-SSL 

4. Run CLI with:

    	get_iplayer [...]

### Web PVR Manager (WPM)

The WPM is not installed with the get_iplayer package.  Use the [manual installation procedure](/wiki/unix).
