**Before you begin**: Linux/Unix packages are maintained by volunteers and may not be updated for some time after a new release of get_iplayer, thus the version of get_iplayer packaged for your system may be obsolete. You can find the version number of the latest get_iplayer release [here](https://github.com/get-iplayer/get_iplayer/releases). If the version packaged for your system is older than the latest release, it is likely that some functionality is broken. After following the instructions below, you may wish to uninstall the get_iplayer package and use the [manual installation instructions](/wiki/manual) to install the latest get_iplayer CLI and Web PVR Manager. 

## OpenBSD

These instructions are for OpenBSD 5.4-release.  The instructions assume that you are logged in as root, but you may perform the installation commands with `sudo`.

### Command-line Interface (CLI)

1. Install get_iplayer package and dependencies from release repository (assumes PKG_PATH configured)

        pkg_add get_iplayer

2. Install components not installed with get_iplayer package

        pkg_add ffmpeg mplayer p5-Net-SMTP-SSL p5-Authen-SASL p5-Net-SMTP-TLS-ButMaintained

3. Run CLI with:

    	get_iplayer [...]

### Web PVR Manager (WPM)

The WPM is not installed with the get_iplayer package.  Use the [manual installation procedure](/wiki/manual).