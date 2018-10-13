---
layout: post
title: replace cmd with powershell
date: '2013-07-18T07:53:53+00:00'
tags:
- powershell
- posh
- windows
- hack
- psh
tumblr_url: http://userdel.com/post/55782573676/replace-cmd-with-powershell
---
If you want to open PowerShell instead of a normal command prompt (cmd.exe) when you enter “cmd” into Run, just open PowerShell as Administrator and enter the below.  It will create a registry key and act much like an alias.

New-Item “HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\App Paths\cmd.exe” | Set-ItemProperty -Name “(default)” -Value “C:\WINDOWS\system32\WindowsPowerShell\v1.0\powershell.exe”
