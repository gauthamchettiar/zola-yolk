+++
title = "Components: Elements"
date = 2026-04-20
description = "Components that insert content: icons, links, marks, quotes, callouts and screen-size-conditional blocks."

[taxonomies]
tags = ["component", "syntax", "zola"]

[extra]
series = "Components"
series_part = 1
+++

Components for *inserting* content. See also [Layouts](@/posts/layout.md) and
[Externals](@/posts/externals.md).

## Calling a Component

{% raw %}Single elements are self-closing tags in `{{ }}`; blocks open and close in
`{% %}` around a Markdown body:{% endraw %}

{% raw %}
```md
{{ <mark text="highlighted" /> }}

{% <note title="Heads up"> %}
Worth **knowing**.
{% </note> %}
```
{% endraw %}

Strings go in quotes; anything else in braces: `new_tab={false}`,
`titles={["Python", "Java"]}`. The same call works in a template.

## Icons

{% raw %}
```md
{{ <icon name="star" /> }}
{{ <icon name="github" style="brands" /> }}
{{ <icon name="star" style="regular" class="text-accent" aria="favorite" /> }}
```
{% endraw %}

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

star&nbsp;&nbsp; : {{ <icon name="star" /> }}  
github : {{ <icon name="github" style="brands" /> }}  
lemon&nbsp; : {{ <icon name="lemon" style="regular" /> }}  

## External Links

{% raw %}
```md
{{ <elink text="Example" href="https://example.com" /> }}
{{ <elink text="Example" href="https://example.com" new_tab={false} /> }}
{{ <elink text="Example" href="https://example.com" show_icon={false} /> }}
```
{% endraw %}

text, href
: required

new_tab, show_icon
: `true` (default), `false`

default&nbsp;&nbsp;&nbsp; : {{ <elink text="Example" href="https://example.com" /> }}  
no new tab : {{ <elink text="Example" href="https://example.com" new_tab={false} /> }}  
no icon&nbsp;&nbsp;&nbsp; : {{ <elink text="Example" href="https://example.com" show_icon={false} /> }}  

## Mark

{% raw %}
```md
{{ <mark text="highlighted" /> }}
{{ <mark text="outlined" color="pink" decoration="border" /> }}
```
{% endraw %}

color
: `white`, `red`, `orange`, `yellow` (default), `lime`, `green`, `cyan`, `blue`, `purple`, `pink`, `muted`

decoration
: `highlight` (default), `border`

| colour | filled | outlined |
|---|---|---|
| `white` | {{ <mark text="white" color="white" /> }} | {{ <mark text="white" color="white" decoration="border" /> }} |
| `red` | {{ <mark text="red" color="red" /> }} | {{ <mark text="red" color="red" decoration="border" /> }} |
| `orange` | {{ <mark text="orange" color="orange" /> }} | {{ <mark text="orange" color="orange" decoration="border" /> }} |
| `yellow` | {{ <mark text="yellow" /> }} | {{ <mark text="yellow" decoration="border" /> }} |
| `lime` | {{ <mark text="lime" color="lime" /> }} | {{ <mark text="lime" color="lime" decoration="border" /> }} |
| `green` | {{ <mark text="green" color="green" /> }} | {{ <mark text="green" color="green" decoration="border" /> }} |
| `cyan` | {{ <mark text="cyan" color="cyan" /> }} | {{ <mark text="cyan" color="cyan" decoration="border" /> }} |
| `blue` | {{ <mark text="blue" color="blue" /> }} | {{ <mark text="blue" color="blue" decoration="border" /> }} |
| `purple` | {{ <mark text="purple" color="purple" /> }} | {{ <mark text="purple" color="purple" decoration="border" /> }} |
| `pink` | {{ <mark text="pink" color="pink" /> }} | {{ <mark text="pink" color="pink" decoration="border" /> }} |
| `muted` | {{ <mark text="muted" color="muted" /> }} | {{ <mark text="muted" color="muted" decoration="border" /> }} |

## Color

Like `mark`, but only the text colour.

{% raw %}
```md
{{ <color text="important" /> }}
{{ <color text="careful" color="red" /> }}
```
{% endraw %}

color
: same colours as `mark`, default `yellow`

