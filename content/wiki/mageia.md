**Before you begin**: Linux/Unix packages are maintained by volunteers and may not be updated for some time after a new release of get_iplayer, thus the version of get_iplayer packaged for your system may be obsolete. You can find the version number of the latest get_iplayer release [here](https://github.com/get-iplayer/get_iplayer/releases). If the version packaged for your system is older than the latest release, it is likely that some functionality is broken. After following the instructions below, you may wish to uninstall the get_iplayer package and use the [manual installation instructions](/wiki/manual) to install the latest get_iplayer CLI and Web PVR Manager. 

## Mageia

These instructions are for Mageia 4.  The instructions assume you are logged in as root, but you may also perform the installation commands with `sudo`.

### Command-line Interface (CLI)

1. (Re-)Install programs from tainted media set

    32-bit:

        urpmi --media tainted ffmpeg mplayer rtmpdump librtmp0

    64-bit:

        urpmi --media tainted ffmpeg mplayer rtmpdump lib64rtmp0

    This step is necessary because the restricted versions of these programs in the core and non-free media sets do not fully support all get_iplayer functionality.

2. Install get_iplayer and related applications

        urpmi get_iplayer id3v2

3. Install Perl modules

        urpmi perl-MP3-Tag perl-MP3-Info perl-XML-Simple perl-Net-SMTP-SSL perl-Authen-SASL perl-Net-SMTP-TLS-ButMaintained
    
4. Install AtomicParsley

    You are encouraged to install a modern version of AtomicParsley from source.  Use the following procedure to build the latest version:

        urpmi automake autoconf make gcc gcc-c++ zlib-devel
        curl -kLO https://bitbucket.org/wez/atomicparsley/get/tip.zip
        unzip tip.zip
        cd wez*
        ./autogen.sh
        ./configure
        make
        make install

    If you can't install from source, an old version of AtomicParsley may be installed from existing Mandriva RPMs.

    32-bit:

        urpmi ftp://rpmfind.net/linux/Mandriva/official/2011/i586/media/contrib/backports/atomicparsley-0.9.0-1-mdv2011.0.i586.rpm

    64-bit:

        urpmi ftp://rpmfind.net/linux/Mandriva/official/2011/x86_64/media/contrib/backports/atomicparsley-0.9.0-1-mdv2011.0.x86_64.rpm

    Enter 'y' for no key/bad signature prompt.

    After installation, you must link the installed binary so that get_iplayer can find it using the properly-cased name:

        ln -sf /usr/bin/atomicparsley /usr/bin/AtomicParsley

5. Run CLI with:

    	get_iplayer [...]

### Web PVR Manager (WPM)

The WPM is not installed with the get_iplayer package.  Use the [manual installation procedure](/wiki/manual).