---
layout: post
title: device eth0 does not seem to be present
date: '2012-05-25T12:15:10+00:00'
tags:
- llinux
- rhel
- centos
- weird
tumblr_url: http://userdel.com/post/23745712822/device-eth0-does-not-seem-to-be-present
---
If you run into this error cloning a VM or changing the NIC on a VM just do the following:
Delete this file /etc/udev/rules.d/70-persistent-net.rules
Reboot
Run system-config-network and re-create
Assuming a RHEL or RHEL-like OS.
