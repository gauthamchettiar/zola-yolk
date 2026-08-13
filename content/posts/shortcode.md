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
callable from Markdown and from a template. Both forms are shown throughout —
switch tabs on any example below and the rest of the page follows.

## Icons

{% code(titles=["markdown content", "template files"], group="usage") %}
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

Opens in a new tab with `rel="noopener noreferrer"` and appends an indicator.

{% code(titles=["markdown content", "template files"], group="usage") %}
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

text
: visible link text. Required.

href
: destination URL. Required.

new_tab
: `true` (default), `false` — opens in a new tab with `rel="noopener noreferrer"`

show_icon
: `true` (default), `false` — appends the external-link indicator

default&nbsp;&nbsp;&nbsp; : {{ elink(text="Example", href="https://example.com") }}  
no new tab : {{ elink(text="Example", href="https://example.com", new_tab=false) }}  
no icon&nbsp;&nbsp;&nbsp; : {{ elink(text="Example", href="https://example.com", show_icon=false) }}  

## Mark

Calls out a run of text, either filled or outlined.

{% code(titles=["markdown content", "template files"], group="usage") %}
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

text
: the text to mark. Required.

color
: `white`, `yellow` (default), `pink`, `green`, `red`, `blue`, `muted`

decoration
: `highlight` (default, filled), `border` (outlined)

filled&nbsp;&nbsp; : {{ mark(text="yellow") }} {{ mark(text="pink", color="pink") }} {{ mark(text="green", color="green") }} {{ mark(text="red", color="red") }} {{ mark(text="blue", color="blue") }}  
outlined : {{ mark(text="yellow", decoration="border") }} {{ mark(text="pink", color="pink", decoration="border") }} {{ mark(text="green", color="green", decoration="border") }} {{ mark(text="red", color="red", decoration="border") }} {{ mark(text="blue", color="blue", decoration="border") }}

## Color

Colours a run of text — like `mark`, but plain: no background, no border,
just colour.

{% code(titles=["markdown content", "template files"], group="usage") %}
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

text
: the text to colour. Required.

color
: `white`, `yellow` (default), `pink`, `green`, `red`, `blue`, `muted`

{{ color(text="yellow") }} {{ color(text="pink", color="pink") }} {{ color(text="green", color="green") }} {{ color(text="red", color="red") }} {{ color(text="blue", color="blue") }}

## Shimmer

Fun, animated multi-colour text. Cycles through the site's existing accent
palette (yellow, pink, green, red, blue) rather than an arbitrary rainbow, so
it stays part of the same colour system instead of clashing with it. Pure
CSS, no JavaScript, and disabled entirely under `prefers-reduced-motion`.

{% code(titles=["markdown content", "template files"], group="usage") %}
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

text
: the text to animate. Required.

type
: `text` (default) — the text itself cycles colour. `background` — the text
  stays a fixed colour while a highlight behind it cycles instead.

style
: `cycle` (default) — jumps between accents in place. `wave` — sweeps a
  moving gradient across the text.

text, cycle&nbsp;&nbsp;&nbsp;&nbsp; : {{ shimmer(text="look at me") }}  
text, wave&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; : {{ shimmer(text="look at me", style="wave") }}  
background, cycle : {{ shimmer(text="look at me", type="background") }}  
background, wave&nbsp; : {{ shimmer(text="look at me", type="background", style="wave") }}

## Quotes

An attributed quotation, rendered as `<figure>` / `<blockquote>` / `<figcaption>`
— the attribution describes the quote, so HTML puts it outside the quote itself.

{% code(titles=["markdown content", "template files"], group="usage") %}
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

body
: the quotation itself. From a template this is the `content` parameter, and
  it takes already-rendered HTML.

author
: who said it. Default none.

cite
: the work it came from, rendered in `<cite>`. Default none.

url
: source URL. Sets the blockquote's `cite` attribute and links the citation.
  Default none.

color
: `white`, `yellow`, `pink` (default), `green`, `red`, `blue`, `muted`

{% quote(author="Alan Kay", cite="1971") %}
The best way to predict the future is to invent it.
{% end %}

{% quote(author="Tim Berners-Lee", cite="Weaving the Web", url="https://example.com", color="green") %}
The Web does not just connect machines, it connects people.
{% end %}

## Admonitions

A callout set apart from the surrounding text, rendered as `<aside>`.

{% code(titles=["markdown content", "template files"], group="usage") %}
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

body
: the callout's content. From a template this is the `content` parameter, and
  it takes already-rendered HTML.

title
: heading text beside the icon. Default none, which floats the lone icon
  beside the first line instead of above it.

icon
: Font Awesome name. Default `circle-info`.

color
: `white`, `yellow` (default), `pink`, `green`, `red`, `blue`, `muted`

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

`note`, `warning`, `danger`, `info` and `tip` are `admonition` with a fixed
color and icon, and a title that defaults to their own name.

{% code(titles=["markdown content", "template files"], group="usage") %}
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

## Light and Dark Mode Content

Whatever is inside `lmode` shows only in light mode, and `dmode` only in dark.

{% code(titles=["markdown content", "template files"], group="usage") %}
```md
{​% lmode() %​}
Only visible in light mode.
{​% end %​}

{​% dmode() %​}
Only visible in dark mode.
{​% end %​}
```
```jinja2
{​% import "macros/blocks.html" as blocks %​}
{​{ blocks::lmode(content="<p>Only visible in light mode.</p>") }​}
{​{ blocks::dmode(content="<p>Only visible in dark mode.</p>") }​}
```
{% end %}

Neither takes parameters. Both variants are emitted and CSS reveals the matching
one, so this works with JavaScript disabled. Toggle the theme in the header:

{% lmode() %}
You are in **light mode** {{ icon(name="sun", aria="sun") }} — this line is hidden in dark mode.
{% end %}

{% dmode() %}
You are in **dark mode** {{ icon(name="moon", aria="moon") }} — this line is hidden in light mode.
{% end %}

## Mobile and Desktop Content

Same idea as `lmode` / `dmode`, but for viewport width instead of theme —
`mobile` shows only below the mobile breakpoint (`48rem`), `desktop` only
above it.

{% code(titles=["markdown content", "template files"], group="usage") %}
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

Neither takes parameters. Unlike `lmode` / `dmode` this needs no data-theme
override or OS-preference fallback — viewport width is always known to CSS,
so a single media query does the whole job, still with no JavaScript. Resize
the window to see these switch:

{% mobile() %}
Your screen is **narrow**!
{% end %}

{% desktop() %}
Your screen is **wide**!
{% end %}
