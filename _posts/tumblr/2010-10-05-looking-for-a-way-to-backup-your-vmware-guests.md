---
layout: post
title: looking for a way to backup your vmware guests?
date: '2010-10-05T11:20:00+00:00'
tags:
- vmware
- backups
tumblr_url: http://userdel.com/post/1250108967/looking-for-a-way-to-backup-your-vmware-guests
---
looking for a way to backup your vmware guests?I’ve been using PHD Virtual Backup for VMWare (formerly esXpress) for almost a year now to backup my VMs (80+ across 8 ESX boxes) and it’s pretty great.  Point it to any CIFS or NFS share and it will do deduplicated backups using small virtual appliances.  You can also do file level recovery for Windows or Linux VMs without any kind of proxy (VCB or otherwise), and full restores quickly.  Replication?  Yep it can do that too and it’s not an extra license you need to buy.  Did I mention it’s very affordable?
