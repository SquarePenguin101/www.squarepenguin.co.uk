## get_iplayer Installation

## Table of Contents

- Requirements
	- [Perl Support](#requirements-perl)
	- [External Programs](#requirements-programs)
- Linux/Unix
    - [Manual Installation](/wiki/manual)
    - Package Installation
        - [Arch](/wiki/arch)
        - [CentOS / RHEL](/wiki/centos)
        - [Debian](/wiki/debian)
        - [Fedora](/wiki/fedora)
        - [FreeBSD / PC-BSD](/wiki/freebsd)
        - [Mageia](/wiki/mageia)
        - [OpenBSD](/wiki/openbsd)
        - [NetBSD](/wiki/netbsd)
        - [openSUSE](/wiki/opensuse)
        - [Raspbian / Raspberry Pi](/wiki/raspbian)
        - [Slackware / Salix](/wiki/slackware)
        - [Ubuntu / Mint](/wiki/ubuntu)
- OS X
    * [Homebrew](/wiki/osxhomebrew)
    * [MacPorts](/wiki/osxmacports)
    * [Manual Installation](/wiki/osxmanual)
- Windows
    * [Installer](/wiki/winsetup)
    * [Manual Installation](/wiki/winmanual)
    * [Cygwin](/wiki/cygwin)
- Other
    - [Development Version](/wiki/gipdev)
	- [Perlbrew](/wiki/perlbrew)

<a name="requirements"></a>
## Requirements

get_iplayer runs on Linux/Unix (numerous flavours supported), OS X (10.5+) or Windows (XP/Vista/7/8/10).

<a name="requirements-perl"></a>
### Perl Support

* Perl 5.8.8+ is required

Two Perl modules (with dependencies) are required for get_iplayer:

* LWP - Required for HTTP access to BBC servers
* XML::Simple - Required for extracting programme metadata

Users of Perl 5.22 and higher must install the CGI module separately to use the Web PVR Manager

Other Perl modules are recommended for added functionality:

* MP3::Info - Catalogue MP3 files in *localfiles* plugin
* MP3::Tag - Full ID3 tagging of MP3 files
* Net::SMTP::SSL and Authen::SASL - Send search results via SSL secure email (e.g. GMail, Yahoo Mail)
* Net::SMTP::TLS::ButMaintained (preferred) or Net::SMTP::TLS - Send search results via TLS secure email (e.g., GMail, iCloud)

<a name="requirements-programs"></a>
### External Programs

get_iplayer employs external programs to download streams and manipulate media files:

- [rtmpdump](http://rtmpdump.mplayerhq.hu/) - Saves Flash audio/video streams to FLV files.
- [ffmpeg](http://ffmpeg.org) - Converts FLV files to MP4, M4A, MP3, or AVI format (for BBC TV, BBC national radio and BBC webcams).
- [AtomicParsley](http://atomicparsley.sourceforge.net) - Metadata tagging for MP4 and M4A files.
- [id3v2](http://id3v2.sourceforge.net) - Metadata tagging for MP3 files. However, the MP3::Tag Perl module is preferred because it supports more complete ID3 tagging.

Details of how external programs are used can be found [here](/wiki/modes#external-programs).
