+++
title = "Supported Shortcodes"
date = 2026-04-20
description = "Shortcodes that insert content: icons, external links, and theme-conditional blocks."

[taxonomies]
tags = ["shortcode", "syntax", "zola"]
+++

Shortcodes for *inserting* content. For the ones that arrange it — borders,
wide blocks and columns — see [Supported Layouts](@/posts/layout.md).

## Icons

This is how you can include an icon in,

<u>markdown content</u>:  
    
```md
{​{ icon(name="star") }​}
{​{ icon(name="github", style="brands") }​}
{​{ icon(name="star", style="regular", class="text-accent", aria="favorite") }​}
```

<u>template files</u>:

```html
{​% import "macros/widgets.html" as widgets %​}
{​{ widgets::icon(name="star") }​}
{​{ widgets::icon(name="github", style="brands") }​}
{​{ widgets::icon(name="star", style="regular", class="text-accent", aria="favorite") }​}
```

star&nbsp;&nbsp; : {{ icon(name="star") }}  
github : {{ icon(name="github", style="brands") }}  
lemon&nbsp; : {{ icon(name="lemon", style="regular") }}  

## External Links

This is how you can include an external link in,

<u>markdown content</u>:

```md
{​{ elink(text="Example", href="https://example.com") }​}
{​{ elink(text="Example", href="https://example.com", new_tab=false) }​}
{​{ elink(text="Example", href="https://example.com", show_icon=false) }​}
```

<u>template files</u>:

```html
{​% import "macros/widgets.html" as widgets %​}
{​{ widgets::elink(text="Example", href="https://example.com") }​}
{​{ widgets::elink(text="Example", href="https://example.com", new_tab=false) }​}
{​{ widgets::elink(text="Example", href="https://example.com", show_icon=false) }​}
```

default&nbsp;&nbsp;&nbsp; : {{ elink(text="Example", href="https://example.com") }}  
no new tab : {{ elink(text="Example", href="https://example.com", new_tab=false) }}  
no icon&nbsp;&nbsp;&nbsp; : {{ elink(text="Example", href="https://example.com", show_icon=false) }}

## Light and Dark Mode Content

This is how you can show content in only one theme,

<u>markdown content</u>:

```md
{​% lmode() %​}
Only visible in light mode.
{​% end %​}

{​% dmode() %​}
Only visible in dark mode.
{​% end %​}
```

Neither takes any parameters. Toggle the theme in the header and the line below
will swap.

{% lmode() %}
You are in **light mode** {{ icon(name="sun", aria="sun") }} — this line is hidden in dark mode.
{% end %}

{% dmode() %}
You are in **dark mode** {{ icon(name="moon", aria="moon") }} — this line is hidden in light mode.
{% end %}
