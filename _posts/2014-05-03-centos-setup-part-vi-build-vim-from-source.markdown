---
layout: post
title: "CentOS Setup (Part VI) - Build vim from Source"
date: 2014-05-03 11:13:35 -0400
comments: true
categories: centos
---

We will compile vim from source because the stock vim in repos doesn't have
ruby, perl, or python support.

Log in as `root`

<!-- more -->

1. Install system-wide ruby, and other languages

    ```
    yum install ruby perl-devel python-devel ruby-devel perl-ExtUtils-Embed ncurses-devel
    ```

1. Install `mercurial` to get vim source from Google Code

    ```
    yum install mercurial
    mkdir Downloads
    cd Downloads
    hg clone https://vim.googlecode.com/hg/ vim
    ```

3. Configure vim build

    ```
    ./configure --with-features=huge --enable-perlinterp --enable-rubyinterp --enable-pythoninterp
    ```

4. Build vim

    ```
    make install
    ```
