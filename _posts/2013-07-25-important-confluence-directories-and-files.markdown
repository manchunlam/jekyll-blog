---
layout: post
title: "Confluence Directories and Files"
date: 2013-07-25 17:40
comments: true
categories: confluence
tags:
  - confluence
---

I can never remember what the `<confluence-install>` and `<conflunce-home>`
directories are. I'm going to write this down because I'm getting really tired
of googling it every time.

|name|location|
|-----|-----|
|`<confluence-install>`|`/opt/atlassian/confluence`|
|`<confluence-home>`|`/var/atlassian/application-data/confluence`|
|Log File|`<confluence-home>/logs/atlassian-confluence.log`|

<p></p>

The above are defaults if you use _Express Install_ to install Confluence on
Linux. The log file is a great place to start debugging failed plug-in
installations.
