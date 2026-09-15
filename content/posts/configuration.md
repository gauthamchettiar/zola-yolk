+++
title = "Configuration"
date = 2026-04-24
description = "Every option the theme reads, where it goes, and what it does — the site-wide defaults in zola.toml and the per-post overrides that beat them."

[taxonomies]
tags = ["config", "theme", "zola"]

[extra]
toc_max_level = 3
+++

Every option the theme reads, in one place: *what it does, where it goes, and
what it falls back to.*

## Two places, one name

Theme options live under `[extra]`, and almost every one of them exists twice —
once in `zola.toml` as the site's default, and once in a post's own front
matter as an override for that post alone.

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

**The two names are always the same.** A post overrides `toc` by writing `toc`,
`series_panel` by writing `series_panel`, `list` by writing `list` — so what you
read in a post's front matter is what you look up in `zola.toml`, with nothing
to translate between them.

The one prefix in the file marks the exception. A key beginning `enable_` is a
whole feature of the theme, switched on or off for the site, and no post
overrides it — there is no per-post `enable_search`, because a single post
cannot put a button in the header. Everything without the prefix is either a
site setting with no per-post meaning at all (`content_sections`, `footer`) or a
default a post may override under its own name.

{% admonition(title="Anything under [extra] is yours", color="blue") %}
Zola never validates `[extra]`. A misspelled key is not an error — it is simply
a key nothing reads, and the theme quietly uses its default. If an option looks
like it is being ignored, check the spelling and the table it belongs to before
anything else.
{% end %}

## Site options

These are the site's own. They are set under `[extra]` in `zola.toml`, and a
post has no say in any of them.

### Content and navigation

{% wide() %}
| Key | What it does | Default |
|---|---|---|
| `content_sections` | The sections posts live in, as folder names under `content/`. Feeds the home page's recent posts list and the pool the series panel draws from | unset — see the note below |
| `recent_limit` | How many posts the home page lists under "Recent posts"; `0` shows every one | `10` |
| `main_menu` | The header links, as an array of tables — each with a `name` and a `url` | unset (no menu) |
| `footer` | Footer text; plain text or Markdown | unset |
| `language_direction` | Writing direction, written to `<html dir="…">` | `"ltr"` |
{% end %}

`content_sections` has no single fallback, which is the one place the theme is
inconsistent with itself. Left unset, the series panel and the series listing
page fall back to every root-level section — but the home page has none, and
prints *No sections specified for displaying recents* instead. Set it.

```toml
[extra]
content_sections = ["posts"]
recent_limit = 10

[[extra.main_menu]]
name = "Posts"
url = "/posts"
```

### Feature switches

The four keys carrying the `enable_` prefix. Each turns a whole feature on or
off for the site, and none of them can be overridden by a post.

{% wide() %}
| Key | What it does | Default |
|---|---|---|
| `enable_theme_switcher` | Shows the dark/light toggle in the header | `true` |
| `enable_search` | Shows the search button. Needs Zola's own `build_search_index = true` as well — the button has nothing to search without it | `true` |
| `enable_mermaid` | Lets ` ```mermaid ` blocks render as diagrams through `render()` | `true` |
| `enable_math` | Lets ` ```math ` blocks render as notation through `render()` | `true` |
{% end %}

Both libraries ship inside the theme's own `static/`, so neither costs a
third-party request. With a flag off, a `mermaid` block falls back to a plain
code block and a `math` block to its raw source — nothing is lost but the
rendering.

### Fonts

One table per family, under `[[extra.fonts]]`.

{% wide() %}
| Key | What it does | Default |
|---|---|---|
| `source` | Subfolder under `static/fonts/` the family was synced into | required |
| `name` | Folder name of the family under that source | required |
| `preload` | Subset files fetched alongside the stylesheet rather than one request behind it | unset |
{% end %}

Only list a `preload` file the site actually draws text with — a preloaded font
that goes unused is a wasted download the browser will warn about in the
console.

## Defaults a post can override

Each key below is written the same way in both places: under `[extra]` in
`zola.toml` to set the site's default, and under `[extra]` in a post's front
matter to override it for that post alone. `list` is one of these too, and has
a section of its own further down.

### Table of contents

{% wide() %}
| Key | What it does | Default |
|---|---|---|
| `toc` | Whether the post gets a collapsible table of contents | `true` |
| `toc_max_level` | Deepest heading shown, `1` (h1) to `6` (h6) | `6` |
| `toc_exclude` | Heading ids left out wherever they occur | `[]` |
{% end %}

An excluded heading is dropped alone and its children move up to take its
place; a heading past `toc_max_level` is dropped *with* its children, since
they are deeper still. That difference is deliberate — the usual reason to
exclude one heading is that it demonstrates heading syntax rather than dividing
the page, and the sections under it are still real.

### Series

