---
layout: post
title: quick and easy fim r2 upgrade guide
date: '2012-08-08T11:38:45+00:00'
tags:
- fim
- fim 2010
- upgrade
- microsoft
- idm
- identity management
tumblr_url: http://userdel.com/post/28993717244/quick-and-easy-fim-r2-upgrade-guide
---
As I pointed out in my last post, Microsoft has some conflicting documentation on TechNet.  Here is a quick guide that should get you a safe upgrade:
Backup everything.  Databases, configs, and bare metal/complete backup of your servers/VMs just incase.  (Side note: Checkout PHD Virtual for good, cheap VMware backup software).
Make sure you are on build 3606 at the very least on both your FIM Service and Synchronization Server.
One of the TechNet guides recommends setting the Recovery type on both databases to Simple so go ahead and do that if they aren’t already.  You can skip this step if you know what you’re doing and want Full on the FIMService database.
Upgrade your Synchronization Server.
Download SharePoint 2010 Foundation, launch it, install Pre-Req’s, and then install it on your Portal Server.
Run the following query on the FIMService database to enable the SQL Broker which is required for the upgrade.  "alter database FIMService set enable_broker with rollback immediate;“
Upgrade your Service and Portal Server.
