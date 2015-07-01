**Before you begin**: Linux/Unix packages are maintained by volunteers and may not be updated for some time after a new release of get_iplayer, thus the version of get_iplayer packaged for your system may be obsolete. You can find the version number of the latest get_iplayer release [here](https://github.com/get-iplayer/get_iplayer/releases). If the version packaged for your system is older than the latest release, it is likely that some functionality is broken. After following the instructions below, you may wish to uninstall the get_iplayer package and use the [manual installation instructions](/wiki/manual) to install the latest get_iplayer CLI and Web PVR Manager. 

## CentOS / RHEL

These instructions are for CentOS / RHEL 6.

### Command-line Interface (CLI)

1. Before You Begin

	Before installing get_iplayer, you must first decide on a source for its dependencies.  The [nux-dextop](http://li.nux.ro/repos.html) repository provides get_iplayer and most of its dependencies.  However, if you already use a third-party repository such as [RPM Fusion](http://rpmfusion.org), [ATrpms](http://atrpms.net) or [RepoForge](http://repoforge.org) for multimedia applications, it is recommended that you install get_iplayer dependencies from there and only use the nux-dextop repository for applications not otherwise available.  This is to avoid potential  dependency conflicts between repositories.  Both options are described below, but it is impossible to cover all permutations, so use the configuration that is right for your system.

	The instructions below assume you are logged in as root.

2. Install from nux-dextop only

	Instructions to configure the nux-dextop repo can be found at:

	<http://li.nux.ro/repos.html> 

	Note that nux-dextop requires the EPEL (Extra Packages for Enterprise Linux) repo.  However, do not use the EPEL RPM referenced in the above page - it is currently obsolete.  The link in the command below is current at time of writing, but check <http://fedoraproject.org/wiki/EPEL/FAQ#howtouse> for the correct value.  

		rpm -Uvh http://download.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm

	Change "x86_64" to "i386" for 32-bit systems. 

	Now install get_iplayer and dependencies (accept repo keys as required):

        yum install get_iplayer

3. Install from nux-dextop with RPM Fusion / ATrpms / RepoForge

	If you are using ATrpms or RepoForge, do not install the EPEL repo.  Install only the nux-dextop repo as described above. If you are using RPM Fusion, install the EPEL repo as well.

	Only id3v2 and get_iplayer are provided exclusively by nux-dextop, so configure yum to resolve only those packages from that repo.  Add the following line to the end of the `[nux-dextop]` section in `/etc/yum.repos.d/nux-dextop.repo`:

		includepkgs=id3v2 get_iplayer

	Now install get_iplayer and dependencies (accept repo keys as required):

        yum install get_iplayer

4. Install AtomicParsley

    AtomicParsley is not available from any of the above repositories.  Use the following procedure to download and build the latest version:

		yum install automake autoconf gcc-c++ zlib-devel
		curl -kLO https://bitbucket.org/wez/atomicparsley/get/tip.zip
		unzip tip.zip
		cd wez*
		./autogen.sh
		./configure
		make
		make install

3. Install additional Perl modules

	Some of the Perl modules are available from the base repo:
	
        yum install perl-XML-Simple perl-Authen-SASL perl-Net-SMTP-SSL 

    The remaining Perl modules may be installed using the [local::lib method](/wiki/manual#manual-perl-locallib).	
5. Run CLI with:

    	get_iplayer [...]

### Web PVR Manager (WPM)

The WPM is not installed with the get_iplayer package.  Use the [manual installation procedure](/wiki/manual).