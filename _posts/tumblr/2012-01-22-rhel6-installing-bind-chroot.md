---
layout: post
title: rhel6 installing bind-chroot
date: '2012-01-22T05:04:00+00:00'
tags:
- linux
- rhel
- dns
- bind
- bleh
- SELinux
tumblr_url: http://userdel.com/post/16285640691/rhel6-installing-bind-chroot
---
Oh Red Hat, sometimes I don’t get you.  So it seems the “recommended” way of installing BIND on RHEL6 is now to just install normally (e.g. “yum install bind”) and let SELinux handle the security.  My beef with this is how frustrating SELinux can be.  Honestly every time I have to troubleshoot an issue with it I’m down at least two hours of my time and it just isn’t worth it to me.  Maybe I’m SELinux retarded but this has always been my experience with it so I usually just end up disabling.
RHEL6 still includes a package in the repository for bind-chroot thankfully.  However, it seems that now when you start named Red Hat does some voodoo by mounting all the normal bind directories and files on the chroot jail directories and files.  Very weird, here’s what I mean:

none on /proc/sys/fs/binfmt_misc type binfmt_misc (rw)
/etc/named on /var/named/chroot/etc/named type none (rw,bind)
/var/named on /var/named/chroot/var/named type none (rw,bind)
/etc/named.conf on /var/named/chroot/etc/named.conf type none (rw,bind)
/etc/named.rfc1912.zones on /var/named/chroot/etc/named.rfc1912.zones type none (rw,bind)
/etc/rndc.key on /var/named/chroot/etc/rndc.key type none (rw,bind)
/usr/lib64/bind on /var/named/chroot/usr/lib64/bind type none (rw,bind)
/etc/named.iscdlv.key on /var/named/chroot/etc/named.iscdlv.key type none (rw,bind)
/etc/named.root.key on /var/named/chroot/etc/named.root.key type none (rw,bind)

I’m guessing that it was too confusing for people having the symlinks and not knowing which files to edit?  At any rate it was definitely different.  So in RHEL6 just remember to edit /etc/named.conf now and then when you start/restart named your new config will actually be in the jail (e.g. /var/named/chroot/etc/named.conf).
The main issue I ran into bind-chroot on RHEL6.2 is that it was sorted of a busted install.  During install the rndc.key file was not generated even though the documentation says it should be.  So if after running yum install bind-chroot and you do not have /etc/rndc.key you need to create it manually:

rndc-confgen -a
chown root:named /etc/rndc.key
chmod 640 /etc/rndc.key

Despite Red Hat’s documentation, the key file actually needs 640 with named as the group or named will not start due to a permissions error.
Also if you are using bind-chroot make sure you disable SELinux by editing /etc/sysconfig/selinux and then rebooting.
