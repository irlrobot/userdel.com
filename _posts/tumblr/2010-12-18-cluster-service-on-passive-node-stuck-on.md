---
layout: post
title: cluster service on passive node stuck on "starting"
date: '2010-12-18T09:49:26+00:00'
tags:
- windows
- cluster
- wtf
tumblr_url: http://userdel.com/post/2362018433/cluster-service-on-passive-node-stuck-on
---
If you have a passive cluster node who’s Cluster Service is stuck on ‘starting’ and you can’t remote desktop the active node (i.e does nothing after entering credentials to log) you basically just need to reboot the active node.  You can first try restarting the Cluster Service on the active node using Computer Management on the passive node and connecting to the active node.  A hard reboot should do the trick failing that.  In my experience, the passive node’s Cluster Service will come right up and seize all the cluster resources as soon as the active node goes down.
One thing I haven’t tried, and didn’t think about until writing this article, is to disable the Heartbeat NIC and possibly the normal LAN NIC on the active node and see what happens.  This could possibly work as well but I’m not sure.
