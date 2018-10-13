---
layout: post
title: install dell open manage system administrator on esx
date: '2011-02-11T12:46:00+00:00'
tags:
- omsa
- dell
- esx
- vmware
tumblr_url: http://userdel.com/post/3238207219/install-dell-open-manage-system-administrator-on
---
For some reason every time I try to install OMSA from the Dell disc before an ESX install it hangs or fails or never even starts, so I always have to install OMSA after the fact manually.  Here’s the steps if you run into the same trouble:
Download the newest OMSA package for Linux.  As of this writing you can get it here - this is version 6.4.  You should be able to poke around dell.com or google for it though to get the latest version though.
Transfer it to your ESX box via scp (WinSCP if you use Windows).  Make sure you create yourself a local account first on the ESX server.
Move the .tar.gz file to a new directory named “omsa” in /tmp (“mkdir /tmp/omsa”) on the ESX host.
Unpack it with “tar xvfz OM-blahblahblah.tar.gz” inside /tmp/omsa.
As root run “./setup.sh” - this script should have been unpacked in the directory with the last command.
Jump through the hoops and choose to install all components (option 7 as of this writing).
Choose to start the service now.
As root run “esxcfg-firewall -o 1311,tcp,in,OpenManageRequest” to open port 1311 through the firewall so you can actually get to the web interface.
Verify install by going to https://servernameORipaddress:1311.
Cleanup your mess in /tmp (“rm -rvf /tmp/omsa”).
