---
layout: post
title: using fim2010 with live@edu or outlook live
date: '2011-09-01T11:51:00+00:00'
tags:
- fim
- fml
- live@edu
- timeillnevergetback
- fim 2010
- idm
- identity management
tumblr_url: http://userdel.com/post/9673418965/using-fim2010-with-liveedu-or-outlook-live
---
So the documentation for using Forefront Identity Manager 2010 with Live@Edu/OutlookLive is pretty much non-existent right now.  I was told that though it’s an officially supported configuration the documentation is still a couple months out from being published.  So if you want to get this setup without a consultant you face an uphill battle.  It took me a few days of running into issue after issue, but finally I got it all working.  Here are my notes on getting a successful install completed.  Hopefully it will help someone:
Request 64bit GALSync.msi      from MS Support.  This is important,      make sure you get the right one from support.
Install FIM Sync Service like      normal on Windows 2008 R2. (this could be a guide on it’s own sorry)
Update FIM via Windows      Update.  Make sure to click      “Update other MS Products” link to get FIM updates.
On Sync Server install hotfix      : The hotfix is http://support.microsoft.com/kb/2272389 and the file name should be      FIMSyncService_x64_KB2272389.
On Sync Server install      GALSync.msi, installer should say “Outlook Live Management      Agent”.  If installer fails to      complete, reboot, remove it if it shows up Add/Remove programs, and try      again.
Create UPN Suffix for same      domain that Live@Edu will use if it is not currently the same in your      domain.
Create an OLSync account in      domain (give it above UPN Suffix) and Live@Edu.
In the      Live@Edu Management Console, create a new role and add OLSync account to it so you can use this account as your service account for syncing between on-prem and hosted.  Alternatively you can follow these instructions.  
Users and Groups
Outlook Live Control Panel
Roles & Auditing
New Role
Name it something like “OLSync Role”
Under Roles click add and choose “GalSynchronizationManagement”
Under Memebers click add and choose your OLSync Account
Save

Go here and start at Step 6: http://help.outlook.com/en-us/140/Dd490636.aspx
After Step 7 in the above link don’t forget to      populate your OU’s with a couple test users if they are empty and be sure      to set an email address for the users as well (otherwise sync will error      out).