{% wide() %}
| Key | What it does | Default |
|---|---|---|
| `series` | The name of the series this post belongs to. Naming one is what puts a post in it. **Post only** | unset |
| `series_part` | Where the post sits in the reading order. `0` marks the overview page. **Post only** | unset |
| `series_panel` | Whether the panel listing the parts appears above the contents | `true` |
| `series_state` | Whether that panel starts open: `"expanded"` or `"collapsed"` | `"expanded"` |
| `series_nav` | Previous/next links under the post | `true` |
{% end %}

A series of one post renders neither panel nor nav — there is nothing to
introduce and nowhere to go next. A part left without a `series_part` still
belongs to the series and is listed, unnumbered, at the end.

### Related posts

{% wide() %}
| Key | What it does | Default |
|---|---|---|
| `related` | Whether posts to read next are listed under the post. On a post it does double duty — see below | `true` |
| `related_limit` | How many to list; `0` shows every match | `0` |
{% end %}

`related` on a post does two jobs. A list of paths picks the posts by hand, in
that order; `false` turns the section off for that post alone.

```toml
[extra]
related = ["posts/markdown.md", "posts/showcase.md"]
```

Left to itself the theme matches by tag: every post sharing at least one tag,
most tags in common first, newest first at equal footing. Other parts of the
post's own series are left out, since the panel at the top already lists them
in order.

## Where a post is listed

`list` decides how far a post travels through the site's listings. It is a
post-level key with a site-wide default of the same name, and it takes one of
three words.

{% wide() %}
| Value | Meaning |
|---|---|
| `"always"` | Every listing. The default |
| `"local"` | Its own section's listing, and its series — nowhere else |
| `"never"` | No listing at all |
{% end %}

```toml
+++
title = "Reachable, but not advertised"

[extra]
list = "never"
+++
```

{% admonition(title="`list` is not `draft`", color="yellow") %}
A post is **rendered at its permalink whichever value it takes**. `list` governs
where a post is advertised, not whether it exists — `list = "never"` keeps a
page reachable by anyone holding the link. To stop a page being built at all,
use Zola's own `draft = true` instead.
{% end %}

Surface by surface:

{% wide() %}
| Surface | `"always"` | `"local"` | `"never"` |
|---|---|---|---|
| Rendered at its permalink | yes | yes | yes |
| Its own section's list, and the count beside it | yes | yes | no |
| Home page "Recent posts" | yes | no | no |
| Tag pages, and the counts on the tag index | yes | no | no |
| Related posts, when found by tag | yes | no | no |
| Series panel and the series listing page | yes | yes | no |
| `atom.xml` | yes | no | no |
| `sitemap.xml` | yes | yes | no |
| Search index | yes | yes | yes — see below |
{% end %}

Two rows are worth explaining. A **series** keeps its `"local"` parts because a
series is a local grouping to begin with; a part held back by `"never"` leaves a
gap in the numbering rather than shifting the parts after it, since each part is
numbered by its own `series_part`. And a **sitemap** keeps `"local"` because
such a post is linked from its own section like any other, while a `"never"`
post is precisely the kind of unlinked page a sitemap would otherwise expose.

A path named by hand in `related` is honoured whatever its `list` says. A
hand-picked link is not a listing.

{% admonition(title="Search is a separate key", color="red") %}
`list` does not touch the search index, and cannot: Zola builds it internally
with no template to filter. A post that should stay out of the search box needs
Zola's own key alongside, at the top level of its front matter rather than
under `[extra]`:

```toml
+++
title = "Reachable, but not advertised"
in_search_index = false

[extra]
list = "never"
+++
```
{% end %}

Holding a post back from the feed and the sitemap means the theme owns
`templates/atom.xml` and `templates/sitemap.xml`, which are Zola's built-ins
plus a filter. When upgrading Zola, diff them against
`components/templates/src/builtins/` in the Zola repository and re-apply the
filter rather than editing around it.

## Zola's own keys worth knowing

Not theme options — these are Zola's, and they sit at the top level of front
matter rather than under `[extra]`. They come up because they overlap with what
`list` does.

{% wide() %}
| Key | What it does |
|---|---|
| `draft` | `true` drops the page from the build entirely: no page at its URL, and absent from every listing, the feed, the sitemap and the search index. Built only with `zola build --drafts` |
| `render` | `false` writes no HTML for the page — but its permalink survives in tag pages and the feed, both then pointing at a URL that 404s. `list = "never"` is almost always what was actually wanted |
| `in_search_index` | `false` keeps the page out of the search index |
| `template` | Renders the page or section with a named template — `content/series/_index.md` uses it to become the series listing page |
{% end %}

One more that is easy to put in the wrong place: `insert_anchor_links` adds a
clickable anchor beside every heading, and belongs under `[markdown]` in
`zola.toml`, taking `"left"`, `"right"`, `"heading"` or `"none"`. Written under
`[extra]`, or set to `true`, it does nothing at all.

## Where to go next

[Markdown Showcase](@/posts/markdown.md)
: Every element the renderer supports, and the `[markdown]` settings that change how it behaves.

[Shortcode: Elements](@/posts/shortcode.md)
: The shortcodes these options switch on and off.

[Shortcodes](@/posts/shortcodes.md)
: The full tour, in three parts.
