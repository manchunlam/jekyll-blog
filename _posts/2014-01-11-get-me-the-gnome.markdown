---
layout: post
title: "Get Me the GNOME"
date: 2014-01-11 21:53:04 -0500
comments: true
categories: centos
---

Sometimes we want a GUI in Linux. However, most of the time we didn't know if
we want it until after the fact. So, here is how to install GNOME,

```sh
yum -y groupinstall "X Window System" "Desktop" "Fonts" "General Purpose Desktop"
```
