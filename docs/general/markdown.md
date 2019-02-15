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

Markdown is not intended as a replacement for HTML, but rather to make it easy to read, write, and edit _prose_. HTML is a publishing format; Markdown is a _writing_ format. Its formatting syntax is very small, corresponding only to a very small subset of HTML tags, and only addresses issues that can be conveyed in plain text. For situations where more complicated HTML structures are required, Markdown allows for [Inline HTML](#inline-html).

## Paragraphs and line breaks

A paragraph is simply one or more consecutive lines of text, separated by one or more blank lines. (A blank line is any line that looks like a blank line; a line containing nothing but spaces or tabs is considered blank.) Normal paragraphs should not be indented with spaces or tabs.

To insert a simple `<br>` line break rather than start a new paragraph, simply finish your text with two spaces, followed by a _single_ carriage return.

## Headers

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

## Blockquotes

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

## Horizontal rules

Three or more hyphens, asterisks, or underscores, when placed on a line on their own, will generate a horizontal rule (`<hr />`). Spaces between the hyphens or asterisks are permitted. Each of the following lines will produce a horizontal rule:

~~~
* * *
***
**********
- - -
__________
~~~

## Code

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

To include a literal backtick character within a code span, you can use double backticks as the opening and closing delimiters:
~~~markdown
``There is a literal backtick (`) here.``
~~~

Which will produce:

~~~html
<p><code>There is a literal backtick (`) here.</code></p>
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

## Tables

Markdown lets you easily create basic tables with a simple syntax. A ‘basic’ table is constructed like so:

~~~markdown
First header | Second header
------------ | -------------
Content cell | Content cell
Content cell | Content cell
~~~

The first line contains column headers; the second line contains a mandatory separator line between the headers and the content; each following line is a row in the table. Columns are always separated by the pipe (|) character. The above Markdown code generates the following HTML:

~~~html
<table>
<thead>
<tr>
  <th>First Header</th>
  <th>Second Header</th>
</tr>
</thead>
<tbody>
<tr>
  <td>Content Cell</td>
  <td>Content Cell</td>
</tr>
<tr>
  <td>Content Cell</td>
  <td>Content Cell</td>
</tr>
</tbody>
</table>
~~~

You can include leading and trailing pipe characters to each line if you wish. They are not required, but can help make a table _look_ more like a table. The following Markdown generates the exact same output as the example above:

~~~markdown
| First header | Second header |
| ------------ | ------------- |
| Content cell | Content cell  |
| Content cell | Content cell  |
~~~

NOTE: **Note:** A table need _at least_ one pipe on each line for Markdown Extra to parse it correctly. This means that the only way to create a one-column table is to add a leading or a tailing pipe, or both of them, to each line.

You can specify alignment for each column by adding colons to separator lines. A colon at the left of the separator line will make the column left-aligned; a colon on the right of the line will make the column right-aligned; colons at both side means the column is center-aligned. The `align` HTML attribute is applied to each cell of the concerned column.

In this example, the prices in the second column will be right-aligned.

~~~markdown
| Item      | Value |
| --------- | -----:|
| Computer  | $1600 |
| Phone     | $12   |
| Pipe      | $1    |
~~~

You can apply span-level formatting to the content of each cell using regular Markdown syntax:

~~~markdown
| Function name | Description                    |
| ------------- | ------------------------------ |
| `help()`      | Display the help window.       |
| `destroy()`   | **Destroy your computer!**     |
~~~

## Links

[TOC=3]

Markdown allows links to be created in two different styles: _Inline_ and _Reference_. In both styles the link text is delineated by [square brackets].

### Links, inline-style

To create an _Inline_ link, place regular parentheses immediately after the link text’s closing square bracket. Inside the parentheses, put the URL where you want the link to point, along with an optional title for the link, surrounded in quotes. For example:

~~~markdown
This is [an example](http://example.com/ "Title") inline link.
[This link](http://example.net/) has no title attribute.
~~~
Will produce:
~~~html
<p>This is <a href="http://example.com/" title="Title"> an example</a> inline link.</p>
<p><a href="http://example.net/">This link</a> has no title attribute.</p>
~~~

As with regular HTML, relative paths are permitted for local resources on the same server.

### Links, reference-style

_Reference-style_ links use a second pair of square brackets, inside of which you place a label of your own choosing to identify the link. The two squares of brackets may, optionally, be separated by a space if you wish.

~~~markdown
This is [an example][id] reference-style link.
This is [an example] [id] reference-style link.
~~~

Then you define the link itself like so:
~~~markdown
[id]: http://example.com "Optional title for the link"
~~~

The link definition(s) can be placed anywhere you like in your document. They are only used for creating links during Markdown processing, and are stripped from your document in the HTML output.

The URL portion of the link definition may, optionally, be surrounded by angle brackets and the title part can be enclosed in double quotes or standard parentheses. Additionally, you can put the title attribute on the next line and use extra spaces or tabs for padding — which tends to look better with longer URLs.

The following four link definitions, therefore, are equivalent:
~~~markdown
[foo]: http://example.com "Optional title for the link"
[foo]: http://example.com (Optional title for the link)
[foo]: <http://example.com> "Optional title for the link"
[foo]: http://example.com/significantly/longer/path/to/resources/than-is-comfortable
       (Optional title for the link)
~~~

Link definition names may consist of letters, numbers, spaces, and punctuation. They are **not** case sensitive.

The implicit link name shortcut allows you to omit the name of the link, in which case the link text itself is used as the name. Just use an empty set of square brackets — e.g., to link the word “Google” to the google.com web site, you could simply write:

~~~markdown
[Google][]
~~~

And then define the link:

~~~markdown
[Google]: http://google.com
~~~

The ‘implicit link name’ trick works even if the link text has spaces in it:

~~~markdown
[Awesome website][]
~~~
~~~markdown
[Awesome website]: http://example.com "Visit the awesome website"
~~~

As previously noted, link definitions can be placed anywhere in your document, as they are stripped out during the conversion to HTML. The intention of reference-style links is to make your document significantly more readable — and, [as noted above](#what-is-markdown), readbility is a core objective of the Markdown syntax. Two common techniques to this end are to place them either immediately after the paragraph in which they are used, or to put them at the bottom of the document, like footnotes. An example of the former technique:

~~~markdown
In recent years it seems that [Google] [1] has dominated the search engine market
in ways that neither [Yahoo] [2] nor [MSN] [3] have managed.

  [1]: http://google.com/        "Google"
  [2]: http://search.yahoo.com/  "Yahoo Search"
  [3]: http://search.msn.com/    "MSN Search"
~~~

Which generates:

~~~html
<p>In recent years it seems that <a href="http://google.com/"title="Google">Google</a>
has dominated the search engine market in ways that neither <a href="http://search.yahoo.com/"
title="Yahoo Search">Yahoo</a> nor <a href="http://search.msn.com/"
title="MSN Search">MSN</a> have managed.</p>
~~~

With Markdown’s reference-style links, a source document much more closely resembles the final output, as rendered in a browser. By allowing you to move the markup-related metadata out of the paragraph, you can add links without interrupting the narrative flow of your prose.

## Images

[TOC=3]

Markdown uses an image syntax that closely resembles the syntax for links, allowing for two styles: _inline_ and _reference_.

### Images, inline-style

Inline image syntax looks like this:

~~~markdown
![Alt text](/path/to/img.jpg)
![Alt text](/path/to/img.jpg "Optional title")
~~~

As you can see, it is very similar to the [inline link](#links-inline-style) syntax. The key features are:
- An exclamation mark: !;
- followed by a set of square brackets, containing the alt attribute text for the image;
- followed by a set of parentheses, containing the URL or path to the image, and an optional title attribute enclosed in either double or single quotes.

### Images, reference-style

Reference-style image syntax looks like this:

~~~markdown
![Alt text][id]
~~~

Where “id” is the name of a defined image reference. Image references are defined using syntax identical to link references:

~~~markdown
[id]: url/to/image  "Optional title attribute"
~~~

WARN: **Warning:** Although you can use single quotes to delineate the title attribute for inline-style images, for reference-style images double quotes must be used.

Currently, Markdown has no syntax for specifying the dimensions of an image; if you need this then you can simply use regular HTML `<img>` tags.



## Other inline elements

[TOC=3]

### Emphasis

Asterisks (\*) and underscores (\_) are used to indicate emphasis. Text wrapped with a single \* or \_ will be wrapped with an HTML `<em>` tag; using double \*’s or double \_’s will wrap the text in a `<strong>` tag. So:
~~~markdown
*single asterisk*
_single underscore_
**double asterisks**
__double underscore__
~~~
Generates:
~~~html
<em>single asterisk</em>
<em>single underscore</em>
<strong>double asterisks</strong>
<strong>double underscore</strong>
~~~
You may use whichever style you prefer; the only restriction is that the same character must be used to open and close an emphasis span.

You can use emphasis in the middle of a word, but in this situation you _must_ use asterisks — underscores will be treated literally. So:

~~~markdown
Abso*friggin*lutely
Abso**friggin**lutely
Abso_friggin_lutely
Abso__friggin__lutely
~~~
Becomes:
~~~html
Abso<em>friggin</em>lutely
Abso<strong>friggin</strong>lutely
Abso_friggin_lutely
Abso__friggin__lutely
~~~

When * or _ are surrounded with spaces they will always be treated as literal asterisks or underscores. If you wish to have either of these characters treated literally in a situation where they _cannot_ be surrounded by spaces, you can backslash-escape them like so:

~~~
\*Some text surrounded by literal asterisks\*
~~~

### Abbreviations

Markdown supports abbreviations (`<abbr>`) using a syntax that follows the two-part ‘reference’ style used by links and images. An abbreviation is defined like so:

~~~markdown
*[HTML]: Hyper Text Markup Language
*[W3C]:  World Wide Web Consortium
~~~

then, elsewhere in the document, write text such as:

~~~markdown
The HTML specification
is maintained by the W3C.
~~~

and any instance of those words in the text will become:
~~~html
The <abbr title="Hyper Text Markup Language">HTML</abbr> specification
is maintained by the <abbr title="World Wide Web Consortium">W3C</abbr>.
~~~

Abbreviations are case-sensitive, and will span on multiple words when defined as such. An abbreviation may also have an empty definition, in which case `<abbr>` tags will be added in the text but the title attribute will be omitted.

~~~markdown
Operation Tigra Genesis is going well.

*[Tigra Genesis]:
~~~

Abbreviation definitions can be anywhere in the document. They are stripped from the final document, just like [link](#links-reference-style) and [image](#images-reference-style) definitions.







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

Markdown generates HTML that will be compatible with both an XHTML and HTML doctype — in other words, element tags such as `<image />`, `<br />`, & `<hr />` will be created with a self-closing forward slash at the end, and closing tags _will_ be created for elements where a closing tag is theoretically optional.

John Gruber has made a [Markdown web dingus](https://daringfireball.net/projects/markdown/dingus) available at Daring Fireball that you can use to try out Markdown and practice getting to grips with the syntax.
