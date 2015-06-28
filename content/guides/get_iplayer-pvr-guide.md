+++
categories = ["", ""]
date = "2015-06-27T01:37:12+01:00"
description = "A beginners guide to the get_iplayer PVR function. A simple explanation of the PVR options are explained in this tutorial."
draft = true
pageimage = ""
pagesubtitle = "COMPREHENSIVE GUIDES TO GET YOU STARTED QUICKLY"
pagetitle = "get_iplayer Guides and Tutorials"
slug = "get_iplayer-pvr-guide"
title = "How to use get_iplayer PVR"
type = "page"

+++

# get_iPlayer PVR Guide

1. [How do I use the get_iplayer PVR function?](#how-do-i-use-the-get-iplayer-pvr-function)
1. [PVR controls](#pvr-controls)
1. [How do I add a PVR record to get_iplayer?](#how-do-i-add-a-pvr-record-to-get-iplayer)
1. [How do I list all PVR records in get_iplayer?](#how-do-i-list-all-pvr-records-in-get-iplayer)
1. [How do I remove or delete a PVR record from get_iplayer?](#how-do-i-remove-or-delete-a-pvr-record-from-get-iplayer)
1. [How do I run saved PVR searches in get_iplayer and automatically download programmes?](#how-do-i-run-saved-pvr-searches-in-get-iplayer-and-automatically-download-programmes)
1. [How do I edit PVR records that I have already created in get_iplayer?](#how-do-i-edit-pvr-records-that-i-have-already-created-in-get-iplayer)

## How do I use the get_iplayer PVR function?

This is a quick guide to the get_iplayer PVR functionality. It'll get you using the function in a couple minutes, but you'll want to make sure you've read the rest of this guide and viewed the examples at the bottom of the guide.

Doing so will make sure you build a well formed and accurate command that will download files where you want, rename them as required and can be set to run without further input from you.

Using the PVR function can be boiled down to the following commands:

### PVR controls

Add PVR

    get_iplayer --pvr-add=PVR_Name

List all PVR

    get_iplayer --pvr-list

Remove PVR

    get_iplayer --pvr-del="name of PVR from list"

Disable PVR

    get_iplayer --pvr-disable="name of PVR from list"

Re-enable PVR

    get_iplayer --pvr-enable="name of PVR from list"

Run PVR

    get_iplayer --pvr

<a name="How_do_I_add_a_PVR_record_to_get_iplayer?"></a>

## How do I add a PVR record to get_iplayer?

To add a PVR record we need to 'build' it up just like we have in the previous examples.

Taking all the above commands together to build up our desired search, quality setting, channel, filename and output folder, we just add the PVR command to turn it into a PVR which you can run automatically.

This makes more sense when written:

    get_iplayer --pvr-add=PVR_Name "search string goes here" --tvmode=best --type=tv --channel="Channel goes here" --file-prefix="<nameshort>-<senum>-<episodeshort>" --output "/path/to/output/polder/goes/here/"

MAKE SURE YOU DON'T LEAVE SPACES IN THE PVR NAME, USE AN UNDERSCORE!

The above code is totally generic. You can change the name of the PVR to suit you, but each 'new' name you give saves a new PVR record.

I'll show you how to list and remove extraneous PVR recordings shortly. So, to change the name of our PVR to match our search string we could write something like:

    get_iplayer --pvr-add=Top_Gear "Top Gear" --tvmode=best --type=tv --channel="BBC Two" --file-prefix="<nameshort>-<senum>-<episodeshort>" --output "/media/TV Shows 1/2 - TV Shows/Top Gear/Season 19"

The above code will add a PVR record for Top_Gear, attempt to download the programme in HD (followed by high quality flash streams - don't worry it'll output as an MP4 automatically for compatibility), make sure that the programme is a TV show, makes sure that the channel the programme is available from is BBC Two, renames the file to match the Plex/XBMC naming conventions and outputs the file to the folder "path/to/Top Gear Folder".

## How do I list all PVR records in get_iplayer?

It's easy to list all the saved PVR records you have created. Just use the following command:

    get_iplayer --pvr-list

For me this outputs:

![get_iplayer-_PVR-List-Output_-example](/img/2015/06/get_iplayer-_PVR-List-Output_-example1.png)

## How do I remove or delete a PVR record from get_iplayer?

From the list of PVR records we see above, you can easily see the names of all your PVR records, which we will need to be able to remove them using the Command Line Interface.

I'll show you how to remove them in the File Manager shortly - or skip to the bottom of the [How do I edit PVR records that I have already created in get_iplayer?](#how-do-i-edit-pvr-records-that-i-have-already-created-in-get-iplayer) section to see how right now. To remove a PVR record, simply add the PVR records name to the 'Remove PVR' command like this:

    get_iplayer --pvr-del="name of PVR from list"

To remove the "Top_Gear" PVR record from the list above, I'd simply use this code:

    get_iplayer --pvr-del=Top_Gear

It's as easy as that. Run that command with the exact name of the PVR record in place of "name of PVR from list" and it will be removed immediately.

It wont give you any confirmation of the removal (it'll look like nothing has happened) but if you re-list your PVR records you will see that the one you specified has been removed.

## How do I run saved PVR searches in get_iplayer and automatically download programmes?

This one is probably the easiest command of all. It simply this:

    get_iplayer --pvr

That's it.

Once you execute that command, get_iplayer will update the list of available programmes and start performing automatic searches and downloads based on the saved PVR records you have created.

It'll output to the directories/folders you specified and rename the files as you instructed, all without any extra input from you.

Easy as pie!

## How do I edit PVR records that I have already created in get_iplayer?

There are two ways to edit a PVR record you have already created. The first is to create another PVR record with the exact same name as the one you want to edit.

This will completely overwrite the old PVR record with the new one you create. This is useful if you only have one or two PVR records to edit. If you are unsure how to create a new PVR record, jump up to the [How do I add a PVR record to get_iplayer?](#how-do-i-add-a-pvr-record-to-get-iplayer) section.

### The following info is relevant to Linux Ubuntu

The second method is to navigate to the hidden PVR directory, where the actual text files storing the PVR records are kept on your hard drive, and edit those files.

Whilst this sounds trickier, it's actually easier for editing a large number of files (to change their output folder/directory if you now need get_iplayer to download them to a different folder for example).

The PVR directory is located in a hidden file inside you 'Home' folder. To navigate to it using the file explorer/manager, open up a new file explorer window and click on 'Home' in the sidebar. To see hidden files you can simply press the "ctrl+h" buttons on your keyboard.

![get_iplayer-_Home-folder_-example](/img/2015/06/get_iplayer-_Home-folder_-example1.png)

**HINT** - you can also reveal hidden files using the menu located right up on the top bar at the top of the screen, but it's slower and harder to find so just use the keyboard shortcut. The file explorer window will fill up with lots of previously unseen folders, all preceded with a full-stop. You need to find and click on the ".get_iplayer" folder, outlined in the screenshot below:

![get_iplayer-_Home-folder-with-hidden-files_-example](/img/2015/06/get_iplayer-_Home-folder-with-hidden-files_-example1.png)

Inside the .get_iplayer folder, you'll find a folder called "PVR".

![get_iplayer-_PVR-folder-highlighted_-example](/img/2015/06/get_iplayer-_PVR-folder-highlighted_-example1.png)

Open this up and you'll find a series of text files. These are the saved information from the PVR records you created through the Command Line Interface.

![get_iplayer-_PVR-records_-example](/img/2015/06/get_iplayer-_PVR-records_-example1.png)

Simply double click on the file you need to edit and it will be opened in a text editor. You can make changes to the record and then hit "Save" to save those changes.

![get_iplayer-_PVR-Record-being-edited_-example](/img/2015/06/get_iplayer-_PVR-Record-being-edited_-example1.png)

That's it, simple as that.

If you make a mistake and corrupt the file, just delete it and recreate the record through the Command Line Interface with the updated info you needed.

**NOTE** - You can use this method to delete, en masse, PVR records that you no longer require. Delete the records from this folder and the PVR searches will no longer run when you execute the "Run PVR" command.
