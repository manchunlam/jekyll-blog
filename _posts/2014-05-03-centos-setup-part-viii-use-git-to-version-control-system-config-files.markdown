---
layout: post
title: "CentOS Setup (Part VIII) - Use git for System Config Files"
date: 2014-05-03 11:21:49 -0400
comments: true
categories: centos
---

Anyone will get tired of redo-ing common config files all the time. A trick I
learnt is to set up a git project at `/`, ignore all files, and only add the
ones I deem worthy.

### **Attention!**

1. Do **not** upload any private keys, certificates, or passwords, etc.
2. Once you upload something to the internet, consider it **compromised**!

<!-- more -->
### Steps

You should log in as `root`.

1. Initialize git project

    ```sh
    cd /
    git init
    ```

2. Ignore all files unless I want to add it

    ```sh
    cd /
    touch .gitignore
    vi .gitignore
    # add the following line (without the #) to ignore everything
    # *

    git add -f <file-I-want>
    # -f: force add (because I ignore everything)
    ```

3. Tell git who you are

    ```sh
    git config --global user.name "Joe Shmoe"
    git config --global user.email foo@example.com
    ```

4. Generate SSH key for no-password push to repos

    ```
    ssh-keygen
    # two files are created
    # ~/.ssh/id_rsa
    # ~/.ssh/id_rsa.pub
    # ONLY give away your public key (id_rsa.pub)
    ```

5. Add your project to a **private** repo

    ```
    git remote add origin git@bitbucket.org:foo/centos-config.git
    ```
