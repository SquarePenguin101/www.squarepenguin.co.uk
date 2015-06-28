## get_iplayer 2.87 Release Notes

## Read This First

The BBC recently made some changes to the iPlayer service and web site that affected get_iplayer.  This is what you need to know after upgrading to get_iplayer 2.87:

- Programmes more than 7 days old are **NOT** available for caching by get_iplayer and therefore will **NOT** appear in search results.  
- It **DOES NOT MATTER** that a programme is still available on the iPlayer site up to its 30-day expiry.  Once 7 days pass from its last broadcast, it is no longer available for caching by get_iplayer.
- You **MUST** download programmes more than 7 days old directly via PID or URL.  If you don't know what that means, it's time to refresh yourself [here](/wiki/documentation#recording).
- get_iplayer 2.87 or higher is **REQUIRED** to download programmes more than 7 days old via PID or URL.  If you're using your own hacked version of get_iplayer, you'll need to do some more hacking.
- There are a few exceptions to the 7-day rule, such as series like Doctor Who that have a full series catch-up policy.  The episodes of those series remain available until the final episode reaches its expiry date.  But again, once 7 days pass from the broadcast of the final episode you should expect those episodes to disappear from the get_iplayer cache.
- If a programme you're looking for does not appear in get_iplayer search results, check it on the iPlayer site **BEFORE** reporting it as an error.  If the programme is more than 7 days old (or its availability is shown as less than 23 days), you must download it directly via PID or URL.
- When in doubt, use the programme PID.  All available programmes can be downloaded via PID regardless of whether or not they are in the get_iplayer cache.
    
        TV: get_iplayer --pid=<PID> ...
        
        Radio: get_iplayer --pid=<PID> --type=radio ...
    

## Installation/Upgrade

Installation information for all platforms can be found here:

<https://github.com/get-iplayer/get_iplayer/wiki/installation>

**WARNING:** Do not use the self update facility (`get_iplayer -u`). It will result in a script that cannot be executed.  Follow the manual installation instructions at the link above.

**WARNING:** get_iplayer 2.87 is broken with Perl v5.10.0 and below.  Until the next release, see this post for a description of the problem and a solution:

<http://www.mail-archive.com/get_iplayer@lists.infradead.org/msg06034.html>

#### Linux/Unix

Note that it may take some time for get_iplayer 2.87 to be packaged for your system.  Until then, use the manual installation instructions at the link above.  

#### Windows

All Windows users **must** use the most recent get_iplayer installer to upgrade to get_iplayer 2.87:

<http://www.infradead.org/get_iplayer_win/get_iplayer_setup_latest.exe>

The embedded version of Perl has been updated for get_iplayer 2.87, so previous installers **will not work**.

The installer will update the following components to the indicated versions:

|Component|Version|  
|---------|-------|  
|get_iplayer script|2.87|  
|Perl support|4.9 [Perl 5.18]|
|MPlayer|svn-r32050 [required downgrade]|
|FFmpeg|2.2.3|
|VLC|2.1.5|
|RTMPDump|2.4-20140302-git-79459a2|
|AtomicParsley|0.9.6-hg109.9183fff907bf|

Note the required downgrade of MPlayer.

## Changes in get_iplayer 2.87

### Adaptations for BBC changes in early Oct 2014
- Implemented downloading for programmes > 7 days old
- Implemented metadata capture for programmes > 7 days old
- Restored downloading with iPlayer Radio URLs

As noted above, programmes more than 7 days old must be downloaded via PID or URL.

### `--whitespace` now only controls white space, and other file naming changes

In previous versions of get_iplayer the `--whitespace` option not only preserved white space in file names, but also retained non-ASCII characters and some punctuation.  This was more by accident than design, but has now been tightened up.  `--whitespace` now only controls whether or not white space is retained in file names (off by default).

New options have been introduced to enable the former behaviour of `--whitespace` and retain non-ASCII characters and punctuation in file names.  They are not described here because their use is strongly - nay, super extra extremely strongly - discouraged. You will find them listed in the Output section of the options list [here](/wiki/options#output-options).

> Just say no to non-ASCII characters in file names.

You are strongly recommended to stick to the default file name formulation, with or without white space.  By default, get_iplayer generates pure-ASCII file names without white space or punctuation, which is the safest and most portable option.  get_iplayer 2.87+ does a slightly better job of converting file names to ASCII by stripping any diacritical marks and preserving the base characters.

> Just say no to non-ASCII characters in file names

If you use a system locale outside Western/Central Europe or the Americas with non-UTF8 encoding, you will likely encounter problems if you attempt to retain non-ASCII characters in file names because those characters won't won't map to your locale's encoding.  

> Just say no to non-ASCII characters in file names

`--fatfilename` is now always applied on Windows and `--hfsfilename` is always applied on OSX.  Both options may be used on Linux/Unix if desired.

### `--info` now short-circuits `--pid`

The `--pid` option previously invoked an immediate download even if `--info` was specified.  Now `--info` will short-circuit that behaviour and only display metadata.  If `--pid` is used without `--info`, it will revert to previous behaviour and start an immediate download. This change was made so that you view the metadata for programmes older than 7 days without triggering a download, as you can for programmes in the cache.

### `--{metadata,subtitles,thumbnail}-only` now work with `--pid` for programmes not in cache

When `--metadata-only`, `--subtitles-only` or `--thumbnail-only` was used with `--pid`, get_iplayer would stop if the indicated PID was not found in its cache.  Now those options will perform their usual functions with `--pid` for programmes not in the cache. This can be used for all programmes, including those more than 7 days old.  

### `--swfurl` option

Using `--swfurl="<URL>"` provides a means to quickly update to a new Flash player URL for rtmpdump if the value embedded in get_iplayer should become obsolete before a new release. `--swfurl=<URL>` is a shortcut for `--rtmp-tv-opts="--swfVfy=<URL>" --rtmp-radio-opts="--swfVfy=<URL>"`.

### Return non-zero exit code if downloads fail

get_iplayer now returns a non-zero exit code when one or more downloads fail.  This is for use when scripting get_iplayer externally, e.g., from shell script or batch file.  Do not depend on the actual value of the exit code, only that it is non-zero. It will usually be the number of failed downloads, but not always.

### `--check-duration`option

The `--check-duration` option can help if you have problems with rtmpdump or mplayer truncating your recordings without signalling an error to get_iplayer.  With this option enabled, get_iplayer will print a message similar to the following for each output file:


    INFO: Duration check: recorded: 00:01:58 expected: 00:02:00 difference: -00:00:02 file: /Users/nobody/get_iplayer/Bells_on_Sunday/Bells_on_Sunday_-_Ripon_Cathedral_b04f8k3x_default.m4a

You can inspect the difference between the recorded duration and the expected duration to gauge whether of not it looks like a truncated recording.  The recorded duration will almost always differ from the expected duration by a small amount, so human judgement is required to evaluate any difference.

### `--quiet` is quieter and `--silent` is silent (almost)

The `--quiet` and `--silent` options were previously synonyms, but are now separate options.  With `--quiet` specified, get_iplayer now will only print messages it generates (usually prefixed with INFO:, WARNING: or ERROR:).  The output from all the helper applications (rtmpdump, ffmpeg, etc.) is suppressed, which was not the case in earlier versions of get_iplayer.  With `--silent` specified, get_iplayer suppresses **all** output except for the PVR report messages, which look like:

    New tv programme: 'Dipdap - 5. Letter', 'Series in which a drawn line creates endless challenges and surprises for the unsuspecting little character, Dipdap.   The Line draws Dipdap a letter. He goes to post it but strong winds get in the way.'

The PVR report messages are displayed for the benefit of users running get_iplayer via cron in order to have a visible report of activity in a PVR run.

Use of `--quiet` and `--silent` is strongly discouraged.  The most likely causes of download problems relate to rtmpdump, so it could be counterproductive to suppress its output.  The `--silent` option cannot be saved in preferences or presets.

**NOTE:** In order to suppress the default search results generated by `get_iplayer --refresh` use `--silent`.  This is a change from 2.86.  Do not use `--silent` when using `--refresh` in conjunction with `--get` or when performing a search along with a cache refresh.

### `--verbose` and `--debug` now applied to ffmpeg/avconv

A small amount of additional output from ffmpeg/avconv will now be displayed when `--verbose` or `--debug` is specified. 

### >>Important note re: obsolete FFmpeg versions<<

In order to apply `--quiet`, `--silent`, `--verbose` or `--debug` to ffmpeg/avconv, get_iplayer employs its `-loglevel` parameter.  This parameter is not available or does not function properly in ancient versions (< 0.7) of ffmpeg/avconv.  If you cannot use a modern version of ffmpeg/avconv for some reason, you must specify `--ffmpeg-obsolete` if you also specify `--quiet`, `--silent`, `--verbose` or `--debug`.  This will prevent those options from being applied to ffmpeg/avconv.

### Support for non-ASCII characters in search arguments and results

get_iplayer can now correctly process non-ASCII characters in search arguments and display them in results.  However, there is **VERY** little use for non-ASCII characters in search arguments.  Only a tiny fraction of BBC programmes have non-ASCII characters anywhere in their searchable metadata, and you can almost always formulate successful searches without them.  This feature was implemented primarily to fix bugs in the Web PVR Manager, where the user isn't always able to control the search arguments used.

In order to support non-ASCII characters, get_iplayer is now character encoding-aware, meaning that it depends on knowing the encoding used for your search arguments and how your console expects output to be encoded.  These encodings are almost always different between Windows and Linux systems, even for similar location and language.  In virtually every case, get_iplayer should be able to automatically detect the necessary encodings at run time. In the unlikely event you ever need to adjust the encodings detected by get_iplayer, more information can be found [here](/wiki/encodings).

There are many possible permutations of locale/language/encoding.  get_iplayer is developed to work with iPlayer, which is a UK-based service that uses the English language.  Inasmuch as get_iplayer has any sort of support policy, there is no promise to support Windows system locales other than UK English (with default code page settings) or Linux/Unix/OSX locales other en_GB.UTF-8.

### Web PVR Manager now speaks UTF-8

As part of implementing support for non-ASCII characters, communication between the Web PVR Manager and get_iplayer and communication between the Web PVR Manager and the user's browser now uses UTF-8 encoding exclusively, on all platforms.  

This should be transparent to users, though there are some edge cases to be aware of.  For example, if you use Linux with a single-byte encoding in your system locale (e.g., ISO-8859-1), and you create files with non-ASCII characters in their names with the get_iplayer CLI, you won't be able to play those files using the PlayFile link in the Web PVR Manager because the file name will be encoded as UTF-8, which won't match the encoding used in the file name on disk.  The Web PVR Manager itself only produces pure-ASCII file names, so do likewise with the CLI if you want to share files between them.

> Just say no to non-ASCII characters in file names

## Fixes in get_iplayer 2.87

- Channel names and schedule URLs updated to match iPlayer site (thanks Jon Davies)
- Fixed bug in generation of Freevo/MythTV XML metadata files (thanks Matthew Boyle)
- Fixed bug that resulted in unplayable podcasts on Windows
- Fixed "Wide character in print" warnings generated by typographer's quotes in search results
- Fixed improper decoding of output path on Windows system options file when path contained non-ASCII characters
- Allow overriding rtmpdump --timeout option via --rtmp-{tv,radio}-opts
- Values for --versions are now case-sensitive (must be lower-case)
- Fixed creating/editing PVR jobs with non-ASCII characters in programme names

## Changelog

The full log of changes since v2.86 can be viewed here:

<https://github.com/get-iplayer/get_iplayer/compare/v2.86...v2.87>