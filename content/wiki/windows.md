## Windows Installation

<a name="installer"></a>
Windows users should install get_iplayer with the provided installer.  Download the latest version from:

<https://github.com/get-iplayer/get_iplayer_win32/releases/latest>

The installer includes all necessary dependencies: AtomicParsley, ffmpeg, rtmpdump and a customised version of [Strawberry Perl](http://strawberryperl.com/).

### Command-line Interface (CLI)

1. Start the installer and follow the wizard steps in the usual manner. There are no user-selectable options in the installer. Once you agree to the licence, an "All Users" installation will be performed, with get_iplayer installed into `C:\Program Files\get_iplayer` (`C:\Program Files (x86)\get_iplayer` on 64-bit Windows).

2. To start the CLI go to `All Programs -> get_iplayer -> get_iplayer` on the Start menu (`All Apps -> get_iplayer -> get_iplayer` on Windows 10). In the Windows 8 Start screen, click the `get_iplayer` tile. The CLI will launch in a console window.  The working directory of the console window will be your home directory (`%HOMEDRIVE%%HOMEPATH%`).

3. Upon launch, get_iplayer will update its programme index cache if necessary. When updating has completed, you will see a cursor waiting at a command prompt. The prompt will look something like `C:\Users\jbloggs>`. Type your get_iplayer commands at the prompt, then hit `Return` after each one to run it. See [Usage and Examples](documentation) for examples of get_iplayer commands.

4. The default location for recorded programmes is the `iPlayer Recordings` folder on your Windows desktop. If get_iplayer cannot locate your desktop folder, it will download into your working directory. If you wish to use a custom location, set it in your get_iplayer preferences. For example:

		get_iplayer --prefs-add --output "D:\iplayer"

### Web PVR Manager (WPM)

The WPM is installed along with the CLI.

1. To start the WPM go to `All Programs -> get_iplayer -> Web PVR Manager` on the Start menu (`All Apps -> get_iplayer -> Web PVR Manager` on Windows 10).  In the Windows 8 Start screen, click the `Web PVR Manager` tile.

2. The WPM server will launch in a console window and your default browser will be opened to this URL:

    <http://localhost:1935>

    If the WPM does not open in your browser automatically, click the link above or enter the address in your web browser.

3. After the WPM has opened in your browser, select the programme types you wish to index (e.g., BBC TV, BBC Radio), then click the `Refresh Cache` button.  A new tab or window will open that shows the cache being refreshed.  Leave that tab or window open to have the cache refreshed automatically every hour.  You can also manually refresh the cache at any time.

4. Stop the WPM by closing the console window where it is running.

### Notes

- The installer will append the installation directory to the value of your system PATH environment variable. You can thus invoke the CLI from any command prompt (e.g., from the taskbar) with any working directory by entering your get_iplayer command at the prompt and hitting `Return`. The Start Menu shortcut described above is installed for convenience.

- The path for the embedded Perl distribution (`perl` subdirectory) and the path to the included atomicparsley, ffmpeg and rtmpdump utilities (`utils` subdirectory) are not permanently added to `%PATH%`. They are temporarily prepended to `%PATH%` only when get_iplayer batch scripts are running. If `%PATH%` is already quite large, e.g. because of other software packages that did not properly update `%PATH%` on install or uninstall, you may experience problems launching perl or external programs. In that case, you will need to clean obsolete entries from your PATH environment variable settings. Run `echo %PATH%` from a command prompt to check the value. This should affect few users.

- When you launch get_iplayer or the Web PVR Manager, you are actually invoking a batch script (`.cmd` file) that wraps the Perl script that comprises the application. The batch script is required to set up the runtime environment for the associated Perl script. **Any other method of launching get_iplayer or the Web PVR Manager is NOT SUPPORTED**.

- **Do not launch get_iplayer or the Web PVR Manager with 'Run as administrator'**. It will open the get_iplayer console window in `C:\WINDOWS\system32`, which is a system directory where you should not be working. It should not be necessary to run the CLI or WPM as an administrator.

<a name="custom"></a>
## Customising get_iplayer on Windows

**NOTE: These instructions are intentionally terse and assume certain knowledge on your part. If you do not understand them, do not attempt to  customise get_iplayer on Windows. Installation and usage of a customised version are NOT SUPPORTED.**

If you wish to make a custom version of get_iplayer on Windows, don't make changes to files created by the installer. Instead, do the following:

- Temporarily install get_iplayer using the Windows installer
- Copy the installation directory (`C:\Program Files\get_iplayer` or `C:\Program Files (x86)\get_iplayer`) to a new location, e.g., `C:\gip`.
- Do a complete uninstall of get_iplayer and remove the default installation directory if necessary (you can always reinstall later).
- Change the CLI (`get_iplayer.pl`) or WPM (`get_iplayer.cgi`) Perl scripts as desired

You can run your customised copy of the CLI or WPM by invoking the appropriate batch script directly (e.g., `C:\gip\get_iplayer.cmd` or `C:\gip\pvr_manager.cmd`), or you can add the new directory `C:\gip` to `%PATH%` and run `get_iplayer` or `pvr_manager` at a command prompt as normal.

If you wish to use your own version of Perl, remove or rename the `perl` subdirectory and get_iplayer should pick it up (perl.exe should be in `%PATH%`). Remember that the LWP, XML::Simple and XML::LibXML modules must be installed in your version of Perl.

If you wish to use your own versions of AtomicParsley, ffmpeg and rtmpdump, remove or rename the `utils` subdirectory (location of the embedded utilities) and get_iplayer should pick up your versions if they are in `%PATH%`. If your utilities are not in `%PATH%`, use the `--atomicparsley`, `--ffmpeg`  and `--rtmpdump` options to configure get_iplayer to use them.
