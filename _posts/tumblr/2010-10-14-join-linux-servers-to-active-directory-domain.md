---
layout: post
title: join linux servers to active directory domain
date: '2010-10-14T07:55:00+00:00'
tags:
- Active Directory
- centrify
- likewise
- linux
- windows
- co-exist
- unpossible
tumblr_url: http://userdel.com/post/1313363186/join-linux-servers-to-active-directory-domain
---
Let’s be serious here for a minute.  There are very few pure Windows or pure Linux/UNIX shops out there anymore, and those that do exist are just hurting themselves by not leveraging the benefits of both.  Yes it is possible for both Linux and Windows to co-exist peacefully.  The world will not implode, I promise.
One of the things Microsoft has gotten right, in my opinion, is Active  Directory.  It’s everywhere and AD isn’t going anywhere anytime soon. Leverage your existing AD environment by joining your Linux boxes to your domain with products like Centrify and Likewise.
The biggest benefit in my opinion is single sign on.  No longer will you need to reset the password for someone on one of the BIND servers when they forgot it for the 93rd time because they only log in once every 7 full moons.  Nor will you need to manage a second directory.  
Both products have free versions that will simply allow you to join the domain, which basically gives you the ability to log into the Linux server with your domain credentials (and thus enforcing password policy as well).  For most servers you can probably get away with just the free version, but if you need more capability (like enforcing GPO’s) then you will want the Enterprise version.  Personally I like Centrify more, but have used Likewise in the past with no issues.
