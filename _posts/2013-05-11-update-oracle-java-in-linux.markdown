---
layout: post
title: "Install/Update Oracle Java in Linux"
date: 2013-05-11 22:41
comments: true
categories: java
tags:
  - linux
  - java
---

Installing Java on CentOS is not as easy as a Windows installer, but it gives
us flexibility to have multiple Java on the same server.

<!-- more -->

1. Download Java from Oracle, please get `*.tar.gz` version

2. Upload the tar-ball to the server

    ```sh
    scp ~/Downloads/jdk-7u55-linux-x64.tar.gz \
      someuser@some-server.com:/home/someuser/tmp
    ```

3. Log in as `root`, move the tar-ball to `/opt`

    ```sh
    mv /home/someuser/tmp/jdk-7u55-linux-x64.tar.gz /opt
    ```

4. Check the `tar`-ed files are all under a directory, then extract it

    ```sh
    cd /opt
    tar -tzvf jdk-7u55-linux-x64.tar.gz
    # -t: list all files in tar-ball
    # all files should be under some kind of top level directory
    # or else, you get files everywhere

    tar -xzvf jdk-7u55-linux-x64.tar.gz
    # -x: extract
    ```

    Your directory structure should look like

    ```text
    /opt
      |-- jdk1.7.0_55
      |-- jre1.7.0_21
    ```

5. Change to extracted directory, and set `java` and `javac`

    ```sh
    cd /opt/jdk1.7.0_55
    # java (i.e. JRE)
    alternatives --install /usr/bin/java java /opt/jdk1.7.0_55/bin/java 1
    # javac (i.e. Java Compiler)
    alternatives --install /usr/bin/javac javac /opt/jdk1.7.0_55/bin/javac 1
    ```

6. Test Java, and check versions

    ```sh
    # test
    which java # should give "/usr/bin/java"
    which javac # should give "/usr/bin/javac"
    # check version
    java -version
    javac -version
    ```

6. Selecting Java

    Let's say you have multiple Javas, you can pick the version you want by

    ```sh
    # as root
    alternatives --config java
    alternatives --config javac
    ```

7. Updating Java

    Repeat steps 1 to 4. Then in Step 5, for `alternatives --install`, do

    ```sh
    alternatives --install /usr/bin/java java /opt/jdk1.7.0_99/bin/java <n+1>
    alternatives --install /usr/bin/javac javac /opt/jdk1.7.0_99/bin/javac <n+1>
    ```

    Where `n` is the number of Java versions you previously have.

    For example, I have `_55` as my first Java; then I should use `2` for `_99`
    update.

8. Link `/usr/bin/java` and `/usr/bin/javac` to the new version

    1. Repeat Step 7, then pick the version of Java you want to link.
    2. Test by repeating step 6.
