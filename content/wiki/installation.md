## get_iplayer Installation

## Table of Contents

- Requirements
	- [Perl](#perl)
	- [External Programs](#external-programs)
- Unix
    - [Manual Installation](/wiki/unix)
    - [Package Installation](/wiki/unixpkg)
- [OS X](/wiki/osx)
- [Windows](/wiki/windows)
- [Development Version](/wiki/gipdev)

<a name="requirements"></a>
## Requirements

get_iplayer runs on Unix (numerous distros supported), OS X (10.5+) and Windows (7/8/10 supported, known to run on XP/Vista).

<a name="perl"></a>
### Perl

* Perl 5.8.8+ is required

Perl modules (with dependencies) required for get_iplayer:

* LWP - HTTP access to BBC servers
* XML::Simple - Extraction of XML programme metadata
* XML::LibXML - HTML parsing

Users of Perl 5.22 and higher must install the CGI module separately to use the Web PVR Manager.

Additional Perl modules are used for optional functionality :

* MP3::Info **[DEPRECATED]** - Catalogue MP3 files in *localfiles* plugin
* MP3::Tag **[DEPRECATED]** - Full ID3 tagging of MP3 files
* Net::SMTP::SSL and Authen::SASL **[DEPRECATED]** - Send search results via SSL secure email (e.g. GMail, Yahoo Mail)
* Net::SMTP::TLS::ButMaintained (preferred) or Net::SMTP::TLS **[DEPRECATED]** - Send search results via TLS secure email (e.g., GMail, iCloud)

<a name="external-programs"></a>
### External Programs

get_iplayer employs external programs to download streams and manipulate media files:

- [AtomicParsley](http://atomicparsley.sourceforge.net) - Metadata tagging for MP4 and M4A files.
- [ffmpeg](http://ffmpeg.org) - Converts MPEG-TS and FLV files to MP4, M4A, MP3, or AVI.
- [id3v2](http://id3v2.sourceforge.net) **[DEPRECATED]** - Metadata tagging for MP3 files.
- [rtmpdump](http://rtmpdump.mplayerhq.hu/) **[DEPRECATED]** - Saves Flash audio/video streams to FLV files.

Details of how external programs are used can be found [here](/wiki/modes#external-programs).
