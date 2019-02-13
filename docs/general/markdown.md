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

## Paragraphs, Headers and Blockquotes

[TOC=3]

### Paragraphs

A paragraph is simply one or more consecutive lines of text, separated by one or more blank lines. (A blank line is any line that looks like a blank line; a line containing nothing but spaces or tabs is considered blank.) Normal paragraphs should not be indented with spaces or tabs.

To insert a simple `<br>` line break rather than start a new paragraph, simply finish your text with two spaces, followed by a _single_ carriage return.

### Headers

To create a Header of the type H1-H6 simply put 1-6 hash marks (`#`) at the beginning of the line. The number of hashes equals the resulting HTML header level.

	# This is an H1
	## This is an H2
	### This is an H3
	(etc)

Additionally, `<h1>` and `<h2>` Headers can optionally be created by “underlining” with equal signs (`=`) and hyphens (`-`), respectively.

```markdown
This is an H1
=============

This is an H2
-------------
```

Any number of the underlining characters (`=` or `-`) will work.

### Blockquotes

Blockquotes are indicated using email-style angle brackets (`>`). It is generally more readable to hard wrap the text and put a `>` before every line, but it’s also permissible to simply put the `>` before just the first line of a hard-wrapped paragraph. Either of the following two code blocks:

```markdown
> This is a blockquote with two paragraphs. Lorem ipsum dolor sit amet,
> consectetuer adipiscing elit. Aliquam hendrerit mi posuere lectus.
> Vestibulum enim wisi, viverra nec, fringilla in, laoreet vitae, risus.
>
> Donec sit amet nisl. Aliquam semper ipsum sit amet velit. Suspendisse
> id sem consectetuer libero luctus adipiscing.
```
```markdown
> This is a blockquote with two paragraphs. Lorem ipsum dolor sit amet,
consectetuer adipiscing elit. Aliquam hendrerit mi posuere lectus.
Vestibulum enim wisi, viverra nec, fringilla in, laoreet vitae, risus.

> Donec sit amet nisl. Aliquam semper ipsum sit amet velit. Suspendisse
id sem consectetuer libero luctus adipiscing.
```

…will generate the following HTML:

```html
<blockquote>
	<p>This is a blockquote with two paragraphs. Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Aliquam hendrerit mi posuere lectus. Vestibulum enim wisi, viverra nec, fringilla in, laoreet vitae, risus.</p>
	<p>Donec sit amet nisl. Aliquam semper ipsum sit amet velit. Suspendisse id sem consectetuer libero luctus adipiscing.</p>
</blockquote>
```

Blockquotes can be nested within each other simply by adding additional levels of angled brackets:

```markdown
> This is the first level of quoting.
>
> > This is nested blockquote.
>
> Back to the first level.
```

Additionally, Blockquotes can contain other Markdown elements, such as Headers, lists, code blocks, etc.

```markdown
> ## This is a header.
>
> 1.   This is the first list item.
> 2.   This is the second list item.
>
> Here's some example code:
>
>     return shell_exec("echo $input | $markdown_script");
```

## Showing code

[TOC=3]

### Inline code

A span of inline text can be marked as code by surrounding it with ‘backtick’ quotes. The span will be wrapped in `<code>…</code>` tags and any ampersands (&) and angle brackets (< or >) will automatically be translated into HTML entities. This makes it easy to use Markdown to write about HTML example code. So:
```markdown
This is regular text with `a demonstration <a href="#"> tag` placed in the middle.
```
Becomes:
~~~html
<p>This is regular text with <code>a demonstration &lt;a href="#"&gt; tag</code> placed in the middle.</p>
~~~

### Code blocks, indented

Pre-formatted code blocks are used for writing about programming or markup source code. Rather than forming normal paragraphs, the lines of a code block are interpreted literally. As with inline code, ampersands and angle brackets will be turned into HTML entities. In addition, Markdown wraps a code block in both `<pre>` and `<code>` tags.

Code blocks can be delineated in several ways. The first and simplest way is to simply indent the block by 4 spaces, or 1 tab.
~~~markdown
This is a normal paragraph

    And this is a <code block>.
~~~
Which becomes:
~~~HTML
<p>This is a normal paragraph</p>

<pre><code>And this is a &lt;code block&gt;.
</code></pre>
~~~
A code block delineated by indentation in this way continues until it reaches a line that is not indented (or the end of the article).

NOTE: **Note:** One level of indentation — 4 spaces or 1 tab — is removed from each line output by a code block created by this ‘indentation’ method. So a line indented by 8 spaces in Markdown will be indented by 4 spaces in the HTML.

### Code blocks, fenced

