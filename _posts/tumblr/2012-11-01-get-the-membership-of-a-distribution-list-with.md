---
layout: post
title: get the membership of a distribution list with powershell
date: '2012-11-01T09:27:00+00:00'
tags:
- powershell
- psh
- script
- windows
- exchange
tumblr_url: http://userdel.com/post/34765424530/get-the-membership-of-a-distribution-list-with
---
Simple one that I’ve had to use time and again but always forget what the command is…

Get-DistributionGroup “listName” | Get-DistributionGroupMember | FT Name,PrimarySMTPAddress >> “C:\blah\listMembers.txt”

Probably a nicer way to export it as a CSV, but if you just add | Export-CSV c:\path\blah.csv you get gibberish in the columns.  I was too lazy to look up how to fix that….
