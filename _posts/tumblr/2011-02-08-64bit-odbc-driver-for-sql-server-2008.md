---
layout: post
title: 64bit odbc driver for sql server 2008
date: '2011-02-08T11:36:58+00:00'
tags:
- vmware
- odbc
- sql server
- oye
tumblr_url: http://userdel.com/post/3184420808/64bit-odbc-driver-for-sql-server-2008
---
So I was just upgrading my Virtual Center server to 4.1 and ran into the issue of creating the 64bit DSN. If you need to create a 64bit DSN to connect to a DB on SQL Server 2008 or 2008 R2, you need to download the SQL Native Client.  You can simply grab the 2008 R2 native client and it will work for both 2008 and 2008 R2.  When you create the DSN it will show up as “SQL Server Native Client 10.0” for the driver name.
