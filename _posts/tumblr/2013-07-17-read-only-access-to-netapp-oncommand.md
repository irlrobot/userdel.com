---
layout: post
title: read-only access to netapp oncommand
date: '2013-07-17T12:29:00+00:00'
tags:
- netapp
- san
- storage
- oncommand
- cli
tumblr_url: http://userdel.com/post/55712125492/read-only-access-to-netapp-oncommand
---
Special thanks to Dan’s Tech Notes for info on creating a read-only group in NetApp OnCommand.  This also works on Data ONTAP 8.

useradmin role add oncommand-login -a login-http-admin,api-system-get-*

useradmin role add oncommand-view -a api-aggr-list-info,api-disk-sanown-list-info,api-license-list-info,api-options-get,api-perf-object-get-instances,api-snmp-status,api-volume-list-info*,cli-priv,api-aggr-options-list-info,api-aggr-check-spare-low,api-cf-status

useradmin role add oncommand-volumes-view -a api-volume-get-root-name,api-snapshot-reserve-list-info,api-volume-get-language,api-volume-options-list-info,cli-date

useradmin role add oncommand-sharedfolders-view -a api-cifs-share-list-iter*,api-nfs-exportfs-list-rules,api-cifs-session-list-iter*

useradmin role add oncommand-qtree-view -a api-qtree-list-iter*

useradmin role add oncommand-disk-view -a api-system-cli,api-disk-list-info,cli-options

useradmin role add oncommand-aggr-view -a api-aggr-get-root-name,api-snapshot-list-info


useradmin group add oncommand-storage-view -r oncommand-login,oncommand-view,oncommand-volumes-view,oncommand-sharedfolders-view,oncommand-qtree-view,oncommand-disk-view,oncommand-aggr-view
