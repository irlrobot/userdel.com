---
layout: post
title: manually install vmware converter agent for Windows
date: '2011-02-17T07:56:44+00:00'
tags:
- vmware
- vmware converter
- windows
tumblr_url: http://userdel.com/post/3345504444/manually-install-vmware-converter-agent-for
---
Today I ran into an issue where I was trying to convert a Windows server but during the VMWare Converter agent install it kept failing with a generic error.  I went ahead and installed the agent manually and voila it worked.
On the server you have VMWare Converter standalone installed, go to “C:\Program Files (x86)\VMware\VMware vCenter Converter Standalone” - obviously substitute the correct driver letter and if you’re not on a 64bit box you can remove the “(x86)” part.
Find the file named “VMware-Converter-Agent.exe” and copy it over to the Windows box.
Run the executable you copied.
Restart the VMWare Converter process and it should just skip right over the need to install the agent after connecting to the box.  You can uninstall the agent manually afterwards if you want.
