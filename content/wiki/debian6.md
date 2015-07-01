## Debian 6

These instructions are for Debian 6 (squeeze) only.

### Command-line Interface (CLI)

The get-iplayer package available in the squeeze repository is obsolete and should not be installed.  The procedure below is one way to install the get-iplayer package from Debian testing (jessie) on Debian squeeze without adding the Debian testing repository to your system.  However, you may wish to add the Debian testing repository or perhaps use some other method. Although installing packages from Debian testing on a stable system is often discouraged, it is currently safe to do so with the get-iplayer package.

1. Add the **squeeze-backports** repository according to these instructions:

    <http://backports.debian.org/Instructions/>

2. Ensure package database is current:

        sudo apt-get update

3. Download the get-iplayer package for Debian testing from your preferred mirror:

    <http://packages.debian.org/testing/all/get-iplayer/download>

4. Install the downloaded DEB file (version 2.82-2 in this example):

        sudo gdebi get-iplayer_2.82-2_all.deb
    
    Required dependencies will also be installed.

5. Install components not installed by gdebi:

        sudo apt-get install atomicparsley id3v2 libmp3-info-perl libmp3-tag-perl libnet-smtp-ssl-perl libauthen-sasl-perl libnet-smtp-tls-perl

6. Install components from squeeze-backports:

        sudo apt-get -t squeeze-backports install ffmpeg mplayer
    
    If you already have ffmpeg and mplayer packages installed, they will be upgraded.  The ffmpeg package must be upgraded since it is not compatible with newer versions of get_iplayer.

7. Run CLI:

        get_iplayer [...]

### Web PVR Manager (WPM)

The WPM is installed along with the CLI.

1. Launch the WPM with:

        get_iplayer_web_pvr

2. Once the WPM is running, connect to it by opening this URL in your browser:

    <http://127.0.0.1:1935>

3. After the WPM has opened in your browser, click the `Refresh Cache` button.  A new tab or window will open that shows the cache being refreshed.  Leave that tab or window open to have the cache refreshed automatically every hour.  You can also manually refresh the cache at any time.

4. Stop the WPM by typing Ctrl-C.