---
layout: post
title: create distribution groups in live@edu with powershell
date: '2011-10-04T17:38:00+00:00'
tags:
- fim
- PowerShell
- live@edu
- blah
tumblr_url: http://userdel.com/post/11041734907/create-distribution-groups-in-liveedu-with
---
So I found out that if you don’t have Exchange on-premise you can’t sync distribution groups to Live@edu which is infinitely lame. If you want to provision a large number of lists (one for every class each semester, for example) in an automated fashion you need to use PowerShell remote commands.  Naturally there wasn’t really any examples out there, so I had to learn some PowerShell.  I now consider this a good thing as I really like PowerShell a lot.  
This link provides a copy of a script I created to read in a CSV file and create lists in Live@edu (or Outlook Live) when it’s run.  Feel free to use it and even enhance it.  I plan on uploading this to the PowerShell script repository soon.  
The way it works is it reads in a CSV with file with the list membership.  Unless you modify the script you will need headings of: Course,CRN,Student.  Course is a display name or friendly name, CRN is the mailbox alias of the list, and Student is the member alias.  Where I work we call our class lists “CRN lists” (short for Course Reference Number) so you will see this naming convention in the script.  Instead of keeping track of the membership changes in like a table or something we just found it easier to simply delete all the CRN lists every morning and recreate them based on the CSV sent over to the FIM server daily.
Feel free to contact me @userdel for more information or help.
