---
author: slowe
comments: true
date: 2013-12-17 09:00:00+00:00
layout: post
slug: updating-ubuntu-cloud-archive-support-with-puppet
title: Updating Ubuntu Cloud Archive Support with Puppet
wordpress_id: 3386
categories:
- Linux
tags:
- Automation
- Linux
- OpenStack
- Puppet
- Ubuntu
---

Some time ago, I showed you [how to use Puppet to add Ubuntu Cloud Archive support][1] to your Ubuntu installation. Since that time, [OpenStack](http://www.openstack.org/) has had a new release (the Havana release) and the Ubuntu Cloud Archive repository has been updated with new packages to support the Havana release. In this post, I'll show you an updated snippet of code to take advantage of these newer packages in the Ubuntu Cloud Archive repository.

For reference, here's the original Puppet code I posted in the first article:

{% gist lowescott/6827241 %}

(If you can't see the code snippet above, please click [here](https://gist.github.com/lowescott/6827241).)

That points your Ubuntu installation to the Grizzly packages.

Here's updated code that will point your installation to the appropriate packages to support OpenStack's Havana release:

{% gist lowescott/7949509 %}

(Click [here](https://gist.github.com/lowescott/7949509) if you can't see the code snippet above.)

As you can see, there is only one small change between the two code snippets: changing "precise-updates/grizzly" in the first to "precise-updates/havana" in the second. (Naturally, this assumes you're using Ubuntu 12.04, the latest LTS release as of this writing.) I know this seems like a pretty simple thing to post, but I wanted to include it here for the sake of completeness and the benefit of future readers.

Feel free to speak up in the comments with any questions, suggestions, or corrections.

[1]: {% post_url 2013-10-04-using-puppet-for-ubuntu-cloud-archive-support %}
