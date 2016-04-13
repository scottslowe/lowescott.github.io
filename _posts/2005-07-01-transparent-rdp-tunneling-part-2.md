---
author: slowe
comments: false
date: 2005-07-01 22:54:45+00:00
layout: post
slug: transparent-rdp-tunneling-part-2
title: Transparent RDP Tunneling, Part 2
wordpress_id: 29
categories: Information
tags:
- Networking
- Encryption
- OSS
- SSL
---

After some fiddling around with [Stunnel](http://stunnel.mirt.net/index.html) on [OpenBSD](http://www.openbsd.org/), I got the transparent RDP tunneling inside SSL working. I still need to run some network captures with Ethereal or similar to make sure that the traffic is encrypted, but I don't see any reason why it won't be. Overall, the process was a bit easier than I expected. Once I get it better documented, I'll find an appropriate format in which to distribute the information for others to use in their own networks.
