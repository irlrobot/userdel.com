---
layout: post
title: block w00tw00t scans with fail2ban
date: '2012-03-02T12:36:00+00:00'
tags:
- fail2ban
- linux
- security
- w00tw00t
- httpd
tumblr_url: http://userdel.com/post/18618537324/block-w00tw00t-scans-with-fail2ban
---
Tired of seeing “/w00tw00t.at.blackhats.romanian.anti-sec:)”, and the other variations, in your logs?  First install fail2ban if you don’t have it already (you will wish you’d known about this sooner).  Create a new file in /etc/fail2ban/filter.d/ called “w00tw00t.conf”.  Inside put:

#block w00tw00t scans of all variations
[Definition]
failregex = ^<HOST> .*“GET \/w00tw00t*
ignoreregex =

Then edit /etc/fail2ban/jail.conf and at the bottom put:

[w00tw00t-scans]
enabled  = true
action   = iptables-allports
sendmail-whois[name=SSH, dest=root, sender=fail2ban@mail.com]
filter   = w00tw00t
logpath  = /var/log/httpd/access_log
maxretry = 1
bantime  = 86400

Restart fail2ban and you’re good to go.  You will now ban any IP running one of these automated scanners from connecting to your server, on any port, for 24 hours and get an email alert when it happens.
