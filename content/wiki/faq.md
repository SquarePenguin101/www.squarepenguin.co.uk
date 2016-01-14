## get_iplayer FAQ

<a name="faq1"></a>
**FAQ 1: I see a programme that is available on the iPlayer web site, but I can't find it with a get_iplayer search.  What's wrong?**

First ascertain: 

1. If you're looking for a radio programme, did you use `--type=radio` in your get_iplayer command? 

2. Are you searching for a TV programme with audio description or signing? That functionality is no longer available in get_iplayer, though you can still use `--versions=audiodescribed` or `--versions=signed` when downloading to select the desired version (if available).

3. Are you searching for programmes by category (`--category=...`)? That functionality is no longer available in get_iplayer, though category information is still included in the metadata added to programmes after download.

4. Was the programme actually broadcast on a BBC channel within the last 7 days?  If so, feel free to post a query with the relevant information in the [squarepenguin.co.uk forums](https://squarepenguin.co.uk/all-forums/).  In the likely event that it was **NOT** actually broadcast on a BBC channel within the last 7 days, read on.

In early October 2014, the BBC made some changes to the iPlayer service and web site that affected get_iplayer.  This is what you need to know:

- If a programme you're looking for does not appear in get_iplayer search results, check it on the iPlayer or iPlayer Radio site **BEFORE** reporting it as an error.
- Web-only and red button programmes are **NOT** available for indexing by get_iplayer and therefore will **NOT** appear in search results. Only programmes scheduled for broadcast on a BBC channel will be indexed.
- Programmes broadcast more than 7 days ago generally are **NOT** available for indexing by get_iplayer and therefore will **NOT** appear in search results.  
- It **DOES NOT MATTER** that a programme is still available on the iPlayer site up to its 30-day expiry.  Once 7 days pass from its last broadcast, it is generally no longer available for indexing by get_iplayer.
- There are a few exceptions to the 7-day rule, such as series like Doctor Who that have a full series catch-up policy. The episodes of those series remain available until the final episode reaches its expiry date.  But again, once 7 days pass from the broadcast of the final episode you should expect those episodes to disappear from the get_iplayer search results. 
- From get_iplayer 2.94, some TV programmes > 7 days old and < 14 days old may also appear in search results due to changes in indexing.
- You **MUST** download **ANY** other programme not found in search results directly via PID or URL. If you don't know what that means, it's time to refresh yourself [here](documentation#recording).
- get_iplayer 2.87 or higher is **REQUIRED** to download programmes more than 7 days old via PID or URL.  If you're using your own hacked version of get_iplayer, you'll need to do some more hacking.
- When in doubt, use the programme PID.  All available programmes can be downloaded via PID regardless of whether or not they are in the get_iplayer cache.
    
        TV: get_iplayer --pid=<PID> ...
        
        Radio: get_iplayer --pid=<PID> --type=radio ...
    
