---
layout: post
title: sccm wmi queries (wql) for building collections containing only all servers
  or all workstations
date: '2012-12-14T07:18:29+00:00'
tags:
- microsoft
- sccm
- systems center
- wmi
- wql
- windows
tumblr_url: http://userdel.com/post/37909699664/sccm-wmi-queries-wql-for-building-collections
---
If you want to build a collection in SCCM for “All Servers” or “All Workstations” here are two WMI queries you can use.
All Servers

select SMS_R_SYSTEM.ResourceID,SMS_R_SYSTEM.ResourceType,SMS_R_SYSTEM.Name,SMS_R_SYSTEM.SMSUniqueIdentifier,SMS_R_SYSTEM.ResourceDomainORWorkgroup,SMS_R_SYSTEM.Client from SMS_R_System inner join SMS_G_System_SYSTEM on SMS_G_System_SYSTEM.ResourceId = SMS_R_System.ResourceId where SMS_G_System_SYSTEM.SystemRole = “Server”

All Workstations/Desktops

select SMS_R_SYSTEM.ResourceID,SMS_R_SYSTEM.ResourceType,SMS_R_SYSTEM.Name,SMS_R_SYSTEM.SMSUniqueIdentifier,SMS_R_SYSTEM.ResourceDomainORWorkgroup,SMS_R_SYSTEM.Client from SMS_R_System inner join SMS_G_System_SYSTEM on SMS_G_System_SYSTEM.ResourceId = SMS_R_System.ResourceId where SMS_G_System_SYSTEM.SystemRole = “Workstation”
