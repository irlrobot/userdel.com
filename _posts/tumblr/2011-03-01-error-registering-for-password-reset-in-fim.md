---
layout: post
title: error registering for password reset in fim
date: '2011-03-01T08:30:00+00:00'
tags:
- bleh
- fim
- fim 2010
- idm
- identity management
tumblr_url: http://userdel.com/post/3583492351/error-registering-for-password-reset-in-fim
---
If you are just getting password reset implemented with FIM 2010 and your client gets "An error was encountered.  Please call helpdesk or your system administrator for further assistance.“ try the following:
Download the PSTools bundle from http://technet.microsoft.com/en-us/sysinternals/bb897553.aspx
Extract PsExec.exe to your C:\ drive
Open a command prompt as administrator and enter "cd c:"
Now enter "psexec.exe -s -d -i cmd.exe”
A new command prompt window should open.  Now enter “mmc.exe”.
Go to File -> Add/Remove Snap-ins
Select Certificates on the left and click the “Add >” button in the middle
Select “Computer Account” from the window that pops up, then Next, and then select “Local computer” and hit Finish
Hit Ok and you should be taken to the MMC window
Expand Certificates on the left, then expand Personal, and finally click on Certificates under Personal
Right click on the “ForefrontIdentityManager” certificate and choose “All tasks” then “Manage Private Keys…”
Click add and enter the name of the account running as the service account for the FIM Service
Make sure “Read” is checked under Allow and hit OK
This apparently is a known bug with build 4.0.2592.0 (current version as of this writing).  Supposedly it will be fixed in Update 1 which does not have a street date just yet.
