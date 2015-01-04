---
layout: post
title: "CentOS Setup (Part I) - Add User with sudo Privilege"
date: 2014-04-27 20:08:16 -0400
comments: true
categories: centos
tags:
  - centos
  - linux
---

You must be `root`.

1. Update repo information, and upgrade packages

    ```
    yum list updates
    yum upgrade
    ```
<!-- more -->

2. Install `man`, so I can read command manuals/help file

    ```
    yum install man
    ```

3. Create a `group`

    In linux, all users belong to some groups.

    When creating a user, the
    recommended practice is to have at least one group with the same name as the
    user.

    ```
    cat /etc/group # see all existing groups
    groupadd someuser # add a group
    ```

2. Add user, and give it `sudo` privilege.

    ```
    cat /etc/passwd # see all existing users

    useradd -m -g someuser -G wheel -s /bin/bash someuser
    # -m: create home directory
    # -g: set initial group, usually the same as the username
    # -G: extra groups that the user belongs to. Use comma separated values
    #     for multiple groups
    #
    #     -G group1,group2,group3
    # -s: specify shell to use (can change later)

    passwd somesuser # set password for user

    vi /etc/pam.d/su
    # uncomment the line that reads "auth  required  pam_wheel.so use_uid"
    # explicitly enforces a user has to be in "wheel" group to use sudo

    yum install sudo
    visudo
    # uncomment the line that reads "%wheel  ALL=(ALL)  ALL"
    # allows "wheel" group users to run all commands (including sudo)

    # logout root, log in as somesuer
    # from a another computer, do `ssh someuser@<ip-address>`
    sudo -s
    # if you become root, then success! You are a "sudo-er".
    ```

4. Disable `root` login

    Now that you can log in as "sudo-er", there is no need to allow anyone to
    log in as `root`. For added security, disable SSH log in as `root`.

    ```
    vi /etc/ssh/sshd_config
    # find the line "PermitRootLogin yes", and change it to
    # "PermitRootLogin no"

    service sshd restart
    ```
