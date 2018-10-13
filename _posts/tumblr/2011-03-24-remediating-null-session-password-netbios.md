---
layout: post
title: remediating "null session / password NetBIOS Access" and "NetBIOS Remote User
  List Disclosure" on domain controller
date: '2011-03-24T10:17:00+00:00'
tags:
- security
- windows
- headache
- qualys
- help!
tumblr_url: http://userdel.com/post/4065945492/remediating-null-session-password-netbios
---
SOLVED (kind of):
Finally was granted the opportunity to do some testing on one of the production domain controllers (always fun to do!) by the boss man since I couldn’t replicate the issue anywhere else.  Turns out if you remove “samr” from the local security policy “Network access: Named pipes that can be accessed anonymously” you can no longer dump the user list from an anonymous, non-domain account.  I’m not sure if this remediates the Qualys scan entirely (I had to put it back in production until we know the consequences of removing it), but for practical purposes the threat of an anonymous account being able to dump your userlist and then start brute forcing is eliminated.  Changing “Network access: Do not allow anonymous enumeration of SAM accounts and shares” to enabled did not however fix the issues (I changed this first then ran a new Qualys scan and it can back with the original results).
The kicker is I still have “samr” in the list for my other DC’s and I can’t dump those user lists, so I’m still kind of at a loss.  There must be some other setting/permission in a GPO or something that I’m over looking.  We’ve upgraded all the way from a 2000 domain over the years and a lot of original policy is still in place.  I think I’ll get a call in to MS for this eventually to see what the real problem is…
UPDATE:
As of 4/10/11 I still haven’t solved this.  Qualys sent me this link via twitter which is the same stuff everyone recommends.  I’m putting in a call to MS this week to see what’s up…
So I recently did a Qualys scan on three of my Windows 2008 R2 domain controllers and all three came back with "null session / password NetBIOS Access" and “NetBIOS Remote User List Disclosure”.  The scan report does not have any remediation steps for Server 2008; I tried the fixes suggested for 2003 (see below).  Everything I’ve found so far while reading TechNet forums and Googling has pointed back to 6 local security policy settings (and also their associated reg keys which are not displayed below) which the scan report also mentions it a round about kind of way:
Network access: Allow anonymous SID / Name translation - Disabled
Network access: Do not allow anonymous enumeration of SAM accounts - Enabled
Network access: Do not allow anonymous enumeration of SAM accounts and shares - Enabled
Network access: Let Everyone permissions apply to anonymous users - Disabled
Network access: Named Pipes that can be accessed anonymously - None
Network access: Shares that can be accessed anonymously - None
These seem to have zero effect.  I’ve got three other domain controllers using identical settings as the three that come back with the vulnerabilities and they come back clean from the scan.  
I’ve confirmed that the vuln’s actually exist and aren’t false positives.  Using the tool enum I’m able to initiate a null session and also enumerate domain user accounts when using a non-domain account from a laptop.  If I try to do this on the other DC’s that come back clean from the scan it fails.
I’ve run MBSA and the Directory Services BPA (Best Practices Analyzer builtin to Server 2008 products) on the DC’s both of which come back clean.  Windows itself thinks anonymous sessions are disabled when they clearly are not!  The built-in “Guest” account is disabled also.
If anyone has any suggestions on fixing this please let me know.  Tweet me @userdel, reply to this post, or email me at josh+qualys@userdel.com!  I’m opening a ticket with Qualys to see what they recommend, but I’m hoping you folks on the intarwebz are a little quicker ;)
