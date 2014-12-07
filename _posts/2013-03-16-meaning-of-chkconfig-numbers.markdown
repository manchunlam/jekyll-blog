---
layout: post
title: "Meaning of chkconfig Numbers"
date: 2013-03-16 22:38
comments: false
categories: centos
---

I always wonder what the numbers after `chkconfig` means.

```sh
#!/bin/sh
#
# /etc/init.d/mysystem
# Subsystem file for "MySystem" server
#
# chkconfig: 2345 95 05 
# description: MySystem server daemon
```

<!-- more -->

Looking at line 6,

1. 2345: this `service` is on at run-levels 2, 3, 4, and 5
2. 95: `service` will start with priority 95 (one of the last ones)
3. 05: `service` will deactivate with priority 05 (one of the first ones)

Read this [page](http://www.tldp.org/HOWTO/HighQuality-Apps-HOWTO/boot.html#boot.script)
for a thorough explanation.
