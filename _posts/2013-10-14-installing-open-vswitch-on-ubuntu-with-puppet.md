---
author: slowe
comments: true
date: 2013-10-14 09:00:00+00:00
layout: post
slug: installing-open-vswitch-on-ubuntu-with-puppet
title: Installing Open vSwitch on Ubuntu with Puppet
wordpress_id: 3311
categories:
- Explanation
tags:
- Automation
- Linux
- Networking
- OVS
- Puppet
- Ubuntu
---

In this post, I'll share with you some [Puppet](http://www.puppetlabs.com/) code that you can include in your manifests to install [Open vSwitch (OVS)](http://openvswitch.org/) packages on Ubuntu. This post, along with a number of others (like [using Puppet for Ubuntu Cloud Archive support][1] or [using Puppet to configure an Apt proxy][2]) stems from my work on building a new home lab in which I'll be doing some OpenStack and NSX testing.

This code makes a couple of assumptions:

1. It assumes that you've established an internal Apt repository (I created one using `reprepro`). In the code below, you'll see that I've used [the Puppet Labs Apt module](http://forge.puppetlabs.com/puppetlabs/apt) to define my internal Apt repository.

2. It assumes that you have Debian packages for OVS in that internal Apt repository. Depending on which version of OVS you need (I needed a newer version than was available in the public repositories), you might be able to get away with just using the public repositories.

OK, with the assumptions out of the way, let's have a look at the code:

{% gist lowescott/6938382 %}

(Click [here](https://gist.github.com/lowescott/6938382) if the code block above isn't visible.)

The code is fairly straightforward; the key is making sure that the appropriate packages are installed _before_ you attempt to install the OVS DKMS module. This is reflected in the `require` statement for the `openvswitch-datapath-dkms` package.

I've only tested this on Ubuntu 12.04 LTS, so use at your own risk on other distributions and other versions.

As always, I encourage you to participate in the discussion by adding your questions, thoughts, suggestions, and/or clarifications in the comments below. All courteous comments are welcome.

[1]: {% post_url 2013-10-04-using-puppet-for-ubuntu-cloud-archive-support %}
[2]: {% post_url 2013-10-10-using-puppet-to-configure-ubuntu-to-use-apt-cacher-ng %}
