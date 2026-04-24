+++
title = "Supported Shortcodes"
date = 2026-04-22
description = "Shortcodes supported by yolk theme."

[taxonomies]
tags = ["shortcode", "sample", "zola"]
+++

## Icons

This is how you can include an icon in your markdown content:

```
{​{ icon(name="star") }​}
{​{ icon(name="github", style="brands") }​}
{​{ icon(name="star", style="classic", class="text-accent", aria="favorite") }​}
```

star&nbsp;&nbsp; : {{ icon(name="star") }}  
github : {{ icon(name="github", style="brands") }}  
lemon&nbsp; : {{ icon(name="lemon", style="regular") }}  

If you want to use the same icon component in templates, include the widget directly:

```jinja
{%- set icon_name = "star" -%}
{%- set icon_style = "solid" -%}
{%- set icon_class = "my-class" -%}
{%- set icon_aria = "favorite" -%}
{% include "partials/widgets/icon.html" %}
```

> Make sure you enable font_awesome in zola.toml
> ```toml
> # zola.toml
> font_awesome = true
> ```

