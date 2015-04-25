---
author: slowe
comments: false
date: 2005-07-07 22:54:40+00:00
layout: post
slug: stupid-tricks-with-the-mac-os-x-firewall
title: Stupid Tricks With The Mac OS X Firewall
wordpress_id: 37
categories: Rant
tags:
- BSD
- Macintosh
- Security
---

Here's an interesting way to block access to your [Mac OS X](http://www.apple.com/macosx/) system. Simply modify your ipfw script to block traffic to or from the 127.0.0.0/8 network. When you do this, your Mac will simply fail to log you in, instead presenting you with an endless spinning disk.

The only workaround is to hold down the Shift key while booting (to initiate a Safe Boot), then disable the StartupItem that launches and configures the firewall.

Of course, I speak from personal experience, having added the aforementioned rules in an effort to block spoofed traffic from accessing the loopback interface. Apparently, Mac OS X is different enough from [FreeBSD](http://www.freebsd.org/) that this advice (advocated on a couple of FreeBSD-related sites I found while searching for ipfw information) is _not_ recommended.
