---
layout: post
title: using fim2010 for ad provisioning with outlook live or live@edu
date: '2011-10-04T17:12:47+00:00'
tags:
- fim
- fim 2010
- lame
- idm
- identity management
- Active Directory
tumblr_url: http://userdel.com/post/11040511950/using-fim2010-for-ad-provisioning-with-outlook
---
If you want to use Forefront Identity Manager 2010 to provision to Active Directory and you are also using Outlook Live or Live@edu you will need a second FIM synchronization server.  Once you install Galsync_x64.msi (obtained from support currently) it modifies metaverse attributes that will prevent your synchronization rules created in FIM from working.  This is “working as intended” according to Microsoft support.  So you need one sync server and one portal server to do AD provisioning, and then one sync server with just the Galsync.msi MA’s for Live@edu provisioning.
