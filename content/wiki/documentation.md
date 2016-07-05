## get_iplayer Usage and Examples

## Table of Contents

* [Searching](#searching)
* [Recording](#recording)
* [Live Recording](#live-recording)
* [Searching the Future Programme Schedule](#searching-the-future-programme-schedule)
* [Searching the Recording History](#searching-the-recording-history)
* [Indexing and Caching Features](#indexing-and-caching-features)
* [Streaming](#streaming)
* [Live Streaming](#live-streaming)
* [Saving Settings](#saving-settings)
* [Using a Web Proxy](#using-a-web-proxy)
* [Option Presets and Shortcuts](#option-presets-and-shortcuts)
* [Subtitles](#subtitles)
* [More Programme Information](#more-programme-information)
* [Filenames and Directories](#filenames-and-directories)
* [Custom Commands](#custom-commands)
* [PVR Usage](#pvr-usage)
* [Scheduling the PVR](#scheduling-the-pvr)
* [External Programs](#external-programs)
* [Metadata Tagging](#metadata-tagging)
* [Substitution Parameters](#substitution-parameters)

## Command Usage

The full get_iplayer UNIX manual page listing all available options can be viewed **[here](/wiki/manpage)**. 

For basic help run:

    get_iplayer -h

For advanced and extended options run:

    get_iplayer --long-help

## Examples

<a name="searching"></a>
### Searching

**[Click Here for All Search Options](/wiki/manpage#search-options)**

get_iplayer performs searches against a local cache of the programme index it creates with data retrieved from BBC sites (see [below](#indexing-and-caching-features)). After your first installation of get_iplayer, you must refresh the programme index cache each calendar week for a month in order to build up 30 days of listings. Once that is done, the 30-day buffer will be maintained as long as you refresh once per calendar week.

Search output appears in this format:

	...
	208:  Doctor Who: Series 7 Part 2 - 1. The Bells of Saint John, BBC One, b01rryzz
	209:  Doctor Who: Series 7 Part 2 - 2. The Rings Of Akhaten, BBC One, b01rx0lj
	210:  Doctor Who: Series 7 Part 2 - 3. Cold War, BBC One, b01s1cz7
	...

Format = index: name - episode, channel, pid 

The index number is intended as an easy-to-type way to indicate a programme to download (see [recording](#recording)). However, index numbers are not persistent. They are regenerated every time the cache is updated. You can also use `<pid>` for recording. The `<pid>` value is persistent across cache refreshes.

**Search examples**

List all TV programmes (`--type=tv` is default):

    get_iplayer

List all TV programmes with names containing 'news':

    get_iplayer --type=tv news

The `--type=tv` option may be used explicitly as well

List all radio programmes with names containing 'news':

    get_iplayer --type=radio news

List all TV programmes with names containing 'news', but hide programmes already recorded:

    get_iplayer --hide news

List all TV programmes with names containing 'bad news':

    get_iplayer "bad news"

Search terms containing white space must be enclosed in quotes.

List all TV programmes showing only `pid`, `name` and `episode` fields:

    get_iplayer --listformat="<pid>: <name>-<episode>"

Search all TV programmes for the word 'hello' in the `name` or `episode` fields:

    get_iplayer --fields=name,episode hello

This applies your search term against a space-delimited concatenation of the indicated fields in the order given (`<name> <episode>`). The other field that may be useful for searching is `desc`, the episode description.

Search all TV programmes for the word 'hello' in the `name`, `episode` or `desc` fields, with expanded output:

    get_iplayer --long hello

The `--long` option implicit sets `--fields=name,episode,desc`.

List all TV programmes from channel 'BBC One':

    get_iplayer --channel="BBC One"

List all TV programmes added to the cache since 24 hours ago:

    get_iplayer --since=24

List all available radio channels:

    get_iplayer --list=channel --type=radio

List all programme metadata and available recording modes for programme with index number 123:

    get_iplayer --info 123

**Search strings as regular expressions**

Search strings are interpreted as [regular expressions](http://www.regular-expressions.info/quickstart.html). If you don't use any regular expression metacharacters in your search string, get_iplayer looks for a substring match. get_iplayer searches are case-insensitive.

For example, this search would find all TV programmes with 'east' anywhere in the name ("EastEnders", "East Midlands Today", "Minibeast Adventure", etc.):

    get_iplayer "east"

whereas this search would only find TV programmes with 'east' at the beginning of their names (^ anchors match to beginning of string), followed by a whitespace character (represented by \s), which would match "East Midlands Today", but not "EastEnders"):

    get_iplayer "^east\s"

Search strings for other fields are also interpreted as regular expressions. To search for programmes on Radio 4 but not on Radio 4 Extra, use a regular expression to anchor a match for the channel name to the end of the string:

    get_iplayer --type=radio --channel="Radio 4$"

To search for a programme whose complete name is a number, use a regular expression to anchor a match at the beginning of the string.  The regular expression differentiates the search string from an index number:

    get_iplayer "^2012"

On the command line, always quote search strings containing regular expressions.

<a name="recording"></a>
### Recording

**[Click Here for All Recording Options](/wiki/manpage#recording-options)**

In its simplest form, recording only requires you to add `--get` to your search command searches to record the matching programmes. You can also record single programs by PID or URL (see below).

Record TV programme number 123 (index number from search results):

    get_iplayer --get 123

Record radio programme number 10123 (index number from search results):

    get_iplayer --get 10123

Record TV programme number 123 and save in `/home/user/TV-files/`:

    get_iplayer --get 123 --output "/home/user/TV-files/"

Record radio programme number 10123 and TV programme number 324:

    get_iplayer --get 10123 324

Record all radio programmes with  "Bells on Sunday" in name:

    get_iplayer --type=radio --get "Bells on Sunday"

Record all TV programmes with "blue peter" in name:

    get_iplayer --get "blue peter"

Record all TV programmes with "blue peter" in the title, plus programme index 123:

    get_iplayer --get "blue peter" 123

Record all programmes with 'hello' in the name, episode or description:

    get_iplayer --long --get hello

<a name="recording-url"></a>
#### Recording with episode URL

Record a radio programme using its episode URL on the iPlayer Radio site:

    get_iplayer "http://www.bbc.co.uk/programmes/b07hfwrr"

Record a TV programme using its episode URL on the iPlayer site:

    get_iplayer "http://www.bbc.co.uk/iplayer/episode/b01sc0wf/Doctors_Series_15_Perfect/"

get_iplayer detects that you have provided a URL, but you may also use the more explicit form with `--url`:

    get_iplayer --url="http://www.bbc.co.uk/programmes/b07hfwrr"

<a name="recording-pid"></a>
#### Recording with episode PID

See [BBC Programme Identifier](https://en.wikipedia.org/wiki/BBC_Programme_Identifier) for a description of PIDs.
    
You simply extract the PID from a programme's episode URL (see above):

	get_iplayer --pid=b07hfwrr
	get_iplayer --pid=b01sc0wf

You do not need to use `--get` with `--pid`.

There are several ways to download multiple PIDs.  For programmes from the last 30 days catalogued in the local index cache, you can explicitly match against the `pid` field (ignored by default) in the cache:

    get_iplayer --get --fields=pid b012h9yn b012hbg5

or you can use the `pid:` prefix to denote that your search terms are PIDs:

    get_iplayer --get pid:b012h9yn pid:b012hbg5

You can also bypass the index cache and record multiple PIDs with the `--pid` option:

Comma-separated list

    get_iplayer --pid=012h9yn,b012hbg5

Multiple `--pid` options

    get_iplayer --pid=b012h9yn --pid=b012hbg5

<a name="recording-force"></a>
#### Re-recording a programme

When a programme is successfully recorded, it is logged in the `download_history` file in get_iplayer's profile directory. If a programme is in the download history it cannot be re-downloaded unless you explicitly use the `--force` option, e.g.:

    get_iplayer --pid=b01sc0wf --force

If an output file with exactly the same name already exists, `--force` will not overwrite it. You must also add the `--overwrite` option:

    get_iplayer --pid b01sc0wf --force --overwrite

Exercise caution when overwriting files.

<a name="recording-versions"></a>
#### Recording alternate versions

A single iPlayer programme episode may be available in several versions. For example, some TV programmes may be available with and without signing or audio description. Some programmes may be available in "original" and "editorial" versions, with the latter being edited after transmission. Some radio programmes may be available in "original" and "podcast" versions, with the latter having music clips removed or other edits made for podcast distribution. Use the `--versions` options to indicate the version you wish to download.

Download a TV programme with audio description, with no download if a version with audio description is not available:

    get_iplayer --get 123 --versions=audiodescribed

Download a TV programme with signing, with no download if a version with signing is not available:

    get_iplayer --get 123 --versions=signed

Multiple versions may be specified as a comma-delimited list, with values being processed from left to right. get_iplayer will attempt to download the first version found.  

Download a TV programme without audio description if a version *with* audio description is not available

    get_iplayer --get 123 --versions=audiodescribed,default

where "default" is used to indicate that the first available version without audio description.

Download the "original" version of a radio programme, but use the "editorial" version if the "original" version is not available:

    get_iplayer --get 12345 --versions=original,editorial

Unless you require TV programmes with audio description or signing, you are unlikely to need `--versions`. The default version determined by get_iplayer is nearly always what you want.

You can discover what versions of a programme are available by using the `--info` option:

    get_iplayer --info 123 

<a name="recording-recursive"></a>
#### Recursive (series/brand) recording

PIDs can also reference brands or series as well as individual programme episodes. You can find the relevant PID in the brand/series home page URL. For example, the brand home page for Casualty is:

<http://www.bbc.co.uk/programmes/b006m8wd>

so the brand PID is 'b006m8wd'. The brand home page can usually be accessed via the "Programme website" link on iPlayer episode pages for TV programmes or the the "Home" link on iPlayer Radio episode pages for radio programmes.

get_iplayer can use brand/series PIDs to recursively download all episodes in the brand or series: 

    get_iplayer --pid=b006m8wd --pid-recursive

The value for `--pid` is the brand/series PID and `--pid-recursive` instructs get_iplayer to examine the brand/series metadata to pick out the associated episode PIDs and download them. If you are using a brand PID, you may find a number of clips included along with the programme episodes. If you don't want to download those clips, add `--pid-recursive-noclips` to your command.

Recursive recording of a brand/series will first print a list of the enclosed series/episodes. If you don't want to record the entire brand and cannot find a home page for a particular series, run the recursive recording in test mode:

    get_iplayer --pid=b006m8wd --pid-recursive --test

Type Ctrl+C to stop get_iplayer after the list of series and episodes has been printed. You can then pick out the PID for the desired series and use it with `--pid-recursive`

**NOTE**: Recursive recording is crude and often unreliable. The metadata that get_iplayer relies upon for recursive recording may be incomplete or incorrect or absent, so not all brands/series can be recorded with `--pid-recursive`. You may also find many episodes listed in a brand/series are no longer available, but get_iplayer will attempt to process them anyway.

<a name="recording-modes"></a>
#### Recording specific media streams

iPlayer programmes are streamed in several formats and quality levels. In general, you should stick to the default settings, which will download the best quality stream for your programme. However, you can also pick specific media streams or maximum quality levels for recording. See [Recording Modes](/wiki/modes) for details.

Record only a specific HD stream for a TV programme, with no fallback to lower-quality streams:

    get_iplayer --get 123 --tvmodes=hlshd

Record only a specific HD stream for a TV programme, with fallback to specific lower-quality stream (mode values processed from left to right):

    get_iplayer --get 123 --tvmodes=hvfhd,hvfsd

Record the medium-quality stream for a TV programme, with fallback to next-lower-quality streams:

    get_iplayer --get 123 --tvmode=good

Record the lowest-quality stream for a radio programme:

    get_iplayer --get 12345 --radiomode=worst

<a name="live-recording"></a>
### Live Recording [DEPRECATED]

**[Click Here for All Recording Options](/wiki/manpage#recording-options)**

List live TV:

    get_iplayer --type=livetv

List live TV and live radio:

    get_iplayer --type=livetv,liveradio

Record a live BBC iPlayer TV programme (e.g. BBC Two):

    get_iplayer --type=livetv --get "BBC Two"
    get_iplayer --type=livetv "http://www.bbc.co.uk/iplayer/live/bbctwo"
    get_iplayer --type=tlivev --pid="bbc_two"

Record a high quality live BBC iPlayer radio programme (e.g. BBC Radio 1):

    get_iplayer --type=liveradio --get "Radio 1"
    get_iplayer --type=liveradio "http://www.bbc.co.uk/radio/player/bbc_radio_one"
    get_iplayer --type=liveradio --pid=bbc_radio_one

<a name="searching-the-future-programme-schedule"></a>
### Searching the Future Programme Schedule

**[Click Here for All Search Options](/wiki/manpage#search-options)**

It is possible to index, search and queue recordings for specific programmes that have not yet been made available. This is currently only available for BBC TV and radio programmes and only searches for up to 14 days in advance. Note that some of the programmes in the BBC schedules are never released on iPlayer and therefore will never get recorded even if you can find them in the search results. Note that indexing can take quite a bit longer with `--refresh-future` specified.

Refresh the cache with future schedules (e.g. for TV). You must do this otherwise you will not be able to search for future programmes:

    get_iplayer --refresh-future --refresh

Save the refreshing of future programmes into your default settings (a good idea if you want the above to be automatic):

    get_iplayer --add-prefs --refresh-future

To search for a programme additionally in the future just use any of the usual search commands but adding --future:

    get_iplayer "Eastenders" --future

You cannot record a programme in the future but you can queue it in the PVR for recording when it becomes available (if at all). In this example the index of the search results for a future episode of Eastenders was '123′:

    get_iplayer --pvr-queue 123

<a name="searching-the-recording-history"></a>
### Searching the Recording History

**[Click Here for All Search Options](/wiki/manpage#search-options)**

The recording history is a text database of the programmes you have recorded since you started using get_iplayer. Its primary purpose is to prevent get_iplayer from downloading the same programme more than once. You can search the recordings history much like the normal programme types.

Search for "Doctor Who" in the history

    get_iplayer --history "Doctor Who""

Show detailed programme metadata for all recorded programmes matching “Doctor Who” in the history

    get_iplayer --history "Doctor Who" --info

Download thumbnails for all recorded programmes matching “Doctor Who” in the history

    get_iplayer --history "Doctor Who" --thumbnailonly

Download thumbnails for all recorded programmes matching “Doctor Who” in the history and where the media file hasn't been deleted.

    get_iplayer --history "Doctor Who" --thumbnailonly --skipdeleted

<a name="indexing-and-caching-features"></a>
### Indexing and Caching Features

**[Click Here for All Config Options](/wiki/manpage#config-options)**

Refresh the TV programme cache (this happens after 4 hrs automatically - see `--expiry` option):

    get_iplayer --refresh

Refresh the programme cache for all types:

    get_iplayer --refresh --type=all

Refresh the TV and radio programme caches:

    get_iplayer --refresh --type=tv,radio

Set the expiry of the caches (in seconds):

    get_iplayer --add-prefs --expiry=3600

Exclude specific channels (e.g., CBBC and CBeebies) from indexing:

    get_iplayer --refresh-exclude="cbeebies,cbbc" --refresh

Index only specific channels (e.g., CBBC and CBeebies):

    get_iplayer --refresh-include="cbbc,cbeebies" --refresh

<a name="streaming"></a>
### Streaming [DEPRECATED]

**[Click Here for All Output Options](/wiki/manpage#output-options)**

Stream a programme in mplayer or xine while recording it to disk (does not yet work in win32):

    get_iplayer --stdout --get 123 | mplayer -cache 3072 -
    get_iplayer --stdout --get 123 | xine stdin:/

Stream a programme in mplayer/vlc/ffplay while not recording it to disk:

    get_iplayer --stream 123 --player="mplayer -cache 3072 -"
    get_iplayer --stream 123 | mplayer -cache 3072 -
    get_iplayer --stream 123 --player="vlc -"
    get_iplayer --stream 123 --player="ffplay -"

<a name="live-streaming"></a>
### Live Streaming [DEPRECATED]

**[Click Here for All Output Options](/wiki/manpage#output-options)**

*Note: Please upgrade to rtmpdump 2.3 or later for reliable live streaming.*

Stream a live BBC iPlayer TV programme to mplayer while not recording it to disk (e.g. BBC Two):

    get_iplayer --stream --type=livetv "BBC Two" --player="mplayer -cache 512 -"
    get_iplayer --stream --type=livetv --pid="bbc_two" | mplayer -cache 512 -
    get_iplayer --stream --type=livetv "http://www.bbc.co.uk/iplayer/live/bbctwo" --player="mplayer -cache 512 -"
    get_iplayer --stream --type=livetv "http://www.bbc.co.uk/iplayer/live/bbctwo" | mplayer -cache 512 -

Stream a live BBC iPlayer radio programme to mplayer while not recording it to disk (e.g. BBC Radio 1):

    get_iplayer --stream --type=liveradio "Radio 1" --player="mplayer -cache 64 -"
    get_iplayer --stream --type=liveradio --pid='bbc_radio_one' | mplayer -cache 64 -
    get_iplayer --stream --type=liveradio "http://www.bbc.co.uk/radio/player/bbc_radio_one" --player="mplayer -cache 64 -"
    get_iplayer --stream --type=liveradio "http://www.bbc.co.uk/radio/player/bbc_radio_one" | mplayer -cache 64 -

<a name="using-a-web-proxy"></a>
### Using a Web Proxy

**[Click Here for All Recording Options](/wiki/manpage#recording-options)**

If you are behind a web proxy you can use the following to specify it:

    get_iplayer --proxy=http://[username:password@]<server:<port

To make only the metadata web requests go through the proxy add the `--partial-proxy` option. If you use RTMP streaming, this will only work if your network allows direct access to the streaming port (typically port 1935).

<a name="saving-settings"></a>
### Saving Settings

**[Click Here for All Config Options](/wiki/manpage#config-options)**

Default user settings can be added, removed or changed as follows:

Save or update proxy settings and verbose mode as user defaults in get_iplayer profile directory (`$HOME/.get_iplayer/options` or `%USERPROFILE%\.get_iplayer\options` in Windows):

    get_iplayer --prefs-add --verbose --proxy=http://proxy.domain.com:3128

See below for options file format.

Additionally save programme type settings (this will only update the specified options - existing options will be retained):

    get_iplayer --prefs-add --type=radio,tv

Remove a specific option from those saved (e.g. --proxy):

    get_iplayer --prefs-del --proxy=http://proxy.domain.com:3128

Show all saved default options:

    get_iplayer --prefs-show

Completely clear all saved default options:

    get_iplayer --prefs-clear

System-wide defaults can be added to `/etc/get_iplayer/options` on Unix/OS X and `%ALLUSERSPROFILE%\get_iplayer\options` in Windows. The format is as follows:

    <option key> <option value>

The option key is the option name with hyphens removed.  For example, `--file-prefix` becomes `fileprefix`.  Boolean options have a value of 0 (off) or 1 (on). Example entries:

    output /path/for/output
    fileprefix <name>-<episode>
    raw 1

<a name="option-presets-and-shortcuts"></a>
### Option Presets and Shortcuts

**[Click Here for All Config Options](/wiki/manpage#config-options)**

User defined groups of options can be added, removed or changed as presets.

Save or update several options in the preset named 'my\_preset' (saved in `~/.get_iplayer/presets/my_preset` or `%USERPROFILE%\.get_iplayer\presets\my_preset` in Windows):

    get_iplayer --preset=my_preset --prefs-add --hide --since=24

Additionally save programme type for preset named 'my\_preset' (this will only update the specified preset - existing preset options will be retained):

    get_iplayer --preset=my_preset --prefs-add --type=radio,TV

[Custom commands](#custom-commands) can be saved in presets:

Unix/OS X

    get_iplayer --preset=mp3_320k --prefs-add --command='ffmpeg -i "<filename>" -vn -c:a libmp3lame -ab 320k -y "<dir>/<fileprefix>.mp3"'

Windows

    get_iplayer --preset=mp3_320k --prefs-add --command="ffmpeg -i \""<filename>"\" -vn -c:a libmp3lame -ab 320k -id3v2_version 3 -write_id3v1 1 -y \""<dir>/<fileprefix>.mp3"\""

Remove a specific option from those saved in the preset named 'my\_preset' (e.g. `--since=24`):

    get_iplayer --preset=my_preset --prefs-del --since=24

Show all saved options in preset named 'my\_preset':

    get_iplayer --preset=my_preset --prefs-show

Completely clear all saved options in preset named 'my\_preset':

    get_iplayer --preset=my_preset --prefs-clear

Use the preset named 'my\_preset' to search for programmes with names containing 'news':

    get_iplayer --preset=my_preset news

Here is a more useful example: a preset that shows me the BBC iPlayer TV programmes added to my cache in the last 24hrs, hides ones I've already downloaded, and exclude some channels.

    get_iplayer --prefs-add --preset=last24 --type=tv --since=24 --hide --versionlist=default --exclude-channel=alba,cbbc,cbeebies,parliament

Now, to run the preset at any time simply type:

    get_iplayer --preset=last24

<a name="subtitles"></a>
### Subtitles

**[Click Here for All Recording Options](/wiki/manpage#recording-options)**

Record programme number 123 with subtitles (if available):

    get_iplayer --subtitles --get 123

A subtitle delay can be inserted (specified in milliseconds, here 5 secs):

    get_iplayer --subtitles --suboffset 5000 --get 123

(Re)download subtitles only (if available):

    get_iplayer --subtitles-only --get 123

<a name="more-programme-information"></a>
### More Programme Information

**[Click Here for All Display Options](/wiki/manpage#display-options)**

#### Programme Detailed Stream Information

Display the Various stream URLs for programme index 123:

    get_iplayer --streaminfo 123

#### Full Program Information Display

Display the programme metadata for index 123:

    get_iplayer --info 123

Display the programme metadata for PID b012hbg5:

    get_iplayer --info --pid=b012hbg5

#### Metadata Files

The programme metadata can be additionally downloaded using the `--metadata=[TYPE]` option. Where [TYPE] is one of xbmc, xbmc\_movie, freevo, generic (The xbmc, xbmc\_movie, freevo metadata types are deprecated).

Save the metadata after a successful download into an xml file:

    get_iplayer --metadata=generic --get 123

Save **only** the metadata for a programme into an xml file (but don't record the programme). This is useful if you forgot to download the metadata when recording.

    get_iplayer --metadata-only --metadata=generic 123

#### Thumbnail

 A programme thumbnail can be automatically downloaded using the `--thumbnail` option.

    get_iplayer --thumbnail --get 123

Save **only** the thumbnail(s) for a programme (but don't record the programme). This is useful if you forgot to get the thumbnail when recording.

    get_iplayer --thumbnail-only 123

#### Update Your Entire Recording Collection with Thumbnails, Metadata and Subtitles

As long as your programmes remain in the directory they were originally recorded into you can retrospectively download the thumbnail, metadata or subtitles of the shows in your recordings history, provided that the resources are still available from the iPlayer site.

Get all thumbnails for files that still exist (in this case for programmes matching 'Doctor Who'):

    get_iplayer --thumbnail-only --history --skipdeleted "Doctor Who"

Get all the metadata files (in generic format) for files that still exist:

    get_iplayer --metadata-only --metadata=generic --history --skipdeleted

Get all subtitles for files that still exist (Note that you can only get subs if the programme is still available on iPlayer):

    get_iplayer --subtitles-only --history --skipdeleted

<a name="filenames-and-directories"></a>
### Filenames and Directories

**[Click Here for All Output Options](/wiki/manpage#output-options)**

#### Filenames

Use a filename prefix format with [substitution parameters](#substitution-parameters):

    --file-prefix="<name>-<episode>-<longname>-<version>-<pid>"

Use a filename prefix format that is friendly to Kodi scrapers:

    --fileprefix="<nameshort><.senum><.episodeshort>"

Details on filename prefixes can be found **[here](/wiki/fileprefix)**.

#### Valid Characters

Several options exist for controlling what characters are allowed in filenames.

Allow use of spaces in filenames (by default these are converted to '\_').

    --whitespace

Use only filenames valid for DOS/Windows FAT filesystem.

    --fatfilename

#### Recording to Specific Directories

Use a specific directory for all programmes recorded:

    --output="/home/user/recordings/"

Override the above for all radio (or TV) programmes recorded:

    --outputradio="/home/user/recordings-radio/"
    --outputtv="/home/user/recordings-tv/"

#### Subdirectories

Use a subdirectory for each programme name:

    --subdir

Use a subdirectory format with [substitution parameters](#substitution-parameters):

    --subdir-format="<nameshort>-<seriesnum>"

<a name="custom-commands"></a>
### Custom Commands

**[Click Here for All Output Options](/wiki/manpage#output-options)**

Run a custom user command after a successful recording using [substitution parameters](#substitution-parameters). Custom commands may be added to presets and pvr jobs for ease of reuse. Examples:

**Extract the audio from a TV or radio programme and transcode to MP3 format at 320kbps constant bit rate (CBR):**

Unix/OS X:

    get_iplayer --get 123 --command='ffmpeg -i "<filename>" -vn -c:a libmp3lame -ab 320k -y "<dir>/<fileprefix>.mp3"'

Windows:

	get_iplayer --get 123 --command="ffmpeg -i \""<filename>"\" -vn -c:a libmp3lame -ab 320k -id3v2_version 3 -write_id3v1 1 -y \""<dir>/<fileprefix>.mp3"\""

To transcode at best variable bit rate (VBR), replace `-ab 320k` with `-aq 0`.

**Re-mux audio and video from a TV programme into a MKV file:**

Unix/OS X:

	get_iplayer --get 123 --command='ffmpeg -i "<filename>" -c:v copy -c:a copy  -y "<dir>/<fileprefix>.mkv"'

Windows:

	get_iplayer --get 123 --command="ffmpeg -i \""<filename>"\" -c:v copy -c:a copy  -y \""<dir>/<fileprefix>.mkv"\""

You can re-mux to an AVI file by changing `.mkv` to `.avi` in the commands above.

**Create a Kodi .nfo file for a TV programme:**

Unix/OS X (with [xsltproc](http://xmlsoft.org/XSLT/xsltproc2.html)):

    get_iplayer --get 123 --metadata=generic --command='xsltproc --output "<dir>/<fileprefix>.nfo" "/path/to/nfo.xsl" "<dir>/<fileprefix>.xml"'

Windows (with [xsltproc](http://xmlsoft.org/XSLT/xsltproc2.html)):

    get_iplayer --get 123 --metadata=generic --command="xsltproc --output \""<dir>/<fileprefix>".nfo\" \"c:\path\to\nfo.xsl\" \""<dir>/<fileprefix>".xml\""

Windows (with [xmlstarlet](http://xmlstar.sourceforge.net)):

    get_iplayer --get 123 --metadata=generic --command="xml tr \"c:\path\to\nfo.xsl\" \""<dir>/<fileprefix>".xml\" > \""<dir>/<fileprefix>".nfo\""

where `nfo.xsl` is:

    <?xml version="1.0"?>
    <xsl:stylesheet version="1.0"
        xmlns:xsl="http://www.w3.org/1999/XSL/Transform"
        xmlns:gip="http://linuxcentre.net/xmlstuff/get_iplayer"
        exclude-result-prefixes="gip">
    <xsl:template match="gip:program_meta_data">
    <episodedetails>
        <aired><xsl:value-of select="gip:lastbcastdate"/></aired>
        <episode><xsl:value-of select="gip:episodenum"/></episode>
        <genre><xsl:value-of select="gip:category"/></genre>
        <id><xsl:value-of select="gip:pid"/></id>
        <plot><xsl:value-of select="gip:desclong"/></plot>
        <season><xsl:value-of select="gip:seriesnum"/></season>
        <studio><xsl:value-of select="gip:channel"/></studio>
        <title><xsl:value-of select="gip:episodeshort"/></title>
        <thumb><xsl:value-of select="gip:thumbnail"/></thumb>
    </episodedetails>
    </xsl:template>
    </xsl:stylesheet>

<a name="pvr-usage"></a>
### PVR Usage

**[Click Here for All PVR Options](/wiki/manpage#pvr-options)**

The PVR functionality allows you to record any number of iPlayer programmes using any combination of search terms that you would normally run on the command line. The PVR searches are saved in `$HOME/.get_iplayer/pvr/` or `%USERPROFILE%\.get_iplayer\pvr\` in Windows.

You can add, delete and list the PVR searches. This feature allows you to run multiple batch recordings from a scheduler such as Unix cron (and possibly the Windows scheduler). A tutorial is on how to set up and use the PVR with cron is **[here](/wiki/pvrcron)**.

Add a new PVR search for a specific programme (i.e. 'series link'):

    get_iplayer --pvr-add=Top_Gear "Top Gear"

Add a new one-off recording PVR search. This will effectively queue the programmes for recording and delete the PVR search after completion:

    get_iplayer --pvr-queue 123 231 32 "Blue Peter"

Add a new one-off recording PVR search for a specific PID:

    get_iplayer --pvr-queue --pid=tv:b01a2b3c

List the PVR searches already added:

    get_iplayer --pvr-list

Remove a PVR search:

    get_iplayer --pvr-del=Top_Gear

Disable a PVR search:

    get_iplayer --pvr-disable=Top_Gear

Re-enable a PVR search:

    get_iplayer --pvr-enable=Top_Gear

Run the PVR (this really should be added to your scheduler such as cron):

    get_iplayer --pvr

<a name="scheduling-the-pvr"></a>
### Scheduling the PVR

**[Click Here for All PVR Options](/wiki/manpage#pvr-options)**

#### Unix/OS X

Add this line to add to user's crontab (use `crontab -e` to edit) - this will run all of the PVR jobs every hour:

    0 * * * * /path/to/get_iplayer --pvr 2>> /tmp/get_iplayer.log

Optionally, to notify by email when programmes have been recorded, add this to the top of your crontab (this will take the stdout from the cron job and send it to the specified email address):

    MAILTO=me@mydomain.com

Or, run the PVR Scheduler from the command line. This will fire off the PVR every hour as long as the command is running:

    get_iplayer --pvrscheduler 3600

#### Windows

With the latest installer there will be an entry in the Start menu to 'Run PVR Scheduler Now'. This will start a command window which will fire off the PVR every 4 hours. Alternatively if, you wish to use the Windows Scheduler see [this guide](http://www.beebotron.org/helper_get_iplayer_help.php) for full instructions.

<a name="external-programs"></a>
### External Programs

**[Click Here for All External Program Options](/wiki/manpage#external-program-options)**

Several external programs can be used by get_iplayer. The required programs for each mode and type are listed **[here](/wiki/modes#external-programs)**. The following options are used to specify the exact path so that get_iplayer knows where they are. If they are already in $PATH then there is no need to specify them:

    --atomicparsley
    --ffmpeg
    --id3v2 [DEPRECATED]
    --rtmpdump [DEPRECATED]

For example, to save the ffmpeg location to your default settings in Windows (you don't need to do this if you use the get_iplayer installer):

    get_iplayer --prefs-add --ffmpeg="C:\Program Files\utils\ffmpeg.exe"

To save the ffmpeg location to your default settings in Unix/OS X (you don't need to do this if ffmpeg is in $PATH):

    get_iplayer --prefs-add --ffmpeg="/usr/bin/ffmpeg"

<a name="metadata-tagging"></a>
### Metadata Tagging

**[Click Here for All Metadata Tagging Options](/wiki/manpage#tagging-options)**

get_iplayer adds metadata tags to output files in MP4, M4A and MP3 **[DEPRECATED]** format.  Details on metadata tagging can be found **[here](/wiki/tagging)**.

<a name="substitution-parameters"></a>
### Substitution Parameters

The following substitutions are available to certain options such as `--command` and `--fileprefix`. To see a list of all available parameters for a specific programme use the `--info` option.

    <available>      = date/time made available (ISO8601 format)
    <brand>          = programme brand title
    <channel>        = programme channel
    <desc>           = brief description
    <desclong>       = long description
    <descmedium>     = medium description
    <descshort>      = short description
    <dir>            = directory of recorded file
    <dldate>         = date when the file was obtained in YYYY-MM-DD format
    <dltime>         = time when the file was obtained in HH:MM:SS format
    <duration>       = programme duration in seconds
    <episode>        = episode title (incl. episode number)
    <episodenum>     = episode number
    <episodepart>    = letter denoting part of multi-part episode
    <episodeshort>   = episode title with episode number stripped
    <expires>        = time when programme will expire (epoch format)
    <ext>            = filename extension of recorded file
    <filename>       = filename of recorded file
    <filepart>       = filename of partially recorded file
    <fileprefix>     = filename prefix of recorded file
    <firstbcast>     = date and time when programme was first broadcast
    <firstbcastdate> = date portion of <firstbcast> in YYYY-MM-DD format
    <firstbcastrel>  = relative time when programme was first broadcast
    <index>          = index number (changes with every cache refresh)
    <lastbcast>      = date and time when programme was last broadcast
    <lastbcastdate>  = date portion of <lastbcast> in YYYY-MM-DD format
    <lastbcastrel>   = relative time when programme was last broadcast
    <longname>       = programme long name
    <mode>           = mode used to record programme
    <name>           = programme name
    <nameshort>      = programme name with series number stripped
    <pid>            = programme ID
    <player>         = programme URL
    <runtime>        = programme runtime in minutes
    <senum>          = series and episode numbers in s##e## format (may be absent)
    <series>         = series title (may be absent)
    <seriesnum>      = series number
    <symlink>        = filename of any symlink file if specified
    <thumbnail>      = programme thumbnail URL
    <timeadded>      = time when programme was added to cache (epoch format)
    <title>          = programme full title
    <type>           = programme type: tv, radio, etc.
    <version>        = selected version e.g 'signed'
    <versions>       = comma separated list of versions
    <web>            = series URL

*Source: linuxcentre.net*
