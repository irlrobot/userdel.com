---
layout: post
title: scan for new disks in linux
date: '2011-04-27T10:43:00+00:00'
tags:
- linux
- vm
tumblr_url: http://userdel.com/post/4988100795/scan-for-new-disks-in-linux
---
If you add a new disk hot to a Linux machine (e.g. a new virtual disk on a VM) and it doesn’t show up you can use the below command as root to scan for new disks:

echo "- - -" > /sys/class/scsi_host/host0/scan
If you get an invalid argument error try typing it in manually instead of pasting the above in.
