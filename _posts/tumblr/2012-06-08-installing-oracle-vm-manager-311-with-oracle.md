---
layout: post
title: installing oracle vm manager 3.1.1 with oracle standard edition
date: '2012-06-08T12:38:10+00:00'
tags:
- linux
- oracle
- pita
- vmware is better
- virtualization
tumblr_url: http://userdel.com/post/24694907679/installing-oracle-vm-manager-311-with-oracle
---
I want to start off by saying I am not an Oracle guy and my expertise is with VMware.  Anyone who has ever purchased an Oracle product will tell you their licensing is abysmal to say the least.  Their licensing model for VMware isn’t any better and they basically force you to use their virtualization product, Oracle VM, unless you have money to blow.
With that said, I was recently tasked with installing a two node Oracle VM cluster to support several database servers we will be migrating off physical boxes.  After a hundred conference calls and another dozen internal meetings, for better or worse we chose to go with Oracle VM.  In this tutorial I won’t talk about setting up the actual Oracle VM servers, just VM Manager.  
Getting up a test/demo box is easy enough.  Spin up Oracle Linux 6, mount the VM Manager 3.1.1 ISO, and hit enter a few times.  If you’re like me and you are far from an Oracle guru then you may need some help getting Oracle Standard Edition installed first so you can run a supported environment (hint: Oracle XE isn’t supported in production =).  Good portion of the below derived from this great writeup (thanks to the author!) mixed with my own experience and specific steps for Oracle VM Manager install.
Download the 64bit version of Oracle Linux 6, whatever is newest.  That would be Update 2 at the time of this writing.
Download the newest version of 64bit Oracle 11gR2 also.  11.2.0.3 at the time of this writing.
Download Oracle VM Manager 3.1.1 or newer.
Get your Oracle Linux install going and when it gets to the part where you pick your server type, just leave it as Basic Server and click the Customize Now radio button to add more features.  You will want to pick the following the package groups: Base System > Base
Base System > Client management tools
Base System > Compatibility libraries
Base System > Hardware monitoring utilities
Base System > Large Systems Performance
Base System > Network file system client
Base System > Performance Tools
Base System > Perl Support
Servers > Server Platform
Servers > System administration tools
Desktops > Desktop
Desktops > Desktop Platform
Desktops > Fonts
Desktops > General Purpose Desktop
Desktops > Graphical Administration Tools
Desktops > Input Methods
Desktops > X Window System
Development > Additional Development
Development > Development Tools
Applications > Internet Browser

Login as root and run all of the below as root until you switch to the Oracle user in Step 18.
Add your servers fully qualified hostname and IP to /etc/hosts
Disable the firewall (“service iptables stop” and “chkconfig iptables off”) and SELinux (edit /etc/sysconfig/selinux and change option to “disabled”).  You can leave the firewall running or turn it back on later if you like, but I’d recommend keeping SELinux off because it’s more of a pain than anything.
Run “xhost +” for allowing connections to the X server
Add the public Oracle Linux repo to update your server and fetch anything else you may need.  "cd /etc/yum.repos.d" and then “wget http://public-yum.oracle.com/public-yum-ol6.repo”.  You may need to change this depending on your Oracle Linux version.
Might be a good idea to update now, but you can skip this step if you want.  "yum -y update".
Run “yum install oracle-rdbms-server-11gR2-preinstall” to get your server prepped for Oracle database install.
Reboot at this point.
Now we can cheat a little to save some time.  Mount your VM Manager 3.1.1 iso and run “createOracle.sh”.  This will create an oracle user, the /u01, add firewall rules, and more.  Handy!
Edit /etc/security/limits.conf and find the line where it says “oracle soft nofile ####” and change #### to 8192.
Run “chown oracle: /u01” to fix the permissions on /u01 (or Oracle install will fail later).
Make sure /u01 is also 755, you can run “chmod 755 /u01” just in case if you aren’t sure what this means =)
Run “passwd oracle” and set the Oracle user password to something secure.
Switch to the oracle user now.
Time to make a decision.  You need to come up with a SID for your Oracle database.  I use “ovm” in the examples below. It is case sensitive!
Edit .bash_profile and add this to the bottom substituting your SID and fully qualified host name where indicated:# Oracle Settings TMP=/tmp; export TMPTMPDIR=$TMP; export TMPDIR
ORACLE_HOSTNAME=HOSTNAME.FQDN; export ORACLE_HOSTNAME ORACLE_UNQNAME=SID_NAME; export ORACLE_UNQNAME ORACLE_BASE=/u01/app/oracle; export ORACLE_BASE ORACLE_HOME=$ORACLE_BASE/product/11.2.0/db_1; export ORACLE_HOMEORACLE_SID=ovm; export ORACLE_SID
PATH=/usr/sbin:$PATH; export PATHPATH=$ORACLE_HOME/bin:$PATH; export PATH
LD_LIBRARY_PATH=$ORACLE_HOME/lib:/lib:/usr/lib; export LD_LIBRARY_PATH CLASSPATH=$ORACLE_HOME/jlib:$ORACLE_HOME/rdbms/jlib; export CLASSPATH


Ok copy over your Oracle 11gR2 zip files to the oracle user’s home directory and unzip (“unzip filename1 && unzip filename2”).
“cd database/ && ./runInstaller”
I won’t go into too much detail here as this post is already stupid long, but you want to install a database and database software; it is relatively straight foward at this point.  Pick standard edition and leave the defaults alone except for Global database name (aka SID) use the SID you came up with in step 19.   You will also need to choose a password used for the sys and other Oracle accounts.
Keep rolling through the install until you reach the end.  If you get warnings that you are missing packages, try running “rpm -q packagename” and see if it exists just a newer version (this is HIGHLY likely especially if you ran yum update earlier).  As long as the package is on the system a newer version will be fine and you can click the ignore all error button and continue the installation.  Run the root scripts when told and finish up.
Not we finally get to install VM Manager!  Mount your Oracle VM Manager 3.1.1 iso (if not still mounted) and “runInstaller.sh”.  Choose option 2 for Production and start filling in the info for the database.  
Enter the FQDN of your host (don’t use localhost), enter the SID you picked, and specify the sys password used during install of Oracle Standard Edition.  Post 1521 is the default so if you didn’t change it during Oracle install leave this as is too.
You can leave the VM Manage schema as ovs or choose something else, and you will need to pick a password for all the various accounts setup for this VM Manager install.  There are crappy password requirements for the Weblogic account so use something with an upper case, lower case, and a number and nothing else for that.  e.g. “1DumbPassword”
Wait about 15 minutes for the install to complete.  At the end it should tell you to remove a file, go ahead and do so.  It will also display information on how to login.
Finally, you will want to install TightVNC so you can use the console viewer functionality in VM Manager (to get console access to your VMs).  "wget http://oss.oracle.com/oraclevm/manager/RPMS/tightvnc-java-1.3.9-3.noarch.rpm" and “rpm -Uvh tightvnc-java-1.3.9-3.noarch.rpm”.
Voila!  You should now have a working Oracle VM Manager 3.1.1 install fully production supported.  
I installed my Oracle VM Manager as a virtual machine on a VMware vSphere cluster.  I have no idea if this is supported or not as I couldn’t get a straight answer from anyone.  As far as I know I am within licensing terms as Oracle VM is “free.”  At least this is what I was told…
