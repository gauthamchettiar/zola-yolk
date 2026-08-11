+++
title = "Supported Layouts"
date = 2026-04-19
description = "Shortcodes for arranging content: borders, wide blocks, and columns."

[taxonomies]
tags = ["layout", "shortcode", "zola"]
+++

Shortcodes for *arranging* content — framing it, letting it break out of the
reading column, and splitting it into columns. For the ones that insert content,
see [Supported Shortcodes](@/posts/shortcode.md).

## Borders

This is how you can draw a border around content in,

<u>markdown content</u>:

```md
{​% border() %​}
Any markdown goes inside.
{​% end %​}

{​% border(size="lg", color="pink") %​}
With a size and a colour.
{​% end %​}
```

sizes&nbsp;&nbsp; : `sm`, `md` (default), `lg`, `xl`  
colours : `white` (default), `yellow`, `pink`, `green`  

{% border(size="sm") %}
`size="sm"` — defaults to `color="white"`
{% end %}

{% border(size="md", color="yellow") %}
`size="md"`, `color="yellow"`
{% end %}

{% border(size="lg", color="pink") %}
`size="lg"`, `color="pink"`
{% end %}

{% border(size="xl", color="green") %}
`size="xl"`, `color="green"`
{% end %}

## Wide Content

This is how you can let content break out of the reading column,

<u>markdown content</u>:

```md
{​% wide() %​}
![a wide screenshot](/images/wide.png)
{​% end %​}

{​% wide(size="xl") %​}
Spans the whole screen.
{​% end %​}
```

sizes : `sm`, `md` (default), `lg`, `xl` (as wide as the screen allows)

Each size is capped at the screen width, so on a narrow screen they all fall back
to the normal column. Widen this window to see them separate.

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
block inside becomes an item, so two paragraphs are already two columns —

<u>markdown content</u>:

```md
{​% row() %​}
Left paragraph.

Right paragraph.
{​% end %​}
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

gaps : `sm`, `md` (default), `lg` — on both `row` and `col`

Columns share the width evenly and wrap to a stack once there is no room, so
this collapses to a single column on a phone. Three fit at the default gap;
for more room, nest a `row` inside [`wide`](#wide-content).

{% row(gap="sm") %}
{% border(size="sm", color="yellow") %}
one
{% end %}
{% border(size="sm", color="pink") %}
two
{% end %}
{% border(size="sm", color="green") %}
three
{% end %}
{% end %}

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

{% code(titles=["Python", "Java"]) %}
```python
print("hi")
```
```java
System.out.println("hi");
```
{% end %}

titles : one label per code block, in order

The body should hold nothing but fenced code blocks: each one becomes a panel,
and panels pair with titles by position. Switching is a radio group rather than
a script, so it works with JavaScript disabled and the arrow keys move between
tabs.
