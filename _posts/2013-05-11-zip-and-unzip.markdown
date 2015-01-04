---
layout: post
title: "zip and unzip"
date: 2013-05-11 22:17
comments: true
categories: linux
tags:
  - linux
---

To `unzip` an archive to a directory, and create that directory
automatically,

```sh
unzip foobar.zip -d somewhere
```

To `zip` all contents in the current directory,

```sh
zip -r foo.zip .
```

<!-- more -->

To compress a directory, __and__ preserve directory structure,

```sh
zip -r tmp.zip ./tmp/
```

Note: when extracted, the result will be
```
tmp
  |-- sub_dir_01
  |     |-- foobar.txt
  |-- some_file.txt
```
