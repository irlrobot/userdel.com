---
layout: post
title: script to launch armitage teamserver quickly
date: '2013-01-10T16:14:27+00:00'
tags:
- armitage
- metasploit
- script
- linux
tumblr_url: http://userdel.com/post/40211420612/script-to-launch-armitage-teamserver-quickly
---
Quickly launch an Armitage teamserver with the servers IP address (eth0 by default, modify the script accordingly) automatically detected and with a pre-set password:

#!/bin/bash
echo “launching multiplayer hacking ;)”
echo “…”

ipaddr=`ip addr show eth0 | grep -w “inet” | gawk ’{ print $2 }’ | cut -f1 -d\/`
echo “IP is $ipaddr”
echo “…”

cd /opt/metasploit/msf3/data/armitage/
/opt/metasploit/msf3/data/armitage/teamserver $ipaddr password
