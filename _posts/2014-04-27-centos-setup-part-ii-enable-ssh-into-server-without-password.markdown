---
layout: post
title: "CentOS Setup (Part II) - Enable SSH into Server without Password"
date: 2014-04-27 20:18:30 -0400
comments: true
categories: centos
---

Log in as whoever (with `sudo` privilege) you want to give access to.

1. Authorize a public key

    ```
    mkdir ~/.ssh
    chmod 700 ~/.ssh
    cd ~/.ssh
    touch .authorized_keys
    vi .authorized_keys
    # copy the person's public key, and paste it into the file

    chmod 600 ~/.ssh/authorized_keys
    # to satisfy StrictModes in /etc/ssh/sshd_config (default)
    ```
<!-- more -->

2. Test password-less login

    ```
    # log out of server

    # from another computer
    ssh someuser@<ip-address>
    ```

    If you can log in without being prompted for a password, then you have
    successfully enabled password-less login.

3. Disable password login

    **Note**

    **Only** do this step if the previous step successful. Otherwise, you will
    be completely logged out of the server

    ```
    sudo su -
    vi /etc/ssh/sshd_config
    # find the line "PasswordAuthentication yes", and change it to
    # "PasswordAuthentication no"

    service sshd restart
    ```
