---
layout: post
title: enable deprovisioning in live@edu with FIM
date: '2011-10-27T07:38:00+00:00'
tags:
- FIM
- fim 2010
- live@edu
- idm
tumblr_url: http://userdel.com/post/11991423235/enable-deprovisioning-in-liveedu-with-fim
---
If you want to delete accounts in Live@edu when you delete an account in your on premise Active Directory you need to change the “DisableWindowsLiveID” in your Hosted MA to “True”.  Right-click on your MA and go to Properties then Configure Additional Parameters:

Keep in mind this will delete the mailbox and the Live ID and thus removing the users SkyDrive and anything they may have in it.
