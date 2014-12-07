---
layout: post
title: "CentOS Setup (Part IV) - Install Package Group"
date: 2014-05-03 10:53:06 -0400
comments: true
categories: centos
---

CentOS provides `group`s, a bunch of related packages. For example, you'd like
to build something from source, CentOS got you covered! Just install the
`Development Tools` group of packages, and you're good to go.

You must be `root`.

1. See all the available groups

    ```
    yum grouplist
    ```
<!-- more -->

1. Install `Development Tools`

    ```
    yum -y groupinstall "Development Tools"
    # -y: say yes to every package in the group
    ```
