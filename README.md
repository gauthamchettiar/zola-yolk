# zola-yolk 🟡

A minimal, monospace Zola theme with dark/light mode, full-text search, and multiple shortcode support. Created with a component-based template architecture for easy extensibility.

**dark-theme**: 
![dark-theme-screenshot](/static/images/screenshots/home-dark.png)

**light-theme**: 
![light-theme-screenshot](/static/images/screenshots/home-light.png)

## Features

- Monospace typography (IBM Plex Mono via Google Fonts)
- Dark / light mode toggle with `localStorage` persistence, respects `prefers-color-scheme`
- Full-text search modal powered by elasticlunr (Ctrl/Cmd+K or click icon)
- Component-based template architecture (`partials/`, `partials/widgets/`, `shortcodes`)

## Installation

### As a git submodule (recommended)

This allows you to easily pull in updates to the theme:

```sh
cd your-zola-site
git submodule add https://github.com/gauthamchettiar/zola-yolk.git themes/zola-yolk
```

### Manual download

Download and extract the repository into `themes/zola-yolk/` inside your site. Use this if you don't want to use git or don't need to track updates.

## Configuration

Below is a comprehensive set of config supported by theme, feel free to customize as per your requirements -

```toml
base_url = "https://example.com/" # Your site's base URL (required for correct link generation and search indexing)
title = "" # Site title (shown in header and used for SEO)
description = "" # Site description (used for SEO)
theme = "zola-yolk" # Set the theme to zola-yolk
compile_sass = true # Theme uses Sass for styling, so enable Sass compilation
build_search_index = true # Required for full-text search functionality
taxonomies = [
    { name = "tags" },
] # Enable tags taxonomy (optional, but required if you want to use tags)

[markdown]
definition_list = true # Enable markdown definition lists
bottom_footnotes = true # Place footnotes at the end of the page

# Code highlighting configuration (optional, but recommended for better code block styling)
[markdown.highlighting]
style = "class"
light_theme = "catppuccin-latte"
dark_theme = "catppuccin-mocha"

[extras]
content_sections = ["posts"] # sections to include in recent posts widget
google_font = {
    body   = ["IBM Plex Mono"],
    header = ["IBM Plex Mono"],
    code   = ["IBM Plex Mono"]
} # Google Fonts configuration for body, header and code (optional, defaults to IBM Plex Mono)

enable_font_awesome_icon = true # adds css for loading Font Awesome icons from CDN, required for icon shortcode, & enabling search and theme toggle icons
enable_theme_switcher = true # show theme switcher in header, requires enable_font_awesome_icon to be true
enable_search = true # show search icon in header and enable search modal, requires enable_font_awesome_icon to be true

footer = "Written with ❤️" # Custom footer text (optional)

# Main menu configurations (required to display main menu links in header)
[[extra.main_menu]]
name = "Posts"
url = "/posts"

[[extra.main_menu]]
name = "Tags"
url = "/tags"
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
tags = ["zola", "example"] # requires taxonomies to be defined in config
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

## License

MIT
