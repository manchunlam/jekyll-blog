# `jekyll` Notes

## Table of Contents

1. [Introduction](#i-introduction)
2. [Code Highlighting](#ii-code-highlighting)
3. [Making a New Page](#iii-making-a-new-page)
4. [Making a New Post](#iv-making-a-new-post)
5. [Important Variables and Their Structure](#v-important-variables-and-their-structure)
6. [Adding Javascript Libraries](#vi-adding-javascript-libraries)
7. [FAQ](#faq)

## I. Introduction

This article documents all my notes on using and developing with `jekyll`

## II. Code Highlighting

Most of my posts have code snippets, **and** bullet points. I'd like to have

1. Code blocks indented with bullets
2. Line numbers for the code snippets
3. Use `github` style markdown blocks

To achieve this, I did

1. Go online, grab a `jekyll` syntax highlighting CSS. I copied and pasted one
    to `_sass/_syntax-highlighting.scss`
2. Change the `_config.yml` file

    1. Change the `markdown` processor to `redcarpet`
    2. Change the `highlighter` processor to `pygments`

3. Add `redcarpet` and `pygments.rb` gems to `Gemfile`
4. Use a _plugin_ to override the default code-block processor

    The plugin is in [`_plugins`]
    (_plugins/jekyll/converters/markdown/redcarpet_markdown.rb).

    When compared to the [default]
    (https://github.com/jekyll/jekyll/blob/v2.5.3/lib/jekyll/converters/markdown/redcarpet_parser.rb#L16-L23)
    , I only added the `options`

    ```ruby
    linespans: 'line'
    ```

    With this option, `Pygments` will automatically generate line numbers for
    all code blocks, with the right CSS class, for the stylesheet to do its
    magic.

## III. Making a New Page

A new page is something like `example.com/my-new-page`. To make this happen,

```sh
mkdir categories
touch categories/index.html
```

In `index.html`, we add the frontmatter `permalink`

```text
---
layout: ...
permalink: "/categories/"
```

And that's it.

You have choice between `.html` or `.md` extensions. You can use all the
`liquid` template methods in either!

Please the [`.md`](about/index.md) and [`.html`](categories/index.html)
examples.

## IV. Making a New Post

All posts go to `_posts` with the following format

```
YEAR-MONTH-DAY-title.markdown
```

An example will be `2014-12-30-my-awesome-blog-post.markdown`

## V. Important Variables and Their Structure

1. `site.categories`

    ```ruby
      { "#{category_name_01}" => [<Post :title, :url>, <Post :title, :url>],
        "#{category_name_02}" => [<Post :title, :url>] }
    ```

    **Note**:

    See [`categories/index.html`](categories/index.html) on how it's used.

    You can use the following to get all posts with the `category` `foobar`

    ```ruby
    site.categories['foobar']
    ```

2. `site.tags`

    ```ruby
    { "#{tag_name_01}" => [<Post :title, :url>, <Post :title, :url>] }
    ```

    To get all posts with the `tag` `foo`

    ```ruby
    site.tags['foo']
    ```

    Please see [`_includes/tag_cloud.html`](_includes/tag_cloud.html) and
    [`tags.html`](tags.html).

3. `page.tags`

    The current `page` is a _Post_, then this will return an array of tag
    **name**s, as specified in the front-matter of the post.

    With this front-matter,

    ```text
    ---
    tags:
      - foo
      - bar
    ---
    ```

    `page.tags` returns

    ```
    ["foo", "bar"]
    ```

## VI. Adding Javascript Libraries

It's not unsual for sites to have javascript libraries. For it to be used in
`jekyll`

1. Make a directory to hold the javascript libraries

    ```sh
    cd $jekyllRoot
    mkdir assets/vendor/javascripts
    ```

    This will prompt `jekyll` to create a directory structure of the same names
    in `_sites`

2. Add any javascript libraries to the above directory
3. Include the library in [`head.html`](_includes/head.html)

## FAQ

1. What is the difference between `categroy` and `tag`

    In short, setting a `category` affects the URL of a post; while setting
    `tag`s have no effect on the URL at all.

    The answer in details is [here](http://stackoverflow.com/a/8710254)
