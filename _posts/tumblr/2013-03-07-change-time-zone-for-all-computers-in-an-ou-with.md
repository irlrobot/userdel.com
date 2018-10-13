---
layout: post
title: change time zone for all computers in an ou with powershell
date: '2013-03-07T13:39:49+00:00'
tags:
- powershell
- psh
- windows
- ad
tumblr_url: http://userdel.com/post/44807327889/change-time-zone-for-all-computers-in-an-ou-with
---
Here’s a little PowerShell script you can use to change the time zone for all computers in a certain OU.

Start-Transcript
Import-Module ActiveDirectory
$cred = Get-Credential

$arr = Get-ADComputer -SearchBase ‘OU=Servers,OU=example,dc=blah,dc=com’ -Filter ’*’ | Select-Object -ExpandProperty Name

#for debugging - manually set the array for testing
#$arr = “server01”, “server02”

foreach ($a in $arr)
 {
 Write $a
 Write “current time zone is”
 invoke-command -cn $a -cred $cred {tzutil /g}
 Write “————–”
 Write “overwriting time zone”
 invoke-command -cn $a -cred $cred {tzutil /s “Central Standard Time”}
 Write “————–”
 }

Stop-Transcript
