---
layout: post
title: using fim with live@edu or outlook live
date: '2011-08-24T05:12:00+00:00'
tags:
- cloud
- fim
- idm
- live@edu
- fim 2010
- identity management
tumblr_url: http://userdel.com/post/9331598712/using-fim-with-liveedu-or-outlook-live
---
The Outlook Live Management Agent (OLSync) is a modified version of GALSync for Outlook Live (Live@edu). It consists of two MAs (OnPremises MA & Hosted MA) that sit on the Synchronization Service server. It uses custom rules extensions to read from AD (OnPremises Connector Space) and to provision to Outlook Live (Hosted Connector Space). It has pre-built (but customizable to some degree) Attribute Flow and Projection/Join rules. 
It may be possible to integrate the provisioning code from the Hosted MA into the synchronization rules in the FIM Portal. To my knowledge, however, this is not currently supported with Live@edu. By “not currently supported,” I mean that Microsoft Live@edu Support may not provide technical support and/or guidance in this scenario. On the other hand, OLSync MA installed on FIM sync server is supported by Live@edu Support. 
You can receive the x64 OLSync MA from Live@edu Support. As I mentioned previously, OLSync is a modified version of GALSync. So, the file that Support will deliver is usually called Galsync.msi. This can be confusing.  When you attempt to install it, the installation wizard should say Outlook Live Management Agent. If not, contact support again.
