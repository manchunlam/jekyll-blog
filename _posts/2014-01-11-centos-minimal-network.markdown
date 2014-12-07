---
layout: post
title: "Centos Minimal Network"
date: 2014-01-11 21:31:32 -0500
comments: true
categories: centos
---

Centos minimal is small, so it's really quick to spin up a VM with it. The
problem is, a lot of things are **turned off** for you.

Even network!

<!-- more -->

To enable your network, do

1. `vi /etc/sysconfig/network-scripts/ifcfg-eth0`
2. In the file, change the settings to the following

    ```text
    DEVICE=eth0
    BOOTPROTO=dhcp
    ONBOOT=yes
    NM_CONTROLLED=no # "NM" stands for Network Manager, it's a GNOME thing
    ```

3. Restart the network service

    ```sh
    service network restart
    ```

4. Check your IP, and ping some websites to verify it's working

    ```sh
    ifconfig eth0
    ping google.com
    ```
