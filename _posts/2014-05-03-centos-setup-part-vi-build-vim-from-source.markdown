---
layout: post
title: "CentOS Setup (Part VI) - Build vim from Source"
date: 2014-05-03 11:13:35 -0400
comments: true
categories: centos
tags:
  - centos
  - linux
---

We will compile vim from source because the stock vim in repos doesn't have
ruby, perl, or python support.

Log in as `root`

<!-- more -->

1. Install system-wide ruby, and other languages

    ```sh
    yum groupinstall "Desktop" "X Window System" "Fonts"
    yum install ruby perl-devel python-devel ruby-devel perl-ExtUtils-Embed \
      ncurses-devel libX11 libX11-devel libXt-devel libXt libSM libSM-devel \
      gtk2
    ```

1. Install `mercurial` to get vim source from Google Code

    ```sh
    yum install mercurial
    mkdir Downloads
    cd Downloads
    hg clone https://vim.googlecode.com/hg/ vim
    ```

3. Configure vim build

    ```sh
    ./configure --with-features=huge --enable-perlinterp --enable-rubyinterp \
      --enable-pythoninterp --with-x=yes --enable-gui=gnome2 \
      --enable-gnome-check
    ```

    If you don't want to use `gnome`, please replace the `gnome`-related switches to

    ```sh
    --enable-gui=gtk2 --enable-gtk2-check
    ```

    **Note**:

    If the configuration fails, you **must** do the following before
    re-configuring

    ```sh
    make distclean
    ```

    Just `make clean` is **not enough**.

4. Build vim

    ```
    sudo make install

    ```

    `sudo` is necessary because the build will install `vim` to
      `/usr/local/bin`, which needs `su` privileges.

**Note**

Don't remove the `~/Downloads/vim` directory, it's necessary for uninstalling
`vim`.

### Uninstall

To uninstall `vim`, please do

```sh
cd Downloads/vim
make uninstall
```
