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

To create a Header of the type H1-H6 simply put 1-6 hash marks (#) at the beginning of the line. The number of hashes equals the resulting HTML header level.

	# This is an H1
	## This is an H2
	### This is an H3
	(etc)

Additionally, `<h1>` and `<h2>` Headers can optionally be created by “underlining” with equal signs (=) and hyphens (-), respectively.

```markdown
This is an H1
=============

This is an H2
-------------
```

Any number of the underlining characters (= or -) will work.





## Blockquotes

Blockquotes are indicated using email-style angle brackets (>). It is generally more readable to hard wrap the text and put a > before every line, but it’s also permissible to simply put the `>` before just the first line of a hard-wrapped paragraph. Either of the following two code blocks:

~~~markdown
> This is a blockquote with two paragraphs. Lorem ipsum dolor sit amet,
> consectetuer adipiscing elit. Aliquam hendrerit mi posuere lectus.
> Vestibulum enim wisi, viverra nec, fringilla in, laoreet vitae, risus.
>
> Donec sit amet nisl. Aliquam semper ipsum sit amet velit. Suspendisse
> id sem consectetuer libero luctus adipiscing.
~~~
~~~markdown
> This is a blockquote with two paragraphs. Lorem ipsum dolor sit amet,
consectetuer adipiscing elit. Aliquam hendrerit mi posuere lectus.
Vestibulum enim wisi, viverra nec, fringilla in, laoreet vitae, risus.

> Donec sit amet nisl. Aliquam semper ipsum sit amet velit. Suspendisse
id sem consectetuer libero luctus adipiscing.
~~~

…will generate the following HTML:

~~~html
<blockquote>
	<p>This is a blockquote with two paragraphs. Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Aliquam hendrerit mi posuere lectus. Vestibulum enim wisi, viverra nec, fringilla in, laoreet vitae, risus.</p>
	<p>Donec sit amet nisl. Aliquam semper ipsum sit amet velit. Suspendisse id sem consectetuer libero luctus adipiscing.</p>
</blockquote>
~~~

Blockquotes can be nested within each other simply by adding additional levels of angled brackets:

~~~markdown
> This is the first level of quoting.
>
> > This is nested blockquote.
>
> Back to the first level.
~~~

Additionally, Blockquotes can contain other Markdown elements, such as Headers, lists, code blocks, etc.

~~~markdown
> ## This is a header.
>
> 1.   This is the first list item.
> 2.   This is the second list item.
>
> Here's some example code:
>
>     return shell_exec("echo $input | $markdown_script");
~~~





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

A span of inline text can be marked as code by surrounding it with ‘backtick’ quotes. The span will be wrapped in `<code>...</code>` tags and any ampersands (&) and angle brackets (< or >) will automatically be translated into HTML entities. This makes it easy to use Markdown to write about HTML example code. So:
~~~markdown
This is regular text with `a demonstration <a href="#"> tag` placed in the middle.
~~~
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

Fenced code blocks have some advantages over their indented counterparts. They are ideal if you need to paste some code into an editor, like a text box in a web browser, that lacks a convenient command to indent multiple lines at once — eg. an entry field in the ExpressionEngine control panel.

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

You can expand the above trick to include certain additional attributes by using a [special attribute block](#special-attributes):

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

TIP: **Tip:** You may have a regular paragraph that just so happens to start with a number-period-space sequence. In this situation you can avoid accidentally triggering an ordered list by escaping the period with a backslash, eg. `40\. What a great Age!`

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
You can also have definitions with more than one term:
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

NOTE: **Important:** Do not double-indent in this way (ie. using 8 spaces or two tabs), else you will trigger a [code block](#code-blocks-in-list-items).





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

### Links, inline style

To create an Inline link, place regular parentheses immediately after the link text’s closing square bracket. Inside the parentheses, put the URL where you want the link to point, along with an optional title for the link, surrounded in quotes. For example:

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

### Links, reference style

Reference-style links use a second pair of square brackets, inside of which you place a label of your own choosing to identify the link. The two squares of brackets may, optionally, be separated by a space if you wish.

~~~markdown
This is [an example][id] reference-style link.
This is [an example] [id] reference-style link.
~~~

Then you define the link itself like so:
~~~markdown
[id]: http://example.com "Optional title for the link"
~~~

The link definition(s) can be placed anywhere you like in your document. They are only used for creating links during Markdown processing, and are stripped from your document in the HTML output.

The URL portion of the link definition may, optionally, be surrounded by angle brackets. The ‘title’ part, if included, should be enclosed in either double quotes or standard parentheses. Additionally, you can put the title attribute on the next line and use extra spaces or tabs for padding — which tends to look better with longer URLs.

The following four link definitions are, therefore, equivalent:
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
in ways that neither [Yahoo] [2] nor [MSN] [3] have quite managed.

  [1]: http://google.com/        "Google"
  [2]: http://search.yahoo.com/  "Yahoo Search"
  [3]: http://search.msn.com/    "MSN Search"
~~~

Which generates:

~~~html
<p>In recent years it seems that <a href="http://google.com/"title="Google">Google</a>
has dominated the search engine market in ways that neither <a href="http://search.yahoo.com/"
title="Yahoo Search">Yahoo</a> nor <a href="http://search.msn.com/"
title="MSN Search">MSN</a> have quite managed.</p>
~~~

With Markdown’s reference-style links, a source document much more closely resembles the final output, as rendered in a browser. By allowing you to move the markup-related metadata out of the paragraph, you can add links without interrupting the narrative flow of your prose.

### Automatic Links

Markdown provides a shortcut style to create ‘automatic’ links for URLs and email addresses — for situations in which you want to show the *actual* text of a URL or email address and also have it be a clickable link. To do so, simply surround the URL or email address with angle brackets, like so:

~~~markdown
<http://example.com/>
~~~

Which Markdown will convert to:

~~~html
<a href="http://example.com/">http://example.com/</a>
~~~

Automatic links for email addresses work in the same way, except that Markdown will also perform a bit of randomized decimal and hex entity-encoding to help obscure your address from address-harvesting spambots. For example, Markdown will turn _either_ of these two code snippets:

~~~markdown
<address@example.com>
~~~
~~~markdown
<mailto:address@example.com>
~~~

into something like this:

~~~html
<a href="&#x6D;&#x61;i&#x6C;&#x74;&#x6F;:&#x61;&#x64;&#x64;&#x72;&#x65;
&#115;&#115;&#64;&#101;&#120;&#x61;&#109;&#x70;&#x6C;e&#x2E;&#99;&#111;
&#109;">&#x61;&#x64;&#x64;&#x72;&#x65;&#115;&#115;&#64;&#101;&#120;&#x61;
&#109;&#x70;&#x6C;e&#x2E;&#99;&#111;&#109;</a>
~~~

which will render in a browser as a clickable link to 'address&commat;example.com'.

NOTE: **Note:** This sort of entity-encoding trick will fool a great many address-harvesting bots, but it most certainly won’t fool all of them. Whilst it’s better than nothing, an address published in this way will probably start receiving spam eventually.





## Images

[TOC=3]

Markdown uses an image syntax that closely resembles the syntax for links, allowing for two different styles: _inline_ and _reference_.

### Images, inline style

Inline image syntax looks like this:

~~~markdown
![Alt text](/path/to/img.jpg)
![Alt text](/path/to/img.jpg "Optional title")
~~~

As you can see, this is very similar to the [inline link](#links-inline-style) syntax.

### Images, reference style

Reference-style image syntax looks like this:

~~~markdown
![Alt text][id]
~~~

Where “id” is the name of a defined image reference. Image references are defined using syntax identical to link references:

~~~markdown
[id]: url/to/image  "Optional title attribute"
~~~

The ‘path’ portion of the image reference may, optionally, be surrounded by angle brackets. The ‘title’ part, if included, should be enclosed in either double quotes or standard parentheses. Additionally, you can put the title attribute on the next line and use extra spaces or tabs for padding — which tends to look better with longer paths.

The following four image references are, therefore, equivalent:

~~~markdown
[foo]: path/to/image.jpg "Optional title for the link"
[foo]: path/to/image.jpg (Optional title for the link)
[foo]: <path/to/image.jpg> "Optional title for the link"
[foo]: very/long/server/path/to/a/deeply/buried/image.jpg
       (Optional title for the link)
~~~

Image reference names may consist of letters, numbers, spaces, and punctuation. They are not case sensitive.

TIP: **Tip:** Although you can use single quotes to delineate the title attribute for _inline-style_ images, for _reference-style_ images double quotes must be used. To avoid having to remember this distinction, it may be simplest to just stick to using double quotes.

Just as with [link](#links-reference-style) and [abbreviation](#abbreviations) definitions, image definitions can be placed anywhere in your document. They are stripped out during processing, and will not appear in the final output.

Currently, Markdown has no syntax for specifying the dimensions of an image; if you need this then you can simply use regular HTML `<img>` tags.





## Emphasis

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





## Footnotes

[TOC=3]

### Creating footnotes

Footnotes a created in a way similar to reference-style links. A footnote consists, firstly, of a marker in the text that will be turned into a linked superscript number. The second part is a footnote definition that can be placed anywhere in the document and which, once processed, will be added to an ordered list of footnotes at the end of the document.

NOTE: **Note:** In this respect footnotes differ from abbreviations, and reference-style links and images, because footnote definitions are **not** removed from the document during processing (though they may be relocated if not already at the end of the document).

Example:

~~~markdown
This is some text with a footnote.[^1]

[^1]: And this is the footnote itself.
~~~

Generates:

~~~html
<p>This is some text with a footnote.
	<sup id="fnref:1">
		<a href="#fn:1" class="footnote-ref">2</a>
	</sup>
</p>
<div class="footnotes">
	<hr />
	<ol>
		<li id="fn:1">
			<p>And this is the footnote itself&#160;
				<a href="#fnref:1" class="footnote-backref">&#8617;&#xFE0E;</a>
			</p>
		</li>
	</ol>
</div>
~~~

This looks a little cryptic, but what the browser will display to the end user is this:

> This is some text with a footnote.<sup><a href="#fnote1b" id="fnote1a">1</a></sup>
> ***
> 1. And this is the footnote itself. <a href="#fnote1a" id="fnote1b">↩︎</a>

### ID names and footnote ordering

Each footnote must have a distinct name. Names can contain any character valid within an `id` attribute in HTML, and that name will be used _solely_ to allow Markdown to link footnote references to footnote definitions. However, it is important to realise that it has **no** effect on the final numbering of the footnotes.

NOTE: **Note:** Footnotes will always be listed in the order they are linked to in the text.

This can seem confusing if you use numbers as your marker IDs and then place those markers in the text out of numerical order. For example, consider this block of Markdown:

~~~markdown
This text has two footnotes[^2], but the linking markers
appear in the text out of numerical order.[^1]

[^1]: This footnote uses '1' as its marker text.
[^2]: This footnote uses '2' as its marker text.

~~~

Once converted it might, at first glance, appear to have erroneously swapped the footnotes around. What is presented to the reader in the web browser is the following:

> This text has two footnotes<sup><a href="#fnote2b" id="fnote2a">1</a></sup>, but the linking markers appear in the text out of numerical order.<sup><a href="#fnote3b" id="fnote3a">2</a></sup>
> ****
> 1. This footnote uses “2” as its marker text. <a href="#fnote2a" id="fnote2b">↩︎</a>
> 2. This footnote uses “1” as its marker text. <a href="#fnote3a" id="fnote3b">↩︎</a>

In fact nothing has gone wrong; Markdown has simply placed the footnotes in the same order as they appear in the text; the fact that they originally used different numbers for their marker IDs is irrelevant.

NOTE: **Important:** You cannot make two links to the same footnotes; if you try to, the second footnote reference will be left as plain text. Similarly, footnote references that are not linked to a valid footnote definition (and vice versa) will remain as plain text.

### Block-level content in footnotes

Just as you can with [list items](#paragraphs-in-list-items), you can include block-level elements in footnotes and it works in much the same way. To include multiple paragraphs in a footnote, simply indent each paragraph after the first by 4 spaces (or 1 tab). As with list items, you can be lazy about this and only indent the first line of the paragraph is you wish.

Additionally, if you want things to align more neatly, you can leave the first line of the footnote empty and put your first paragraph on the line below (indented by the same 4 spaces or 1 tab). All of the following footnote definitions are equivalent and generate the same HTML:

~~~markdown
[^1]: The European languages are members of the same family. Their
    separate existence is a myth. For science, music, sport, etc,
    Europe uses the same vocabulary.

    The languages only differ in their grammar, their pronunciation
    and their most common words.

~~~
~~~markdown
[^1]: The European languages are members of the same family. Their
separate existence is a myth. For science, music, sport, etc,
Europe uses the same vocabulary.

    The languages only differ in their grammar, their pronunciation
and their most common words.

~~~
~~~markdown
[^1]:
    The European languages are members of the same family. Their
    separate existence is a myth. For science, music, sport, etc,
    Europe uses the same vocabulary.

    The languages only differ in their grammar, their pronunciation
    and their most common words.

~~~

This following footnote definition will generate a footnote containing an unordered list:

~~~markdown
[^1]: The European languages are members of the same family. Their
    separate existence is a myth.

    - Here’s a reason
    - Here’s another reason
	- I'm all out of reasons.

~~~

And this one generates a footnote containing a blockquote, which in turn contains 2 paragraphs.:

~~~markdown
[^1]: The European languages are members of the same family. Their
separate existence is a myth. As Freud never said:

    > The languages only differ in their grammar, their
pronunciation and their most common words.

    > But they’re all lovely.

~~~





## Inline HTML

For any markup that is not covered by Markdown’s syntax, you simply use HTML itself. There’s no need to indicate that you’re switching from Markdown to HTML; you just use the tags.

Span-level HTML tags — `<span>`, `<cite>`, or `<del>`, for example — can be used anywhere in a Markdown block (a paragraph, list item, header, table, blockquote, code block, etc). You can even use regular HTML tags instead of Markdown formatting, if you are so inclined.

There are certain restrictions regarding *block* elements in Markdown:

1. The opening tag of a block element must not be indented by more than three spaces. Any tag indented more than that will be treated as a code block according to standard Markdown rules.
2. When the block element is inside a list item, all its content should be indented with the same amount of space as the list item is indented. (More indentation won’t do any harm as long as the first opening tag is not indented too much, becoming a code block — see first rule.)

<!--
The only restrictions are that block-level HTML elements — e.g. `<div>`, `<table>`, `<pre>`, `<p>`, etc. — must be separated from surrounding content by blank lines, and the start and end tags of the block should not be indented with tabs or spaces. Markdown is smart enough not to add extra (unwanted) `<p>` tags around HTML block-level tags. -->

For example, to add a `figure` element to a Markdown article:

~~~html
This is a regular paragraph.

<figure>
    <img src="/imgs/pink_elephant.jpg" alt="a pink elephant">
    <figcaption>Fig.1 - Sighted in Nowhereland</figcaption>
</figure>

This is another regular paragraph.
~~~

Markdown is smart enough not to add extra (unwanted) `<p>` tags around HTML block-level tags. Furthermore, if you try and insert block-level HTML inside a paragraph, Markdown will split the paragraph appropriately. For example, this text:

~~~html
This Markdown paragraph has some <span>span-level
	(inline) html</span> in the middle.
~~~

Gives:

~~~html
<p>This Markdown paragraph has some <span>span-level
	(inline) html</span> in the middle.</p>
~~~

However, if we try to force a `<div>` into a Markdown paragraph:

~~~html
This Markdown paragraph has a <div>block-level element</div> in
the middle. That's not allowed in HTML!
~~~

We end up with:

~~~html
<p>This Markdown paragraph has a</p>
<div>block-level element</div>
<p>in the middle. That’s not allowed in HTML!</p>
~~~





## Markdown inside HTML

Markdown syntax inside _span-level_ HTML elements is processed as normal.

In order for Markdown syntax to be processed inside *block-level* HTML elements, you can add the attribute  `markdown="1"` to the HTML element in question. This attribute will be stripped from the generated output, but will permit Markdown syntax to be correctly processed inside that HTML element. Note that the effects of the attribute are not passed onward to other, nested HTML elements. So if your Markdown document contains:

~~~html
<div>
	This text has some **heavy** emphasis.
</div>
~~~
Then the asterisks will be treated literally and the generated output will be entirely unchanghed. Whereas:
~~~html
<div markdown="1">
	This text has some **heavy** emphasis.
</div>
~~~

will be turned into:

~~~html
<div>
    This text has some <strong>heavy</strong> emphasis.
</div>
~~~

Markdown will apply the correct formatting intelligently according to the block element you put the markdown attribute on. If you apply the markdown attribute to a `<p>` tag for instance, it will only produce span-level elements inside — it won’t allow things such as lists, blockquotes, code blocks.

However, in some circumstances this can be ambiguous, such as:

~~~html
<table>
	<tr>
		<td markdown="1">This is *true* markdown text.</td>
	</tr>
</table>
~~~

A table cell can contain both span and block elements. In cases like this one, Markdown will only apply span-level rules. If you wish to enable block constructs, simply write `markdown="block"` instead.





## Special attributes

You can set the id and class attribute on certain elements using a special attribute block. The desired attributes are placed inside curly brackets at the end of the line, with multiple attributes being separated by spaces. (An id is denoted using a hash (#) and a class is indicated by using a dot (.), just like in <abbr title="cascading style sheets">CSS</abbr>). For example:

~~~markdown
Primary header {#element_id .class_name}
==============
~~~

Which will become:

~~~html
<h1 id="element_id" class="class_name">Primary header</h1>
~~~

Other attributes, including custom ones, can be added by specifying the attribute name, followed by an equal sign, followed by the value of the attribute.

~~~markdown
En Français {#header2 .section_header lang=fr}
----------------
~~~

The above Markdown syntax will become:

~~~html
<h2 id="header2" class="section_header" lang="fr">En Français</h2>
~~~

NOTE: **Note:** The value of an attribute cannot contain spaces, and so this technique can only used for attributes with simple values.

Special attribute blocks can be applied to:

- headers
- fenced code blockquotes
- links
- images

For image and links, put the special attribute block immediately after the parenthesis containing the address:

~~~markdown
[link](url){#id .class}  
![img](url){#id .class}
~~~

Or if using reference-style links and images, put it at the end of the definition line like this:

~~~markdown
[link][linkref]
![img][linkref]

[linkref]: url "optional title" {#id .class}
~~~





## Smart Typography

[TOC=3]

Markdown in ExpressionEngine employs some parts of the SmartyPants library to add some 'smart' typographic nicety to your prose. This allows authors to write using plain old 'straight' quotes, plain dashes (hyphens) and plain dots, safe in the knowledge that their final HTML document will contain curly quotes, en/em-dashes, and proper ellipses.

NOTE: **Note:** These automatic substitutions will not take place within `<pre>`, `<code>`, `<kbd>`, or `<script>` tag blocks — contexts within which such changes may not be required or appropriate.

The precise transformations that get applied are as follows:

### Quotes

Various types of quotes are turned into their 'typographic' (curly) equivalents. The kinds of quotes processed in this way are normal (straight) quotes, ‘backtick’-style quotes, and ‘comma’-style quotes. So:

~~~markdown
'normal single quotes'

"normal single quotes"

``backtick-style quotes''

,,comma-style quotes``
~~~

becomes:

~~~html
&#8216;normal single quotes&#8217;

&#8220;normal single quotes&#8221;

&#8220;backtick-style quotes&#8221;

,,comma-style quotes&#8220;
~~~

which the browser will present as:

~~~
‘normal single quotes’

“normal single quotes”

“backtick-style quotes”

,,comma-style quotes“
~~~

### Dashes

Double-dashes will be converted into en-dash entities. Triple-dashes will be converted to em-dash entities. So:

~~~markdown
An en dash simply means ‘through’, eg. 18 July--12 November.

An em dash is a break---not to be confused with a hyphen.
~~~

becomes:

~~~html
<p>An en dash simply means ‘through’, eg. 18 July&#8211;12 November.</p>
<p>An em dash is a break&#8212;not to be confused with a hyphen.</p>
~~~

### Ellipses

Three dots in a row will be converted to a proper ellipsis entity:

~~~markdown
An ellipsis can indicate ... deleted text.
~~~

becomes:

~~~html
<p>An ellipsis can indicate &#8230; deleted text.</p>
~~~

TIP: **Tip:** If you wish characters (that would otherwise be substituted) to be interpreted *literally*, you can use [backslash escapes](#backslash-escapes). For instance, to describe somebody's height you can type `John is 5\'11\" tall`.





## Auto-escaping for special characters

HTML uses two characters, in particular, that require special treatment: `<` and `&`. Left angle brackets are used to start tags, whilst ampersands denote the beginning of an HTML entity. To use them as literal characters HTML authors need to escape them by using their entity equivalents (eg. `&lt;` and `&amp;` respectively) - something that soon becomes a tiresome chore and can easily be forgotten, leading to a failed HTML validation.

Markdown allows you to use these characters naturally, taking care of all the necessary escaping for you. If you use an ampersand as part of an HTML entity, it remains unchanged; otherwise it will be translated into `&amp;`.

For example, if you want to include a copyright symbol in your article, you can write:

~~~markdown
&copy;
~~~

and Markdown will leave it alone. But if you write:

~~~markdown
AT&T
~~~

Markdown will translate it to:

~~~html
AT&amp;T
~~~

Similarly, because Markdown supports [inline HTML](#inline-html), if you use angle brackets as delimiters for HTML tags, Markdown will treat them as such. But if you write:

~~~markdown
4 < 5
~~~

Markdown will translate it to:

~~~html
4 &lt; 5
~~~

TIP: **Tip:** Inside Markdown’s code spans and blocks, angle brackets and ampersands are _always_ encoded automatically. This makes it easy to use Markdown to write about HTML code — unlike native HTML, in which every single < and & in your example code would need to be escaped).





## Backslash escapes

In addition to [automatic escaping](#auto-escaping-for-special-characters), you can use backslash escapes to generate literal characters which would otherwise have special meaning in Markdown’s formatting syntax. For example, if you wanted to surround a word with literal asterisks (instead of an HTML `<em>` tag), you can use backslashes before the asterisks, like this:

~~~markdown
\*literal asterisks\*
~~~

Markdown provides backslash escapes for the following characters:

| Char   | Entity              | Char name           |
| ------ | ------------------- | ------------------- |
| \      | `&#92;`             | backslash           |
| `      | `&#96;`             | backtick            |
| *      | `&#42;`             | asterisk            |
| _      | `&#95;`             | underscore          |
| &#39;  | `&#39;`             | single quote        |
| &#34;  | `&#34;`             | double quote        |
| { }    | `&#123;` / `&#125;` | curly braces        |
| [ ]    | `&#91;` / `&#93;`   | square brackets     |
| ( )    | `&#40;` / `&#41;`   | parentheses         |
| #      | `&#35;`             | hash mark           |
| +      | `&#43;`             | plus sign           |
| -      | `&#45;`             | minus sign (hyphen) |
| .      | `&#46;`             | dot                 |
| !      | `&#33;`             | exclamation mark    |
| :      | `&#58;`             | colon               |
| \|     | `&#124;`            | pipe (vertical bar) |

NOTE: **Note:** Unlike [automatic escaping](#auto-escaping-for-special-characters), backslash escapes use *decimal-encoded* entities rather than named entities. In this respect backslash escapes are like the substitutions performed by [smart typography](#smart-typography).





## Extras

Markdown generates HTML that will be compatible with both an XHTML and HTML doctype — in other words, element tags such as `<image />`, `<br />`, & `<hr />` will be created with a self-closing forward slash at the end, and closing tags _will_ be created for elements where a closing tag is theoretically optional.

John Gruber has made a [Markdown web dingus](https://daringfireball.net/projects/markdown/dingus) available at Daring Fireball that you can use to try out Markdown and practice getting to grips with the syntax.





## Abbreviations

Markdown supports abbreviations (`<abbr>`) using a syntax somewhat similar to the two-part ‘reference’ technique used by links and images. You define abbreviations like so:

~~~markdown
*[HTML]: Hyper Text Markup Language
*[W3C]:  World Wide Web Consortium
~~~

Then, wherever those specified abbreviations appear in your document, they will be processed accordingly. So:

~~~markdown
The HTML specification
is maintained by the W3C.
~~~

Becomes:

~~~html
The <abbr title="Hyper Text Markup Language">HTML</abbr> specification
is maintained by the <abbr title="World Wide Web Consortium">W3C</abbr>.
~~~

Abbreviations **are** case-sensitive, and will span on multiple words when defined as such. An abbreviation may also have an empty definition, in which case `<abbr>` tags will be added in the text but the title attribute will be omitted.

~~~markdown
Operation Tigra Genesis is going well.

*[Tigra Genesis]:
~~~

Abbreviation definitions can be placed anywhere in your document. They are stripped from the final output, just like [link](#links-reference-style) and [image](#images-reference-style) definitions.
