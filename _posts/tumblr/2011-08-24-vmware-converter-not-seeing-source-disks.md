---
layout: post
title: vmware converter not seeing source disks
date: '2011-08-24T12:42:21+00:00'
tags:
- vmware
- p2v
- gotcha
tumblr_url: http://userdel.com/post/9343210435/vmware-converter-not-seeing-source-disks
---
If you have trouble with VMware Converter not seeing any disks for the source server try connecting to the source machine with a non-domain, local administrator account.  Also try running it as Administrator if it’s a 2008 server (right-click “Run as Administrator”).  This has happened to me a couple times recently and using the local admin account has worked each time.
