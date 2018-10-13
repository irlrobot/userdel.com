---
layout: post
title: spn's explained
date: '2010-11-02T13:20:00+00:00'
tags:
- spn
- windows
- kerberos
tumblr_url: http://userdel.com/post/1463951178/spns-explained
---
spn''s explainedBest explanation of Service Principal Name’s (SPN) I have seen.
To sum it up:

An SPN is just a *name* that we’ve given to a “service" which is in the format of ServiceType/HostName and occasionally ServiceType/HostName:PortNumber. And it is set on which ever account is handling authentication for that service.
