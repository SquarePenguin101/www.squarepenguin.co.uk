## get_iplayer 2.84 Release Notes

## Installation

Installation information for all platforms may be found here:

<https://github.com/get-iplayer/get_iplayer/wiki/installation>

Please note that it may take some time for get_iplayer 2.84 to be packaged for your particular system.

#### Windows Installer

A new version of the get_iplayer Windows installer is available:

<http://www.infradead.org/get_iplayer_win/get_iplayer_setup_latest.exe>

All Windows users should use this installer to upgrade to get_iplayer 2.84.  The installer will update the following components to the indicated versions:

- get_iplayer main script: 2.84
- get_iplayer Perl support: 4.7 (with Strawberry Perl 5.16.3)

You may also be prompted to update rtmpdump if your previous installation was performed within a few days after 2.83 was released.  The update fixes a packaging issue.  There is no functional change in rtmpdump, but accept the upgrade anyway.

## Changes in get_iplayer 2.84

### Subtitle Fixes and New Formats

Around mid-September 2013, the BBC began producing subtitles with a new file structure that broke get_iplayer's conversion of raw subtitles from TTML format to SRT format used by many media players.  get_iplayer has been updated to accommodate the new file structure.  However, with this new file structure, get_iplayer cannot  ascertain changes in speaker.

A new `--subsfmt` option has been added to offer alternative formats for subtitles.  This option accepts the following value:

**compact**: Leading hyphen (without line break) demarcates change in speaker.  All line breaks retained.  Text rendered in default subtitle colour for media player.  This format typically has shorter lines of text than the default format.

The default format used if `--subsfmt` is omitted or has any value other than **compact**:  Line break followed by leading hyphen demarcates change in speaker.  All other line breaks removed, so lines must be wrapped by media player.  Text rendered in default subtitle colour for media player.  If your media player cannot wrap text, use **compact** format.

If you wish to switch to the **compact** format subtitles for a particular programme, you can re-download only the subtitles with:

	get_iplayer --subtitles-only --overwrite --subsfmt=compact --get <index>
	OR
	get_iplayer --subtitles-only --overwrite --subsfmt=compact --pid <pid>	

NOTE: This will overwrite the previous subtitles (.srt) file.

Also added `--subsrequired` option to prevent programme download if subtitles are unavailable or empty.

### Restored Embedded Video Download

Due to changes on the BBC News site, recent embedded videos became unavailable because get_iplayer's HTML scraping did not recognise new page structures.  The problem was more acute on Windows where an unrelated bug in a supporting Perl module prevented more embedded videos from downloading.  Because the packaged version of Strawberry Perl required an update, a new installer was required to propagate the fixes to Windows users.

### WMA Removed from Recording Mode Shortcuts

The **wma** recording mode has been removed from the recording mode shortcuts (good, better, best, default).  On Windows, WMA recording is a less than reliable fallback when rtmpdump fails to download Flash format catch-up programmes.  It can also prove confusing to users since Windows MPlayer may stop downloading a WMA stream without reporting an error.

The **wma** mode is still supported, but it must now be explicitly specified via `--modes=wma`, `--radiomode=wma` or `--liveradiomode=wma`.  The previous default behaviour may be restored with `--modes=default,wma`. If your preferences or PVR jobs are set to use **wma**, they will still work as before.   

### New Metadata Fields

Several new metadata fields have been added:

- **category**: the primary programme category (first item in **categories** list)
- **firstbcastdate**: date portion of **firstbcast**
- **lastbcastdate**: date portion of **lastbcast**

The new metadata fields may be used as substitution parameters for `--file-prefix` and `--subdir-format`.

### Other Changes

- Fixed bugs in populating **firstbcast** and **lastbcast** metadata fields
- `--fatfilename` is set automatically if `--whitespace` is specified (Windows only)
- 256-char output path limit now enforced for Windows only
- Search string generated with "Add Series" in Web PVR Manager is now properly escaped

## Changelog

The full log of changes since v2.83 can be viewed here:

<https://github.com/get-iplayer/get_iplayer/compare/v2.83...v2.84>