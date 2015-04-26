---
author: slowe
comments: true
date: 2008-06-18 11:05:17+00:00
layout: post
slug: finding-unix-enabled-accounts-in-active-directory-mmc
title: Finding UNIX-Enabled Accounts in Active Directory MMC
wordpress_id: 744
categories: Information
tags:
- ActiveDirectory
- Interoperability
- Microsoft
- Windows
---

In UNIX/Linux integration scenarios, it's useful to know which accounts have been UNIX-enabled, i.e., have had the UID number, NIS domain, login shell, and home directory attributes configured.

It's certainly very possible to do this with command-line tools such as AdFind or DsQuery, but users may also find it useful to have a saved query available within the Active Directory Users & Computers console for easy reference.

The way to do this is define a custom query using this string:

	(objectCategory=Person)(objectClass=User)(uidNumber=*)

If you add _just this text_ and nothing else in the "Find Custom Search" dialog box (the Advanced tab), then the console will automatically add ampersands and additional parentheses to turn it into a "proper" LDAP query that will show you any account that has a UID number configured. Certainly, additional fields like loginShell or unixHomeDirectory could be added as well, but this query will probably be sufficient for most instances.

I started not to publish this, but figured if I couldn't remember the exact syntax then someone else might not be able to remember the syntax either. This one is as much for me as it is for others.
