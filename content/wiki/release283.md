## get_iplayer 2.83 Release Notes

## Installation

Installation information for all platforms may be found here:

<https://github.com/get-iplayer/get_iplayer/wiki/installation>

Please note that it may take some time for get_iplayer 2.83 to be packaged for your particular system.

#### Windows Installer

Windows users should use the most recent installer to update:

<https://github.com/get-iplayer/get_iplayer_win32/releases/latest>

The installer will also upgrade dependencies to the following versions:

- Strawberry Perl 5.16.2
- RTMPDump 2.4-git-20130109
- FFmpeg 1.2
- MPlayer svn-36348
- AtomicParsley 0.9.4-hg103.396d3bd13c73
- LAME 3.99.5
- VLC 2.0.6

## Changes in get_iplayer 2.83

### SWF URL Fixed

get_iplayer 2.83 contains an updated SWF player URL to fix the unpleasantness encountered in early June 2013 when the BBC expired the old SWF player URL and broke all TV downloads.

If you used the workaround described here:

<https://github.com/get-iplayer/get_iplayer/wiki/swfurl>

you should remove the associated changes to your preferences when you upgrade to 2.83.  Revisit that page and read the section on reverting your changes.  For experienced users:

	get_iplayer --prefs-del --rtmp-tv-opts="X" --rtmp-radio-opts="X"  --rtmp-livetv-opts="X" --rtmp-liveradio-opts="X"

Yes, that is a single "X" for each option. Any non-empty value will suffice when deleting those preferences.

**Windows Users:** The new installer will attempt to clean up those preference settings.  However, you should also run the command above to make sure that your settings have been cleaned.

### New Documentation Wiki

All get_iplayer documentation has been moved to the project wiki:

<https://github.com/get-iplayer/get_iplayer/wiki>

The old linuxcentre.net site has been dead for three years and cannot be updated, so this move is long overdue.  The wiki is a work in progress, but it still contains useful information.  The wiki may be edited by any registered GitHub user, so please feel free to make additions and corrections.

### Recording Mode Changes

Recording modes have changed slightly in 2.83. The built-in mode for TV programmes has changed so that the best SD quality TV will now be downloaded by default.  Additional mode shortcuts have also been introduced which should simplify the configuration of recording modes for most users. Read the **Shortcuts** section in the document below for an explanation of the changes:

<https://github.com/get-iplayer/get_iplayer/wiki/modes>

One thing to emphasise here in case you decide to ignore the documentation: If you normally run get_iplayer without specifying a recording mode, your TV downloads will be nearly twice as large and may take up to twice as long as with 2.83.  Read the modes documentation referenced above for instructions on how to revert to pre-2.83 behaviour.

### avconv Used in Preference to ffmpeg Where Available

If get_iplayer detects that avconv is installed, it will use it in preference to ffmpeg by default.  No more scary messages about ffmpeg being deprecated.  This change will typically only affect Debian-based Linux distributions, where the Libav fork of FFmpeg is installed by default, but will apply to any system with avconv installed.  If you wish to switch back to ffmpeg, you can override this default with the `ffmpeg` option.  Also, an `avconv` option has been added as a synonym for `ffmpeg`.

### XBMC File Naming

The syntax for substitution parameters has been extended slightly.  It is now possible to define separators in `fileprefix` that are omitted when the associated parameter is empty.  You should now be able to use a single `fileprefix` setting that will make XBMC happy (most of the time).  Details here:  

<https://github.com/get-iplayer/get_iplayer/wiki/fileprefix>

### Support for Secure Email

get_iplayer can send HTML-formatted search results via email.  This feature will now work with email providers that require secure connections (TLS or SSL), such as GMail.  Additional Perl modules are required to support secure email - see the [installation instructions](/wiki/installation) for details.  The Windows installer will install the necessary Perl modules.

An example:

	get_iplayer "doctor who" --email=somebody@somewhere.com --email-user=you@gmail.com --email-password=secret --email-smtp=smtp.gmail.com --email-security=TLS

### Subtitles

- Subtitles are now saved with UTF-8 encoding.  Many media players will auto-detect the encoding for subtitles, but in some circumstances you may need to configure additional options.  For example, the command-line version of MPlayer requires the `-utf8` command line option.
- Subtitles may now be downloaded with audiodescribed programmes

### Other Changes

- Live TV functionality restored after being broken by BBC changes
- Added `noartwork` option to prevent thumbnail image being written in media file metadata
- Added `rtmpdump` option as a synonym for `flvstreamer`
- Updated channel schedule URLs (for `refreshfuture`)
- get_iplayer is now compatible with Perlbrew

## Changelog

The full log of changes since v2.82 can be viewed here:

<https://github.com/get-iplayer/get_iplayer/compare/v2.82...v2.83>