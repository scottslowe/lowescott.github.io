---
author: slowe
comments: true
date: 2006-11-24 22:28:29+00:00
layout: post
slug: virtualcenter-patch-released
title: VirtualCenter Patch Released
wordpress_id: 371
categories: News
tags:
- Security
- Virtualization
- VMware
---

(Thanks to [virtualization.info](http://www.virtualization.info/) for [alerting us](http://www.virtualization.info/2006/11/security-vmware-virtualcenter-client.html) to this release.) VMware has posted an [update to VirtualCenter](http://www.vmware.com/download/vi/vc-201-200611-patch.html) that addresses a potential security problem with the Virtual Infrastructure clients and the VirtualCenter server. Apparently, the potential security flaw is that SSL server certificate validation was not being performed, allowing a potential man-in-the-middle attack. The update enables the validation of SSL certificates; the exact procedure for how this is done is documented in [this VMware KB article](http://kb.vmware.com/kb/4646606).
