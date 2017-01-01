---
author: slowe
comments: true
date: 2016-12-31
layout: post
title: OPML-to-Markdown Conversion Script
categories: Information
tags:
- Linux
- CLI
- Markdown
---

In this post, I'd like to share a script I wrote to help with converting Outline Processor Markup Language (OPML) documents to Markdown. If you read the recent [update on my Linux migration plans][xref-2], you may recall that I identified OPML files (created in OmniOutliner) as an area where some work was going to be required. This script is the result of my efforts in this area.

&lt;aside&gt;Before I continue, I want to very briefly point out that this script was written to help in _my_ specific use case. It's quite likely that you'll want or need to adjust the behaviors of this script in order to meet the needs of your particular use case.&lt;/aside&gt;

This script takes advantage of two tools: `pandoc` and `sed`. `pandoc` is [a third-party tool][link-1] that is easily installed on Ubuntu using `apt` or `apt-get`. (I haven't checked other Linux distributions, but I suspect packages are available there as well.) `pandoc` is also available for OS X, making it a very handy cross-platform tool to have in my toolchest. (See [this post][xref-1] for more information on how you can use `pandoc` in a Markdown-heavy environment.) `sed`, of course, is a very well-known tool that is almost guaranteed to be available on just about any Linux distribution (and other UNIX-like OSes, including OS X). If you're interested in using this script, you'll want to first ensure you have these two tools present on your system.

Here's the script, heavily commented so as to make it easier to understand what's happening:

``` shell
#!/usr/bin/env bash

# Assign help text to variable for user later
HELP="Usage: opml2mmd [SOURCE] [DEST]"

# If the user supplied "--help", then provide help text
if [ $1 = "--help" ]; then
    echo $HELP
    echo
    exit
fi

# Ensure that exactly 2 parameters were given
# Display error message and help text otherwise
if [ $# -ne 2 ]; then
    echo "Error: Incorrect number of parameters"
    echo
    echo $HELP
    echo
    exit
fi

# Check that source exists and is a normal file
# Display error message otherwise
if [ ! -f $1 ]; then
    echo "Error: invalid source file supplied"
    echo
    exit
fi

# Assign parameters to variables for use later
SRC=$1
DST=$2

# Use pandoc to convert OPML to MMD (assumes pandoc is in the search path);
# then use sed to transform the document (assumes sed is in the search path)
pandoc --from=opml --to=markdown_mmd --atx-headers $SRC | \
sed -e 's/^## /* /g' | \
sed -e 's/^### /    * /g' | \
sed -e 's/^#### /        * /g' > $DST
```

Although the script is really straightforward, let's break it down just a bit:

* The bulk of the script is error detection/error prevention/validation---making sure that the right number of parameters is supplied, that the source file exists, etc.
* After the validation, the script takes the first parameter as the source, and the second parameter as the destination.
* The heart of the script is the `pandoc` command toward the end. This line tells `pandoc` to take an OPML file (`--from=opml`) and convert it to MultiMarkdown (`to=markdown_mmd`). The `--atx-headers` option instructs `pandoc` to use the standard hash marks (`#`) to denote header lines.
* The output of the file conversion is passed to STDOUT by `pandoc`, which is then passed through `sed` three times to convert Markdown headings to bulleted lists. (Additional passes may be needed, depending on the number of heading levels in your document.) _This is what makes this script useful for me (more on that in a moment)._ Finally, the output is redirected to the destination file.

I'd like to briefly talk about why I convert Markdown headings to bulleted lists. See, I use OPML as an outline that includes data, not just headings. Most OPML-to-Markdown conversion tools, including `pandoc`, simply assume that each line in an OPML file should be a heading. For me (and this may vary for others), any second-level or higher entries in the OPML file are data, _not_ headings. Thus, I use `sed` and regular expressions to convert second-level and third-level headings into bulleted lists.

So far, I've tested this on a number of my OPML files, and it seems to work well. I'm open to suggestions for improvement, of course, which is why I've published this in [my GitHub "scripts" repository][link-2]. If you see a better way to handle things in the script, please feel free to fork the repository, make your changes, and submit a pull request.

Thanks!



[link-1]: http://pandoc.org/
[link-2]: https://github.com/lowescott/scripts
[xref-1]: {% post_url 2014-05-09-some-useful-markdown-tols-for-os-x %}
[xref-2]: {% post_url 2016-12-16-linux-migration-initial-progress-report %}
