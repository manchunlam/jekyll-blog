---
layout: post
title: "CentOS Setup (Part III) - Install Essentials"
date: 2014-04-27 20:47:27 -0400
comments: true
categories: centos
---

You must be `root`. We will installing 2 extra repos, `epel`, and `remi`. These
repos provide a better selection of, and more up-to-date, packages than standard
CentOS repos.

1. Install `wget`, so you can get files online from the terminal

    ```
    yum install wget
    ```
<!-- more -->

1. Get some protection, use GPG keys before installing extra repos
    * `epel`
        1. Go to [Fedora Project](https://fedoraproject.org/keys)
        2. Find the section _RPM-GPG-KEY-EPEL-6_
        3. Copy the link to the key file

            Mine was `https://fedoraproject.org/static/0608B895.txt`
        4. Install the key on the system

            ```
            wget https://fedoraproject.org/static/0608B895.txt
            # get the key file
            mv 0608B895.txt /etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-6
            # move to place where rpm understands
            rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-6
            # import the key
            rpm -qa gpg*
            # verify the key is installed correctly
            ```
    * `remi`
        1. Go to [Les RPM de Remi - Repository](http://rpms.famillecollet.com/)
        2. Search for `RPM-GPG-KEY-remi`, and copy URL to file

            Mine was `http://rpms.famillecollet.com/RPM-GPG-KEY-remi`
        3. Install the key on the system

            ```
            wget http://rpms.famillecollet.com/RPM-GPG-KEY-remi
            mv RPM-GPG-KEY-remi /etc/pki/rpm-gpg/RPM-GPG-KEY-remi
            rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-remi
            rpm -qa gpg*
            ```

1. Install `epel` repo

    ```
    wget http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
    # get the "installer"
    rpm -Uvh epel-release-6-8.noarch.rpm
    # -U: upgrade (synonymous with "install" in this case)
    # -v: verbose output (see what you've done)
    # -h: show progress bar
    ```

4. Install `remi` repo, and enable it

    ```
    wget http://rpms.famillecollet.com/enterprise/remi-release-6.rpm
    rpm -Uvh remi-release-6.rpm
    vi /etc/yum.repos.d/remi.repo
    # find the section "[remi]" (usually the first section)
    # change "enabled=0" to "enabled=1"
    ```

5. Verify our repos are being recognized

    ```
    yum repolist
    ```

6. Upgrade all the packages!

    ```
    yum list updates
    yum upgrade
    ```