An alternative, and arguably more flexible, way to delineate code blocks is by ‘fencing’ them. Fenced code blocks are like Markdown’s regular code blocks, except that they’re _not_ indented and instead rely on start and end fence lines to delimit the code block. The code block starts with a line containing three or more tilde (~) characters, and ends with the first line with the _same_ number of tilde characters. For instance:
```markdown
This paragraph precedes...

~~~
...a one-line code block
~~~
```

You can, optionally, use backtick (`) characters instead of tilde.

~~~markdown
```
This is also a one-line code block
```
~~~

Fenced code blocks have some advantages over their indented counterparts. They are ideal if you need to paste some code into an editor that lacks a convenient command to indent multiple lines at once, like a text box in a web browser — eg. an entry field in the ExpressionEngine control panel.

Also, they can be used immediately following a list, whereas indented code blocks cannot (because Markdown would view the indent as signifying a paragraph in the list — see [Paragraphs in list items](#paragraphs-in-list-items)). Like so:

```markdown
1.  List item

	Not an indented codeblock, but a second paragraph
	in the list item.

~~~
But this IS a code block.
~~~
```

Lastly, fenced code blocks allow you to specify a class name that will apply to a code block — useful if you want to assign language-specific styling, or to tell a syntax highlighter what syntax to use. To do so, simply place a class name at the end of the opening code fence. It can be preceded by a dot, but this is not required.


```
~~~.html
<div>
	<p>The monkey climbed the <em>enormous</em> tree.</p>
</div>
~~~
```

You can also use a [special attribute block](#special-attributes):

```
~~~ {.html #example-1}
<p>This link takes you <a href="http://amazing.com">somewhere amazing</a>, so click it!</p>
~~~
```


## Lists

[TOC=3]

Markdown supports ordered (numbered), unordered (bulleted), and definition lists. To create a list in Markdown, simply start each list item with the appropriate ‘list marker’.

List markers typically sit at the left margin but may be indented by up to three spaces, and they must be followed by one or more spaces or a tab. The character used for the list marker will vary according to the type of list required.

### Unordered lists
The list markers for unordered lists are asterisks, pluses and hyphens, and they are entirely interchangeable. So:

```markdown
+ Mercury
* Venus
* Mars
- Jupiter
+ Saturn
- Uranus
* Neptune
```

will generate the following HTML output:

```html
<ul>
	<li>Mercury</li>
	<li>Venus</li>
	<li>Mars</li>
	<li>Jupiter</li>
	<li>Saturn</li>
	<li>Uranus</li>
	<li>Neptune</li>
</ul>
```

### Ordered lists
Ordered lists, naturally enough, use numbers followed by periods. Note, however, that the actual numbers used *have no impact on the generated HTML*, with the exception of the **first** number (see Tip below). So the following code blocks:

```markdown
1.  Car
2.  Plane
3.  Ship
```
```markdown
1.  Car
102.  Plane
27.  Ship
```

…are equivalent to each other, and will both generate the following HTML:

```html
<ol>
	<li>Car</li>
	<li>Plane</li>
	<li>Ship</li>
</ol>
```

NOTE: **Note:** If an ordered list starts with a number _other_ than 1, Markdown will honor that in the HTML output. So an unordered list in Markdown that starts with `5. Car` will output an opening tag of `<ol start="5">`. This allows you to continue a list after (for example) an intervening paragraph of text.

TIP: **Tip:** You may have a regular paragraph that just happens to start with a number-period-space sequence. If so, you can avoid accidentally triggering an ordered list by escaping the period with a backslash, eg. `40\. What a great Age!`

### Definition lists

Definition lists are only slightly more complicated. They consist of terms and definitions, like a dictionary. In Markdown these take the form of a single-line term followed, on the next line, by a colon and the definition for that term.

The colon is the list marker, and follows the standard rules for list markers: it typically sits at the left margin but may be indented by up to three spaces, and it must be followed by one or more spaces or a tab.

Further terms must be separated from the previous definition by a blank line.

```markdown
Apple
:  Pomaceous fruit of plants of the genus Malus in
   the family Rosaceae.

Orange
:  The fruit of an evergreen tree of the genus Citrus.
```
```HTML
<dl>
<dt>Apple</dt>
<dd>Pomaceous fruit of plants of the genus Malus in the family Rosaceae.</dd>
<dt>Orange</dt>
<dd>The fruit of an evergreen tree of the genus Citrus.</dd>
</dl>
```
TIP: **Tip:** It is the *Definition* part of a Term/Definition pair that is treated as the list item by Markdown, and as such the definition can take advantage of features such as [optional indenting](#optional-indenting-text-in-list-items), and [multiple paragraphs](#paragraphs-in-list-items).

You can also have terms with more than one definition:
```markdown
Apple
:   Pomaceous fruit of plants of the genus Malus in
    the family Rosaceae.
:   An American computer company.

Orange
:   The fruit of an evergreen tree of the genus Citrus.
```
And definitions with more than one term:
```markdown
Term 1
Term 2
:   Definition a

Term 3
:   Definition b
```

### Optional indenting text in list items

It looks neater, and could be considered more readable, if text in a list item is indented:
```markdown
*   Lorem ipsum dolor sit amet, consectetuer adipiscing elit.
    Aliquam hendrerit mi posuere lectus. Vestibulum enim wisi,
    viverra nec, fringilla in, laoreet vitae, risus.
*   Donec sit amet nisl. Aliquam semper ipsum sit amet velit.
    Suspendisse id sem consectetuer libero luctus adipiscing.
```
But it doesn't need to be. The following Markdown syntax block will generate the exact same HTML as the one above.
```markdown
*   Lorem ipsum dolor sit amet, consectetuer adipiscing elit.
Aliquam hendrerit mi posuere lectus. Vestibulum enim wisi,
viverra nec, fringilla in, laoreet vitae, risus.
*   Donec sit amet nisl. Aliquam semper ipsum sit amet velit.
Suspendisse id sem consectetuer libero luctus adipiscing.
```
The same is true for the definition parts of a definition list (remember, it is the definition that is treated as a list item). The following two blocks will generate identical HTML:
```markdown
Mollusc
:  An invertebrate of a large phylum which includes
   snails, slugs, mussels, and octopuses. They have
   a soft unsegmented body and live in aquatic or damp
   habitats, and most kinds have an external calcareous shell.
```
```markdown
Mollusc
:  An invertebrate of a large phylum which includes
snails, slugs, mussels, and octopuses. They have a
soft unsegmented body and live in aquatic or damp
habitats, and most kinds have an external calcareous shell.
```

### Paragraphs in list items

List items can contain paragraphs. If you put blank lines between items, you’ll get `<p>` tags wrapped around the list item text:

```markdown
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
NOTE: **Note:** A list item will receive paragraph tags if it has a blank space either above **or** below it. Exceptions to this are the first list item (which only reacts to a blank line below it), and the last item (which only reacts to a blank line above it).

List items may consist of multiple paragraphs. Each subsequent paragraph in a list item must be indented by either 4 spaces or one tab:

```markdown
1.  This is a list item with two paragraphs. Lorem ipsum dolor
    sit amet, consectetuer adipiscing elit. Aliquam hendrerit
    mi posuere lectus.

	The second paragaph. Vestibulum enim wisi, viverra nec
    vitae, risus. Donec sit amet nisl. Aliquam semper ipsum
    sit amet velit.

2.  Suspendisse id sem consectetuer libero luctus adipiscing.
```

To wrap definition text in `<p>` tags, make sure that there is a line between the term and the definition.

```markdown
Term 1

:   This is a definition with two paragraphs. Lorem ipsum
    dolor sit amet, consectetuer adipiscing elit. Aliquam
    hendrerit mi posuere lectus.

	The second paragaph of this definition. Vestibulum enim
    vitae, risus. Donec sit amet nisl. Aliquam semper ipsum
    sit amet velit.

:   Second definition for term 1, also wrapped in a paragraph
    because of the blank line preceding it.
	```

### Blockquotes in list items
To put a blockquote within a list item, the blockquote’s `>` delimiters need to be indented:
```markdown
+   This list item contains a blockquote.

    > This is a blockquote
    > inside the list item
```

### Code blocks in list items
To put a code block within a list item, the code block needs to be indented *twice* — 8 spaces or two tabs:
```markdown
+   This list item contains a code block.

        <some code inside a list item>
```

### Nesting lists

Lists can be nested, placing a new list inside a list item. To do so, simply indent the list item(s) of he nested lists by 4 spaces or 1 tab. The type of list that you nest in this way need not be of the same type as the parent list.

```markdown
- First list item
- Second list item
    1. First nested list item
    2. Second nested list item
    3. Third nested list item
- Third list item
```
```html
<ul>
	<li>First list item</li>
	<li>Second list item</li>
	    <ol>
			<li>First nested list item</li>
		    <li>Second nested list item</li>
		    <li>Third nested list item</li>
		</ol>
	<li>Third list item</li>
</ul>
```

WARN: **Warning:** Do not double-indent in this way (8 spaces or two tabs) or else you will trigger a [code block](#code-blocks-in-list-items).



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

### Special attributes

xxxxxxxxxx

## Extras

John Gruber has made a [Markdown web dingus](https://daringfireball.net/projects/markdown/dingus) available at Daring Fireball that you can use to try out Markdown and practice getting to grips with the syntax.
