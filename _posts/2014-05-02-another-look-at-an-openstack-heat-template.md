---
author: slowe
comments: true
date: 2014-05-02 09:00:00+00:00
layout: post
slug: another-look-at-an-openstack-heat-template
title: Another Look at an OpenStack Heat Template
wordpress_id: 3448
categories:
- Explanation
tags:
- Automation
- Linux
- OpenStack
- OSS
- Interoperability
- Networking
- Virtualization
---

In an earlier post, I provided [an introduction to OpenStack Heat][1], and provided an example Heat template that launched two instances with a logical network and a logical router. Here I am going to provide another view of a Heat template that does the same thing, but uses YAML and the HOT format instead of JSON and the CFN format.

Here's the full template (click [here](https://gist.github.com/lowescott/1ed38b586a1751138c8d) if the code box below isn't showing up):

{% gist lowescott/1ed38b586a1751138c8d %}

I won't walk through the whole template again, but rather just talk briefly about a couple of the differences between this YAML-encoded template and the earlier JSON-encoded template:

* You'll note the syntax is _much_ simpler. JSON can trip you up on commas and such if you're not careful; YAML is simpler and cleaner.

* You'll note the built-in functions are different, as I pointed out in [my first Heat post][1]. Instead of using `Ref` to refer to an object defined elsewhere in the template, HOT uses `get_resource` instead.

Aside from these differences, you'll note that the resource types and properties match between the two; this is because resource types are separate and independent from the template format.

Feel free to post any questions, corrections, or clarifications in the comments below. Thanks for reading!

[1]: {% post_url 2014-05-01-an-introduction-to-openstack-heat %}
