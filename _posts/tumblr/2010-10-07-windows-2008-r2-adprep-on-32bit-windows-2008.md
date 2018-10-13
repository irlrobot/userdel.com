---
layout: post
title: windows 2008 r2 adprep on 32bit windows 2008
date: '2010-10-07T11:59:00+00:00'
tags:
- adprep
- gotcha
- windows
- active directory
tumblr_url: http://userdel.com/post/1263675292/windows-2008-r2-adprep-on-32bit-windows-2008
---
So Windows Server 2008 R2 is 64 bit only.  What if you are running 32bit Windows Server 2008 on your domain controllers?  Instead of adprep you need to run adprep32 from the 2008 R2 disc on the 32bit DC’s.
