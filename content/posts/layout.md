+++
title = "Supported Layouts"
date = 2026-04-19
description = "Shortcodes for arranging content: borders, wide blocks, columns and tabs."

[taxonomies]
tags = ["layout", "shortcode", "zola"]
+++

Shortcodes for *arranging* content. For the ones that insert it, see
[Supported Shortcodes](@/posts/shortcode.md).

Each is a thin wrapper over a macro in `macros/blocks.html`, so the same thing
is callable from Markdown and from a template. Both forms are shown throughout.

## Borders

<u>markdown content</u>:

```md
{​% border() %​}
Any markdown goes inside.
{​% end %​}

{​% border(size="lg", color="pink", style="dashed") %​}
With a size, a colour and a line style.
{​% end %​}
```

<u>template files</u>:

```jinja2
{​% import "macros/blocks.html" as blocks %​}
{​{ blocks::border(content="<p>Any HTML.</p>", size="lg", color="pink") }​}
```

sizes&nbsp; : `sm`, `md` (default), `lg`, `xl`  
colours : `white` (default), `yellow`, `pink`, `green`, `muted`  
styles&nbsp; : `solid` (default), `dashed`, `dotted`, `double`

{% border(size="sm") %}
`size="sm"` — defaults to `color="white"` and `style="solid"`
{% end %}

{% border(size="md", color="yellow", style="dashed") %}
`size="md"`, `color="yellow"`, `style="dashed"`
{% end %}

{% border(size="lg", color="pink", style="dotted") %}
`size="lg"`, `color="pink"`, `style="dotted"`
{% end %}

{% border(size="xl", color="green", style="double") %}
`size="xl"`, `color="green"`, `style="double"`
{% end %}

`double` needs at least 3px to separate into two lines, so it looks solid at
`size="sm"`.

## Wide Content

<u>markdown content</u>:

```md
{​% wide() %​}
![a wide screenshot](/images/wide.png)
{​% end %​}

{​% wide(size="xl") %​}
Spans the whole screen.
{​% end %​}
```

<u>template files</u>:

```jinja2
{​% import "macros/blocks.html" as blocks %​}
{​{ blocks::wide(content="<p>Wider than the column.</p>", size="lg") }​}
```

sizes : `sm`, `md` (default), `lg`, `xl` (as wide as the screen allows)

Each size is capped at the screen width, so on a narrow screen they all fall
back to the normal column. Widen this window to see them separate.

{% wide(size="sm") %}
{% border(color="yellow") %}
`size="sm"`
{% end %}
{% end %}

{% wide(size="md") %}
{% border(color="pink") %}
`size="md"` — the default
{% end %}
{% end %}

{% wide(size="lg") %}
{% border(color="green") %}
`size="lg"`
{% end %}
{% end %}

{% wide(size="xl") %}
{% border() %}
`size="xl"`
{% end %}
{% end %}

## Columns and Rows

`row` lays its contents out side by side; `col` stacks them. Every top-level
block inside becomes an item, so two paragraphs are already two columns.

<u>markdown content</u>:

```md
{​% row() %​}
Left paragraph.

Right paragraph.
{​% end %​}
```

<u>template files</u> — Tera cannot combine a macro call with `~` in one
expression, so build the columns with `set` first:

```jinja2
{​% import "macros/blocks.html" as blocks %​}
{​% set a = blocks::col(content="<p>Left</p>", span="2") %​}
{​% set b = blocks::col(content="<p>Right</p>") %​}
{​{ blocks::row(content=a ~ b) }​}
```

{% row() %}
Left paragraph.

Right paragraph.
{% end %}

Wrap blocks in `col` to group several of them into one column:

```md
{​% row() %​}
{​% col() %​}
### Left
Text under the heading.
{​% end %​}
{​% col() %​}
### Right
Text under the heading.
{​% end %​}
{​% end %​}
```

{% row() %}
{% col() %}
#### Left
Text under the heading.
{% end %}
{% col() %}
#### Right
Text under the heading.
{% end %}
{% end %}

gaps : `sm`, `md` (default), `lg` — on both `row` and `col`

### Proportions

`span` works like a table's colspan: a column with `span="2"` is exactly twice
the width of a default one. Both the flex basis and the grow factor scale with
it, so the ratio holds at any container width.

```md
{​% row() %​}
{​% col(span="2") %​}
Twice the width.
{​% end %​}
{​% col() %​}
Half of that.
{​% end %​}
{​% end %​}
```

{% row(gap="sm") %}
{% col(span="2") %}
{% border(size="sm", color="yellow") %}
`span="2"`
{% end %}
{% end %}
{% col() %}
{% border(size="sm", color="green") %}
`span="1"`
{% end %}
{% end %}
{% end %}

{% row(gap="sm") %}
{% col(span="3") %}
{% border(size="sm", color="pink") %}
`span="3"`
{% end %}
{% end %}
{% col() %}
{% border(size="sm") %}
`1`
{% end %}
{% end %}
{% end %}

A span only applies to a `col` (or a `row` nested in another `row`), so a bare
paragraph needs wrapping in `col` before it can take one.

Columns collapse to a stack on narrow screens. Three fit at the default gap;
for more room, nest a `row` inside [`wide`](#wide-content).

## Tabbed Code Blocks

`code` shows several code blocks as tabs — handy for the same example in more
than one language.

<u>markdown content</u>:

````md
{​% code(titles=["Python", "Java"]) %​}
```python
print("hi")
```
```java
System.out.println("hi");
```
{​% end %​}
````

<u>template files</u>:

```jinja2
{​% import "macros/blocks.html" as blocks %​}
{​{ blocks::code(content=panels, titles=["Python", "Java"], id="api") }​}
```

titles : one label per code block, in order

{% code(titles=["Python", "Java"]) %}
```python
print("hi")
```
```java
System.out.println("hi");
```
{% end %}

The body should hold nothing but fenced code blocks: each one becomes a panel,
and panels pair with titles by position. Switching is a radio group rather than
a script, so it works with JavaScript disabled and the arrow keys move between
tabs. The shortcode uses Zola's per-page `nth` to keep groups apart; from a
template, pass your own `id`.
