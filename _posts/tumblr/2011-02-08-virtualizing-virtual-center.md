---
layout: post
title: virtualizing virtual center
date: '2011-02-08T11:50:00+00:00'
tags:
- vmware
- woop
tumblr_url: http://userdel.com/post/3184605096/virtualizing-virtual-center
---
With Virtual Center 4.1 being 64bit only I went ahead and finally virtualized Virtual Center.  It was relatively painless making the conversion and I’m glad I finally did.  You can probably find 20 bazillion articles out there on why you should or shouldn’t run Virtual Center on a VM.  Really it comes down to the fact that you get all the benefits of being on a VM for the small cost of not being able to vMotion or have DRS kick in while the Virtual Center VM is off.  HA still works while Virtual Center is down (you only need it for the initial configuration), so if your host that has the VM goes down it will pop back up on another in just a few short minutes.  My boss was fine with that and it fits in our environment so I did it.  YMMV obviously and you should do your own research on whether or not it’s a fit for you.
To do the upgrade/migration to 4.1, you run a data migration tool on the old server first (included on the ISO) and then run it again on the new server to basically import and install everything.  The DB upgrades are done automagically for you during the installer and don’t take long at all.  The only thing I had trouble with afterwards was all my hosts were showing up disconnected with two error messages:
A general system error occurred:  invalid response.
License expired.
Ahh the ever helpful generic error message!  Number two certainly wasn’t true either; I confirmed this on the VMWare.com support site.  Turns out all that needed to be done was right-click on each host and choose “Connect”.  I disabled HA first on both my clusters and turned it back on after each was re-connected, though.  Apparently during the upgrade process something didn’t go as expected (probably the auto-upgrading of the HA agents).
I’m one step closer to a 100% virtual data center.
