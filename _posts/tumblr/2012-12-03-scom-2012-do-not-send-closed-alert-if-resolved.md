---
layout: post
title: scom 2012 do not send closed alert if resolved within sending delay of new
  alert
date: '2012-12-03T07:57:40+00:00'
tags:
- SCOM
- ARGGG
- microsoft
- stupid
tumblr_url: http://userdel.com/post/37115784373/scom-2012-do-not-send-closed-alert-if-resolved
---
scom 2012 do not send closed alert if resolved within sending delay of new alertOver the last couple weeks I have learned that SCOM 2012 is utterly retarded.  It’s way too noisy and creating overrides or disabling notifications is a confusing experience.  Simple features like scheduling a reoccurring or granular (between such and such hours) maintenance mode and creating a group to exclude another existing group or OU are non-existent.  The layout and UI are just downright un-intuitive and over-complicated for a solution who’s main function is to alert you to a problem and help you fix it quickly.  I really hate this product.  The thing that sent me over the edge this morning was the simple fact that if I create a subscription and have a send delay on the alerts, the New alerts won’t get sent if things work themselves out within the delay but the Closed alerts still get sent and there is no simple way to fix this.  Time to start looking for something else.
