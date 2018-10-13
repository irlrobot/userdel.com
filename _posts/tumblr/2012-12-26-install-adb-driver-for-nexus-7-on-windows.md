---
layout: post
title: install adb driver for nexus 7 on windows
date: '2012-12-26T13:25:33+00:00'
tags:
- android
- windows
- nexus
- blerg
tumblr_url: http://userdel.com/post/38893898715/install-adb-driver-for-nexus-7-on-windows
---
If you have a Nexus 7 and you are following the developer.android.com tutorial and trying to run your first Android app you may be wondering why ADT won’t see your device.  Thanks to this helpful article I found the solution:
In ADT go to the ‘Window’ menu at the top and then select ''Android SDK Manager’ from the dropdown.  A new window should open and start loading available things to download.
Under the ''Extras’ section, look for ''Google USB Driver’ then install it by ticking the box and clicking “Install packages…”.
Go to Device Manager in Windows and you should see your Nexus under ''Other devices’ with a yellow exclamation mark indicating its missing a driver.  Right click on it and choose ''Update driver software’.  When it asks for the driver location it will be in your ADT bundle directory at "adt-bundle-windows\sdk\extras\google\usb_driver".
Finish through the driver wizard and plug in your Nexus 7.  Be sure USB debugging is enabled.
