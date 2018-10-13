---
layout: post
title: do not use lockdown mode in vmware
date: '2012-05-24T05:20:00+00:00'
tags:
- arrrrgggg
- vmware
- wtf
- stupid
tumblr_url: http://userdel.com/post/23668191614/do-not-use-lockdown-mode-in-vmware
---
PSA: Do not use Lockdown Mode on your ESXi servers.  Yesterday I ran into a major headache.  One of my ESXi 5 hosts went down and it happened to the be hosting my Virtual Center VM.  My Host Isolation Response is set to Shutdown which should have gracefully powered off my Virtual Center server and started it up another host.  Except that it didn’t; it stayed powered off.  Being the security minded SysAdmin that I am, I had Lockdown Mode enabled on all my hosts.  Huge Mistake.
If Lockdown Mode is enabled you literally cannot manage the host at all unless it’s through the vSphere Client connected to your Virtual Center server.  Literally.  Like not even through the console via KVM, DRAC, iLO, etc.  So you can have physical access to the ESXi server but you absolutely cannot disable Lockdown Mode or interact with the host in anyway that would allow you to get your server back up.  Unbelievable.
After calling into support and confirming this their solution was to install a new ESXi server, connect it to my storage, and cold migrate the vCenter server to it.  This is the only time VMware has let me down.  This all could have been fixed if they allowed you to disable Lockdown Mode from the console.  If I have KVM or physical access to the host anyway, it’s game over security-wise VMware.  Fix this!
EDIT:  I should state that I still have a ticket open with VMware to figure out why my vCenter Server wasn’t started back up on another host in my HA cluster.  Also, if your Virtual Center isn’t virtualized it’s less of a headache, but still very stupid that you cannot disable Lockdown Mode from the console.
