---
author: slowe
comments: false
date: 2005-07-18 09:18:41+00:00
layout: post
slug: minor-linux-ad-hiccup-fixed-hopefully
title: Minor Linux-AD Hiccup Fixed (Hopefully)
wordpress_id: 53
categories: Explanation
tags:
- Interoperability
- ActiveDirectory
- Kerberos
- Linux
- Microsoft
- Windows
---

I think I have resolved one minor Linux-AD integration hiccup. In setting up the Kerberos authentication, various instructions I had found (including some from Microsoft) indicated I needed to create a _user_ account for the Linux servers, then use `ktpass` to generate the Kerberos keytab. This works, but being the stickler for detail that I am, I really wanted to use a computer account instead of a user account.

After fiddling with it for a while, I finally managed to make it work. The `ktpass` command should look something like this:

	ktpass -princ host/fqdn@REALM -mapuser DOMAIN\name$
	-crypto DES-CBC-MD5 -pass password -ptype KRB5_NT_PRINCIPAL
	-out filename

The missing piece, for me, was specifying "DOMAIN\name$" for the mapuser parameter. Without it, the command kept generating an error.

I don't know for sure that this will work, but I will be testing this within the next day or so to see how it goes.
