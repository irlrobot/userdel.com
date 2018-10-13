---
layout: post
title: delete multiple domain accounts quickly
date: '2011-07-05T10:48:00+00:00'
tags:
- script
- vbscript
- Active Directory
- Windows
tumblr_url: http://userdel.com/post/7269148947/delete-multiple-domain-accounts-quickly
---
A few times a year I need to manually delete several hundred accounts from a few disparate systems, one of those being Active Directory.  I’m working on getting an Identity Management package in place but it’s slow going thanks to politics…
Anywho, here is a little VBscript you can use to delete a list of users from your domain.  I can confirm this works on a 2008 R2 domain and 2003 domain.  The list should be a text file containing a single User Logon Name (aka SAM Account Name) on each line for every user you want to delete.  Change the LDAP part (OU’s and DC’s) accordingly.  Save it as a .vbs file and run it from the same location where the list is stored.  Please note this will not delete an Exchange Mailbox:

Set objFSO = CreateObject(“Scripting.FileSystemObject”)
Set objTextFile = objFSO.OpenTextFile(“list.txt”,1)
Set wshShell = CreateObject (“WSCript.shell”)
Do Until objTextFile.AtEndOfStream
 strInput = objTextFile.Readline
 wshshell.run “cmd /C dsrm CN=” & strInput & “,CN=Users,OU=Users,DC=your,DC=domain -noprompt”

Loop
set wshshell = nothing
WScript.Quit
