---
layout: post
title: how to fsck
date: '2011-01-19T17:56:00+00:00'
tags:
- fsck
- linux
tumblr_url: http://userdel.com/post/2834972490/how-to-fsck
---
Someone asked me today how you properly fsck a Linux ext3 partition, so I figured it might be worth posting for others.
Run a backup and/or verify your last backup.  This is the most important step.  Whenever you are doing anything that can alter your file system you always want to assume the worst.
Stop or close any services or processes that are using the partition.  Use lsof or fuser to see what might be using it.
Unmount the partition.  Do not fsck while it’s mounted.  If need be reboot and make sure it doesn’t get mounted during boot.
Finally run “fsck -C -V -y /dev/disk” where disk is the drive and partition number you want to run the file system check on.  For example, “fsck -C -V -y /dev/sdb1” would be for /dev/sdb1.  The -C option gives you a handy progress bar, the -V option is for verbose, and the -y option will accept all changes so you don’t have to hit the enter key a hundred times if you have a lot of errors.
When the fsck completes you can mount the partition again and verify all your data is intact.
