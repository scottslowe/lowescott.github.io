---
author: slowe
comments: false
date: 2006-01-14 11:55:46+00:00
layout: post
slug: cisco-nat-issue
title: Cisco NAT Issue
wordpress_id: 157
categories: Rant
tags:
- Cisco
- NAT
- Networking
- Security
---

I've been helping a customer try to resolve a network address translation (NAT) problem on a [Cisco](http://www.cisco.com/) router for the last week or so, and the solution to the problem is escaping me. What's worse, all the documentation I can find from Cisco says the current configuration is correct.

It's a really simple situation. Customer has a web server at their office that needs to be accessible from the outside. OK, fine, no problem, I use---in accordance with the Cisco documentation---the `ip nat inside source static` command to create a static NAT entry. I then use the appropriate `show` commands to verify that the static entry exists in the NAT table. It does.

However, when an external host goes to connect, it can't. The only way external hosts can connect is during that brief period of time after the internal web server initiates some communications to the outside world and the router "reinstates" the NAT entry, just as if the NAT entry was _not_ static. The only workaround we've found is to schedule a batch file that uses a `wget` statement to download a very small web page from an external host every 10 minutes. This keeps the NAT translation active and the web server is fully accessible from the outside world.

If anyone has any ideas as to why this doesn't work, please let me know.
