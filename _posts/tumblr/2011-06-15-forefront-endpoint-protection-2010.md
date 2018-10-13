---
layout: post
title: forefront endpoint protection 2010
date: '2011-06-15T12:07:00+00:00'
tags:
- anti-virus
- security
- fep2010
- mcafee
tumblr_url: http://userdel.com/post/6561090202/forefront-endpoint-protection-2010
---
So I’m in the middle of replacing McAfee with FEP2010 and I must say so far I’m impressed.  I was a little concerned at first about using SCCM to manage it, but I think I’m over that now.  My beef with SCCM is simply that it’s too complicated and messy.  Despite what MS says, it’s no different than SMS (certainly not any easier to use).  Once you have SCCM up and running, installing FEP is a breeze.  Setup is quick and simple and pushing policy is cake.  If you are still using a separate WSUS server for updates this is the only real work you’ll need to do.
So if you have SCCM up and running already all you need to do is run the FEP installer executable on your SCCM management server.  It will create a new DB and then add some new things in the SCCM console; easy as that.  You’ll see a new collection called “FEP Collections” which have some special locked collections that show you things like failed deployments, which computers have out of date definitions, which have malware, and many other things.  There will also be a “Forefront Endpoint Protection” section until Computer Management now which is where you can define custom policies.  Finally, you’ll notice it automatically creates some packages and advertisements for you.  Told you it was easy!
If you have a separate WSUS server you should configure it to auto approve the FEP definition updates so all your clients stay up to date.  To do that check out this guide on TechNet.  
Deploying is also pretty simple and I’m not even going to detail of any of that here since this guide does a fantastic job.
