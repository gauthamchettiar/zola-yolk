# zola-yolk 🟡

A minimal, monospace Zola theme with dark/light mode, full-text search, and multiple shortcode support. Created with a component-based template architecture for easy extensibility.

Shortcodes: [`icon`](#icon-shortcode), [`elink`](#elink-shortcode), [`border`](#border-shortcode), [`wide`](#wide-shortcode), [`row` / `col`](#row--col-shortcodes), [`code`](#code-shortcode), [`lmode` / `dmode`](#lmode--dmode-shortcodes).

**dark-theme**: 
![dark-theme-screenshot](/static/images/screenshots/home-dark.png)

**light-theme**: 
![light-theme-screenshot](/static/images/screenshots/home-light.png)

## Features

- Monospace typography (IBM Plex Mono via Google Fonts)
- Dark / light mode toggle with `localStorage` persistence, respects `prefers-color-scheme`
- Full-text search modal powered by elasticlunr (Ctrl/Cmd+K or click icon)
- Self-hosted fonts and SVG icons (via `scripts/py-ssg-tools`)
- Component-based template architecture (`partials/`, `macros/`, `shortcodes/`)
- Semantic HTML throughout — recolour the whole theme by editing one file

## Customizing

All colours, fonts and spacing are CSS custom properties in **`sass/_tokens.scss`**.
Editing that one file restyles the site; nothing else hardcodes a colour.

```scss
--color-bg: light-dark(#faf8f2, #1a1a1a);  // light value, dark value
```

Colours use [`light-dark()`](https://developer.mozilla.org/en-US/docs/Web/CSS/color_value/light-dark),
so each token declares both themes on one line. Which one applies is decided by
`color-scheme`, which the theme toggle pins via `data-theme` on `<html>`.

Every accent meets WCAG AA (4.5:1) against its background, and the light accents
are tuned to sit as high in lightness as that allows with chroma pushed to the
edge of sRGB — so they are as vivid as they can be while staying readable. If
you lighten them further they will start failing contrast; the measured ratio is
noted in a comment beside each one.

The rest of the stylesheet is split by role:

| File | Contains |
|---|---|
| `sass/_tokens.scss` | design tokens — start here |
| `sass/_base.scss` | bare element styles (`h1`, `a`, `table`, `button`, …) |
| `sass/_layout.scss` | page frame: header, breadcrumb, nav |
| `sass/_components.scss` | icon, post meta, listings, search dialog |

Most of the theme is styled by element rather than by class, so semantic markup
picks up the right styling automatically — a `<button>` you add anywhere already
looks like the theme's buttons.

Punctuation that looks like content — the `[brackets]` around menu items, the
`/` between breadcrumbs, and the `{ key = value }` post metadata — is drawn with
CSS `::before`/`::after`, not written into the templates. Change it in the CSS.

### Browser support

The theme uses `light-dark()`, `oklch()`, `<dialog>` and `<search>`, which need
Chrome 123+, Safari 17.5+ or Firefox 120+ (mid-2024 onwards).

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
base_url = "https://example.com/" 
title = "" 
description = ""      # used for <meta name="description"> and Open Graph
theme = "zola-yolk" 
compile_sass = true 
build_search_index = true 
generate_feeds = true # theme links to the feed from <head> when enabled
taxonomies = [
    { name = "tags" },
]

[markdown]
definition_list = true
bottom_footnotes = true

[markdown.highlighting]
style = "class"
light_theme = "catppuccin-latte"
dark_theme = "catppuccin-mocha"

[extra]
content_sections = ["posts"]
recent_limit = 10 # posts shown under "Recent posts" on the homepage; 0 = all

enable_theme_switcher = true
enable_search = true

footer = "Written with ❤️"

[[extra.fonts]]
source = "google"
name = "IBM Plex Mono"

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

## Fonts

Fonts are self-hosted. Use `scripts/py-ssg-tools` to sync Google Fonts into `static/fonts/`:

```sh
cd scripts/py-ssg-tools
uv run pst sync fonts --name "IBM Plex Mono" --dest ../../static/fonts/google --weights 400,700 --subset latin
```

Declare each font in `zola.toml`:

```toml
[[extra.fonts]]
source = "google"
name = "IBM Plex Mono"
```

The `source` matches the subfolder under `static/fonts/` and `name` matches the synced folder inside it.

## Icons

Icons are SVG files stored in `static/icons/font-awesome/`. Use `scripts/py-ssg-tools` to sync them:

```sh
cd scripts/py-ssg-tools
uv run pst sync icons --source font-awesome --dest ../../static/icons/font-awesome/ --version 7.x
```

### Icon shortcode

```
{{ icon(name="star") }}
{{ icon(name="github", style="brands") }}
{{ icon(name="star", style="regular", class="my-class", aria="favourite") }}
```

Valid `style` values: `solid` (default), `regular`, `brands`.

Icon names come from [Font Awesome 6 Free](https://fontawesome.com/search?o=r&m=free).

To use the icon macro directly in templates:

```jinja2
{% import "macros/widgets.html" as widgets %}
{{ widgets::icon(name="star") }}
{{ widgets::icon(name="github", style="brands", class="my-class", aria="GitHub") }}
```

## Elink shortcode

Renders an external hyperlink. Opens in a new tab with `rel="noopener noreferrer"` and appends an external-link icon by default.

```
{{ elink(text="Link text", href="https://example.com") }}
{{ elink(text="Same tab", href="https://example.com", new_tab=false) }}
{{ elink(text="No icon", href="https://example.com", show_icon=false) }}
```

Parameters:

- `text` — visible link text (required)
- `href` — destination URL (required)
- `new_tab` — open in a new tab (default: `true`)
- `show_icon` — append an external-link icon (default: `true`)

## Border shortcode

Draws a themed frame around a block of content. The body is regular Markdown, so
text, lists, images and code blocks all work inside it.

```
{% border() %}
![screenshot](/images/example.png)
{% end %}

{% border(size="lg", color="pink") %}
Anything Markdown can produce.
{% end %}
```

Parameters:

- `size` — `sm` (1px), `md` (2px), `lg` (4px), `xl` (8px) — default: `md`
- `color` — `white`, `yellow`, `pink`, `green` — default: `white`

Colours are the theme's own tokens, so they follow dark/light mode automatically:
`yellow` is the primary accent, `pink` the secondary accent, `green` the link
colour, and `white` the body text colour.

Variants are plain attribute selectors in `sass/_components.scss`, so adding a
size or colour is a one-line CSS change — the shortcode needs no edit.

## Wide shortcode

Lets a block escape the reading column — useful for wide screenshots, big tables
and diagrams that feel cramped at the default measure.

```
{% wide() %}
![a wide screenshot](/images/wide.png)
{% end %}

{% wide(size="xl") %}
Spans the whole screen.
{% end %}
```

Parameters:

- `size` — `sm`, `md` (default), `lg`, `xl`

Against the default 42rem column, the sizes are roughly 48rem, 56rem, 72rem, and
"as wide as the screen allows". Every size is capped at the viewport minus
`--page-gutter`, so on a narrow screen they all fall back to the normal column
width rather than causing sideways scrolling.

It works at any nesting depth — inside `<article>`, or inside another shortcode:

```
{% wide(size="lg") %}
{% border(color="pink") %}
A bordered box at the wide width.
{% end %}
{% end %}
```

## Row / Col shortcodes

`row` lays its contents out side by side, `col` stacks them. Every top-level
block inside becomes an item, so two paragraphs are already two columns — no
per-item markup needed:

```
{% row() %}
![left](/images/a.png)
![right](/images/b.png)
{% end %}
```

Wrap blocks in `col` to group several of them into a single column:

```
{% row() %}
{% col() %}
### Left
Text under the heading.
{% end %}
{% col() %}
### Right
Text under the heading.
{% end %}
{% end %}
```

Give a column more of the width with `span`, which works like a table's colspan
— `span="2"` is exactly twice the width of a default column:

```
{% row() %}
{% col(span="2") %}
Twice the width.
{% end %}
{% col() %}
Half of that.
{% end %}
{% end %}
```

Parameters (both shortcodes):

- `gap` — `sm`, `md` (default), `lg`
- `span` — shares of the row's width (default: `1`)

Columns share the width evenly unless given a span, and collapse to a single
column on narrow screens with no media query of your own. A span only applies
to a `col` or a nested `row`, so a bare paragraph needs wrapping in `col`
before it can take one.

Spacing between items comes from `gap`, and the items' own margins are cleared
so the two don't compound. For more room than the reading column allows, nest
the row inside [`wide`](#wide-shortcode).

## Code shortcode

Shows several code blocks as tabs — the same example in more than one language.

````
{% code(titles=["Python", "Java"]) %}
```python
print("hi")
```
```java
System.out.println("hi");
```
{% end %}
````

Parameters:

- `titles` — one label per code block, in order

The body should hold nothing but fenced code blocks: each becomes one panel,
and panels pair with titles by position.

Switching is a radio group rather than a script, so it works with JavaScript
disabled and the arrow keys move between tabs. Zola's per-page `nth` counter
namespaces each group, so several `code` blocks on one page stay independent.
Up to 8 tabs are styled; raise the `@for` bound in `sass/_components.scss` for
more.

## Lmode / Dmode shortcodes

Show content in only one theme. Whatever you put inside `lmode` appears in light
mode only, and inside `dmode` in dark mode only — handy for screenshot pairs.

```
{% lmode() %}
![light](/images/home-light.png)
{% end %}

{% dmode() %}
![dark](/images/home-dark.png)
{% end %}
```

Neither takes any parameters — the body is regular Markdown, so text, lists,
images and code blocks all work inside.

Both variants are emitted and CSS reveals the matching one, so this works
without JavaScript (falling back to `prefers-color-scheme`). The hidden variant
is `display: none`, so screen readers only announce the visible one — but note
both images are still downloaded.

The underlying classes work on any element, if you'd rather not use a shortcode:

```html
<div class="only-dark">Shown only in dark mode.</div>
<span class="only-light">Shown only in light mode.</span>
```

## License

MIT
