---
author: slowe
comments: true
date: 2008-12-05 09:30:11+00:00
layout: post
slug: vmware-srm-10-update-1-released
title: VMware SRM 1.0 Update 1 Released
wordpress_id: 1085
categories: News
tags:
- NFS
- Virtualization
- VMware
- VMwareSRM
---

Many thanks to Dave Lawrence, aka VMguy, for the heads-up: Update 1 for VMware Site Recovery Manager 1.0 [has been released](http://vmguy.com/wordpress/index.php/archives/263). Missing in this update: NFS support. I mention that only because I heard numerous references to NFS Support in SRM 1.0U1 at NetApp Insight a few weeks ago. Of course, they also mentioned a March 2009 timeframe, so I was a bit surprised when I saw that Update 1 had been released.

However, there are plenty of other goodies besides NFS support available in Update 1 of SRM 1.0:

* SRM has separated the permission to test a recovery plan and to actually run a recovery plan. This allows more junior admins to test the plan, but reserve actually running the plan for a more senior admin, for example.

* RDM support, which enables failover for MSCS clusters

* Batch IP property customization

And more, but for the all the details, see Dave's post or [the Release Notes!](http://www.vmware.com/support/srm/srm_10_releasenotes.html)
