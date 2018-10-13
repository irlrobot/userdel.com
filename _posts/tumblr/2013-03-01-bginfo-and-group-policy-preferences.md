---
layout: post
title: bginfo and group policy preferences
date: '2013-03-01T12:09:00+00:00'
tags:
- windows
- group policy
tumblr_url: http://userdel.com/post/44310748159/bginfo-and-group-policy-preferences
---
After you download BgInfo and get your configuration file created you can easily create a GPO using Group Policy Preferences to have it load on any computer on your domain.  
Copy the BgInfo.exe and your config.bgi to \your.domain\NETLOGON share.
Create a new GPO and goto Computer > Preferences > Windows Settings > Files
Right and click and goto New > File
Under Action make sure it says Update
Under source file put “\your.domain\NETLOGON\Bginfo.exe”
Under destination file put “C:\Program Files\BgInfo\Bginfo.exe”
Click OK to close and then repeat step 3 to add another file
Again under Action make sure it says Update
Under source file put “\your.domain\NETLOGON\yourConfig.bgi”
Under destination file put “C:\Program Files\BgInfo\yourConfig.bgi”
Click OK to close
Now back in the GPO window goto the Registry section (Computer > Preferences > Windows Settings > Registry)
Right and click and goto New > Registry Item
Under Action make sure it says Update
Change Hive to “HKEY_LOCAL_MACHINE”
For key path add “SOFTWARE\Microsoft\Windows\CurrentVersion\Run”
For Value Name add “BgInfo”
For Value Type set it to “REG_SZ”
In Value Data put (including the quotes) “C:\Program Files\BgInfo\Bginfo.exe” “C:\Program Files\BgInfo\yourConfig.bgi” /silent /timer:0 /NOLICPROMPT"
Your GPO is now ready, add a scope and test it out.
