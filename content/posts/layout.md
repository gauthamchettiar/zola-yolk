+++
title = "Components: Layouts"
date = 2026-04-19
description = "Components for arranging content: borders, wide blocks, columns and tabs."

[taxonomies]
tags = ["layout", "component", "zola"]

[extra]
# Demo headings inside a row/col example, not sections.
toc_exclude = ["left", "right"]
series = "Components"
series_part = 2
+++

Components for *arranging* content. For the ones that insert it, see
[Components: Elements](@/posts/shortcode.md). For the ones that lean on a
bundled external library, see [Components: Externals](@/posts/externals.md).

The body is Markdown; from a template, unindented HTML passes through as is.

## Borders

{% raw %}
```md
{% <border> %}
Any markdown goes inside.
{% </border> %}

{% <border size="lg" color="pink" style="dashed"> %}
With a size, a colour and a line style.
{% </border> %}
```
{% endraw %}

sizes&nbsp; : `sm`, `md` (default), `lg`, `xl`  
colours : `white` (default), `red`, `orange`, `yellow`, `lime`, `green`, `cyan`, `blue`, `purple`, `pink`, `muted`  
styles&nbsp; : `solid` (default), `dashed`, `dotted`, `double`

{% <border size="sm"> %}
`size="sm"` — defaults to `color="white"` and `style="solid"`
{% </border> %}

{% <border size="md" color="yellow" style="dashed"> %}
`size="md"`, `color="yellow"`, `style="dashed"`
{% </border> %}

{% <border size="lg" color="pink" style="dotted"> %}
`size="lg"`, `color="pink"`, `style="dotted"`
{% </border> %}

{% <border size="xl" color="green" style="double"> %}
`size="xl"`, `color="green"`, `style="double"`
{% </border> %}

{% <border size="md" color="red" style="dashed"> %}
`size="md"`, `color="red"`, `style="dashed"`
{% </border> %}

{% <border size="md" color="blue" style="dotted"> %}
`size="md"`, `color="blue"`, `style="dotted"`
{% </border> %}

`double` needs at least 3px to separate into two lines, so it looks solid at
`size="sm"`.

## Alignment

{% raw %}
```md
{% <align align="center"> %}
Centered text.
{% </align> %}
```
{% endraw %}

align
: `left` (default), `center`, `right`


{% <align align="center"> %}
Centered text.
{% </align> %}

### Center, Left, & Right
Presets of `align`:

{% raw %}
```md
{% <center> %}
Centered text.
{% </center> %}

{% <right> %}
Right-aligned text.
{% </right> %}
```
{% endraw %}

{% <center> %}
Centered text.
{% </center> %}

{% <right> %}
Right-aligned text.
{% </right> %}

## Wide Content

{% raw %}
```md
{% <wide> %}
![a wide screenshot](/images/wide.png)
{% </wide> %}

{% <wide size="xl"> %}
Spans the whole screen.
{% </wide> %}
```
{% endraw %}

sizes : `sm`, `md` (default), `lg`, `xl` (as wide as the screen allows)

Capped at the screen width; widen the window to see them differ.

{% <wide size="sm"> %}
{% <border color="yellow"> %}
`size="sm"`
{% </border> %}
{% </wide> %}

{% <wide size="md"> %}
{% <border color="pink"> %}
`size="md"` — the default
{% </border> %}
{% </wide> %}

{% <wide size="lg"> %}
{% <border color="green"> %}
`size="lg"`
{% </border> %}
{% </wide> %}

{% <wide size="xl"> %}
{% <border> %}
`size="xl"`
{% </border> %}
{% </wide> %}

## Columns and Rows

`row` puts each top-level block side by side; `col` stacks them.

{% raw %}
```md
{% <row> %}
Left paragraph.

Right paragraph.
{% </row> %}
```
{% endraw %}

{% <row> %}
Left paragraph.

Right paragraph.
{% </row> %}

Wrap blocks in `col` to group several of them into one column:

{% raw %}
```md
{% <row> %}
{% <col> %}
### Left
Text under the heading.
{% </col> %}
{% <col> %}
### Right
Text under the heading.
{% </col> %}
{% </row> %}
```
{% endraw %}

{% <row> %}
{% <col> %}
### Left
Text under the heading.
{% </col> %}
{% <col> %}
### Right
Text under the heading.
{% </col> %}
{% </row> %}

gaps : `sm`, `md` (default), `lg` — on both `row` and `col`

### Col/Row Proportions

`span` works like colspan: `span="2"` is twice the width of a default column.

{% raw %}
```md
{% <row> %}
{% <col span="2"> %}
Twice the width.
{% </col> %}
{% <col> %}
Half of that.
{% </col> %}
{% </row> %}
```
{% endraw %}

{% <row gap="sm"> %}
{% <col span="2"> %}
{% <border size="sm" color="yellow"> %}
`span="2"`
{% </border> %}
{% </col> %}
{% <col> %}
{% <border size="sm" color="green"> %}
`span="1"`
{% </border> %}
{% </col> %}
{% </row> %}

{% <row gap="sm"> %}
{% <col span="3"> %}
{% <border size="sm" color="pink"> %}
`span="3"`
{% </border> %}
{% </col> %}
{% <col> %}
{% <border size="sm"> %}
`1`
{% </border> %}
{% </col> %}
{% </row> %}

Columns stack on narrow screens. For more room, nest a `row` in [`wide`](#wide-content).

## Tabs

`tabs` shows several code blocks as tabs.

{% raw %}
````md
{% <tabs titles={["Python", "Java"]}> %}
```python
print("hi")
```
```java
System.out.println("hi");
```
{% </tabs> %}
````
{% endraw %}

titles : one label per code block, in order  
group&nbsp; : optional name; blocks sharing one switch together  
id&nbsp;&nbsp;&nbsp;&nbsp; : optional; only needed for two otherwise identical blocks

{% <tabs titles={["Python", "Java"]}> %}
```python
print("hi")
```
```java
System.out.println("hi");
```
{% </tabs> %}

Works without JavaScript. Blocks with the same `group` switch together — pick
a language in either block below:

{% <tabs titles={["Python", "Java"]} group="lang"> %}
```python
print("hello")
```
```java
System.out.println("hello");
```
{% </tabs> %}

{% <tabs titles={["Python", "Java"]} group="lang"> %}
```python
print("bye")
```
```java
System.out.println("bye");
```
{% </tabs> %}
