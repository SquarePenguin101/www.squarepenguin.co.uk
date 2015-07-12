## get_iplayer 2.89-2.90 Release Notes

**NOTE:** get_iplayer v2.88 was withdrawn before general release. get_iplayer v2.90 was a quick repair to 2.89.  v2.90 is the successor to v2.87.

## Read This First

There were major changes in the recent 2.87 release.  If you didn't update to 2.87, read the [release notes](/wiki/release287) now. Then [read this](/wiki/faq#faq1).  And [again](/wiki/faq#faq1) for good measure.

### Downloading via PID

There have been major changes in 2.89 (see below).  From now on, you are more likely to be required to use programme identifiers (PIDs) to download programmes than in the past.  Now is the time to acquaint yourself with this mode of operation by reading [this](/wiki/documentation#recording) and [this](https://squarepenguin.co.uk/guides/tv-download-guide/#how-do-i-record-a-programme-with-get-iplayer) (external link).  Then **try it yourself** before asking for help.  It's documented and involves only a few extra keystrokes, so it should not present an obstacle to you.  The other thing you must remember about downloading via PID is that you must include `--type=radio` in your command when downloading radio programmes with `--pid`.  

And no, this doesn't work for the Web PVR Manager.  If you don't want to learn how to use your command prompt, you can use the Quick URL box.  Paste in the programme's episode page URL from the iPlayer site and click **Record**.  If you are downloading a radio programme, you must check the "BBC Radio" box for **Programme type**.

See information below about downloading multiple PIDs.


## Installation/Upgrade

Installation information for all platforms can be found here:

<https://github.com/get-iplayer/get_iplayer/wiki/installation>

After installing, **immediately** refresh your TV and radio cache information:

    get_iplayer --refresh --type=tv,radio

#### Linux/Unix

Note that it may take a long  time for get_iplayer 2.89 to be packaged for your system.  Until then, use the manual installation instructions at the link above.  

#### Windows

All Windows users **must** use the most recent get_iplayer installer to upgrade to get_iplayer 2.89:

<http://www.infradead.org/get_iplayer_win/get_iplayer_setup_latest.exe>

The embedded version of Perl was updated for get_iplayer 2.87, so previous installers **will not work**.

The installer will update the following components to the indicated versions:

|Component|Version|  
|---------|-------|  
|get_iplayer main script|2.89|  




## Partial restoration of search functions broken by removal of BBC data feeds in late Oct 2014

As you're probably aware, the BBC killed the data feeds get_iplayer used to populate its programme data cache.  The cache is what supports searching in get_iplayer, and thus also supports the PVR functionality.  Those functions have been partially restored, but you consider those repairs as only a stopgap solution until the BBC blow up get_iplayer again.

You should now once again be able to search for TV and radio programmes from the the past 7 days.  However, there are serious limitations you should be aware of:

- Most programmes should be available, but some will almost certainly be missing.  The data sources now in use cannot be considered to be as reliable as the previous data feeds.  
- Cache refreshes are noticeably slower than with the previous data feeds.  You may wish to acquaint yourself with the `--refresh-include` and `--refresh-exclude` options if you need to winnow your programme data cache.
- Some cache information may be missing or incorrect.  Further changes to get_iplayer may be necessary, but it is not possible to guarantee that the new data sources will contain the same information as the previous data feeds.
- Metadata fields such as episode and series numbers may be missing.  In the absence of the previous data feeds, this information may no longer be available.  Use caution if customising `--fileprefix` for your output files.  In particular, make sure that unexpected values of `<senum>` don't cause problems. The default value of `--fileprefix` contains `<pid>` in avoid to avoid collisions.
- No episode thumbnails are cached for radio programmes - they are no longer available.  Station logos are used as a substitute.  However, the episode thumbnail should be applied when a radio programme is downloaded.  You will only notice this if you use the Web PVR Manager. Some old episode thumbnails my remain in your cache for a few days until those entries expire.
- It is not possible to search for audiodescribed versions of TV programmes. You can still download audiodescribed versions, but you'll have to search for them on the iPlayer site to find the PIDs.  Signed versions of TV programmes should still be searchable, but check the iPlayer site if in doubt.
- It is not possible to search radio programmes by category (`--category` option). TV programmes still have category information, though it may be less complete than before.  If you have PVR searches that rely on category information, check them ASAP and adjust as necessary.  In general, it would be wise for you to stop using category information in searches.
- Radio programmes are tagged with only a top level category (e.g., Comedy or Drama).  Subcategories may return in the next release.

> Programmes can be downloaded via PID if they are not available in your search results.

## What happens when the BBC blows up get_iplayer again?

You should expect this to happen, and sooner rather than later.  If the new programme data sources are removed, do this:

    get_iplayer --prefs-add --refresh-feeds=schedule
    
    get_iplayer --refresh --type=tv,radio

and (hopefully) continue as normal.  This will switch get_iplayer to use different sources for programme data.  After the switch, searching will be even more limited:

- Some programmes from the past 7 days will almost certainly be missing.  This alternate data source should be reliable, but is limited compared the previous data feeds.
- Cache refreshes will be a **LOT** slower.  You will want to acquaint yourself with the `--refresh-include` and `--refresh-exclude` options if you need to winnow your programme data cache.
- Some cache information may be missing or incorrect.  Further changes to get_iplayer may be necessary, but it is not possible to guarantee that these alternate data sources will contain the same information as the previous data feeds.
- Metadata fields such as episode and series numbers may be missing.  In the absence of the previous data feeds, this information may no longer be available.  Use caution if customising `--fileprefix` for your output files. In particular, make sure that unexpected values of `<senum>` don't cause problems. The default value of `--fileprefix` contains `<pid>` in avoid to avoid collisions.
- It will not be possible to search for audiodescribed **OR** signed versions of TV programmes. You will still be able to download audiodescribed and signed versions, but you'll have to search for them on the iPlayer site to find the PIDs.
- It will not be possible to search radio **OR** TV programmes by category.  If you have PVR searches that rely on category information, you will need to check them ASAP and adjust as necessary.

**NOTE:** This fallback mechanism may be killed by the BBC before it can be used by get_iplayer, so there is no guarantee it will work when the time comes.


> Programmes can be downloaded via PID if they are not available in your search results.

## What happens when the BBC blows up get_iplayer yet again?

No idea. All the data sources now employed by get_iplayer to support programme searches are very likely to disappear in the near future. A number of different solutions have been proposed, but much work needs to be done.  It is likely that get_iplayer's search capabilities will be greatly reduced, or perhaps removed altogether in favour of a separate application.  There are further changes in store at the BBC which may kill get_iplayer completely, so only time will tell. 

If you have some contribution to make towards future solutions, subscribe to the get_iplayer mailing list and have your say: 

<http://lists.infradead.org/mailman/listinfo/get_iplayer>

## What about BBC podcasts?

get_iplayer's podcast indexing and search functions were never affected.  They work just as they always have.

## Other changes in get_iplayer 2.89

### Support for entering multiple PIDs for downloading with `--pid`

You can now enter multiple PIDs in two ways:

Comma-separated list

    get_iplayer --pid PID1,PID2,PID3

Multiple `--pid` options

    get_iplayer --pid PID1 --pid PID2 --pid PID3

Remember to include `--type=radio` with `--pid` when downloading radio programmes.

You can also do the same thing with episode page URLs:

    get_iplayer --url URL1,URL2,URL3

    get_iplayer --url URL1 --url URL2 --url URL3

Remember to include `--type=radio` with `--url` when downloading radio programmes.

Prefer `--pid` to `--url` where possible - it is slightly quicker and more reliable.  And no, you can't download multiple PIDs or multiple URLs with the Web PVR Manager.


## Other fixes in get_iplayer 2.89

- Fixed `"default" is not defined in %Encode::EXPORT_TAGS` error for Perl 5.10.0 and below
- Fixed `Malformed UTF-8 character error` generated after upgrading via self-update facility (`get_iplayer -u`)
- Fixed bad metadata tags created due to disappearance of data feeds.  However, some metadata fields may still be missing for some programmes.
- Fixed missing thumbnails for programmes < 7 days old downloaded via PID.  However, some thumbnails may still be missing for some programmes.
- Fixed live TV streaming broken by BBC removal of TV simulcast pages.  However, live streaming is unreliable at best, so it still may not work for you.


## Changelog

The full log of changes since v2.87 can be viewed here:

<https://github.com/get-iplayer/get_iplayer/compare/v2.87...v2.90>