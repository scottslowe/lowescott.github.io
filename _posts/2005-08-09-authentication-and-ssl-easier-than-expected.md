---
author: slowe
comments: false
date: 2005-08-09 10:42:26+00:00
layout: post
slug: authentication-and-ssl-easier-than-expected
title: Authentication and SSL Easier Than Expected
wordpress_id: 71
categories: Information
tags:
- Collaboration
- SSL
- OSS
---

My work with [INN](http://www.isc.org/products/INN/) 2.3.5 as an internal news server is progressing, and I must admit that the configuration of authentication and SSL is going well. Authentication works like a champ, leveraging PAM and therefore automatically leveraging the Kerberos/LDAP integration with Active Directory I implemented a short while ago. The SSL stuff is just a bit trickier; I initially tried the old faithful [Stunnel](http://stunnel.mirt.net/index.html), but found that INN thought the connection was coming from itself and not a reader. That caused INN to respond differently. I'll start looking at native SSL support within INN next, but that can wait until tomorrow.
