# zola-yolk 🟡

A minimal, monospace Zola theme with dark/light mode, full-text search, and multiple shortcode support. Created with a component-based template architecture for easy extensibility.

Shortcodes: [`icon`](#icon-shortcode), [`elink`](#elink), [`mark`](#mark), [`quote`](#quote), [`admonition`](#admonition) ([`note`](#admonition) / [`warning`](#admonition) / [`danger`](#admonition) / [`info`](#admonition) / [`tip`](#admonition)), [`border`](#border), [`wide`](#wide), [`row` / `col`](#row--col), [`code`](#code), [`lmode` / `dmode`](#lmode--dmode).

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

From a template:

```jinja2
{% import "macros/widgets.html" as widgets %}
{{ widgets::icon(name="star") }}
```

- `name` — Font Awesome icon name (required)
- `style` — `solid` (default), `regular`, `brands`
- `source` — icon pack subfolder (default: `font-awesome`)
- `class` — extra CSS classes
- `aria` — accessible label; omit to render the icon decorative

Icon names come from [Font Awesome Free](https://fontawesome.com/search?o=r&m=free).

## Shortcodes

Every shortcode is a thin wrapper over a macro, so each one is callable from
Markdown **and** from a template, with identical output. Content-inserting
macros live in `macros/widgets.html`; the ones that arrange content live in
`macros/blocks.html`.

Block shortcodes take their content as the body; the matching macro takes it as
a `content` argument of already-rendered HTML.

### Elink

An external hyperlink. Opens in a new tab with `rel="noopener noreferrer"`.

```
{{ elink(text="Link text", href="https://example.com") }}
```
```jinja2
{{ widgets::elink(text="Link text", href="https://example.com") }}
```

- `text`, `href` — required
- `new_tab` — default `true` · `show_icon` — default `true`

### Mark

Calls out a run of text.

```
{{ mark(text="highlighted") }}
{{ mark(text="outlined", color="pink", decoration="border") }}
```
```jinja2
{{ widgets::mark(text="highlighted", color="green") }}
```

- `text` — required
- `color` — `white`, `yellow` (default), `pink`, `green`, `red`, `blue`, `muted`
- `decoration` — `highlight` (default), `border`

### Quote

An attributed quotation, rendered as `<figure>` / `<blockquote>` /
`<figcaption>` — the attribution describes the quote, so HTML puts it outside
the quote itself.

```
{% quote(author="Alan Kay", cite="1971") %}
The best way to predict the future is to invent it.
{% end %}
```
```jinja2
{{ blocks::quote(content="<p>…</p>", author="Alan Kay", cite="1971") }}
```

- `author` — who said it · `cite` — the work, rendered in `<cite>`
- `url` — source URL; sets the blockquote's `cite` attribute and links the citation
- `color` — `white`, `yellow`, `pink` (default), `green`, `red`, `blue`, `muted`

### Admonition

A callout set apart from the surrounding text, rendered as `<aside>`.

```
{% admonition(title="Careful", icon="triangle-exclamation", color="pink") %}
This one bites.
{% end %}
```
```jinja2
{{ blocks::admonition(content="<p>Worth knowing.</p>", title="Note") }}
```

- `title` — optional heading · `icon` — Font Awesome name (default: `circle-info`)
- `color` — `white`, `yellow` (default), `pink`, `green`, `red`, `blue`, `muted`

`note`, `warning`, `danger`, `info` and `tip` are presets of `admonition` with
a fixed color and icon, and a title that defaults to their own name:

```
{% note() %}
Worth knowing.
{% end %}

{% warning(title="Careful") %}
This one bites.
{% end %}
```

| shortcode | color   | icon                  |
| --------- | ------- | --------------------- |
| `note`    | yellow  | `note-sticky`         |
| `warning` | pink    | `triangle-exclamation`|
| `danger`  | red     | `circle-exclamation`  |
| `info`    | green   | `circle-info`         |
| `tip`     | blue    | `lightbulb`           |

Each takes the same `title` parameter as `admonition`, defaulting to its own
name (`"Note"`, `"Warning"`, …) instead of none.

### Border

Draws a themed frame around a block.

```
{% border(size="lg", color="pink", style="dashed") %}
Anything Markdown can produce.
{% end %}
```
```jinja2
{{ blocks::border(content="<p>…</p>", size="lg", color="pink", style="dashed") }}
```

- `size` — `sm` (1px), `md` (2px, default), `lg` (4px), `xl` (8px)
- `color` — `white` (default), `yellow`, `pink`, `green`, `red`, `blue`, `muted`
- `style` — `solid` (default), `dashed`, `dotted`, `double`

`double` needs at least 3px to separate into two lines, so it looks solid at
`size="sm"`.

### Wide

Lets a block escape the reading column.

```
{% wide(size="lg") %}
![a wide screenshot](/images/wide.png)
{% end %}
```
```jinja2
{{ blocks::wide(content="<p>…</p>", size="lg") }}
```

- `size` — `sm`, `md` (default), `lg`, `xl`

Every size is capped at the viewport minus `--page-gutter`, so on a narrow
screen they all fall back to the normal column width.

### Row / Col

`row` lays its contents out side by side, `col` stacks them. Every top-level
block inside a row becomes a column, so two images need no per-item markup.

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

Tera cannot combine a macro call with `~` in one expression, so from a template
build the columns with `set` first:

```jinja2
{% set a = blocks::col(content="<p>Left</p>", span="2") %}
{% set b = blocks::col(content="<p>Right</p>") %}
{{ blocks::row(content=a ~ b) }}
```

- `gap` — `sm`, `md` (default), `lg`
- `span` — shares of the row's width, like a table colspan (default: `1`)

Columns collapse to a single column on narrow screens with no media query of
your own. For more room than the reading column allows, nest the row inside
`wide`.

### Code

Shows several code blocks as tabs.

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
```jinja2
{{ blocks::code(content=panels, titles=["Python", "Java"], id="api") }}
```

- `titles` — one label per code block, in order
- `group` — optional name; blocks sharing one switch together

The body should hold nothing but fenced code blocks: each becomes one panel,
paired with a title by position. Switching is a radio group rather than a
script, so it works with JavaScript disabled and the arrow keys move between
tabs. The shortcode uses Zola's per-page `nth` to namespace each block; from a
template, pass your own `id`. Up to 8 tabs are styled — raise the `@for` bound
in `sass/_components.scss` for more.

Blocks given the same `group` move as one: picking a tab in any of them picks
the tab at the same position in all the others, which suits a page that shows
the same example over and over in two forms. Each block still owns its radios,
so this is the only part that needs JavaScript (`partials/tabs.html`); without
it every block simply switches on its own.

A group switch resizes every block on the page at once, including ones above
the one clicked — which would otherwise drag the scroll position along as they
resize. `partials/tabs.html` measures the clicked block's position before and
after the sync and scrolls by the difference in the same frame, so nothing
above the click visibly moves.

### Lmode / Dmode

Show content in only one theme.

```
{% lmode() %}
![light](/images/home-light.png)
{% end %}

{% dmode() %}
![dark](/images/home-dark.png)
{% end %}
```
```jinja2
{{ blocks::lmode(content="<p>Light only.</p>") }}
{{ blocks::dmode(content="<p>Dark only.</p>") }}
```

Neither takes parameters. Both variants are emitted and CSS reveals the
matching one, so this works without JavaScript. The underlying classes work on
any element if you would rather not use a shortcode:

```html
<div class="only-dark">Shown only in dark mode.</div>
```

## License

MIT
