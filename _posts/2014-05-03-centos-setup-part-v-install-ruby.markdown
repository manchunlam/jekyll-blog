---
layout: post
title: "CentOS Setup (Part V) - Install Ruby"
date: 2014-05-03 10:56:35 -0400
comments: true
categories: centos
---

CentOS comes with Ruby, but it's kind of old. Here, I will show you how to use
`rbenv` to get the latest and greatest ruby versions. And, you can switch ruby
version **per project**.

Log in as the user where any future applications will run under.

<!-- more -->

1. Get `rbenv`, and `ruby-build`

    These applications allow you to install different ruby versions on a
    per-application bases.

    1. `rbenv`
        * follow the [instructions](https://github.com/sstephenson/rbenv#basic-github-checkout)
    2. `ruby-build`
        * follow the [instructions](https://github.com/sstephenson/ruby-build#installing-as-an-rbenv-plugin-recommended)
2. Install desired version of ruby

    ```
    rbenv install --list # see all available ruby versions
    rbenv install 1.9.3-p545 # install this version
    rbenv rehash # let rbenv know new things are installed
    rbenv global 1.9.3-p545 # unless otherwise specified, the shell ruby version
    ```

3. Switch ruby version in your project

    ```
    cd <projectRoot>
    rbenv local <myRubyVersion> # e.g. rbenv local 1.9.3-p448
    ```
