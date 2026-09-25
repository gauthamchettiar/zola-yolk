+++
title = "Configuration"
date = 2026-04-16
description = "Every option the theme reads: the site-wide defaults in zola.toml and the per-post keys that override them."

[taxonomies]
tags = ["config", "theme", "zola"]

[extra]
toc_max_level = 3
+++

Every option the theme reads, what it does, and what it falls back to.

## How options work

Theme options live under `[extra]` — in `zola.toml` for the site, in a post's
front matter for that post alone. A post wins, using the same key name.

{% row(gap="sm") %}
{% col() %}

**`zola.toml` — the default**

```toml
[extra]
toc = true
toc_max_level = 6
```
{% end %}
{% col() %}

**a post — the exception**

```toml
+++
title = "No contents here"

[extra]
toc = false
+++
```
{% end %}
{% end %}

Keys prefixed `enable_` are the exception: they switch a feature on for the
whole site, and no post overrides them.

{% admonition(title="Anything under [extra] is yours", color="blue") %}
Zola never validates `[extra]`. A misspelled key is not an error — it is a key
nothing reads, and the theme quietly uses its default. If an option looks like
it is being ignored, check the spelling first.
{% end %}

## Site options

Set these in `zola.toml`. Posts have no say in any of them.

{% wide() %}
| Key | What it does | Default |
|---|---|---|
| `content_sections` | The sections posts live in, as folder names under `content/`. Feeds the home page's recent posts and the pool the series panel draws from | unset — set it |
| `recent_limit` | How many posts the home page lists; `0` shows every one | `10` |
| `main_menu` | Header links, as an array of tables with a `name` and a `url` | unset |
| `footer` | Footer text, as Markdown | `"Written with ❤️"` |
| `language_direction` | Writing direction, written to `<html dir="…">` | `"ltr"` |
| `enable_theme_switcher` | The dark/light toggle in the header | `true` |
| `enable_search` | The search button. Needs Zola's own `build_search_index = true` as well | `true` |
| `enable_mermaid` | Lets ` ```mermaid ` blocks render as diagrams through `render()` | `true` |
| `enable_math` | Lets ` ```math ` blocks render as notation through `render()` | `true` |
{% end %}

Left unset, `content_sections` makes the home page print *No sections specified
for displaying recents*.

```toml
[extra]
content_sections = ["posts"]
recent_limit = 10

[[extra.main_menu]]
name = "Posts"
url = "/posts"
```

### Fonts

One table per family, under `[[extra.fonts]]`.

{% wide() %}
| Key | What it does | Default |
|---|---|---|
| `source` | Subfolder under `static/fonts/` the family was synced into | required |
| `name` | Folder name of the family under that source | required |
| `preload` | Subset files fetched alongside the stylesheet rather than one request behind it | `[]` |
{% end %}

Only preload a file the site actually draws text with — an unused one is a
wasted download the browser warns about.

## Post options

Each of these is a site default in `zola.toml` and an override in a post, under
the same name.

{% wide() %}
| Key | What it does | Default |
|---|---|---|
| `list` | Where the post is listed — see below | `"always"` |
| `toc` | Whether the post gets a collapsible table of contents | `true` |
| `toc_max_level` | Deepest heading shown, `1` (h1) to `6` (h6) | `6` |
| `toc_exclude` | Heading ids left out wherever they occur | `[]` |
| `series` | The series this post belongs to. Naming one is what joins it. Posts only | unset |
| `series_part` | Position in the reading order; `0` marks the overview. Posts only | unset |
| `series_panel` | The panel listing the parts, above the contents | `true` |
| `series_state` | Whether that panel starts `"expanded"` or `"collapsed"` | `"expanded"` |
| `series_nav` | Previous/next links under the post | `true` |
| `related` | Posts to read next, matched by shared tags. A list of paths picks them by hand instead; `false` turns the section off | `true` |
| `related_limit` | How many to list; `0` shows every match | `0` |
{% end %}

```toml
+++
title = "Part two"

[extra]
series = "Shortcodes"
series_part = 2
related = ["posts/markdown.md", "posts/showcase.md"]
+++
```

## Where a post is listed

`list` takes one of three words, and decides how far a post travels through the
site's listings.

{% wide() %}
| Surface | `"always"` | `"local"` | `"never"` |
|---|---|---|---|
| Rendered at its permalink | yes | yes | yes |
| Its own section's list | yes | yes | no |
| Series panel and series listing | yes | yes | no |
| `sitemap.xml` | yes | yes | no |
| Home page "Recent posts" | yes | no | no |
| Tag pages and tag counts | yes | no | no |
| Related posts, when matched by tag | yes | no | no |
| `atom.xml` | yes | no | no |
| Search index | yes | yes | yes |
{% end %}

A path named by hand in `related` is honoured whatever its `list` says — a
hand-picked link is not a listing.

{% admonition(title="`list` is not `draft`", color="yellow") %}
A post is **rendered at its permalink whichever value it takes**. `list`
governs where a post is advertised, not whether it exists — `list = "never"`
keeps a page reachable by anyone holding the link. To stop a page being built
at all, use Zola's own `draft = true`.
{% end %}

{% admonition(title="Search is a separate key", color="red") %}
`list` cannot touch the search index: Zola builds it internally, with no
template to filter. Keeping a post out of the search box needs Zola's own key,
at the top level of the front matter rather than under `[extra]`:

```toml
+++
title = "Reachable, but not advertised"
in_search_index = false

[extra]
list = "never"
+++
```
{% end %}

## Zola's own keys worth knowing

Not theme options — these are Zola's, and sit at the top level of front matter
rather than under `[extra]`. They come up because they overlap with `list`.

{% wide() %}
| Key | What it does |
|---|---|
| `draft` | `true` drops the page from the build entirely. Built only with `zola build --drafts` |
| `render` | `false` writes no HTML, but the permalink survives in tag pages and the feed, pointing at a URL that 404s. `list = "never"` is almost always what was wanted |
| `in_search_index` | `false` keeps the page out of the search index |
| `template` | Renders the page with a named template — `content/series/_index.md` uses it to become the series listing |
{% end %}

One more that is easy to misplace: `insert_anchor_links` adds a clickable
anchor beside every heading, and belongs under `[markdown]` in `zola.toml`,
taking `"left"`, `"right"`, `"heading"` or `"none"`. Under `[extra]`, or set to
`true`, it does nothing.

## Where to go next

[Markdown Showcase](@/posts/markdown.md)
: Every element the renderer supports, and the `[markdown]` settings behind them.

[Shortcode: Elements](@/posts/shortcode.md)
: The shortcodes these options switch on and off.

[Shortcodes](@/posts/shortcodes.md)
: The full tour, in three parts.
