**Before you begin**: Linux/Unix packages are maintained by volunteers and may not be updated for some time after a new release of get_iplayer, thus the version of get_iplayer packaged for your system may be obsolete. You can find the version number of the latest get_iplayer release [here](https://github.com/get-iplayer/get_iplayer/releases). If the version packaged for your system is older than the latest release, it is likely that some functionality is broken. After following the instructions below, you may wish to uninstall the get_iplayer package and use the [manual installation instructions](/wiki/manual) to install the latest get_iplayer CLI and Web PVR Manager.

## Mageia

These instructions are for Mageia 5. Information for Mageia 4 can be found [here](/wiki/mageia4). These instructions assume you are logged in as root, but you may also perform the installation commands with `sudo`.

### Command-line Interface (CLI)

1. Ensure media sets are up-to-date

        urpmi.update -a tainted

2. (Re-)Install programs from tainted media set

    32-bit:

        urpmi --media tainted ffmpeg mplayer rtmpdump librtmp1

    64-bit:

        urpmi --media tainted ffmpeg mplayer rtmpdump lib64rtmp1

    This step is necessary because the restricted versions of these programs in the core and non-free media sets do not fully support all get_iplayer functionality.

3. Install get_iplayer and related applications

        urpmi get_iplayer atomicparsley

4. Install Perl modules

        urpmi perl-MP3-Tag perl-MP3-Info perl-XML-Simple perl-Net-SMTP-SSL perl-Authen-SASL perl-Net-SMTP-TLS-ButMaintained

5. Run CLI with:

    	get_iplayer [...]

### Web PVR Manager (WPM)

The WPM is not installed with the get_iplayer package.  Use the [manual installation procedure](/wiki/manual#manual-wpm).
