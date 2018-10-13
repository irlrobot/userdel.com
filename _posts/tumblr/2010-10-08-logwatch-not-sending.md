---
layout: post
title: logwatch not sending?
date: '2010-10-08T11:54:00+00:00'
tags:
- rhel
- centos
- linux
- logwatch
- logs
- cron
tumblr_url: http://userdel.com/post/1270480668/logwatch-not-sending
---
Logwatch is great, but occasionally it just will not send the reports for whatever reason.  I’ve gotten into the habit of just setting up a cronjob in root’s crontab to run each morning and send me the report.  You can use this if you have the same trouble:

30 7 * * * /etc/log.d/logwatch –service ALL –range yesterday –mailto username@domain.com
