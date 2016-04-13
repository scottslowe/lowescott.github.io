---
author: slowe
comments: false
date: 2005-06-29 23:48:12+00:00
layout: post
slug: transparent-rdp-tunneling
title: Transparent RDP Tunneling
wordpress_id: 26
categories: Information
tags:
- Networking
- BSD
- Encryption
- SSL
---

As part of my experimentation with [OpenBSD](http://www.openbsd.org/) 3.7, I'm going to try to setup a way of transparently tunneling RDP (Remote Desktop Protocol, used by Windows Remote Desktop/Terminal Services) inside SSL. I'm thinking that I can use IP aliases and [Stunnel](http://stunnel.mirt.net/index.html) to have "ordinary" RDP encapsulated in SSL by Stunnel and then passed off to another instance of Stunnel at the other end. Then, from the RDP client, I just connect to one of the IP aliases and the rest is handled transparently.

When I get it working, I'll post more details here as well as on the Mercurion Systems web site.
