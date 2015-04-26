---
author: slowe
comments: false
date: 2006-04-17 21:45:50+00:00
layout: post
slug: freenas-on-esx-server
title: FreeNAS on ESX Server
wordpress_id: 225
categories: Information
tags:
- BSD
- ESX
- NAS
- Virtualization
- VMware
- Interoperability
---

As part of ongoing interoperability testing with [ESX Server](http://www.vmware.com/products/esx/), I tested running [FreeNAS](http://www.freenas.org/) (version 0.65) on ESX Server 2.5.3 today. Since FreeNAS is based on [FreeBSD](http://www.freebsd.org/) (which [VMware](http://www.vmware.com/) states is a supported guest operating system for ESX Server), I didn't really expect any major surprises. I was wrong.

Basically, I couldn't make it work. Despite trying both the BusLogic SCSI adapter (the default) and the LSI Logic adapter, the FreeNAS distribution wouldn't see the virtualized SCSI hard disks, and therefore I could never install FreeNAS to the hard disk for use. Without the XML configuration file on a read/write media, FreeNAS lost its settings (such as the IP address or the network interface to use) every time it rebooted.

It's odd that FreeBSD, a supported guest OS, didn't appear to work, yet I was able to make [OpenBSD](http://www.openbsd.org/) (an _unsupported_ guest OS) run without any major problems.

Anyone have any tips for making FreeNAS 0.65 work under VMware ESX Server?
