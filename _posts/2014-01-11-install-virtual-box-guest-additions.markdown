---
layout: post
title: "Install Virtual Box Guest Additions"
date: 2014-01-11 21:58:46 -0500
comments: true
categories: centos virtual-box
---

Virtual Box provides some pretty awesome features to the guest OS, like
"Drag and drop files", "Copy and Paste" between host and guest OS.

Installation with commandline is pretty straight forward

<!-- more -->

```sh
# prep work
yum update kernel*
yum install gcc kernel-devel kernel-headers dkms make bzip2 perl
export KERN_DIR=/usr/src/kernels/`uname -r` # get current kernel version
cd /usr/src/kernels/`uname -r`/include/drm
ln -s /usr/include/drm/drm.h .
ln -s /usr/include/drm/drm_fourcc.h .
ln -s /usr/include/drm/drm_mode.h .
ln -s /usr/include/drm/drm_sarea.h .
shutdown -r now
# mounting and installing Guest Additions
mkdir /media/VirtualBoxGuestAdditions
mount -r /dev/cdrom /media/VirtualBoxGuestAdditions # -r means mount it as read-only
/media/VirtualBoxGuestAdditions/./VBoxLinuxAdditions.run
shutdown -r now
```
