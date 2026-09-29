+++
title = "Shortcode: Elements"
date = 2026-04-20
description = "Shortcodes that insert content: icons, links, marks, quotes, callouts and screen-size-conditional blocks."

[taxonomies]
tags = ["shortcode", "syntax", "zola"]

[extra]
series = "Shortcodes"
series_part = 1
+++

Shortcodes for *inserting* content. See also [Layouts](@/posts/layout.md) and
[Externals](@/posts/externals.md).

## Icons

{% tabs(titles=["markdown content", "template files"], group="usage") %}
```md
{​{ icon(name="star") }​}
{​{ icon(name="github", style="brands") }​}
{​{ icon(name="star", style="regular", class="text-accent", aria="favorite") }​}
```
```jinja2
{​% import "macros/widgets.html" as widgets %​}
{​{ widgets::icon(name="star") }​}
{​{ widgets::icon(name="github", style="brands") }​}
{​{ widgets::icon(name="star", style="regular", class="text-accent", aria="favorite") }​}
```
{% end %}

name
: Font Awesome icon name. Required.

style
: `solid` (default), `regular`, `brands`

source
: icon pack, a subfolder of `static/icons/`. Default `font-awesome`.

class
: extra CSS classes. Default none.

aria
: accessible label. Omit it and the icon renders `aria-hidden`, which is what
  you want whenever the surrounding text already names it.

star&nbsp;&nbsp; : {{ icon(name="star") }}  
github : {{ icon(name="github", style="brands") }}  
lemon&nbsp; : {{ icon(name="lemon", style="regular") }}  

## External Links

{% tabs(titles=["markdown content", "template files"], group="usage") %}
```md
{​{ elink(text="Example", href="https://example.com") }​}
{​{ elink(text="Example", href="https://example.com", new_tab=false) }​}
{​{ elink(text="Example", href="https://example.com", show_icon=false) }​}
```
```jinja2
{​% import "macros/widgets.html" as widgets %​}
{​{ widgets::elink(text="Example", href="https://example.com") }​}
{​{ widgets::elink(text="Example", href="https://example.com", new_tab=false) }​}
{​{ widgets::elink(text="Example", href="https://example.com", show_icon=false) }​}
```
{% end %}

text, href
: required

new_tab, show_icon
: `true` (default), `false`

default&nbsp;&nbsp;&nbsp; : {{ elink(text="Example", href="https://example.com") }}  
no new tab : {{ elink(text="Example", href="https://example.com", new_tab=false) }}  
no icon&nbsp;&nbsp;&nbsp; : {{ elink(text="Example", href="https://example.com", show_icon=false) }}  

## Mark

{% tabs(titles=["markdown content", "template files"], group="usage") %}
```md
{​{ mark(text="highlighted") }​}
{​{ mark(text="outlined", color="pink", decoration="border") }​}
```
```jinja2
{​% import "macros/widgets.html" as widgets %​}
{​{ widgets::mark(text="highlighted") }​}
{​{ widgets::mark(text="outlined", color="pink", decoration="border") }​}
```
{% end %}

color
: `white`, `red`, `orange`, `yellow` (default), `lime`, `green`, `cyan`, `blue`, `purple`, `pink`, `muted`

decoration
: `highlight` (default), `border`

| colour | filled | outlined |
|---|---|---|
| `white` | {{ mark(text="white", color="white") }} | {{ mark(text="white", color="white", decoration="border") }} |
| `red` | {{ mark(text="red", color="red") }} | {{ mark(text="red", color="red", decoration="border") }} |
| `orange` | {{ mark(text="orange", color="orange") }} | {{ mark(text="orange", color="orange", decoration="border") }} |
| `yellow` | {{ mark(text="yellow") }} | {{ mark(text="yellow", decoration="border") }} |
| `lime` | {{ mark(text="lime", color="lime") }} | {{ mark(text="lime", color="lime", decoration="border") }} |
| `green` | {{ mark(text="green", color="green") }} | {{ mark(text="green", color="green", decoration="border") }} |
| `cyan` | {{ mark(text="cyan", color="cyan") }} | {{ mark(text="cyan", color="cyan", decoration="border") }} |
| `blue` | {{ mark(text="blue", color="blue") }} | {{ mark(text="blue", color="blue", decoration="border") }} |
| `purple` | {{ mark(text="purple", color="purple") }} | {{ mark(text="purple", color="purple", decoration="border") }} |
| `pink` | {{ mark(text="pink", color="pink") }} | {{ mark(text="pink", color="pink", decoration="border") }} |
| `muted` | {{ mark(text="muted", color="muted") }} | {{ mark(text="muted", color="muted", decoration="border") }} |

## Color

Like `mark`, but only the text colour.

{% tabs(titles=["markdown content", "template files"], group="usage") %}
```md
{​{ color(text="important") }​}
{​{ color(text="careful", color="red") }​}
```
```jinja2
{​% import "macros/widgets.html" as widgets %​}
{​{ widgets::color(text="important") }​}
{​{ widgets::color(text="careful", color="red") }​}
```
{% end %}

color
: same colours as `mark`, default `yellow`

{{ color(text="white", color="white") }} {{ color(text="red", color="red") }} {{ color(text="orange", color="orange") }} {{ color(text="yellow") }} {{ color(text="lime", color="lime") }} {{ color(text="green", color="green") }} {{ color(text="cyan", color="cyan") }} {{ color(text="blue", color="blue") }} {{ color(text="purple", color="purple") }} {{ color(text="pink", color="pink") }} {{ color(text="muted", color="muted") }}
## Shimmer

