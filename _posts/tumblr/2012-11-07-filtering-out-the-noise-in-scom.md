---
layout: post
title: filtering out the noise in scom
date: '2012-11-07T07:32:22+00:00'
tags:
- bleh
- microsoft
- scom
tumblr_url: http://userdel.com/post/35204383637/filtering-out-the-noise-in-scom
---
I’ve decided to tackle SCOM 2012 at my new employer.  It was installed by a previous SysAdmin but basically left out of the box with ALL alerts on EVERYTHING constantly spamming the inboxes of the rest of the team.  I am very sick of these emails.
SCOM is interesting in that by default you really do get alerts for everything.  Even stupid crap you don’t care about like an occasional spike in CPU usage or some service configured with the SYSTEM account or disk latency warnings in the middle of the night during backups.  I have zero experience with SCOM but I can already tell you this is going to be one hell of a love/hate relationship.  I found one article that has already GREATLY helped in reducing the amount of notifications.
SCOM has three severity levels for the alerts included in Management Packs: Information, Warning, and Critical.  It also has three priority levels:  Low, Medium, and High.  Each alert is assigned a priority level and most alerts, unless they are REALLY bad, are assigned medium out of the box in MP’s.  Stuff like a system down though will have be a Critical/High alert by default.  What you can do is create a subscription for only High priority Critical alerts and this will right away reduce the noise from SCOM.  You can then use the SCOM console to see all alerts and tweak individual alerts by adding an override to change the priority to High if it’s something you want to be notified on.  More to come as I play around with SCOM more but make sure you check out the article by Kevin Holman to get started.
