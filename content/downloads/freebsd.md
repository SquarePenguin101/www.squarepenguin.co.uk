+++
categories = ["", ""]
date = "2016-07-05T13:27:45+01:00"
description = "Installation instructions for get_iplayer on FreeBSD / PC-BSD."
draft = false
pageimage = ""
pagesubtitle = "COMPREHENSIVE GUIDES TO GET YOU STARTED QUICKLY"
pagetitle = "get_iplayer installation guides"
slug = "freebsd"
title = "get_iplayer FreeBSD / PC-BSD installation guide"
Type = "downloads"
+++

**Before you begin**: Linux/Unix packages are maintained by volunteers and may not be updated for some time after a new release of get_iplayer, thus the version of get_iplayer packaged for your system may be obsolete. You can find the version number of the latest get_iplayer release [here](https://github.com/get-iplayer/get_iplayer/releases). If the version packaged for your system is older than the latest release, it is likely that some functionality is broken. After following the instructions below, you may wish to uninstall the get_iplayer package and use the [manual installation instructions](/wiki/unix) to install the latest get_iplayer CLI and Web PVR Manager. 

## FreeBSD / PC-BSD

These instructions are for FreeBSD / PC-BSD 10.2.  The instructions assume that you are logged in as root, but the installation commands may also be performed with `sudo`.

### Command-line Interface (CLI)

1. Install Perl

        pkg install perl5

    NOTE: Perl will likely already be installed if you installed a desktop environment.

2. Install get_iplayer

        pkg install get_iplayer

3. Install additional external programs

        pkg install AtomicParsley id3v2 ffmpeg

    **FreeBSD Only:** The `--aactomp3` option for get_iplayer will not work with the packaged version of ffmpeg because it is not built with support for the LAME MP3 encoder.

4. Install additional Perl modules

        pkg install p5-MP3-Tag p5-MP3-Info p5-Net-SMTP-SSL p5-Net-SMTP-TLS-ButMaintained

5. Run CLI:

        get_iplayer [...]

### Web PVR Manager (WPM)

The WPM is installed as a system service, but it is broken as delivered.  Instructions to fix it are given below, but you are encouraged to use the [manual installation procedure](/wiki/manual).

1. Create a location to store preferences, caches, and downloads

	As installed, the WPM will not work because it does not have a writeable location configured for get_iplayer preferences and caches.  The default download location is /tmp, which means your downwloads would be wiped on reboot.

	Create a working directory for the WPM service with the commands below.  The WPM service runs as the *get_iplayer* user, so the directory must be writable by that user.
	 	
		mkdir /usr/home/get_iplayer
		chown get_iplayer:get_iplayer /usr/home/get_iplayer

2. Patch the WPM service script

	The rtmpdump utility requires that the HOME environment variable point to a writeable location in order to store the `.swfinfo` file used for SWF verification.  get_iplayer also uses HOME to locate preferences and caches.  The WPM service runs as the *get_iplayer* user, but HOME is set for the *root* user and cannot be written by the WPM.  The effect is that no caches can be saved and thus no programmes appear in the WPM search results.  SWF verification also will fail.

	Open the WPM service script (`/usr/local/etc/rc.d/get_iplayer`) in a text editor.  The last line of the script should be:

		run_rc_command "$1"

	Insert the line below immediately **before** the last line:

		export HOME="${get_iplayer_chdir}"

	The last two lines in the script should now be:

		export HOME="${get_iplayer_chdir}"
		run_rc_command "$1"

	Save the edited file.

	These changes have the effect of setting HOME for the WPM service script to the working directory created in #1.  The *get_iplayer* user - and thus the WPM service and rtmpdump - can write to that location.  Preferences and caches for the *get_iplayer* user can be stored and the WPM will work correctly.

3. Configure the WPM service

	Add the following lines to /etc/rc.conf:
	
		get_iplayer_enable="YES"
		get_iplayer_chdir="/usr/home/get_iplayer"
		get_iplayer_bind_port="1935"

	These settings:
	* Enable the WPM service.  It will now start at boot time.
	* Set the WPM working directory.  This is where downloads will be saved by default.
	* Set the port where the WPM listens for connections.  The default value in the FreeBSD port is 9370, but has been reset here to 1935, the value typically used on other platforms. Port 1935 is used to support RTMP streaming from the WPM.  If you don't require that functionality, you can omit the `get_iplayer_bind_port` setting and keep the default port.
	
4. Start the WPM service in a terminal window with this command

		service get_iplayer start

5. Once the WPM is running, connect to it by opening this URL in your browser:

	<http://127.0.0.1:1935>

	OR
  
	<http://127.0.0.1:9370>

	if you kept the default FreeBSD port setting.

6. After the WPM has opened in your browser, click the `Refresh Cache` button.  A new tab or window will open that shows the cache being refreshed.  Leave that tab or window open to have the cache refreshed automatically every hour.  You can also manually refresh the cache at any time.