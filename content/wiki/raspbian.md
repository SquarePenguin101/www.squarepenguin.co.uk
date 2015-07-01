**Before you begin**: Linux/Unix packages are maintained by volunteers and may not be updated for some time after a new release of get_iplayer, thus the version of get_iplayer packaged for your system may be obsolete. You can find the version number of the latest get_iplayer release [here](https://github.com/get-iplayer/get_iplayer/releases). If the version packaged for your system is older than the latest release, it is likely that some functionality is broken. After following the instructions below, you may wish to uninstall the get_iplayer package and use the [manual installation instructions](/wiki/manual) to install the latest get_iplayer CLI and Web PVR Manager. 

## Raspbian / Raspberry Pi

These instructions are for Raspbian wheezy.

### Command-line Interface (CLI)

Although the Debian get-iplayer package is incorporated in Raspbian repositories, Raspbian users are recommended to use the get_iplayer repository version (see below).  If you must use the Debian package, refer to the above instructions for Debian installation.  Note that the version of AtomicParsley packaged with Raspbian frequently fails with files downloaded with get_iplayer.

#### get_iplayer Repository Installation

1. Add the repository

    Paste these _five_ lines into a terminal window:

	    sudo bash -c "cat > /etc/apt/sources.list.d/packages.hedgerows.org.uk.list <<EOF
	    deb http://packages.hedgerows.org.uk/raspbian wheezy/
	    deb-src http://packages.hedgerows.org.uk/raspbian wheezy/
	    EOF
	    "

2. Update, and install the repository signing key, and update again:

	    sudo apt-get update
	    sudo apt-get --allow-unauthenticated -y install jonhedgerows-keyring
	    sudo apt-get update

3. Install the get-iplayer package

    	sudo apt-get install get-iplayer

4. Run CLI with:

    	get_iplayer [...]

### Web PVR Manager (WPM)

The WPM is installed along with the CLI.

1. Launch the WPM in a terminal window with this command:

    	get_iplayer_web_pvr

2. Once the WPM is running, connect to it by opening this URL in your browser:

    <http://127.0.0.1:1935>

3. After the WPM has opened in your browser, click the `Refresh Cache` button.  A new tab or window will open that shows the cache being refreshed.  Leave that tab or window open to have the cache refreshed automatically every hour.  You can also manually refresh the cache at any time.

4. Stop the WPM by typing Ctrl-C.