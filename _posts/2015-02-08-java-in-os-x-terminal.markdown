---
layout: post
title: "Java in OS X Terminal"
date: 2015-02-08 17:50:00 -0500
categories: markdown
tags:
  - java
  - "OS X"
---

To specify `java` version in OS X terminal, add the following to `.zshrc` (or
`.bashrc`

```sh
export JAVA_HOME="`/usr/libexec/java_home -v '1.7*'`"
```

To check what versions of `java` you have installed,

```sh
ls -al /Library/Java/JavaVirtualMachines
```

Please see this stackoverflow [thread]
  (http://stackoverflow.com/questions/17885494/how-can-i-change-mac-oss-default-java-vm-returned-from-usr-libexec-java-home)
