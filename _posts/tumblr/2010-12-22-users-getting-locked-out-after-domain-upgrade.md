---
layout: post
title: users getting locked out after domain upgrade
date: '2010-12-22T04:40:00+00:00'
tags:
- windows
- domain
- NTLM
- LM
- authentication
- wtf
tumblr_url: http://userdel.com/post/2415343309/users-getting-locked-out-after-domain-upgrade
---
This is fairly obscure, but who knows it may help someone down the road.  Last Friday we started a domain upgrade from 2003 to 2008 R2.  We got two of our three DC’s upgraded and saved the last one for Monday morning.  When we came in Monday all hell broke lose.  Users could log in, but when they opened Outlook they were prompted for credentials and even if they entered them correctly Outlook would just keep prompting them.  Same thing if they tried to browse file shares on our DFS.  The Help Desk was getting hammered and after a couple hours and a call to Microsoft we found the problem: 
HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Lsa\LmCompatibilityLevel
Long story short, this key on all our XP clients (yes we are still on XP…) is set to 0 and on the new DC’s it was set to 5.  Whenever a user logged in they were immediately locked out hence the prompting of creds.  We changed the key on the DC’s to 2 one at a time rebooting each afterwards and then everything was fine.  Phew.
More info on the LM levels…
For reference, the full range of values for the LMCompatibilityLevel value that are supported by Windows NT 4.0 and Windows 2000 include: 
• Level 0 - Send LM and NTLM response; never use NTLM 2 session security. Clients use LM and NTLM authentication, and never use NTLM 2 session security; domain controllers accept LM, NTLM, and NTLM 2 authentication.
• Level 1 - Use NTLM 2 session security if negotiated. Clients use LM and NTLM authentication, and use NTLM 2 session security if the server supports it; domain controllers accept LM, NTLM, and NTLM 2 authentication. 
• Level 2 - Send NTLM response only. Clients use only NTLM authentication, and use NTLM 2 session security if the server supports it; domain controllers accept LM, NTLM, and NTLM 2 authentication. 
• Level 3 - Send NTLM 2 response only. Clients use NTLM 2 authentication, and use NTLM 2 session security if the server supports it; domain controllers accept LM, NTLM, and NTLM 2 authentication. 
• Level 4 - Domain controllers refuse LM responses. Clients use NTLM authentication, and use NTLM 2 session security if the server supports it; domain controllers refuse LM authentication (that is, they accept NTLM and NTLM 2). 
• Level 5 - Domain controllers refuse LM and NTLM responses (accept only NTLM 2). Clients use NTLM 2 authentication, use NTLM 2 session security if the server supports it; domain controllers refuse NTLM and LM authentication (they accept only NTLM 2).
The MS tech I worked with recommended setting the clients to level 2 and the DC’s to level 3.  He also told me that the default on XP is supposed to be 1 and the DC’s should have default to 3.  However, when I promoted my last DC it was also set to level 5.  This registry key is not present in the image I used (I looked at 10 other servers I loaded with it and it’s not even there) and we aren’t pushing that registry key by group policy (as far as I can tell) so I have no idea how it’s getting there if the default is supposedly 3.  
I’m going to keep poking around to see if I can find out how it’s getting set to 5.  I’ve inherited this domain so it’s possible the previous 4 or 5 admins have used some black magic.  I also want to look at the clients because the image the Help Desk uses doesn’t set this key either and again I don’t see any group policy that is setting it so I don’t know why it is being set to 0.  In the meantime if anyone has any insight it would be much appreciate.
*EDIT*
I checked a PC at home that has Win XP Pro loaded from the disc and it’s level is set to 0.  So it looks like the MS guy is wrong - XP defaults to 0 and 2008 R2 defaults to 5.
