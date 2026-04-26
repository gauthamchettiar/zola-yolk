# zola-yolk 🟡

A minimal, monospace Zola theme with dark/light mode, full-text search, and multiple shortcode support. Created with a component-based template architecture for easy extensibility.

## Features

- Monospace typography (IBM Plex Mono via Google Fonts)
- Dark / light mode toggle with `localStorage` persistence, respects `prefers-color-scheme`
- Full-text search modal powered by elasticlunr (Ctrl/Cmd+K or click icon)
- Component-based template architecture (`partials/`, `partials/widgets/`, `partials/head/`)

## Installation

### As a git submodule (recommended)

```sh
cd your-zola-site
git submodule add https://codeberg.org/gthmchttr/zola-yolk.git themes/zola-yolk
```

### Manual download

Download and extract the repository into `themes/zola-yolk/` inside your site.

## Configuration

Set the theme in your `zola.toml`:

```toml
theme = "zola-yolk"
```

### Taxonomies

To enable tag pages, add to `zola.toml`:

```toml
taxonomies = [
    { name = "tags" },
]
```

## Content structure

```
content/
  _index.md          # Home page intro (optional)
  posts/
    _index.md        # Posts section (title shown on /posts)
    my-post.md
```

Each post supports front matter:

```toml
+++
title = "My Post"
date = 2026-04-24
description = "A short description."

[taxonomies]
tags = ["zola", "example"]
+++
```

## Icon shortcode

Requires `enable_font_awesome_icon = true` in `zola.toml`.

```
{{ icon(name="star") }}
{{ icon(name="github", style="brands") }}
{{ icon(name="star", style="regular", class="my-class", aria="favourite") }}
```

Valid `style` values: `solid` (default), `regular`, `brands`.

Icon names come from [Font Awesome 6 Free](https://fontawesome.com/search?o=r&m=free).

To use the icon widget directly in templates:

```jinja2
{%- set icon_name = "star" -%}
{%- set icon_style = "solid" -%}
{% include "partials/widgets/icon.html" %}
```

## Keyboard shortcuts

| Shortcut | Action |
|---|---|
| `Ctrl/Cmd + K` | Open search |
| `Escape` | Close search |

## License

MIT
