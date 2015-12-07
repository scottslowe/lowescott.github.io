---
author: slowe
comments: true
date: 2006-09-28 21:37:11+00:00
layout: post
slug: cocoalicious-fix
title: Cocoalicious Fix
wordpress_id: 341
categories: Explanation
tags:
- Macintosh
- Web
---

As noted in [this comment](http://weblog.scifihifi.com/2006/08/12/delicious-api-url-switch/#comment-15131) on the [Sci-Fi Hi-Fi weblog](http://weblog.scifihifi.com/) article about the recent [problems with Cocoalicious](http://weblog.scifihifi.com/2006/08/12/delicious-api-url-switch/), it turns out that it may be necessary to change the del.icio.us API URI not only in the Preferences, but also in Keychain Access.

Huh? In Keychain Access? Yep, you heard that right. Changing the URI in Keychain Access from "http://" to "https://" and then relaunching Cocoalicious seems to fix the issue. Note that you'll have to re-enter your del.icio.us account password after making the change in Keychain Access, and note that you'll also end up with two entries in your login keychain for the del.icio.us API. One entry will have the "http://" prefix, and the second will have the "https://" prefix. I tried going back and deleting the non-SSL entry, but it just ends up getting recreated anyway so you might as well not worry about it.

I can't guarantee this will fix everyone, but it seems to have helped a number of us (for whatever reason).
