<!--
    This source file is part of the open source project
    ExpressionEngine User Guide (https://github.com/ExpressionEngine/ExpressionEngine-User-Guide)

    @link      https://expressionengine.com/
    @copyright Copyright (c) 2003-2019, EllisLab Corp. (https://ellislab.com)
    @license   https://expressionengine.com/license Licensed under Apache License, Version 2.0
-->

# Markdown in ExpressionEngine

[TOC]

ExpressionEngine’s implementation of Markdown, for the most part, follows [Jon Gruber's implementation of Markdown](http://daringfireball.net/projects/markdown/), but it also uses syntax from a couple of other Markdown libraries to build upon Gruber’s foundation. Since each of these third party implementations has its own user guide, EE users previously needed to refer to multiple sources in order to obtain an overall guide to EE's Markdown syntax.  

In order to remedy this situation we have combined and summarised those third party guides into a single, unified reference source on this page.

## An introduction to Markdown

### What is Markdown?

_Markdown_ is a text-to-HTML conversion tool for web writers. Its syntax is intended for one purpose: to be used as a format for writing for the web. Markdown allows you to write using an easy-to-read, easy-to-write plain text format, and have it converted to structurally valid HTML.

Readability is paramount, and a Markdown-formatted document should be publishable as-is, as plain text, without looking like it’s been marked up with tags or formatting instructions. Indeed, the single biggest source of inspiration for Markdown’s syntax is the format of plain text email.

For more information about the philosophy and concepts behind Markdown, visit the relevant sections of [Daring Fireball](https://daringfireball.net/projects/markdown/syntax#philosophy).

### What Markdown is not

Markdown is not intended as a replacement for HTML, but to make it easy to read, write, and edit _prose_. HTML is a publishing format; Markdown is a writing format. Its formatting syntax is very small, corresponding only to a very small subset of HTML tags, and only addresses issues that can be conveyed in plain text. For situations where more complicated HTML structures are required, Markdown allows for [Inline HTML](#inline-html).

## Basic syntax

[TOC=3]

### Paragraphs, Headers and Blockquotes

A paragraph is simply one or more consecutive lines of text, separated by one or more blank lines. (A blank line is any line that looks like a blank line — a line containing nothing but spaces or tabs is considered blank.) Normal paragraphs should not be indented with spaces or tabs.

To insert a simple `<br>`-type line break rather than start a new paragraph, simply finish your text with two spaces and followed by a _single_ carriage return.

To create a Header of the type `<h1>`-`<h6>` simply put 1-6 hash marks (#) at the beginning of the line. The number of hashes equals the resulting HTML header level.

```md
# This is an H1
## This is an H2
### This is an H3
(etc)
```

Additionally, `<h1>` and `<h2>` Headers can optionally be created by “underlining” with equal signs (`=`) and hyphens (`-`), respectively.

```md
This is an H1
=============

This is an H2
-------------
```

Any number of underlining =’s or -’s will work.

## More advanced syntax

[TOC=3]
