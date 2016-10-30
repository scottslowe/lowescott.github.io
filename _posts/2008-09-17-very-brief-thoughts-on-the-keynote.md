---
author: slowe
comments: true
date: 2008-09-17 12:22:24+00:00
layout: post
slug: very-brief-thoughts-on-the-keynote
title: Very Brief Thoughts on the Keynote
wordpress_id: 925
categories: Musing
tags:
- VDI
- Virtualization
- VMware
- VMworld2008
---

Now that the keynote has wrapped up, I just wanted to post a few very brief thoughts, perhaps questions, about the keynote and the technologies and initiatives discussed.

First off, as I have seen others point out on the VMworld Twitter broadcast channel, I wonder how well AppSpeed's remediation functionality would work with applications other than web-based applications. Not all applications can scale using additional VMs. Sure, you can generally scale web-based applications by throwing on more web server VMs, but what about Microsoft Exchange 2007? Or SQL Server 2008? Or some other database server? I speculated in the keynote liveblog that perhaps the hot-add functionality that VMware is supposed to be adding to future versions of ESX/ESXi will help, but there's been absolutely no discussion of that. At least, not that I've seen.

I also briefly mentioned in the keynote liveblog that I wonder how well some of these technologies would work in the offline VDI scenario.

Finally, there seems to be some feature/functionality conflicts between stuff like vStorage Thin Provisioning and VMware FT that have yet to be resolved. Granted, this is all prototype/pre-beta stuff so VMware has time to resolve this.

What about you? What kinds of things like this have you spotted?
