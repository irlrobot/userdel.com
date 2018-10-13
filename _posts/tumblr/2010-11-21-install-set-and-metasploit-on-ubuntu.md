---
layout: post
title: install set and metasploit on ubuntu
date: '2010-11-21T05:48:06+00:00'
tags:
- SET
- infosec
- metasploit
- social engineering
- ubuntu
- linux
tumblr_url: http://userdel.com/post/1636875195/install-set-and-metasploit-on-ubuntu
---
The Social Engineer Toolkit is an amazing tool that leverages Metasploit to do some incredible things.  You can find SET and numerous other tools in BackTrack ready to go, or you can install it yourself on an existing Ubuntu (10.10) setup like I did.
First, get Metasploit installed by following these instructions from Metasploit.com.  Make sure you do the steps in the “Extensions” section as well.  You can skip the part about adding the cronjob for updating unless you really want, because in SET you can update Metasploit from the menu quickly.  
Next you’ll need to install Postgres.  It’s the recommended Metasploit DB, but you can use something else if you really want.  For the “Enable the database on startup” section just “sudo bash” from your normal user account and it will create the file inside the .msf3 directory of that users home folder.  You will want a root shell for running SET anyway and this will make it so you don’t need to actually login as root.
Now you are ready to install SET.  Change to the /opt directory and do “svn co http://svn.secmaniac.com/social_engineering_toolkit set/”.  You should now be able to go into /opt/set and run “./set” (as root) to fire up the Social Engineer Toolkit.  You should see the options to update both Metasploit and SET right from the menu.  You should update both now and each time you open SET.
Finally, you’ll want to install a few more things to use SET to its full potential.
sudo apt-get install ettercap
sudo apt-get install sendmail
sudo apt-get install openjdk-6-jdk
Now you can edit /opt/set/config/set_config and enable the various options.  Have a look here for an explanation on the various options.  At the very least you definitely want “SELF_SIGNED_APPLET = ON” (make sure openjdk-6-jdk is installed) as that is hands down one of the best features of SET.
Social-Engineer.org has a lot of other great stuff on the site, besides SET, related to Social Engineering.  They have a fantastic Podcast that I highly recommend, a newsletter, and a blog all dedicated to Social Engineering.  Big thanks to the crew over there for a fantastic tool!
