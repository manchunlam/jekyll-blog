---
layout: post
title: "Development Tools"
date: 2014-01-11 21:47:47 -0500
comments: true
categories: centos
tags:
  - centos
  - linux
---

To build anything in Linux, you need `make`, `autoconf`, etc. To get them, we
need _Develop Tools_ group in Centos

```sh
yum -y groupinstall "Development Tools" # -y means say yes to everything
```

Now you can compile things from source!
