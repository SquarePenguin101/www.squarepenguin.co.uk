## OS X Manual Installation

### Perl Support
Perl is part of the OS X base system, so no installation is necessary.

Additional Perl modules may be installed using the [local::lib method](/wiki/manual#manual-perl-locallib) described for Linux/Unix.  Note that the LWP and XML::Simple modules are already installed with the system Perl on OS X.

### External Programs

1. Download a bundle containing the external programs from one of the links below (select the link appropriate for your version of OS X):

    OS X 10.6 (Snow Leopard) or higher, 64-bit Intel only:

    <http://sourceforge.net/projects/get-iplayer/files/osx/utils/x86_64/20141227/get_iplayer-osx-utils-x86_64-20141227.zip>

    OS X 10.5 (Leopard), 32-bit Intel only:

    <http://sourceforge.net/projects/get-iplayer/files/osx/utils/i386/20141227/get_iplayer-osx-utils-i386-20141227.zip>

    **NOTE:** There is no bundle available for PowerPC machines.

2. Extract the zip file, open a command prompt and navigate to the directory containing the extracted files.  For example:

        cd ~/Downloads/get_iplayer-osx-utils-x86_64-20141227

3. Create the installation directory if it does not exist:

        sudo mkdir -p /usr/local/bin

4. Install the external programs:

        sudo install -m 755 AtomicParsley id3v2 rtmpdump ffmpeg ffplay ffprobe ffserver mplayer mencoder /usr/local/bin

### Command-line Interface (CLI)

Create the installation directory if it does not exist:

    sudo mkdir -p /usr/local/bin

then use the CLI [manual installation procedure](/wiki/manual#manual-cli) described for Linux/Unix.

### Web PVR Manager (WPM)

Create the installation directory if it does not exist:

    sudo mkdir -p /usr/local/bin

then use the WPM [manual installation procedure](/wiki/manual#manual-cli) described for Linux/Unix.