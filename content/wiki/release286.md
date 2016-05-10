## get_iplayer 2.86 Release Notes

## Installation/Upgrade

Installation information for all platforms can be found here:

<https://github.com/get-iplayer/get_iplayer/wiki/installation>

Please note that it may take some time for get_iplayer 2.86 to be packaged for your particular system.

#### Windows

Windows users should use the most recent installer to update:

<https://github.com/get-iplayer/get_iplayer_win32/releases/latest>

The installer will update the following components to the indicated versions:

- get_iplayer main script: 2.86
- ffmpeg: 2.1.4

## Changes in get_iplayer 2.86

### Fix for missing thumbnails

The BBC recently changed the way that programme thumbnail images are generated. For some programmes, this change meant that get_iplayer produced a thumbnail that was a grey rectangle rather than the appropriate image.  get_iplayer has been patched to work around this problem.  NOTE: Thumbnails may still appear as grey rectangles in the Web PVR Manager search results until the old thumbnail URLs are flushed out of your caches over time. However, the downloaded files should have the correct thumbnail embedded.

### Support for iPlayer Radio Site URLs

You can now use URLs in the form `http://www.bbc.co.uk/programmes/b007k447` on the get_iplayer command line to download radio programmes.  These URLs may also be used in the "Quick URL" field of the Web PVR Manager.  The URLs should correspond to episode player pages in the iPlayer Radio site (<http://www.bbc.co.uk/radio/>).  Note that there are other types of pages in the site that have the same URL form.  This feature relies on HTML scraping and should therefore be regarded as fragile.  If it fails, you should take the PID from the end of the URL and use it with `--pid`, e.g., `get_iplayer --type=radio --pid=b007k447`.

### Zero-padding in `<episodenum>` and `<seriesnum>`

In `--fileprefix` or `--subdir-format`, you can now use parameters in the form `<00episodenum>` or `<00seriesnum>` to produce values padded with zeroes. Padded string width is determined by number of zeroes, so the above would pad "5" to "05". If you are also using an optional prefix character, it must come before the padding indicator, e.g., `<.00episodenum>`.

### AVI container option for DivX files

You may use `--avi` to transcode downloaded video files into a AVI container (.avi file).  The purpose of this new option is enable production of DivX files for older hardware media players that cannot handle MP4 containers.  `--avi` **does not** automatically produce a DivX output file.  It must be used in conjunction with `--ffmpeg-tv-opts`.  For example, converting a flashvhigh download while retaining the approximate input bit rates might look like:

    get_iplayer --get 65 --mode=flashvhigh --ffmpeg-tv-opts="-c:a libmp3lame -c:v mpeg4 -b:a 96k -b:v 1404k" --avi

The above is just a rough example - you will need to work out the correct parameters for your own needs.  See also:

<http://trac.ffmpeg.org/wiki/How%20to%20encode%20Xvid%20/%20DivX%20video%20with%20ffmpeg>

**Do not** use `--avi` to simply re-mux the normal H.264/AAC video/audio content.  If your media player cannot handle MP4 files, it is highly likely it cannot handle those stream formats.
### Trim download history

If you have accumulated a very large download history file, you may want to truncate it while retaining enough history data to avoid repeat downloads of recent  programmes.  You can now use the `--trim-history` option:

    get_iplayer --trim-history=N

N is an integer value &gt;= 1 that represents the number of days to retain in your download history.  All download history entries older than the `--trim-history` value will be deleted.  You cannot use `0` to delete all download history - use `all` instead.  Every time you run `--trim-history`, the previous `download_history` file is backed up in your profile directory (`$HOME/.get_iplayer`, `%USERPROFILE%\.get_iplayer` on Windows) as `download_history.old`.  Only one backup version is retained.

`--trim-history` is a standalone option that preempts any other get_iplayer options in the command line.  **DO NOT** add it to your preferences. `--trim-history` works only from the command line.  It is not implemented for the Web PVR Manager.

### Other Changes

- `--isodate` is now applied to the value of `--subdir`, if present.
- `--mp3` may now be used as an alias for `--aactomp3`.
- New `--hfsfilename` option to remove colons in output file names when `--whitespace` is also in use.  This is a minor convenience for OSX users who don't like the fact that Finder displays colons as forward slashes.
- New `--tag-id3sync` option to save ID3 tags for MP3 files in synchronised form.  This provides a workaround for a Windows bug that corrupts the display of MP3 thumbnail images in Windows Explorer and Windows Media Player.  This option only applies to MP3 files (local/regional radio programmes or national radio programmes converted with `--aactomp3`.  It has no effect unless you are using the MP3::Tag Perl module (supplied by Windows installer).

## Changelog

The full log of changes since v2.85 can be viewed here:

<https://github.com/get-iplayer/get_iplayer/compare/v2.85...v2.86>