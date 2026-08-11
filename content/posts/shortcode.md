+++
title = "Supported Shortcodes"
date = 2026-04-20
description = "Shortcodes that insert content: icons, links, marks, quotes, callouts and theme-conditional blocks."

[taxonomies]
tags = ["shortcode", "syntax", "zola"]
+++

Shortcodes for *inserting* content. For the ones that arrange it — borders,
wide blocks, columns and tabs — see [Supported Layouts](@/posts/layout.md).

Every shortcode here is a thin wrapper over a macro, so the same thing is
callable from Markdown and from a template. Both forms are shown throughout.

## Icons

<u>markdown content</u>:

```md
{​{ icon(name="star") }​}
{​{ icon(name="github", style="brands") }​}
{​{ icon(name="star", style="regular", class="text-accent", aria="favorite") }​}
```

<u>template files</u>:

```jinja2
{​% import "macros/widgets.html" as widgets %​}
{​{ widgets::icon(name="star") }​}
{​{ widgets::icon(name="github", style="brands") }​}
```

name : Font Awesome icon name &nbsp;·&nbsp; style : `solid` (default), `regular`, `brands`  
class : extra CSS classes &nbsp;·&nbsp; aria : label; omitted makes the icon decorative

star&nbsp;&nbsp; : {{ icon(name="star") }}  
github : {{ icon(name="github", style="brands") }}  
lemon&nbsp; : {{ icon(name="lemon", style="regular") }}  

## External Links

Opens in a new tab with `rel="noopener noreferrer"` and appends an indicator.

<u>markdown content</u>:

```md
{​{ elink(text="Example", href="https://example.com") }​}
{​{ elink(text="Example", href="https://example.com", new_tab=false) }​}
{​{ elink(text="Example", href="https://example.com", show_icon=false) }​}
```

<u>template files</u>:

```jinja2
{​% import "macros/widgets.html" as widgets %​}
{​{ widgets::elink(text="Example", href="https://example.com") }​}
```

text, href : required &nbsp;·&nbsp; new_tab : default `true` &nbsp;·&nbsp; show_icon : default `true`

default&nbsp;&nbsp;&nbsp; : {{ elink(text="Example", href="https://example.com") }}  
no new tab : {{ elink(text="Example", href="https://example.com", new_tab=false) }}  
no icon&nbsp;&nbsp;&nbsp; : {{ elink(text="Example", href="https://example.com", show_icon=false) }}  

## Mark

Calls out a run of text, either filled or outlined.

<u>markdown content</u>:

```md
{​{ mark(text="highlighted") }​}
{​{ mark(text="outlined", color="pink", decoration="border") }​}
```

<u>template files</u>:

```jinja2
{​% import "macros/widgets.html" as widgets %​}
{​{ widgets::mark(text="highlighted", color="green") }​}
```

colors : `white`, `yellow` (default), `pink`, `green`, `muted`  
decoration : `highlight` (default), `border`

filled&nbsp;&nbsp; : {{ mark(text="yellow") }} {{ mark(text="pink", color="pink") }} {{ mark(text="green", color="green") }}  
outlined : {{ mark(text="yellow", decoration="border") }} {{ mark(text="pink", color="pink", decoration="border") }} {{ mark(text="green", color="green", decoration="border") }}

## Quotes

An attributed quotation, rendered as `<figure>` / `<blockquote>` / `<figcaption>`
— the attribution describes the quote, so HTML puts it outside the quote itself.

<u>markdown content</u>:

```md
{​% quote(author="Alan Kay", cite="1971") %​}
The best way to predict the future is to invent it.
{​% end %​}
```

<u>template files</u>:

```jinja2
{​% import "macros/blocks.html" as blocks %​}
{​{ blocks::quote(content="<p>…</p>", author="Alan Kay", cite="1971") }​}
```

author : who said it &nbsp;·&nbsp; cite : the work, rendered in `<cite>`  
url : source URL, sets the blockquote's `cite` attribute and links the citation  
colors : `white`, `yellow`, `pink` (default), `green`, `muted`

{% quote(author="Alan Kay", cite="1971") %}
The best way to predict the future is to invent it.
{% end %}

{% quote(author="Tim Berners-Lee", cite="Weaving the Web", url="https://example.com", color="green") %}
The Web does not just connect machines, it connects people.
{% end %}

## Admonitions

A callout set apart from the surrounding text, rendered as `<aside>`.

<u>markdown content</u>:

```md
{​% admonition(title="Note") %​}
Worth knowing.
{​% end %​}

{​% admonition(title="Careful", icon="triangle-exclamation", color="pink") %​}
This one bites.
{​% end %​}
```

<u>template files</u>:

```jinja2
{​% import "macros/blocks.html" as blocks %​}
{​{ blocks::admonition(content="<p>Worth knowing.</p>", title="Note") }​}
```

title : optional heading &nbsp;·&nbsp; icon : Font Awesome name, default `circle-info`  
colors : `white`, `yellow` (default), `pink`, `green`, `muted`

{% admonition(title="Note") %}
Worth knowing.
{% end %}

{% admonition(title="Careful", icon="triangle-exclamation", color="pink") %}
This one bites.
{% end %}

{% admonition(icon="lightbulb", color="green") %}
An icon with no title works too.
{% end %}

## Light and Dark Mode Content

Whatever is inside `lmode` shows only in light mode, and `dmode` only in dark.

<u>markdown content</u>:

```md
{​% lmode() %​}
Only visible in light mode.
{​% end %​}

{​% dmode() %​}
Only visible in dark mode.
{​% end %​}
```

<u>template files</u>:

```jinja2
{​% import "macros/blocks.html" as blocks %​}
{​{ blocks::lmode(content="<p>Light only.</p>") }​}
{​{ blocks::dmode(content="<p>Dark only.</p>") }​}
```

Neither takes parameters. Both variants are emitted and CSS reveals the matching
one, so this works with JavaScript disabled. Toggle the theme in the header:

{% lmode() %}
You are in **light mode** {{ icon(name="sun", aria="sun") }} — this line is hidden in dark mode.
{% end %}

{% dmode() %}
You are in **dark mode** {{ icon(name="moon", aria="moon") }} — this line is hidden in light mode.
{% end %}
