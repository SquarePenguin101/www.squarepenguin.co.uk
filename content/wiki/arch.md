**Before you begin**: Linux/Unix packages are maintained by volunteers and may not be updated for some time after a new release of get_iplayer, thus the version of get_iplayer packaged for your system may be obsolete. You can find the version number of the latest get_iplayer release [here](https://github.com/get-iplayer/get_iplayer/releases). If the version packaged for your system is older than the latest release, it is likely that some functionality is broken. After following the instructions below, you may wish to uninstall the get_iplayer package and use the [manual installation instructions](/wiki/manual) to install the latest get_iplayer CLI and Web PVR Manager. 

## Arch Linux

These instructions are for Arch Linux

### Command-line Interface (CLI)

1. Install packages available in official repositories

		sudo pacman -S rtmpdump ffmpeg id3v2 perl-xml-simple perl-mp3-info

2. Prepare to build packages from Arch User Repository (AUR)

	Although not covered here, you may also be able to install the AUR packages with an AUR helper, for example, [Yaourt](https://wiki.archlinux.org/index.php/Yaourt).

	First, make a base directory for the package builds:

		mkdir ~/abs

	Then download, build and install each package in turn, as shown below.

3. Install get_iplayer

	There are 2 AUR packages for get_iplayer. The *get_iplayer* package installs a release version of get_iplayer. The *get_iplayer-git* package installs a later development snapshot of get_iplayer, so it may contain new features or changes not incorporated in the current release version.

		cd ~/abs
		curl -kLO https://aur.archlinux.org/packages/ge/get_iplayer/get_iplayer.tar.gz
		tar xzf get_iplayer.tar.gz
		cd get_iplayer
		makepkg -s
		sudo pacman -U get_iplayer*.tar.xz

	OR

		cd ~/abs
		curl -kLO https://aur.archlinux.org/packages/ge/get_iplayer-git/get_iplayer-git.tar.gz
		tar xzf get_iplayer-git.tar.gz
		cd get_iplayer-git
		makepkg -s
		sudo pacman -U get_iplayer-git*.tar.xz

4. Install AtomicParsley

	There are 2 AUR packages for AtomicParsley.  The *atomicparsley* package is very old and not recommended for use with get_iplayer.  The *atomicparsley-largefiles-hg* package installs the latest development version of AtomicParsley.  However, it requires you to install Mercurial and its dependencies.

		cd ~/abs
		curl -kLO https://aur.archlinux.org/packages/at/atomicparsley/atomicparsley.tar.gz
		tar xzf atomicparsley.tar.gz
		cd atomicparsley
		makepkg -s
		sudo pacman -U atomicparsley*.tar.xz

	OR

		cd ~/abs
		curl -kLO https://aur.archlinux.org/packages/at/atomicparsley-largefile-hg/atomicparsley-largefile-hg.tar.gz
		tar xzf atomicparsley-largefile-hg.tar.gz
		cd atomicparsley-largefile-hg
		makepkg -s
		sudo pacman -U atomicparsley-largefile-hg*.tar.xz

	If you want to install a modern version of AtomicParsley without also installing Mercurial and its dependencies, you can build from source.  Use the following procedure to build the latest version:

	If you haven't already done so, install required development tools:

        sudo pacman -S --needed base-devel
        
    Now download and build AtomicParsley

		cd ~/abs
        curl -kLO https://bitbucket.org/wez/atomicparsley/get/tip.zip
        unzip tip.zip
        cd wez*
        ./autogen.sh
        ./configure
        make
        sudo make install


5. Install Perl modules

	If you haven't already done so, install required development tools:

		sudo pacman -S --needed base-devel
		
	Then proceed to installing the remaining Perl modules:

		cd ~/abs
		curl -kLO https://aur.archlinux.org/packages/pe/perl-mp3-tag/perl-mp3-tag.tar.gz
		tar xzf perl-mp3-tag.tar.gz
		cd perl-mp3-tag
		makepkg -s
		sudo pacman -U perl-mp3-tag*.tar.xz
	
		cd ~/abs
		curl -kLO https://aur.archlinux.org/packages/pe/perl-net-smtp-tls/perl-net-smtp-tls.tar.gz
		tar xzf perl-net-smtp-tls.tar.gz
		cd perl-net-smtp-tls
		makepkg -s
		sudo pacman -U perl-net-smtp-tls*.tar.xz

### Web PVR Manager (WPM)

The WPM is installed along with the CLI.

1. Launch the WPM in a terminal window with this command:

        get_iplayer.cgi --listen 127.0.0.1 --port 1935

2. Once the WPM is running, connect to it by opening this URL in your browser:

    <http://127.0.0.1:1935>

3. After the WPM has opened in your browser, click the `Refresh Cache` button.  A new tab or window will open that shows the cache being refreshed.  Leave that tab or window open to have the cache refreshed automatically every hour.  You can also manually refresh the cache at any time.

4. Stop the WPM by typing Ctrl-C.