## get_iplayer FAQ

<a name="faq1"></a>
**FAQ 1: I see a programme that is available on the iPlayer web site, but I can't find it with a get_iplayer search.  What's wrong?**

First ascertain: 

1. If you're looking for a radio programme, did you use `--type=radio` in your get_iplayer command? 

2. If you're looking for a TV programme with audio description, did you use `--versions=audiodescribed` in your get_iplayer command? 

3. If you're looking for a TV programme that is signed, did you use `--versions=signed` in your get_iplayer command? 

4. Was the programme last broadcast within the last 7 days?  If so, feel free to post a query with the relevant information in the [squarepenguin.co.uk forums](https://squarepenguin.co.uk/all-forums/).  In the likely event that it was **NOT** broadcast within the last 7 days, read on.

In early October 2014, the BBC made some changes to the iPlayer service and web site that affected get_iplayer.  This is what you need to know:

- Programmes more than 7 days old are **NOT** available for caching by get_iplayer and therefore will **NOT** appear in search results.  
- It **DOES NOT MATTER** that a programme is still available on the iPlayer site up to its 30-day expiry.  Once 7 days pass from its last broadcast, it is no longer available for caching by get_iplayer.
- You **MUST** download programmes more than 7 days old directly via PID or URL.  If you don't know what that means, it's time to refresh yourself [here](/wiki/documentation#recording).
- get_iplayer 2.87 or higher is **REQUIRED** to download programmes more than 7 days old via PID or URL.  If you're using your own hacked version of get_iplayer, you'll need to do some more hacking.
- There are a few exceptions to the 7-day rule, such as series like Doctor Who that have a full series catch-up policy.  The episodes of those series remain available until the final episode reaches its expiry date.  But again, once 7 days pass from the broadcast of the final episode you should expect those episodes to disappear from the get_iplayer cache.
- If a programme you're looking for does not appear in get_iplayer search results, check it on the iPlayer site **BEFORE** reporting it as an error.  If the programme is more than 7 days old (or its availability is shown as less than 23 days), you must download it directly via PID or URL.
- When in doubt, use the programme PID.  All available programmes can be downloaded via PID regardless of whether or not they are in the get_iplayer cache.
    
        TV: get_iplayer --pid=<PID> ...
        
        Radio: get_iplayer --pid=<PID> --type=radio ...
    