---
author: slowe
comments: true
date: 2012-04-30 09:00:00+00:00
layout: post
slug: updated-launchd-property-list-file-for-synergy
title: Updated launchd Property List File for Synergy
wordpress_id: 2601
categories: Information
tags:
- Macintosh
- OSS
---

After posting my article on [running the Synergy server automatically on OS X Lion][1], a reader added a comment suggesting that it wasn't recommended to use a shell script to launch a process via `launchd`. I haven't been able to find any information to back up that recommendation, but I did create a new `launchd` property list file that doesn't require (or use) a shell script to start `synergys`.

Here's the updated property list file:

{% highlight xml %}
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE plist PUBLIC "-//Apple Computer/DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
<key>Label</key>
<string>org.synergy-foss.synergys</string>
<key>ProgramArguments</key>
<array>
<string>/usr/bin/synergys</string>
<string>-f</string>
<string>-c</string>
<string>/etc/synergy.conf</string>
</array>
<key>RunAtLoad</key>
<true/>
<key>ServiceDescription</key>
<string>Synergy server daemon</string>
</dict>
</plist>
{% endhighlight %}

After making the changes and rebooting, everything seems to work just fine. Thanks for the tip!

[1]: {% post_url 2012-04-24-running-synergy-server-automatically-on-os-x-lion %}
