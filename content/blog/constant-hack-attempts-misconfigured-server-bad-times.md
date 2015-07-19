+++
categories = ["Announcements"]
date = "2013-08-19T16:45:54+01:00"
description = "Square Penguin was knocked offline yesterday for a period of 18 hours or so. That is a crazy amount of time for any site to go down, even a small one like this."
draft = false
pageimage = "/img/2015/06/wisdom_of_the_ancients.png"
aliases = "/constant-hack-attempts-misconfigured-server-bad-times"
title = "Constant hack attempts + Misconfigured server = bad times"
+++

<a href="http://xkcd.com/979/"><figure><img style="float:right;" alt="XKCD_wisdom_of_the_ancients" src="/img/2015/06/wisdom_of_the_ancients.png" width="485" height="270" /></figure></a>

Square Penguin was knocked offline yesterday for a period of 18 hours or so. That is a crazy amount of time for any site to go down, even a small one like this.

Running Wordpress always attracts a continual stream of attempted brute force login attempts along with the occasional SQL injection attack or even something a little more troublesome. As a result, I've got some measures in place to prevent intrusions and these have been working as expected.

<!--more-->I also make use of a Varnish caching server that sits in front of the web server to speed up the delivery of pages to visitors. Sometime early yesterday afternoon, something changed in that server configuration and the originating IP addresses of all visitors were no longer getting forwarded. As a result, every visit appeared to be coming from my Varnish Server.

One of the security measures in place seeks to ban bots and attackers based on their site activity and uses their IP address to implement that ban. With all IP addresses suddenly coming from my own server, it was moments before the number of hack attempts tripped the automated intrusion detection and locked out the IP. Alterations to this policy have been put in place to prevent such an eventuality occurring again, and to prevent potential abuse.

Long story short, this took the site offline entirely and I didn't receive notification from my monitoring service. It was not until I visited the site that I discovered the problem.

The misconfigured server has now been fixed, an improved monitoring process from another provider has been put in place to ensure I receive immediate notification of future downtime (tested to be functioning correctly) and Square Penguin now sits behind the vast resources and protection offered by Cloudflare, which I was previously running in CDN only mode.

Some visitors may experience 5 seconds of security vetting on their first visit to the site but between this and other measures future downtimes should be measured in minutes, not hours. This may be a 'hobby' site, but that doesn't mean I find it acceptable that it experienced such a large period of downtime and I apologise for the inconvenience any visitors faced due to the downtime.

SP
