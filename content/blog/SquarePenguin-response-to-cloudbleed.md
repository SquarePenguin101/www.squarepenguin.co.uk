+++
breadcrumb = ""
pageimage = ""
title = "SquarePenguin's response to CloudBleed"
categories = ["Maintenance",""]
draft = false
pagetitle = "get_iplayer Formus blog"
slug = "squarepenguin-response-to-cloudbleed"
date = "2017-02-24T17:05:08Z"
description = ""
pagesubtitle = "NOTICES | ANNOUNCEMENTS | UPDATES"

+++

Last night [Cloudflare](https://blog.cloudflare.com/incident-report-on-memory-leak-caused-by-cloudflare-parser-bug/) and [Google's 'Project Zero'](https://bugs.chromium.org/p/project-zero/issues/detail?id=1139) security team published details of a serious security incident affecting websites that use the 'reverse proxy' feature of Cloudflare. 

squarepenguin.co.uk uses this reverse proxy feature and **WAS** *potentially* affected to a **LIMITED** extent. 

Cloudflare has contacted me to confirm that squarepenguin.co.uk was not amongst the core of domains severely affected, but that does not preclude leaking of data from this site in less likely ways as ALL cloudflare sites were *potentially* affected. 

Despite the extraordinarily low probability of a leak I have taken the following action to mitigate any possible leak:

1. Invalidated all current session cookies forcing all visitors to re-login. 
2. Forcing all users to change their passwords at next login (sorry, must be done!)
3. Changed the 'secrets' used to protect the admin area of the site
4. Reassessed Cloudflare usage and removed unneeded features
5. Written this notice explaining the situation to all squarepenguin.co.uk users.

<!--more-->
## When might data have leaked?

Users who logged in to their accounts between 13/02/2017 and 18/02/2017 are potentially most affected. If you didn't log in but visited the site during this time less sensitive data (such as your IP address) may have been exposed. 

## What data might have been leaked?

1. session cookies (including authorization tokens permitting login)
2. User IP addresses
3. User email addresses
4. Passwords

### Umm...passwords?

It's possible (though incredibly, astronomically unlikely) that passwords for some users who logged in during the times above were exposed by Cloudflare's bug and potentially cached on the public internt for a short time.

What else I know:

There has been no server breach. squarepenguin.co.uk has not been hacked. Databases have not been stolen, plain text passwords have not been taken and they aren't stored in plain text in any case.

myBB encrypts user passwords using the MD5 hashing algorithm paired with a unique randomly generated 'salt'. MD5 is a weak hashing algorithm vulnerable to brute force attacks, even with the addition of a salt, but it's what's available when using this forum software. 

But when logging in it's necessary to transmit your password for hashing and comparison with the value stored in the database. It's possible that users who logged in since 13/02/2017 until 18/02/2017 had their passwords put at risk of exposure upon requesting login. 

The exact nature of the leak means that no actual hack took place and encrypted passwords were not stolen but there was the potential for the plaini text password to be caputure by Cloudflare, erroneously written to an HTML page and then to be made accessible to the public internet for a limited time. 

Full details of the mechanism of the leak are at the links in the first paragraph of this post and below.

Potential exposure of a plain text password is a catastrophic possibility and there will be no 'playing down' of this fact. This is why I'm forcing password changes and recommending the following:

#### Out of an abundance of caution - if you reuse your squarepenguin password on any other site and you logged into squarepenguin.co.uk between 13/02/2017 and 18/02/2017 you should change it on that site too. 

A little perspective:

I would like to reiterate in my defence here that at no point was squarepenguin.co.uk insecure or breached and the issue lay with a third party partner - but that doesn't change the fact that your password *could* have been exposed, no matter how unimaginably small that chance was, or who is to 'blame'.

I take the security of this site very seriously. 

I will reiterate the chances of any user here having their password exposed is vanishingly small **particularly as squarepenguin.co.uk is now known to not be amongst the core of affected sites**.

But, at the scale of the internet the chance for the vanishingly small to actually occur is always a possibility. 

So I am acting out of an abundance of caution and with due respect to the wider scale of this breach which affects *millions* of site that sit behind Cloudflare's reverse proxy feature. 

## OK, so what actually happened?

For non-technical users the original incident reports can be overwhelming so here is a very brief breakdown of what happened...

### How the reverse proxy works

Sites using the 'reverse proxy' feature of Cloudflare sit 'within' Cloudflare's network. 

Requests made to view a page on a site using this feature actually reach the edge of Cloudflare's network where they are 'terminated'. Then Cloudflare itself makes another request back to the 'origin' server for that site (i.e the one where this site actually runs), gets the page the user requested and then serves it back to them.

### Why would you use this setup?

By 'terminating' connections at the edge of Cloudflare's network, users never 'see' the origin server for a website. This allows Cloudflare to offer DDoS protection services by swallowing/rerouting attacks away from origin servers. 

It also allow other features like caching resources (CSS, JavaScript, photos, files etc) at the edge of Cloudflare's network. This means when a user makes a request for a page from a site, Cloudflare can simply serve back a cached version to the user. 

Because these caches sit at the edges of Cloudflare's network, and Cloudflare's network have over 80 points of presence (PoP's) around the world, it speeds up delivery of pages to users wherever they are in the world by serving resources from the cache physically closes to them, vastly improving loading speed and user experience. 

Cloudlfare offers other advanced features alongside simple caching. It also allows site admins to rewrite the HTML portion of webpages served back to visitors. 

This allows things like minification, email address obfuscation, hotlink protection and lot of other useful features without admins having to implement these features themselves (particularly useful in circumstances where it's not possible to implement them due to various constraints).  

Indeed, for a largely static site like squarepenguin.co.uk it can be a very simple and powerful way of adding functionality. 

## What went wrong?

Three advanced features Cloudflare offered contained a bug that, in certain circumstances, caused data to be written into the cached HTML pages when performing legitimate alterations (like obfuscating email addresses) which should not have been there. 

Squarepenguin.co.uk used the 'email address obfuscation' feature and was affected by the bug associated with it during the period 13/02/2017 - 18/02/2017. 

Data written into the cached pages could, depending on the way the site the data came from worked, contain:

- passwords
- private API keys
- Authorization tokens
- session cookies
- header data including users IP address
- chunks of POST data (like comments/messages even from 'private' areas of a chat/dating site for example)
- frames of videos 

You get the picture. This alone would be a big deal. 

## What worsened the impact of this bug?

In itself this bug was a big deal. What made it even more so was the 'persistence' of the leaked data. 

Because the leaked data was being injected into HTML of web pages and served on the public internet, services that index that public data picked it up and saved it to their own caches. 

Internet giants like Google, Bing, Yandex, Baidu and untold numbers of other caching/search services began to cache their own versions of these web pages contining the leaks. Caching is a mainstay of the internet, it's vital for making is fast and useable so this is expected behaviour. 

When Cloudflare was notified of the bug though, this external caching meant it couldn't simply fix the issue and carry on. Instead it had to try to ensure that each and every one of the services that cached the leaked data was notified and that they removed that data. 

This is an impossible task - regardless of the 24 hour a day week long herculean response Cloudflare engineers undertook to address this bug. For instance, despite assurances that data had been removed, I personally found leaked API keys and oAuth bearer tokens (as bad as passwords) publically searchable in Google's cache well after claims were made that it was removed. 

That data has been reported and removed but whilst most reputable public caches have now cleared the leaked data it's not possible to verify that *all* caches have done so. Many smaller private caches and those run by nation states (think NSA et al) may not have cleared this data and this leaves open the possibility of abuse. 

## What should I do?

Change your password here (you'll be forced to do so at next login anyway) and if you use the password here on other sites, go and change it there too. 

There is no evidence that any password here has been breached at all, but it is prudent to take this action as the *possibility* that it *could* have been exposed is impossible to confirm as zero. 



