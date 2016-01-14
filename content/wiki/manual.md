## Manual Installation on Linux/Unix

- [Perl Support](#manual-perl)
	- [Packaged Modules](#manual-perl-packaged)
	- [local::lib](#manual-perl-locallib)
- [External Programs](#manual-external-programs)
- [Command-line Interface (CLI)](#manual-cli)
- [Web PVR Manager (WPM)](#manual-wpm)
- [Release Archives](#manual-archives)
	
<a name="manual-perl"></a>
### Perl Support

Perl is part of the base system for most Linux/Unix distributions.  If not, it will almost certainly be available in your system's package repositories.

<a name="manual-perl-packaged"></a>
#### Packaged Modules

Many Perl modules used by get_iplayer should be available in the package repositories for your system.  However, the naming convention for packaged Perl modules differs between distributions.  Generally speaking, a module's namespace separator ("::") is replaced by a hyphen, a prefix (and sometimes a suffix) are added, and the name is sometimes changed to lower case.  Consider an example: 

The package names for the **XML::Simple** Perl module in some different distributions are:

* DEB-based (Debian, Ubuntu): **libxml-simple-perl**
* RPM-based (openSUSE, Fedora): **perl-XML-Simple**
* Ports-based (OpenBSD, MacPorts): **p5-xml-simple** or **p5-XML-Simple**

One variation from the above scheme is important to know.  The package names for the required **LWP** module are:

* DEB-based (Debian, Ubuntu): **libwww-perl**
* RPM-based (openSUSE, Fedora): **perl-libwww-perl**
* Ports-based (OpenBSD, MacPorts): **p5-libwww**

<a name="manual-perl-locallib"></a>
#### local::lib

All the Perl modules utilised by get_iplayer may not be available via the package manager for your system.  It is generally unwise to employ superuser access to force additional modules into your system's Perl installation. As an alternative, you can create a local module library with [cpanminus](http://search.cpan.org/~miyagawa/App-cpanminus/) and the Perl [local::lib](http://search.cpan.org/~ether/local-lib) module.  Your local library will contain just the additional Perl modules you need. The instructions below are taken from:

<http://stackoverflow.com/questions/2980297/how-can-i-use-cpan-as-a-non-root-user>

To install cpanminus and local::lib and set up your local library in ~/perl5:

	curl -L "http://cpanmin.us" | perl - -l ~/perl5 App::cpanminus local::lib
	eval `perl -I ~/perl5/lib/perl5 -Mlocal::lib`
	echo 'eval `perl -I ~/perl5/lib/perl5 -Mlocal::lib`' >> ~/.profile

**NOTE**: If your system does not have `curl` try `wget`.  Replace `curl -L` with `wget -O-`.

This example is for the bash shell and assumes that your profile is loaded from ~/.profile, but you may prefer to use ~/.bash_profile.  You may also prefer to initialise your environment in ~/.bashrc and load that file from ~/.profile or ~/.bash_profile. The equivalent locations are different for different shells, e.g., ~/.login and ~/.cshrc for csh or ~/.login and ~/.tcshrc for tcsh.  The "eval" statement initialises environment variables necessary for local::lib to function, so place it in whichever file you use to set up your shell environment.

After your local library is set up, you can install modules with `cpanm Module::Name [Module::Name ...]`. For example, to install the Perl modules for get_iplayer:

	cpanm LWP XML::Simple MP3::Tag MP3::Info Authen::SASL Net::SMTP::SSL Net::SMTP::TLS::ButMaintained

Users of Perl 5.22 and higher must also install the `CGI` module separately to use the Web PVR Manager

<a name="manual-external-programs"></a>
### External Programs

The external programs used by get_iplayer should be available in the package repositories for your system.  The package name will almost always be the same as the program itself.  For example, to install the utilities for get_iplayer in Fedora: 

	sudo yum install rtmpdump ffmpeg atomicparsley id3v2

Replace `sudo yum install` with `sudo apt-get install` (Debian), `sudo zypper install` (openSUSE), `sudo pacman -S` (Arch Linux), `sudo pkg_add` (OpenBSD) or `sudo pkg install` (FreeBSD).

**NOTE:** For Debian and Debian-derived distros (Ubuntu, Mint, etc.), you may need to substitute *libav-tools* for *ffmpeg*.

A few distros do not provide all the necessary external programs in their official repositories.  You may need to acquire external programs from other repositories or - in rare instances - be required to build your own.  Please check your distribution's repositories before installing.

<a name="manual-cli"></a>
### Command-line Interface (CLI)

1. Download the latest release to working directory

	    curl -kLO https://raw.github.com/get-iplayer/get_iplayer/latest/get_iplayer

	NOTE: If your system does not have `curl` try `wget`.  Replace `curl -kLO` with `wget --no-check-certificate`.

2. Ensure the script is executable

    	chmod 755 ./get_iplayer

3. Execute the script once to initialise the config directory ($HOME/.get_iplayer) and download plugins

    	./get_iplayer

4. Optionally install get_iplayer somewhere in PATH (e.g., /usr/local/bin)

    	sudo install -m 755 ./get_iplayer /usr/local/bin

5. Run CLI (assumed installed in PATH) with:

    	get_iplayer [...]

<a name="manual-wpm"></a>
### Web PVR Manager (WPM)

1. Download the latest release to working directory

		curl -kLO https://raw.github.com/get-iplayer/get_iplayer/latest/get_iplayer.cgi

	NOTE: If your system does not have `curl` try `wget`.  Replace `curl -kLO` with `wget --no-check-certificate`.

2. Ensure the script is executable

    	chmod 755 ./get_iplayer.cgi

3. Optionally install get_iplayer.cgi somewhere in PATH (e.g., /usr/local/bin)

    	sudo install -m 755 ./get_iplayer.cgi /usr/local/bin

4. Launch WPM in a terminal window (assumed installed in PATH):

    	get_iplayer.cgi --listen 127.0.0.1 --port 1935

5. If CLI is not in PATH, its location must be explicitly set

    	get_iplayer.cgi --listen 127.0.0.1 --port 1935 --getiplayer /path/to/get_iplayer

6. Once the WPM is running, connect to it by opening this URL in your browser:

    <http://127.0.0.1:1935>

7. After the WPM has opened in your browser, click the `Refresh Cache` button.  A new tab or window will open that shows the cache being refreshed.  Leave that tab or window open to have the cache refreshed automatically every hour.  You can also manually refresh the cache at any time.

8. Stop the WPM by typing Ctrl-C.

<a name="manual-archives"></a>
### Release Archives

If you would prefer to download an archive of any get_iplayer release, you can find it here:

<https://github.com/get-iplayer/get_iplayer/releases>