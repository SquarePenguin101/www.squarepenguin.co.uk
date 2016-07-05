## Unix Installation

- [Perl](#perl)
	- [Packaged Modules](#perl-packaged)
	- [local::lib](#perl-locallib)
- [External Programs](#external-programs)
- [Command-line Interface (CLI)](#cli)
- [Web PVR Manager (WPM)](#wpm)

<a name="perl"></a>
### Perl

Perl is part of the base system for most Unix distros.  If not, it will almost certainly be available in your system's package repositories.

<a name="perl-packaged"></a>
#### Packaged Modules

Perl modules required by get_iplayer should be available in the package repositories for your system.  However, the naming convention for packaged Perl modules differs between distros.  Generally speaking, a module's namespace separator ("::") is replaced by a hyphen, a prefix (and sometimes a suffix) are added, and the name is sometimes changed to lower case. The package names for the **LWP**, **XML::Simple** and **XML::LibXML** modules in some different distros are:

* DEB-based (e.g., Ubuntu): **libwww-perl** **libxml-simple-perl** **libxml-libxml-perl**
* RPM-based (e.g., Fedora): **perl-libwww** **perl-XML-Simple** **perl-XML-LibXML**
* Ports-based (e.g, OpenBSD): **p5-libwww** **p5-XML-Simple** **p5-XML-LibXML**

Users of Perl 5.22 and higher may also need to install the `CGI` module to use the Web PVR Manager. 

* DEB-based (e.g., Ubuntu): **libcgi-pm-perl**
* RPM-based (e.g., Fedora): **perl-CGI**
* Ports-based (e.g, OpenBSD): **p5-CGI**

For example, to install the Perl modules for get_iplayer in Arch Linux with Perl 5.24:

    pacman -S perl-libwww perl-xml-simple perl-xml-libxml perl-cgi

Replace the command above with the appropriate package names and installation command for your system (e.g., `apt-get install`, `pkg install`, `dnf install`).  If you are not logged in as root, you will need to preface your installation commands with `sudo`.

<a name="perl-locallib"></a>
#### local::lib

If Perl modules utilised by get_iplayer are not available via the package manager for your system, it is generally unwise to employ superuser access to force additional modules into your system's Perl installation. As an alternative, you can create a local module library with [cpanminus](http://search.cpan.org/~miyagawa/App-cpanminus/) and the Perl [local::lib](http://search.cpan.org/~ether/local-lib) module.  Your local library will contain just the additional Perl modules you need. The instructions below are taken from:

<http://stackoverflow.com/questions/2980297/how-can-i-use-cpan-as-a-non-root-user>

To install cpanminus and local::lib and set up your local library in ~/perl5:

	curl -L "http://cpanmin.us" | perl - -l ~/perl5 App::cpanminus local::lib
	eval `perl -I ~/perl5/lib/perl5 -Mlocal::lib`
	echo 'eval `perl -I ~/perl5/lib/perl5 -Mlocal::lib`' >> ~/.profile

**NOTE**: If your system does not have `curl` try `wget`.  Replace `curl -L` with `wget -O-`.

This example is for the bash shell and assumes that your profile is loaded from ~/.profile, but you may prefer to use ~/.bash_profile.  You may also prefer to initialise your environment in ~/.bashrc and load that file from ~/.profile or ~/.bash_profile. The equivalent locations are different for different shells, e.g., ~/.login and ~/.cshrc for csh or ~/.login and ~/.tcshrc for tcsh.  The "eval" statement initialises environment variables necessary for local::lib to function, so place it in whichever file you use to set up your shell environment.

After your local library is set up, you can install modules with `cpanm Module::Name [Module::Name ...]`. For example, to install the Perl modules for get_iplayer on a platform with Perl 5.22:

    cpanm LWP XML::Simple XML::LibXML CGI

<a name="external-programs"></a>
### External Programs

The external programs used by get_iplayer should be available in the package repositories for your system. The package name will usually be the same as the program itself, though not always.  For example, to install the utilities for get_iplayer in Arch Linux:

	pacman -S atomicparsley ffmpeg id3v2 rtmpdump

Replace the command above with the appropriate package names and installation command for your system (e.g., `apt-get install`, `pkg install`, `dnf install`).  If you are not logged in as root, you will need to preface your installation commands with `sudo`.

NOTE: For Debian and Debian-derived distros (Ubuntu, Mint, etc.), you may need to substitute *libav-tools* for *ffmpeg*.

NOTE: Some distros may offer multiple versions of ffmpeg. Install the most recent version available if possible. If the program executable is not named "ffmpeg" (e.g., "ffmpeg2"), use the `--ffmpeg` option to  configure get_iplayer to use the correct program executable.

A few distros do not have packaged versions of all the necessary external programs in their repositories.  You may need to acquire external programs from unofficial repositories or - in rare instances - be required to build your own.  Check your distro's repositories before installing.

<a name="cli"></a>
### Command-line Interface (CLI)

1. Download the latest release to working directory

        curl -kLO https://raw.github.com/get-iplayer/get_iplayer/master/get_iplayer

	NOTE: If your system does not have `curl` try `wget`.  Replace `curl -kLO` with `wget --no-check-certificate`.

2. Install get_iplayer CLI script

    	install -m 755 ./get_iplayer /usr/local/bin

    **NOTE**: If you are not logged is as root, you will need to preface your install command with `sudo`.

    If you don't wish to install get_iplayer in $PATH, ensure your local copy is executable:

    	chmod 755 ./get_iplayer

3. Run CLI at a command prompt

    	get_iplayer [...]

<a name="wpm"></a>
### Web PVR Manager (WPM)

1. Download the latest release to working directory

		curl -kLO https://raw.github.com/get-iplayer/get_iplayer/master/get_iplayer.cgi

	NOTE: If your system does not have `curl` try `wget`.  Replace `curl -kLO` with `wget --no-check-certificate`.

3. Install get_iplayer.cgi WPM script

    	install -m 755 ./get_iplayer.cgi /usr/local/bin

    **NOTE**: If you are not logged is as root, you will need to preface your install command with `sudo`.

    If you don't wish to install get_iplayer.cgi in $PATH, ensure your local copy is executable:

    	chmod 755 ./get_iplayer.cgi

4. Launch the WPM server at a command prompt

    	get_iplayer.cgi --listen 127.0.0.1 --port 1935

5. Once the WPM server is running, connect to it by opening <http://127.0.0.1:1935> in your web browser.

6. After the WPM has opened in your browser, select the programme types (e.g., BBC TV, BBC Radio) you wish to index, then click the `Refresh Cache` button.  A new tab or window will open that shows the cache being refreshed.  Leave that tab or window open to have the cache refreshed automatically every hour.  You can also manually refresh the cache at any time.

7. Stop the WPM by typing Ctrl-C.