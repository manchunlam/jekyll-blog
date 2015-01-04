---
layout: post
title: "CentOS Setup (Part VII) - Build apache from Source"
date: 2014-05-03 11:17:38 -0400
comments: true
categories: centos
tags:
  - centos
  - linux
---

We will install from Apache source to get the latest 2.4.x version.

You must be `root`.

<!-- more -->

1. Download the apache `.tar.bz2` source file

    ```
    mkdir -p Downloads/httpd
    cd Downloads/httpd
    wget http://mirror.sdunix.com/apache//httpd/httpd-2.4.9.tar.bz2
    # as of writing, this is the latest stable version
    ```

2. Add FQDN and hostname to `/etc/hosts`

    ```
    vi /etc/hosts
    # find the line beginning with "127.0.0.1", add FQDN and hostname to the end
    # for example:
    # 127.0.0.1 localhost localhost.localdomain localhost4 localhost4.localdomain4 bar.example.com bar
    ```

4. Install `apr`

    ```
    yum remove apr # in case apr is already installed
    mkdir -p Downloads/apr
    cd Downloads/apr
    wget http://mirror.nexcess.net/apache//apr/apr-1.5.0.tar.bz2
    rpmbuild -ts apr-1.5.0.tar.bz2
    rpmbuild -tb apr-1.5.0.tar.bz2
    cd /root/rpmbuild/RPMS/x86_64/
    rpm -Uvh apr-*.rpm
    rpm -qa | grep "apr" # make sure they are installed
    ```

5. Install `apr-util`

    ```
    yum remove apr-util
    mkdir -p Downloads/apr-util
    cd Downloads/apr-util
    wget http://mirror.nexcess.net/apache//apr/apr-util-1.5.3.tar.bz2
    rpmbuild -ts apr-util-1.5.3.tar.bz2
    yum install sqlite-devel expat-devel libuuid-devel postgresql-devel \
      mysql-devel freetds-devel unixODBC-devel openldap-devel openssl-devel \
      nss-devel
    rpmbuild -tb apr-util-1.5.3.tar.bz2
    cd /root/rpmbuild/RPMS/x86_64/
    rpm -Uvh apr-util-*.rpm
    rpm -qa | grep "apr-util"
    ```

6. Install `distcache`

    ```
    mkdir -p Downloads/distcache
    cd Downloads/distcache
    wget \
      http://dl.fedoraproject.org/pub/fedora/linux/releases/18/Fedora/source/SRPMS/d/distcache-1.4.5-23.src.rpm
    rpmbuild --rebuild distcache-1.4.5-23.src.rpm
    cd /root/rpmbuild/RPMS/x86_64/
    rpm -Uvh distcache-*.rpm
    rpm -qa | grep "distcache"
    ```

4. Install `httpd` (apache)

    ```
    rpmbuild -ts httpd-2.4.9.tar.bz2
    rpmbuild -tb httpd-2.4.9.tar.bz2
    cd /root/rpmbuild/RPMS/x86_64/
    ls -al
    rpm -Uvh httpd-2.4.9-1.x86_64.rpm
    rpm -qa | grep "httpd"
    ```

5. Start `apache`, make sure it works

    ```
    service httpd start
    ```

    Then in your browser, go to `http://<ip-address>`. If you see a page with

    ```
    It works!
    ```

    Server is up and running!
