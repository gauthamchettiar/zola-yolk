# zola-yolk

A minimal, monospace Zola theme with dark/light mode, full-text search, Font Awesome icon support, and a component-based template architecture.

## Features

- Monospace typography (IBM Plex Mono via Google Fonts)
- Dark / light mode toggle with `localStorage` persistence, respects `prefers-color-scheme`
- Full-text search modal powered by elasticlunr (Ctrl/Cmd+K or click icon)
- Font Awesome 6 icon support via shortcode and template widget
- Component-based template architecture (`partials/`, `partials/widgets/`, `partials/head/`)
- Year-grouped post listings on section and tag pages
- Configurable via `zola.toml` `[extra]` — no template edits required for common features

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

# Required for search
build_search_index = true

# Required for definition lists and footnotes
[markdown]
definition_list = true
bottom_footnotes = true

[markdown.highlighting]
theme = "catppuccin-mocha"  # or any theme supported by Zola

[extra]
# Folder names under content/ to include in the recent posts widget
content_sections = ["posts"]

# Load Font Awesome — set true if you use {{ icon(...) }} anywhere
font_awesome = true

# Show dark/light mode toggle button in the header
theme_mode = true

# Show search button in the header (requires build_search_index = true)
search = true

# Google Fonts families to load (each becomes a family= param)
google_fonts = [
    "IBM+Plex+Mono:ital,wght@0,300;0,400;0,500;1,300;1,400",
]

# Navigation menu items
[[extra.main_menu]]
name = "Posts"
url = "/posts"

[[extra.main_menu]]
name = "Tags"
url = "/tags"
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

Requires `font_awesome = true` in `zola.toml`.

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
