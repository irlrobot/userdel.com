---
layout: post
title: set out of office for another user with exchange 2007
date: '2010-10-19T10:49:54+00:00'
tags:
- exchange
- gotcha
- windows
- email
tumblr_url: http://userdel.com/post/1352337497/set-out-of-office-for-another-user-with-exchange
---
In order to set an out of office for another user in Exchange 2007 you need to give yourself Full Access to the mailbox in the Exchange Management Console.  You can do this by right clicking on the user/mailbox and going to the “Manage Full Access permission…” menu.  After you do that create a new mail profile (Control Panel -> Mail) in Windows for that mailbox and open up Outlook.  Once in Outlook you’ll be able to set the out of office for that user.
You have to do this even if you are an Exchange or Domain Admin.
