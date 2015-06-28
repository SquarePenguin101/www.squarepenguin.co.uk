## Windows Installer

Windows users should install get_iplayer with the provided installer.  Download the latest version from:

<http://www.infradead.org/get_iplayer_win/get_iplayer_setup_latest.exe>

**NOTE:** You must run the installer while logged in as a user that has administrator privileges.  If you are the only user on your PC you should already have administrator privileges. If you are logged in as a normal user and elevate your privileges by signing in as an administrator at the UAC prompt or by invoking the installer via "Run as Administrator", the menu shortcuts and output directory will be installed for the administrator account, not the logged-in user.  You can temporarily assign your user account to the Administrators group to run the installer. If you subsequently run get_iplayer while logged in as a different, non-administrator user you will not be able to access the output directory configured by the installer.  You will need to use the `--output` option to specify a separate output directory (can be saved in preferences).   The "Recording -> Override Recordings Folder" setting serves the same function for the Web PVR Manager.

### Perl Support

The installer will install a private customised version of [Strawberry Perl](http://strawberryperl.com/) that includes all necessary Perl modules.  It will not interfere with any other Perl distribution you may already have installed.

### External Programs

The installer will download and install all the required Windows support programs.

### Command-line Interface (CLI)

1. Start the installer and follow the wizard in the usual manner.  Select all components for installation The installer will download and install get_iplayer, Perl and the Windows support programs: RTMPDump, FFmpeg, MPlayer, LAME, AtomicParsley and VLC Media Player. 

2. To start the CLI go to `All Programs -> get_iplayer -> Get_iPlayer` on the Start menu.  In the Windows 8 Start screen, click the `Get_iPlayer` tile.   The CLI will launch in a console window.  The working directory of the console window will be the get_iplayer installation directory, typically `C:\Program Files\get_iplayer` or `C:\Program Files (x86)\get_iplayer` on 64-bit Windows.  The CLI expects to operate in that directory, so do not change to another location.

3. The first time MPlayer runs (i.e., the first time you download a regional or local radio programme) after a fresh installation, it will scan the available fonts on your system to update its font cache.  This scan will produce a large volume of extra output in your console window.  This will not affect the programme download, though it may take a long time if you have a large number of fonts installed.  MPlayer will update its font cache whenever it detects that your installed fonts have changed.

4. **NOTE**: Unless you opt to change the default value, the installer sets the location for recorded programmes to `iPlayer Recordings` on the Windows desktop of the administrator user who ran the installer.  If you have multiple users running get_iplayer on one Windows PC, the other users will need to configure their own output folders with the CLI:

		get_iplayer --prefs-add --output "%USERPROFILE%\Desktop\iPlayer Recordings"

### Web PVR Manager (WPM)

The WPM is installed along with the CLI.
    
1. To start the WPM go to `All Programs -> get_iplayer -> Web PVR Manager` on the Start menu.  In the Windows 8 Start screen, click the `Web PVR Manager` tile.  

2. The WPM will launch in a console window and your default browser will be opened to this URL:

    <http://localhost:1935>

    If the WPM does not open in your browser automatically, click the link above or enter the address in your web browser.

3. After the WPM has opened in your browser, click the `Refresh Cache` button.  A new tab or window will open that shows the cache being refreshed.  Leave that tab or window open to have the cache refreshed automatically every hour.  You can also manually refresh the cache at any time.

4. Stop the WPM by typing Ctrl-Break in the console window where it is running.