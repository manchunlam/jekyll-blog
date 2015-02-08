---
layout: post
title: "Codeblock in Bitbucket"
date: 2015-02-08 12:26:00 -0500
categories: markdown
tags:
  - markdown
  - bitbucket
---

`bitbucket` uses a different kind of codeblock syntax, and I can never remember
how to do indentations correctly.

This is a note to remind myself.

1. Rule 1

    ```text
    You need 4 leading spaces to start a codeblock
    ```

    For example,

    ```text
    ## A Header

        :::sh
        echo 'foo'
    ```

2. Rule 2

    ```text
    You need 4 more spaces for each level of indentation
    ```

    Let's say I want to indent a codeblock under a bullet point

    ```text
    1. foo

            :::sh
            echo 'foo'
    ```

    **Explanation**

    A bullet point is one-level of indentation. Therefore, we need 4 leading
    spaces (in addition to the original 4 to start a codeblock) for proper
    codeblock indentation.

    ```text
    4 spaces to start + 4 spaces for indentation = 8 leading spaces
    ```

### Example

```text
# foobar

    :::sh
    echo 'foo'

1. foo

        :::sh
        echo 'foo'

2. bar

    1. foo
    2. bar

            :::sh
            echo 'foo'

    3. yay
```
