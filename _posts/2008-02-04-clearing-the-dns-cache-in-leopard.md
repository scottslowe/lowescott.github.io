---
author: slowe
comments: true
date: 2008-02-04 16:13:41+00:00
layout: post
slug: clearing-the-dns-cache-in-leopard
title: Clearing the DNS Cache in Leopard
wordpress_id: 622
categories: Tutorial
tags:
- Macintosh
- Networking
---

In previous versions of Mac OS X, I could use this command to flush the DNS resolver cache:

	lookupd -flushcache

However, in Mac OS X version 10.5 "Leopard," this command no longer works! I had an occasion today where I needed to flush the DNS resolver cache due to a configuration error in the lab. Fortunately a quick Google search turned up [this page](http://www.hongkiat.com/blog/how-to-clear-dns-cache-in-mac-osx-leopard/), where I found that the correct command to use in Leopard is this one:

	dscacheutil -flushcache

Works like a champ!
