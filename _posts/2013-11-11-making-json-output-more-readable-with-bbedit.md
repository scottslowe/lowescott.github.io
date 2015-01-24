---
author: slowe
comments: true
date: 2013-11-11 09:00:00+00:00
layout: post
slug: making-json-output-more-readable-with-bbedit
title: Making JSON Output More Readable with BBEdit
wordpress_id: 3328
categories:
- Tutorial
tags:
- JSON
- Linux
- Macintosh
- Productivity
- Web
---

In this post I'm going to show you how to make JSON (JavaScript Object Notation) output more readable using a BBEdit Text Filter. This post comes out of some recent work I've done in learning how to interact with various REST APIs. My initial REST API explorations have focused on the NVP/NSX API, but I plan to soon expand my explorations to include other APIs, like OpenStack.

&lt;aside&gt;You might be wondering _why_ I'm exploring REST APIs and stuff like JSON. I believe that having a better understanding of the APIs these products use will help drive a deeper and more complete understanding of the underlying products. I could be wrongtime will tell.&lt;/aside&gt;

BBEdit Text Filters, as you may already know, simply take the current text (or selected text) in BBEdit, do something to it, and then output the result. The "do something to it" is, of course, the magic. You can, for example---and this something that I do---use the MultiMarkdown command-line executable to transform a (Multi)Markdown document in BBEdit to HTML. All that is required is to place the script (or a link to the script) in the `~/Library/Application Support/BBEdit/Text Filters` directory. The script just needs to accept input on STDIN, transform it in whatever way you want, and spit out the results on STDOUT. BBEdit does the rest.

In this case, you're going to use an extremely simple Bash shell script containing a single Python command to transform JSON-serialized output into a more human-readable format.

First, let's take a look at some JSON-serialized output. Here's the output from an API call to NVP/NSX to list the logical switches:

{% gist lowescott/7370184 %}

(To view the information if the code block isn't available, click [here](https://gist.github.com/lowescott/7370184).)

It _is_ human-readable, but just barely. How can we make this a bit easier for humans to read and parse? Well, it turns out that OS X (and probably most recent flavors of Linux) come with a version of Python pre-installed, and the pre-installed version of Python comes with the ability to "prettify" (make more human readable) JSON text. (In the case of OS X 10.8 "Mountain Lion", the pre-installed version of Python is version 2.7.2.) With grateful thanks to the folks on Twitter who introduced me to this trick, the command you would use in this instance is as follows:

    python -m json.tool

Very simple, right? To turn this into a BBEdit Text Filter, we need only wrap this into a very simple shell script, such as this:

{% gist lowescott/7364842 %}

(If you aren't able to see the code block above, please click [here](https://gist.github.com/lowescott/7364842).)

Place this script (or a link to this script) in the `~/Library/Application Support/BBEdit/Text Filters` directory, restart BBEdit, and you should be good to go. Now you can copy and paste the output from an API call like the output above, run it through this text filter, and get output that looks like this:

{% gist lowescott/7370142 %}

(Click [here](https://gist.github.com/lowescott/7370142) if the code block above isn't visible.)

Given that I'm new to a lot of this stuff, I'm sure that I have probably overlooked something along the way. There might be better and/or more efficient ways of handling this, or better tools to use. If you have any suggestions on how to improve any of this---or just suggestions on how I might do better in my API explorations---feel free to speak out in the comments below.
