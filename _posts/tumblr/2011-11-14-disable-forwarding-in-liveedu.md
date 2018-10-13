---
layout: post
title: disable forwarding in live@edu
date: '2011-11-14T12:48:00+00:00'
tags:
- Live@edu
- hacklol
tumblr_url: http://userdel.com/post/12801210349/disable-forwarding-in-liveedu
---
The Lost and Found Identity blog has a great article on how to disable users from forwarding mail in Live@edu, but I just wanted to dumb down the steps a little bit.  First make a remote PowerShell connection to Live@edu and then do the following:
Set-RemoteDomain Default -AutoForwardEnabled $false
New-ManagementRole -Parent MyBaseOptions_DefaultMailboxPlan -Name MyBaseOptions_DefaultMailboxPlan_NoForwarding
Set-ManagementRoleEntry MyBaseOptions_DefaultMailboxPlan_NoForwarding\Set-Mailbox -Parameters DeliverToMailboxAndForward,ForwardingAddress,ForwardingSmtpAddress –RemoveParameter
Set-ManagementRoleEntry MyBaseOptions_DefaultMailboxPlan_NoForwarding\New-InboxRule -Parameters ForwardAsAttachmentTo,ForwardTo,RedirectTo –RemoveParameter
New-ManagementRoleAssignment -Policy RoleAssignmentPolicy-DefaultMailboxPlan -Role MyBaseOptions_DefaultMailboxPlan_NoForwarding
Remove-ManagementRoleAssignment MyBaseOptions_DefaultMailboxPlan-RoleAssignmentPolicy-DefaultMai
This will prevent your users from being able to forward any mail by disabling the GUI options and removing the Inbox Rule option that allows forwarding.
