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

Markdown is not intended as a replacement for HTML, but to make it easy to read, write, and edit _prose_. HTML is a publishing format; Markdown is a _writing_ format. Its formatting syntax is very small, corresponding only to a very small subset of HTML tags, and only addresses issues that can be conveyed in plain text. For situations where more complicated HTML structures are required, Markdown allows for [Inline HTML](#inline-html).

## Block elements

[TOC=3]

### Paragraphs

A paragraph is simply one or more consecutive lines of text, separated by one or more blank lines. (A blank line is any line that looks like a blank line; a line containing nothing but spaces or tabs is considered blank.) Normal paragraphs should not be indented with spaces or tabs.

To insert a simple `<br>`-type line break rather than start a new paragraph, simply finish your text with two spaces, followed by a _single_ carriage return.

### Headers

To create a Header of the type H1-H6 simply put 1-6 hash marks (`#`) at the beginning of the line. The number of hashes equals the resulting HTML header level.

	# This is an H1
	## This is an H2
	### This is an H3
	(etc)

Additionally, `<h1>` and `<h2>` Headers can optionally be created by “underlining” with equal signs (`=`) and hyphens (`-`), respectively.

    ```
    This is an H1
    =============

    This is an H2
    -------------
    ```

Any number of the underlining characters (`=` or `-`) will work.

### Blockquotes

Blockquotes are indicated using email-style angle brackets (`>`). It is generally more readable to hard wrap the text and put a `>` before every line:

```
> This is a blockquote with two paragraphs. Lorem ipsum dolor sit amet,
> consectetuer adipiscing elit. Aliquam hendrerit mi posuere lectus.
> Vestibulum enim wisi, viverra nec, fringilla in, laoreet vitae, risus.
>
> Donec sit amet nisl. Aliquam semper ipsum sit amet velit. Suspendisse
> id sem consectetuer libero luctus adipiscing.
```

…but it’s also permissible to simply put the `>` before just the first line of a hard-wrapped paragraph:

```
> This is a blockquote with two paragraphs. Lorem ipsum dolor sit amet,
consectetuer adipiscing elit. Aliquam hendrerit mi posuere lectus.
Vestibulum enim wisi, viverra nec, fringilla in, laoreet vitae, risus.

> Donec sit amet nisl. Aliquam semper ipsum sit amet velit. Suspendisse
id sem consectetuer libero luctus adipiscing.
```

Either of the above methods will output the following:

```html
<blockquote>
	<p>This is a blockquote with two paragraphs. Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Aliquam hendrerit mi posuere lectus. Vestibulum enim wisi, viverra nec, fringilla in, laoreet vitae, risus.</p>
	<p>Donec sit amet nisl. Aliquam semper ipsum sit amet velit. Suspendisse id sem consectetuer libero luctus adipiscing.</p>
</blockquote>
```

Blockquotes can be nested within each other simply by adding additional levels of angled brackets:

```
> This is the first level of quoting.
>
> > This is nested blockquote.
>
> Back to the first level.
```

Additionally, Blockquotes can contain other Markdown elements, such as Headers, lists, code blocks, etc.

```
> ## This is a header.
>
> 1.   This is the first list item.
> 2.   This is the second list item.
>
> Here's some example code:
>
>     return shell_exec("echo $input | $markdown_script");
```

### Lists

Markdown in ExpressionEngine supports ordered (numbered) and unordered (bulleted) lists. List markers typically start at the left margin, but may be indented by up to three spaces. List markers must be followed by one or more spaces or a tab.

Unordered lists use asterisks, pluses, and hyphens — interchangably — as list markers. In other words, the following three code blocks:

```
* Red
* Green
* Blue
```

```
- Red
- Green
- Blue
```

```
+ Red
+ Green
+ Blue
```

…are equivalent, and will each convert to:

```html
<ul>
	<li>Red</li>
	<li>Green</li>
	<li>Blue</li>
</ul>
```

Ordered lists use numbers followed by periods. It's worth noting that the actual numbers used have no impact on the generated HTML, with the exception of the _first_ number (see Tip below). So the following code blocks:

```
1.  Car
2.  Plane
3.  Ship
```
```
1.  Car
7.  Plane
2.  Ship
```
```
1.  Car
1002.  Plane
27.  Ship
```

…are equivalent and will generate the exact same HTML output, namely:

```html
<ol>
	<li>Car</li>
	<li>Plane</li>
	<li>Ship</li>
</ol>
```

TIP: **Tip:** If an ordered list starts with a number different than 1, Markdown will honor that in the HTML output by applying a `start` attribute to the opening tag. So an unordered list in Markdown that starts with `5. Car` will output an opening tag of `<ol start="5">`. This allows you to continue a list after (for example) an intervening paragraph of text.

List items may consist of multiple paragraphs. If you put blank lines between items, you’ll get `<p>` tags for the list item text. You can create multi-paragraph list items by indenting the paragraphs by 4 spaces or 1 tab: Each subsequent paragraph in a list item must be indented by either 4 spaces or one tab.

Putting blank lines between list items (either above or below) will give you `<p>` tags for the list item text.

```
- Eggs

- Ham

- Coffee
```
```HTML
<ul>
	<li><p>Eggs</p></li>
	<li><p>Ham</p></li>
	<li><p>Coffee</p></li>
</ul>
```

To get multiple paragraphs within a list item, indent the paragraphs by 4 spaces (or 1 tab).

```
1. This will be a list item with multiple paragraphs.

    See? Here’s a second paragraph.

2. And this is another list item (wrapped in a paragraph tag because of the spacer line above it).
3. This list item, however, is NOT wrapped in a paragraph.
```
Outputs:
```HTML
<ol>
	<li>
		<p>This will be a list item with multiple paragraphs.</p>
		<p>See? Here’s a second paragraph.</p>
	</li>
	<li>
		<p>And this is another list item (wrapped in a paragraph tag because of the spacer line above it).</p>
	</li>
	<li>This list item, however, is NOT wrapped in a paragraph.</li>
</ol>
```




## Span elements

[TOC=3]

### Item 1

xxxxxxxxx

### Item 2

xxxxxxxxx


## More advanced syntax

[TOC=3]

### Inline html

For any markup that is not covered by Markdown’s syntax, you simply use HTML itself. There’s no need to indicate that you’re switching from Markdown to HTML; you just use the tags.

The only restrictions are that block-level HTML elements — e.g. `<div>`, `<table>`, `<pre>`, `<p>`, etc. — must be separated from surrounding content by blank lines, and the start and end tags of the block should not be indented with tabs or spaces. Markdown is smart enough not to add extra (unwanted) `<p>` tags around HTML block-level tags.

For example, to add an HTML table to a Markdown article:

```html
This is a regular paragraph.

<table>
    <tr>
        <td>Foo</td>
    </tr>
</table>

This is another regular paragraph.
```

NOTE: **Note:** Markdown formatting syntax is not processed within block-level HTML tags. E.g., you can't use Markdown-style `*emphasis*` inside an HTML block.

Span-level HTML tags — e.g. `<span>`, `<cite>`, or `<del>` — can be used anywhere in a Markdown paragraph, list item, or header. If you want, you can even use HTML tags instead of Markdown formatting; e.g. if you’d prefer to use HTML `<a>` or `<img>` tags instead of Markdown’s link or image syntax, go right ahead.

TIP: **Tip:** Unlike block-level HTML tags, Markdown syntax **is** processed within span-level tags.

### Auto-escaping for special characters

xxxxxxxxx

## Extras

John Gruber has made a [Markdown web dingus](https://daringfireball.net/projects/markdown/dingus) available at Daring Fireball that you can use to try out Markdown and practice getting to grips with the syntax.
