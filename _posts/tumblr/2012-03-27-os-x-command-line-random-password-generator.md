---
layout: post
title: os x command line random password generator
date: '2012-03-27T05:59:00+00:00'
tags:
- os x
- nix
- cli
- weeee
tumblr_url: http://userdel.com/post/20006623380/os-x-command-line-random-password-generator
---
If you want a quick little random password generator (uppercase, lowercase, and numbers) from the terminal in OS X you can add something like this to your .bashrc

randompass() {
        LANG=C
        local l=$1
        [ “$l” == “” ] && l=12
        tr -dc A-Za-z0-9_ < /dev/urandom | head -c ${l} | xargs
}

It defaults to 12 characters but takes any numeric argument.  So usage to create a 21 character random password would be

randompass 21

Make sure to source .bashrc after you add that to give it a try.  If you haven’t already created .bashrc and .bash_profile on your Mac, do that first and then add in the following to .bash_profile

source ~/.bashrc

This will also work for any other *nix as well.
