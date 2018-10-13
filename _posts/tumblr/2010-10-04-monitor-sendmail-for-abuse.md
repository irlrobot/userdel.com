---
layout: post
title: monitor sendmail for abuse
date: '2010-10-04T10:47:00+00:00'
tags:
- linux
- script
- sendmail
- cron
tumblr_url: http://userdel.com/post/1243383620/monitor-sendmail-for-abuse
---
So at least once a week one of my (L)users will reply to a phishing email and in turn their account will be used to start sending out more spam.  I have a cronjob setup to run a script every 30 minutes to monitor my mail queue and alert me when there are more than 75 emails sitting in the queue.  Under normal load my queue should never exceed even 50 emails, but after 75 I know something is definitely wrong.  Then I have another script that will delete all mail in the queue from a specific user.
Read on for the scripts and how to use them…

Mail queue checking script:

#!/bin/bash
#checkmailq.sh
#monitor the mailq and alert me if its larger than 75 messages
qcheck=/tmp/qchk.txt
trap “rm -f $qcheck ; exit” EXIT
mailq | awk ’ $1 $2==“Totalrequests:” && $3 > 75 { print “Messages in Queue:”,$3 } $2 $3==“Queuestatus…” { q=$1 } ’ > $qcheck
if test -s $qcheck; then
        mail -s “Mail Queue Alert on ServerName” yourAddress@your.Domain < $qcheck
fi

Kill mail from a user script:

#!/bin/bash
#killmail.sh
#delete all mail in the queue from a specific user
function delete_items ()
{       
        while read line1; do
                rm -vf /var/spool/mqueue/*$line1
        done
}
awk < /tmp/abuser ’{print $1}’ | delete_items
rm -f /tmp/abuser

The first script just checks the mail queue and looks for the line containing “Total requests” to see if that number is greater than 75.  If so it will send an email alert, otherwise it does nothing.  You will want to create a cronjob for running the script every 30 minutes or so.  Then when you get an email alert you can login into your sendmail box and run:

mailq | less

This will output a list of all mail in the queue waiting to be processed.  The last column shows the sender and underneath all the recipients.  It will be very obvious which account is being abused.  Next you will want to lock that account and then kill any sessions that user has open (either a webmail frontend or pop/imap).  After that you can run:

mailq | grep username > /tmp/abuser
killmail.sh

This will find all mail from the abused account and dump the lines containing the message ID’s into a file in /tmp/abuser.  Then the killmail.sh script will go through that file line by line deleting the mail from the mqueue directory based on the message ID.  
Make sure the user doesn’t reuse the same password once you unlock it ;)
