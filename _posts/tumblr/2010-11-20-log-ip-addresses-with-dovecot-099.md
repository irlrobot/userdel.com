---
layout: post
title: log ip addresses with dovecot 0.99
date: '2010-11-20T13:24:30+00:00'
tags:
- rhel
- centos
- dovecot
- linux
- sendmail
tumblr_url: http://userdel.com/post/1629464474/log-ip-addresses-with-dovecot-099
---
Anyone running RHEL4 will appreciate this.  If you want to see the IP Addresses of users successfully logging in via POP3/IMAP with dovecot 0.99 then you need to set “auth_verbose = yes” in dovecot.conf.  Later versions (1.0+) have some different options available in the configuration file, but they don’t work in 0.99.  
Now in maillog (or wherever you log dovecot to) you can see where your users are logging in from the format of:

Nov 20 16:15:56 serverName pop3-login:  Login:  username [::ffff:192.168.1.5]

This is helpful for when an account on your system is hijacked and the attacker is spoofing the from address so when you check your mail queue you can’t tell which user account the mail is coming from.  Now you can grab the relay/source IP address from the header of the outgoing email and grep through maillog to find out which user is logging in from that address.  Once you find out which account is being abused proceed as usual.
