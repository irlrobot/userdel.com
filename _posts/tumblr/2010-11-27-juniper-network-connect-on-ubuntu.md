---
layout: post
title: juniper network connect on ubuntu
date: '2010-11-27T16:10:00+00:00'
tags:
- linux
- ubuntu
- java
- juniper
tumblr_url: http://userdel.com/post/1707428917/juniper-network-connect-on-ubuntu
---
Ubuntu will use OpenJDK by default which works fine for most things.  However, if you have a Juniper SSL VPN and try to use network connect you will continuously get a “session timeout” error when you try to connect.  To remedy this you need to install the real deal Sun/Oracle Java 6:

sudo apt-get install sun-java6-jre sun-java6-jdk
sudo apt-get remove openjdk-*-*
sudo apt-get install sun-java6-plugin

If you try to remove OpenJDK first you will get a bogus dependency error (at least on 10.10), so you’ll need to do the above in order.  Removing OpenJDK will also remove the Icedtea browser plugin hence the need to install the plugin again.
