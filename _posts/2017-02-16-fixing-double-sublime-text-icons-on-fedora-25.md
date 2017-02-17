---
author: slowe
comments: true
date: 2017-02-16
layout: post
title: Fixing Double Sublime Text Icons on Fedora 25
categories: Information
tags:
- Linux
- CLI
- Fedora
---

In [my previous post][xref-1] on how to install [Sublime Text 3][link-1] (ST3) on [Fedora 25][link-2], I mentioned that I have observed instances where launching ST3 via the `subl` command creates an additional icon in the Dash. While searching for a solution to an issue with LibreOffice icons, I found a fix for this problem.

The fix is to add this line to the `sublime-text.desktop` file (typically found in `/usr/share/applications`):

    StartupWMClass=subl

This tells Fedora and GNOME that when a window with the WMClass of "subl" appears, it should be considered a Sublime Text window. Once you add this line to the `sublime-text.desktop` file, then launching ST3 either via the GUI or via the `subl` command should create only a single ST3 icon in the Dash.

Now, back to trying to figure out this LibreOffice icon issue...



[link-1]: http://www.sublimetext.com/
[link-2]: https://getfedora.org/
[xref-1]: {% post_url 2017-02-09-installing-sublime-text-3-on-fedora-25 %}
