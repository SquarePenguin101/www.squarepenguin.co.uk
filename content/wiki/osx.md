## OS X Installation

- [Manual Installation](#manual)
- [Homebrew Installation](#homebrew)

<a name="manual"></a>
### Manual Installation

<a name="perl"></a>
#### Perl

Perl is part of the OS X base system, so no installation is necessary. Note also that the LWP, XML::Simple, and XML::LibXML modules are already installed with the system Perl on OS X. If you do not use the system Perl (e.g., you use Perlbrew), you will need to install those modules for your Perl version.

<a name="external-programs"></a>
#### External Programs

1. Download a bundle containing the external programs from one of the links below (select the link appropriate for your version of OS X):

    OS X 10.6 (Snow Leopard) or higher, 64-bit Intel only:

    <http://sourceforge.net/projects/get-iplayer/files/osx/utils/x86_64/20160402/get_iplayer-osx-utils-x86_64-20160402.zip>

    OS X 10.5 (Leopard), 32-bit Intel only **[DEPRECATED, NOT SUPPORTED]**:

    <http://sourceforge.net/projects/get-iplayer/files/osx/utils/i386/20141227/get_iplayer-osx-utils-i386-20141227.zip>

    **NOTE:** There is no bundle available for PowerPC machines.

2. Extract the zip file, open a command prompt and navigate to the directory containing the extracted files.  For example:

        cd ~/Downloads/get_iplayer-osx-utils-x86_64-20160402

3. Create the installation directory if it does not exist

        sudo mkdir -p /usr/local/bin

4. Install the external programs

        sudo install -m 755 AtomicParsley ffmpeg ffplay ffprobe ffserver id3v2 rtmpdump /usr/local/bin

<a name="cli"></a>
#### Command-line Interface (CLI)

1. Download the latest release to working directory

        curl -kLO https://raw.github.com/get-iplayer/get_iplayer/master/get_iplayer

2. Create the installation directory if it does not exist:

        sudo mkdir -p /usr/local/bin

3. Install get_iplayer CLI script

    	sudo install -m 755 ./get_iplayer /usr/local/bin

5. Run CLI at a command prompt

    	get_iplayer [...]

<a name="wpm"></a>
#### Web PVR Manager (WPM)

1. Download the latest release to working directory

		curl -kLO https://raw.github.com/get-iplayer/get_iplayer/master/get_iplayer.cgi

2. Create the installation directory if it does not exist:

        sudo mkdir -p /usr/local/bin

3. Install get_iplayer.cgi WPM script

    	sudo install -m 755 ./get_iplayer.cgi /usr/local/bin

5. Launch the WPM server at a command prompt

    	get_iplayer.cgi --listen 127.0.0.1 --port 1935

6. Once the WPM server is running, connect to it by opening the URL below in your web browser:

    <http://127.0.0.1:1935>

7. After the WPM has opened in your browser, select the programme types (e.g., BBC TV, BBC Radio) you wish to index, then click the `Refresh Cache` button.  A new tab or window will open that shows the cache being refreshed.  Leave that tab or window open to have the cache refreshed automatically every hour.  You can also manually refresh the cache at any time.

8. Stop the WPM by typing Ctrl-C.

<a name="homebrew"></a>
### Homebrew Installation

get_iplayer can also be installed with [Homebrew](http://brew.sh). Tap the get_iplayer repository and install with:

    brew install dinkypumpkin/get_iplayer/get_iplayer

If you do not use the OS X system Perl (e.g., you use Homebrew Perl or Perlbrew), you must install the LWP, XML::Simple and XML::LibXML modules.

Upgrade to future releases with:

    brew update
    brew upgrade get_iplayer

#### Command-line Interface (CLI)

1. Run CLI at a command prompt with:

        get_iplayer [...]

#### Web PVR Manager (WPM)

1. Run WPM at a command prompt with:

        get_iplayer_web_pvr

2. The WPM server will launch in a console window and your default browser will be opened to this URL: 

    <http://127.0.0.1:1935>

    If not, click the link above or enter the URL in your web browser.

3. After the WPM has opened, click the `Refresh Cache` button.  A new tab or window will open that shows the cache being refreshed.  Leave that tab or window open to have the cache refreshed automatically every hour.  You can also manually refresh the cache at any time. 

4. Stop the WPM by typing Ctrl-C.
