+++
categories = ["", ""]
date = "2016-07-05T13:27:45+01:00"
description = "Installation instructions for get_iplayer on Mageia."
draft = false
pageimage = ""
pagesubtitle = "COMPREHENSIVE GUIDES TO GET YOU STARTED QUICKLY"
pagetitle = "get_iplayer installation guides"
slug = "mageia"
title = "get_iplayer Mageia installation guide"
Type = "downloads"
+++

**Before you begin**: Linux/Unix packages are maintained by volunteers and may not be updated for some time after a new release of get_iplayer, thus the version of get_iplayer packaged for your system may be obsolete. You can find the version number of the latest get_iplayer release [here](https://github.com/get-iplayer/get_iplayer/releases). If the version packaged for your system is older than the latest release, it is likely that some functionality is broken. After following the instructions below, you may wish to uninstall the get_iplayer package and use the [manual installation instructions](https://github.com/get-iplayer/get_iplayer/wiki/unix) to install the latest get_iplayer CLI and Web PVR Manager.

## Mageia

These instructions are for Mageia 5. These instructions assume you are logged in as root, but you may also perform the installation commands with `sudo`.

### Command-line Interface (CLI)

1. Ensure media sets are up-to-date

        urpmi.update -a tainted

2. (Re-)Install programs from tainted media set

    32-bit:

        urpmi --media tainted ffmpeg rtmpdump librtmp1

    64-bit:

        urpmi --media tainted ffmpeg rtmpdump lib64rtmp1

    This step is necessary because the restricted versions of these programs in the core and non-free media sets do not fully support all get_iplayer functionality.

3. Install get_iplayer and related applications

        urpmi get_iplayer atomicparsley

4. Install Perl modules

        urpmi perl-MP3-Tag perl-MP3-Info perl-XML-Simple perl-Net-SMTP-SSL perl-Authen-SASL perl-Net-SMTP-TLS-ButMaintained

5. Run CLI with:

    	get_iplayer [...]

### Web PVR Manager (WPM)

The WPM is not installed with the get_iplayer package.  Use the [manual installation procedure](https://github.com/get-iplayer/get_iplayer/wiki/unix/).
