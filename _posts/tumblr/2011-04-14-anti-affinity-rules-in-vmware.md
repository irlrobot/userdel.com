---
layout: post
title: anti-affinity rules in vmware
date: '2011-04-14T07:36:52+00:00'
tags:
- drs
- vmware
- affinity rules
- sweet
tumblr_url: http://userdel.com/post/4607471909/anti-affinity-rules-in-vmware
---
A lot of people I’ve chatted with about VMware haven’t heard of or used anti-affinity rules with their DRS cluster.  This is very useful for making sure things like all your domain controllers or clustered VM’s aren’t on the same ESX(i) host and it’s very easy to set up.
Right click on your cluster and go to “Edit Settings”.
If DRS isn’t enabled you can’t do this, but you really have no reason not to have this enabled anyway.
Go to “Rules” under “VMware DRS”.
Click “Add”.
Change the type to “Separate Virtual Machines”.
Click “Add” and pick your VM’s.
It’s that easy.  You can have multiple rules for different types of VM’s to separate.  I have three rules that separate all my DC’s, Exchange, and SQL servers respectively.  You can also define which hosts the VM’s should (or must) reside on by choosing “Virtual Machines to Hosts” from the drop down instead.  For example, if you have four ESX hosts that have more RAM than other hosts you may want to make sure your Exchange servers are always running on the hosts with the most RAM available.
You’ll notice you can also keep a group of VM’s together if you wanted.  You can also create groups of Hosts and apply rules to specific Host groups instead of selecting the Hosts individually in the rule creation.  Poke around a bit more and you can figure out pretty easily how to do this.
