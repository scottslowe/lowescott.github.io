---
author: slowe
comments: true
date: 2012-11-12 11:29:10+00:00
layout: post
slug: libvirt-ovs-integration-revisited
title: Libvirt-OVS Integration Revisited
wordpress_id: 2943
categories:
- Interoperability
- Linux
- Networking
- Virtualization
tags:
- Interoperability
- Libvirt
- Linux
- Networking
- OSS
- OVS
- Virtualization
---

A few days ago, I posted an article about [using VLANs with Open vSwitch (OVS) and libvirt][1]. In that article, I stated that libvirt 1.0.0 was needed. Unfortunately (or maybe fortunately?), I was wrong. The libvirt-OVS integration works in earlier versions, too.

In my [earlier OVS-libvirt post][1], I supplied this snippet of XML to define a libvirt network that you could use with OVS:

{% gist lowescott/4057683 %}

You would use that libvirt network definition in conjunction with a domain configuration like this:

I just tested this on Ubuntu 12.04.1 with libvirt 0.10.2, and _it worked just fine._ I think the problems I experienced in my earlier testing were all related to incorrect XML configurations. Some other write-ups of the libvirt-OVS integration seem to imply that you need to use the `profileid` parameter to link the domain XML configuration and the network XML configuration, but my testing seems to show that the real link is the portgroup name.

I haven't yet tested this on earlier versions of libvirt, but I can confirm that it works with Ubuntu 12.04 using manually compiled versions of libvirt 0.10.2 and libvirt 1.0.0.

If anyone has any additional information to share, please speak up in the comments.

[1]: {% post_url 2012-11-07-using-vlans-with-ovs-and-libvirt %}
