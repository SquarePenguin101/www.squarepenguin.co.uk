+++
categories = ["Maintenance"]
date = "2014-09-14T22:59:16+01:00"
description = "get_iplayer Forums at squarepenguin.co.uk now enforces full-site encryption via https (ssl), including support for Perfect Forward Secrecy."
draft = false
pageimage = ""
slug = "squarepenguin-co-uk-now-enforces-full-site-https"
title = "squarepenguin.co.uk now enforces full-site https"

+++

<img style="float:right;" src="/img/2015/06/padlock-icon.png" alt="padlock-icon" width="350" height="350" />

It's taken [slightly less time than reddit](http://www.redditblog.com/2014/09/hell-its-about-time-reddit-now-supports.html) but still over a year since I first wanted to implement SSL here at get_iplayer Forums and today I'm happy to say the deed is finally done!

From today all connections to both the front end and user admin areas will be encrypted. You'll see the padlock icon in your address bar (except for ie6, in which case you'll probably see nothing and won't even be able to read this!) and you can view squarepenguin.co.uk's SSL report here: 

[https://www.ssllabs.com/ssltest/analyze.html?d=squarepenguin.co.uk](https://www.ssllabs.com/ssltest/analyze.html?d=squarepenguin.co.uk)

This is a vast improvement in security, particularly for user passwords during the log in process, and the implementation of support for [PFS](https://www.eff.org/deeplinks/2013/08/pushing-perfect-forward-secrecy-important-web-privacy-protection) should mean that in the unlikely even of a breach an attacker won't be able to decrypt all previous sessions.

As ever, my recommendation is that you use unique 25+ character passwords using case-sensitive letters, numbers and special characters for EVERY single site you use. If that sounds like too much hard work, get a password manager and let [Lastpass](https://lastpass.com/), [Dashlane](https://www.dashlane.com/en), [Roboform](http://www.roboform.com/) or [KeePass](http://keepass.info/) do the work for you.

I've been testing the site for a short while before it went live but with any new feature and a switch to a new IP address there exists the possibility of unexpected behaviour and unforeseen problems. The current configuration will likely be updated to respond to server/visitor behaviour so I ask that if you notice anything wrong or experience a problem please let me know via the contact form link in the site footer.
<!--more-->
