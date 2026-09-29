+++
title = "Shortcode: Layouts"
date = 2026-04-19
description = "Shortcodes for arranging content: borders, wide blocks, columns and tabs."

[taxonomies]
tags = ["layout", "shortcode", "zola"]

[extra]
# Demo headings inside a row/col example, not sections.
toc_exclude = ["left", "right"]
series = "Shortcodes"
series_part = 2
+++

Shortcodes for *arranging* content. For the ones that insert it, see
[Shortcode: Elements](@/posts/shortcode.md). For the ones that lean on a
bundled external library, see [Shortcode: Externals](@/posts/externals.md).

Each example shows the shortcode and its template macro.

## Borders

{% tabs(titles=["markdown content", "template files"], group="usage") %}
```md
{​% border() %​}
Any markdown goes inside.
{​% end %​}

{​% border(size="lg", color="pink", style="dashed") %​}
With a size, a colour and a line style.
{​% end %​}
```
```jinja2
{​% import "macros/blocks.html" as blocks %​}
{​{ blocks::border(content="<p>Any markdown goes inside.</p>") }​}
{​{ blocks::border(content="<p>With a size, a colour and a line style.</p>", size="lg", color="pink", style="dashed") }​}
```
{% end %}

sizes&nbsp; : `sm`, `md` (default), `lg`, `xl`  
colours : `white` (default), `red`, `orange`, `yellow`, `lime`, `green`, `cyan`, `blue`, `purple`, `pink`, `muted`  
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

{% border(size="md", color="red", style="dashed") %}
`size="md"`, `color="red"`, `style="dashed"`
{% end %}

{% border(size="md", color="blue", style="dotted") %}
`size="md"`, `color="blue"`, `style="dotted"`
{% end %}

`double` needs at least 3px to separate into two lines, so it looks solid at
`size="sm"`.

## Alignment

{% tabs(titles=["markdown content", "template files"], group="usage") %}
```md
{​% align(align="center") %​}
Centered text.
{​% end %​}
```
```jinja2
{​% import "macros/blocks.html" as blocks %​}
{​{ blocks::align(content="<p>Centered text.</p>", align="center") }​}
```
{% end %}

align
: `left` (default), `center`, `right`


{% align(align="center") %}
Centered text.
{% end %}

### Center, Left, & Right
Presets of `align`:

{% tabs(titles=["markdown content", "template files"], group="usage") %}
```md
{​% center() %​}
Centered text.
{​% end %​}

{​% right() %​}
Right-aligned text.
{​% end %​}
```
```jinja2
{​{ blocks::align(content="<p>Centered text.</p>", align="center") }​}
{​{ blocks::align(content="<p>Right-aligned text.</p>", align="right") }​}
```
{% end %}

{% center() %}
Centered text.
{% end %}

{% right() %}
Right-aligned text.
{% end %}

## Wide Content

{% tabs(titles=["markdown content", "template files"], group="usage") %}
```md
{​% wide() %​}
![a wide screenshot](/images/wide.png)
{​% end %​}

{​% wide(size="xl") %​}
Spans the whole screen.
{​% end %​}
```
```jinja2
{​% import "macros/blocks.html" as blocks %​}
{​{ blocks::wide(content='<p><img src="/images/wide.png" alt="a wide screenshot" /></p>') }​}
{​{ blocks::wide(content="<p>Spans the whole screen.</p>", size="xl") }​}
```
{% end %}

sizes : `sm`, `md` (default), `lg`, `xl` (as wide as the screen allows)

Capped at the screen width; widen the window to see them differ.

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

`row` puts each top-level block side by side; `col` stacks them.

{% tabs(titles=["markdown content", "template files"], group="usage") %}
```md
{​% row() %​}
Left paragraph.

Right paragraph.
{​% end %​}
```
```jinja2
{​% import "macros/blocks.html" as blocks %​}
{​% set a = blocks::col(content="<p>Left</p>", span="2") %​}
{​% set b = blocks::col(content="<p>Right</p>") %​}
{​{ blocks::row(content=a ~ b) }​}
```
{% end %}

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
### Left
Text under the heading.
{% end %}
{% col() %}
### Right
Text under the heading.
{% end %}
{% end %}

gaps : `sm`, `md` (default), `lg` — on both `row` and `col`

### Col/Row Proportions

`span` works like colspan: `span="2"` is twice the width of a default column.

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

Columns stack on narrow screens. For more room, nest a `row` in [`wide`](#wide-content).

## Tabs

`tabs` shows several code blocks as tabs.

{% tabs(titles=["markdown content", "template files"], group="usage") %}
````md
{​% tabs(titles=["Python", "Java"]) %​}
```python
print("hi")
```
```java
System.out.println("hi");
```
{​% end %​}
````
```jinja2
{​% import "macros/blocks.html" as blocks %​}
{​{ blocks::tabs(content=panels, titles=["Python", "Java"], id="api") }​}
```
{% end %}

titles : one label per code block, in order  
group&nbsp; : optional name; blocks sharing one switch together

{% tabs(titles=["Python", "Java"]) %}
```python
print("hi")
```
```java
System.out.println("hi");
```
{% end %}

Works without JavaScript. Blocks with the same `group` switch together — every
example on this page uses `group="usage"`. From a template, pass your own `id`.