Animated multi-colour text. Off under `prefers-reduced-motion`.

{% tabs(titles=["markdown content", "template files"], group="usage") %}
```md
{​{ shimmer(text="look at me") }​}
{​{ shimmer(text="smooth", type="background", style="wave") }​}
```
```jinja2
{​% import "macros/widgets.html" as widgets %​}
{​{ widgets::shimmer(text="look at me") }​}
{​{ widgets::shimmer(text="smooth", type="background", style="wave") }​}
```
{% end %}

type
: `text` (default), `background`

style
: `cycle` (default), `wave`

text, cycle&nbsp;&nbsp;&nbsp;&nbsp; : {{ shimmer(text="look at me") }}  
text, wave&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; : {{ shimmer(text="look at me", style="wave") }}  
background, cycle : {{ shimmer(text="look at me", type="background") }}  
background, wave&nbsp; : {{ shimmer(text="look at me", type="background", style="wave") }}

## Quotes

{% tabs(titles=["markdown content", "template files"], group="usage") %}
```md
{​% quote(author="Alan Kay", cite="1971") %​}
The best way to predict the future is to invent it.
{​% end %​}
```
```jinja2
{​% import "macros/blocks.html" as blocks %​}
{​{ blocks::quote(content="<p>The best way to predict the future is to invent it.</p>", author="Alan Kay", cite="1971") }​}
```
{% end %}

author, cite, url
: who said it, the work, and a source link. All optional.

color
: same colours as `mark`, default `pink`

{% quote(author="Alan Kay", cite="1971") %}
The best way to predict the future is to invent it.
{% end %}

{% quote(author="Tim Berners-Lee", cite="Weaving the Web", url="https://example.com", color="green") %}
The Web does not just connect machines, it connects people.
{% end %}

## Admonitions

{% tabs(titles=["markdown content", "template files"], group="usage") %}
```md
{​% admonition(title="Note") %​}
Worth knowing.
{​% end %​}

{​% admonition(title="Careful", icon="triangle-exclamation", color="pink") %​}
This one bites.
{​% end %​}
```
```jinja2
{​% import "macros/blocks.html" as blocks %​}
{​{ blocks::admonition(content="<p>Worth knowing.</p>", title="Note") }​}
{​{ blocks::admonition(content="<p>This one bites.</p>", title="Careful", icon="triangle-exclamation", color="pink") }​}
```
{% end %}

title
: optional

icon
: Font Awesome name, default `circle-info`

color
: same colours as `mark`, default `yellow`

{% admonition(title="Note") %}
Worth knowing.
{% end %}

{% admonition(title="Careful", icon="triangle-exclamation", color="pink") %}
This one bites.
{% end %}

{% admonition(icon="lightbulb", color="green") %}
An icon with no title works too.
{% end %}

### Admonition Presets

`note`, `warning`, `danger`, `info` and `tip`: `admonition` with a fixed colour and icon.

{% tabs(titles=["markdown content", "template files"], group="usage") %}
```md
{​% note() %​}
Worth knowing.
{​% end %​}

{​% warning(title="Careful") %​}
This one bites.
{​% end %​}
```
```jinja2
{​% import "macros/blocks.html" as blocks %​}
{​{ blocks::admonition(content="<p>Worth knowing.</p>", title="Note", icon="note-sticky", color="yellow") }​}
{​{ blocks::admonition(content="<p>This one bites.</p>", title="Careful", icon="triangle-exclamation", color="pink") }​}
```
{% end %}

{% note() %}
Worth knowing.
{% end %}

{% warning() %}
This one bites.
{% end %}

{% danger() %}
Don't do this in production.
{% end %}

{% info() %}
Good to know.
{% end %}

{% tip(title="Shortcut") %}
There's a faster way to do this.
{% end %}

## Expand

A collapsible section.

{% tabs(titles=["markdown content", "template files"], group="usage") %}
```md
{​% expand(title="Show the answer", state="expanded") %​}
42.
{​% end %​}

{​% expand(title="In a border", style="border") %​}
Framed.
{​% end %​}
```
```jinja2
{​% import "macros/blocks.html" as blocks %​}
{​{ blocks::expand(content="<p>Hidden until opened.</p>", title="Show the answer", style="border") }​}
```
{% end %}

title
: summary text. Default `Details`.

state
: `expanded`, `collapsed` (default)

style
: `simple` (default), `border`

{% expand() %}
Hidden until opened.
{% end %}

{% expand(title="Show the answer", state="expanded") %}
The answer is forty-two.
{% end %}

{% expand(title="Show the answer, bordered", style="border") %}
The answer is still forty-two.
{% end %}

{% expand(title="Open by default, bordered", state="expanded", style="border") %}
A bordered expand, already open.
{% end %}

## Mobile and Desktop Content

`mobile` shows below `48rem`, `desktop` above it.

{% tabs(titles=["markdown content", "template files"], group="usage") %}
```md
{​% mobile() %​}
Only visible on small screens.
{​% end %​}

{​% desktop() %​}
Only visible on larger screens.
{​% end %​}
```
```jinja2
{​% import "macros/blocks.html" as blocks %​}
{​{ blocks::mobile(content="<p>Only visible on small screens.</p>") }​}
{​{ blocks::desktop(content="<p>Only visible on larger screens.</p>") }​}
```
{% end %}

Resize the window to see these switch:

{% mobile() %}
Your screen is **narrow**!
{% end %}

{% desktop() %}
Your screen is **wide**!
{% end %}
