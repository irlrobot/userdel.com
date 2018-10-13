---
layout: post
title: add users to a group based on an ad attribute
date: '2013-03-05T07:28:06+00:00'
tags:
- windows
- powershell
- psh
- Active Directory
- AD
tumblr_url: http://userdel.com/post/44630608667/add-users-to-a-group-based-on-an-ad-attribute
---
Props to TechNet forums user philldogger for this one.  If you want to build a group in AD based on the value of an attribute that the users will have (e.g. make a DFS group based on Department) you can do this:

Import-Module ActiveDirectory
Get-ADUser -filter{department -like “Accounting”} | %{Add-ADGroupMember dfs_dept_Accounting $_.SamAccountName}

In this example I am specifying the “department” AD attribute and looking for anyone who’s Department is set to “Accounting” and adding them to my AD group named “dfs_dept_Accounting”.  
If you want to script it so the group membership is updated as new people join, add this line below the importing of the AD PowerShell module.

Get-ADGroupMember dfs_dept_Accounting | %{remove-adgroupmember dfs_dept_Accounting $_.SamAccountName -Confirm:$false}

This will wipe out the group and then re-add everyone.  You can have one script per group you’d like to be updated, or combine multiple into one script.  Fair warning though, if you have a good sized AD the script’s could take a long time to run and may hammer your DC’s so do due diligence.