{{ <color text="white" color="white" /> }} {{ <color text="red" color="red" /> }} {{ <color text="orange" color="orange" /> }} {{ <color text="yellow" /> }} {{ <color text="lime" color="lime" /> }} {{ <color text="green" color="green" /> }} {{ <color text="cyan" color="cyan" /> }} {{ <color text="blue" color="blue" /> }} {{ <color text="purple" color="purple" /> }} {{ <color text="pink" color="pink" /> }} {{ <color text="muted" color="muted" /> }}
## Shimmer

Animated multi-colour text. Off under `prefers-reduced-motion`.

{% raw %}
```md
{{ <shimmer text="look at me" /> }}
{{ <shimmer text="smooth" type="background" style="wave" /> }}
```
{% endraw %}

type
: `text` (default), `background`

style
: `cycle` (default), `wave`

text, cycle&nbsp;&nbsp;&nbsp;&nbsp; : {{ <shimmer text="look at me" /> }}  
text, wave&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; : {{ <shimmer text="look at me" style="wave" /> }}  
background, cycle : {{ <shimmer text="look at me" type="background" /> }}  
background, wave&nbsp; : {{ <shimmer text="look at me" type="background" style="wave" /> }}

## Quotes

{% raw %}
```md
{% <quote author="Alan Kay" cite="1971"> %}
The best way to predict the future is to invent it.
{% </quote> %}
```
{% endraw %}

author, cite, url
: who said it, the work, and a source link. All optional.

color
: same colours as `mark`, default `pink`

{% <quote author="Alan Kay" cite="1971"> %}
The best way to predict the future is to invent it.
{% </quote> %}

{% <quote author="Tim Berners-Lee" cite="Weaving the Web" url="https://example.com" color="green"> %}
The Web does not just connect machines, it connects people.
{% </quote> %}

## Admonitions

{% raw %}
```md
{% <admonition title="Note"> %}
Worth knowing.
{% </admonition> %}

{% <admonition title="Careful" icon="triangle-exclamation" color="pink"> %}
This one bites.
{% </admonition> %}
```
{% endraw %}

title
: optional

icon
: Font Awesome name, default `circle-info`

color
: same colours as `mark`, default `yellow`

{% <admonition title="Note"> %}
Worth knowing.
{% </admonition> %}

{% <admonition title="Careful" icon="triangle-exclamation" color="pink"> %}
This one bites.
{% </admonition> %}

{% <admonition icon="lightbulb" color="green"> %}
An icon with no title works too.
{% </admonition> %}

### Admonition Presets

`note`, `warning`, `danger`, `info` and `tip`: `admonition` with a fixed colour and icon.

{% raw %}
```md
{% <note> %}
Worth knowing.
{% </note> %}

{% <warning title="Careful"> %}
This one bites.
{% </warning> %}
```
{% endraw %}

{% <note> %}
Worth knowing.
{% </note> %}

{% <warning> %}
This one bites.
{% </warning> %}

{% <danger> %}
Don't do this in production.
{% </danger> %}

{% <info> %}
Good to know.
{% </info> %}

{% <tip title="Shortcut"> %}
There's a faster way to do this.
{% </tip> %}

## Expand

A collapsible section.

{% raw %}
```md
{% <expand title="Show the answer" state="expanded"> %}
42.
{% </expand> %}

{% <expand title="In a border" style="border"> %}
Framed.
{% </expand> %}
```
{% endraw %}

title
: summary text. Default `Details`.

state
: `expanded`, `collapsed` (default)

style
: `simple` (default), `border`

{% <expand> %}
Hidden until opened.
{% </expand> %}

{% <expand title="Show the answer" state="expanded"> %}
The answer is forty-two.
{% </expand> %}

{% <expand title="Show the answer, bordered" style="border"> %}
The answer is still forty-two.
{% </expand> %}

{% <expand title="Open by default, bordered" state="expanded" style="border"> %}
A bordered expand, already open.
{% </expand> %}

## Mobile and Desktop Content

`mobile` shows below `48rem`, `desktop` above it.

{% raw %}
```md
{% <mobile> %}
Only visible on small screens.
{% </mobile> %}

{% <desktop> %}
Only visible on larger screens.
{% </desktop> %}
```
{% endraw %}

Resize the window to see these switch:

{% <mobile> %}
Your screen is **narrow**!
{% </mobile> %}

{% <desktop> %}
Your screen is **wide**!
{% </desktop> %}
