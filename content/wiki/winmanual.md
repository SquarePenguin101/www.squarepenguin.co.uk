## Windows Manual Installation

Windows users are strongly recommended to use the [get_iplayer Windows installer](/wiki/winsetup).  However if you must use your own Perl distribution and your own versions of rtmpdump, ffmpeg, etc., it is possible to do a manual installation on Windows.  The instructions below describe one way to perform a manual installation, but you may find a different method works better on your system.

### Perl Support

It is recommended that you install [Strawberry Perl](http://strawberryperl.com/).  That is the only distribution of Perl for Windows used to test get_iplayer.  However, other Perl distributions are likely to work.

Use the CPAN client from your Perl distribution to install additional modules for get_iplayer (some modules may already be part of the base install):

	cpan LWP MP3::Info MP3::Tag Net::SMTP::SSL Authen::SASL Net::SMTP::TLS::ButMaintained XML::Simple

### External Programs

You will need to locate or build the external programs yourself.  You can see the versions used by the get_iplayer Windows installer if you download this file:

<http://www.infradead.org/get_iplayer_win/get_iplayer_config_latest.ini>

The file is in INI format.  The "url" value in each section contains the  download URL for that program.  Extract the downloaded archives and install the binaries to your location of choice.

**NOTE:** LAME and VLC support obsolete functionality and thus are not generally required for manual installation.  They appear in the above .INI file for use by the Windows installer.  If you wish to use VLC as media viewer, perform a full VLC installation separately.

### Command-line Interface (CLI)

1. Download an archive of the latest get_iplayer release from:

	<https://github.com/get-iplayer/get_iplayer/releases>

2. After downloading, extract the archive.  These instructions assume the archive has been extracted to `C:\tmp\get_iplayer`.

3. Create an installation directory for the get_iplayer scripts.  These instructions assume you are using `C:\get_iplayer`.

4. Copy the scripts to the installation directory.  You need both the get_iplayer script and its batch file wrapper:

		cd C:\tmp\get_iplayer
		rem main script must have .pl extension added
		copy get_iplayer C:\get_iplayer\get_iplayer.pl
		copy windows\get_iplayer\get_iplayer.cmd C:\get_iplayer

5. Go to installation directory
	
		cd C:\get_iplayer

6. Fix batch file wrapper (`get_iplayer.cmd`) for standalone use

	The batch file is coded so that it expects get_iplayer.pl to be in the user's working directory (this is how the installer version works).  The batch file should be changed to look for get_iplayer.pl in the installation directory, regardless of the user's working directory.  This means you can install the CLI somewhere in PATH and use it from any location.

	Open the batch file in a text editor and change the path to get_iplayer.pl.  Change:

		@echo off
		perl.exe get_iplayer.pl %*
	to
		
		@echo off
		perl.exe "%~dp0\get_iplayer.pl" %*

	and save the file.
	
	NOTE: the batch file assumes that perl.exe is installed somewhere in PATH.  If it is not, put the full path to perl.exe in the batch file.	
7. Execute get_iplayer once to initialise the config directory (`%USERPROFILE%\.get_iplayer`) and download plugins

    	get_iplayer

8. Configure external programs

	If the external programs needed by get_iplayer are not installed in PATH, you must explicitly configure their locations in your get_iplayer preferences.  For example:

		get_iplayer --prefs-add --rtmpdump="C:\path\to\rtmpdump.exe" --ffmpeg="C:\path\to\ffmpeg.exe" --mplayer="C:\path\to\mplayer.exe" --atomicparsley="C:\path\to\atomicparsley.exe"

9. Configure output directory

	Programmes will be downloaded to the working directory by default, so you will probably want to configure a permanent output directory.  The example below is the configuration used by the Windows installer version, but you may configure any directory of your choice.

		mkdir "%USERPROFILE%\Desktop\iPlayer Recordings"
		get_iplayer --prefs-add --output "%USERPROFILE%\Desktop\iPlayer Recordings"

10. Run CLI with:

    	get_iplayer [...]
    	

### Web PVR Manager (WPM)

Ensure the CLI has been installed as described above.

1. Copy the scripts to installation directory.   You need both the get_iplayer.cgi script and its batch file wrapper:

		cd C:\tmp\get_iplayer
		copy get_iplayer.cgi C:\get_iplayer
		copy windows\get_iplayer\get_iplayer.cgi.cmd C:\get_iplayer
	
2. Go to installation directory
	
		cd C:\get_iplayer

3. Fix batch file wrapper (`get_iplayer.cgi.cmd`) for standalone use

	The batch file is coded so that it expects get_iplayer.cgi and get_iplayer.cmd to be in the user's working directory (this is how the installer version works).  The batch file should be changed to look for those files in the installation directory, regardless of the user's working directory.  This means you can install the WPM somewhere in PATH and use it from any location.

	Open the batch file in a text editor and change the path to get_iplayer.cmd. Change:

		@echo off
		perl.exe get_iplayer.cgi --port 1935 --listen=127.0.0.1 --getiplayer .\get_iplayer.cmd

	to
		
		@echo off
		perl.exe "%~dp0\get_iplayer.cgi" --port 1935 --listen=127.0.0.1 --getiplayer "%~dp0\get_iplayer.cmd"

	and save the file.

	NOTE: the batch file assumes that perl.exe is installed somewhere in PATH.  If it is not, put the full path to perl.exe in the batch file.

4. Launch WPM in a console window with this command:

    	get_iplayer.cgi.cmd

5. Once the WPM is running, connect to it by opening this URL in your browser:

    <http://localhost:1935>

6. After the WPM has opened in your browser, click the `Refresh Cache` button.  A new tab or window will open that shows the cache being refreshed.  Leave that tab or window open to have the cache refreshed automatically every hour.  You can also manually refresh the cache at any time.

7. Stop the WPM by typing Ctrl-C.