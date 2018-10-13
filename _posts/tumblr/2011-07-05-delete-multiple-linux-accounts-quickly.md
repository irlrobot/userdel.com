---
layout: post
title: delete multiple linux accounts quickly
date: '2011-07-05T10:58:42+00:00'
tags:
- linux
- script
- bash
tumblr_url: http://userdel.com/post/7269468011/delete-multiple-linux-accounts-quickly
---
I mentioned in my post about deleting multiple AD domain accounts quickly that I had to do this for a few disparate systems.  One of those other systems is a mail server running RHEL.  Here is a simple shell script that takes a file containing a username on each line and deletes all the accounts:

#!/bin/bash

function delete_account ()
{       
        while read line1; do
                userdel -r $line1
                echo “DUHLETED, goodbye $line1 its been real!”
        done
}
awk < /home/bob/toBeDeleted ’{print $1}’ | delete_account
