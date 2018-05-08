+++
categories = ["", ""]
date = "2015-07-09T22:11:38+01:00"
description = "A quick installation guide to get get_iplayer installed on your Mac in just a few minutes."
draft = false
pageimage = ""
pagesubtitle = "COMPREHENSIVE GUIDES TO GET YOU STARTED QUICKLY"
pagetitle = "get_iplayer installation guides"
slug = "mac-os-x"
title = "macOS Quick Install Guide • get_iplayer"
Type = "downloads"
breadcrumb = "get_iplayer macOS Quick Install Guide"
+++

# macOS Quick Install Guide

**NOTE: Only macOS 10.10 (Yosemite) or higher is supported for get_iplayer. Users of earlier releases may attempt a manual installation of get_iplayer, but it is unsupported and get_iplayer may fail. See the "More Info?" section below for a link to instructions for manual installation.**

## Install with Homebrew

**NOTE 1:** macOS 10.10 (Yosemite) or higher is required to install get_iplayer with Homebrew.

**NOTE 2:** The get_iplayer Homebrew package is not supported by the get_iplayer developers, nor is it supported in the forums. If you encounter any problems installing or running get_iplayer from this package, [report them to Homebrew](https://discourse.brew.sh). If you encounter problems actually downloading programmes, use the [forums](/forums/).

Homebrew is a package management solution for macOS. It's very easy to install, just go to the [Homebrew website](http://brew.sh/) and copy and paste the one line installation code into your terminal window. 

Once you've installed Homebrew, it's just one more line to install get_iplayer:

    brew install get_iplayer

### Upgrade to future releases with:

    brew update
    brew upgrade get_iplayer
     
### Get started by reading the guides and release notes

There is loads of info in the [guides](/guides/) section to get you downloading programmes in a snap. Make sure you read the whole guide to understand what's happening and why you need to do things a certain way.

Find the [release notes](https://github.com/get-iplayer/get_iplayer/wiki/releasenotes) in the wiki. Read at least the notes for the latest release. Things can change quite a lot between releases and you'll find explanations there as to why get_iplayer is working the way it is. 

#### Web PVR Manager

Start the Web PVR Manager from your terminal window with:

    get_iplayer.cgi --listen 127.0.0.1 --port 1935

Connect to the Web PVR Manager by opening the URL below in your web browser:

<http://127.0.0.1:1935>
    
## More info?

You can take a look at the [macOS installation page](https://github.com/get-iplayer/get_iplayer/wiki/osx/) in the wiki for a bit more info and for instructions on performing a manual installation. 

## Stuck?

Post in the [forums](/forums/) and we'll help you out. Make sure to read up on [how to submit an acceptable support request](/forums/thread-706.html) first. 
