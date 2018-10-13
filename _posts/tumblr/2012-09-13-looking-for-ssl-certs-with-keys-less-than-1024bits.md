---
layout: post
title: looking for ssl certs with keys less than 1024bits
date: '2012-09-13T05:50:16+00:00'
tags:
- windows
- security
- nmap
- ssl
tumblr_url: http://userdel.com/post/31459018852/looking-for-ssl-certs-with-keys-less-than-1024bits
---
On September 11, 2012 Microsoft released an update that will block SSL certificates that use RSA keys less than 1024bits.  If you are looking for a way to discover if there are weak certificates in use on your network one tool you can use is good ol nmap.  nmap has a handy dandy scripting engine that you can use to do things like look for certain vulnerabilities.  Lucky for us their is a script built into the default bundle that comes with nmap that we can use to find SSL certs and their bit length.
A basic scan would look like this dumping everything to standard out:

nmap -sV -sC -v network/subnet

If you have a lot of hosts to scan you probably need a report:

nmap -sV -sC -v –webxml -oX sslCerts.xml 192.168.1.1/24
xsltproc sslCerts.xml sslCerts.html

Then you can open sslCerts.html in your browser and voila.  This assumes you have xsltproc available on your OS of course.  
