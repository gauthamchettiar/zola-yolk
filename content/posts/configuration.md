+++
title = "Configuration"
date = 2026-04-16
description = "Every option the theme reads: the site-wide defaults in zola.toml and the per-post keys that override them."

[taxonomies]
tags = ["config", "theme", "zola"]

[extra]
toc_max_level = 3
+++

Theme options live under `[extra]`: in `zola.toml` for the site, in a post's
front matter for that post. The post wins. `enable_` keys are site-only.
Zola doesn't validate `[extra]`, so a misspelled key is silently ignored.

## Site options

{% wide() %}
| Key | What it does | Default |
|---|---|---|
| `content_sections` | Folders under `content/` that hold posts. Feeds recent posts, series and the sitemap filter | every root section |
| `recent_limit` | Posts on the home page; `0` = all | `10` |
| `main_menu` | Header links (`name`, `url`). The current one is white | unset |
| `footer` | Footer text, Markdown | `"Written with ❤️"` |
| `language_direction` | `<html dir>` | `"ltr"` |
| `series_page` | Series listing section; series labels link to it when a series has no overview | `"series"` |
| `series_label_texts` | Label text per series name; beats `series_label_text` | unset |
| `enable_search` | Search menu item (and <kbd>Ctrl</kbd>/<kbd>Cmd</kbd> + <kbd>K</kbd>). Needs `build_search_index = true` | `true` |
| `enable_mermaid` | ` ```mermaid ` through `render()` | `true` |
| `enable_math` | ` ```math ` through `render()` | `true` |
{% end %}

### Fonts

One `[[extra.fonts]]` table per family: `source` (folder under
`static/fonts/`), `name` (the synced folder) and optional `preload` (subset
files to fetch early — only ones the site actually uses).

## Post options

Site defaults in `zola.toml`, overridable per post.

{% wide() %}
| Key | What it does | Default |
|---|---|---|
| `list` | Where the post is listed — see below | `"always"` |
| `toc` | Table of contents | `true` |
| `toc_state` | `"collapsed"` or `"expanded"` | `"collapsed"` |
| `toc_max_level` | Deepest heading, `1`–`6` | `6` |
| `toc_exclude` | Heading ids to leave out | `[]` |
| `series` | Series name (posts only) | unset |
| `series_part` | Position; `0` = overview (posts only) | unset |
| `series_label` | "Part X of N …" under the date (not on the overview) | `true` |
| `series_label_text` | Label text; `{part}`, `{count}`, `{series}` filled in | `"Part {part} of {count} from series “{series}”"` |
| `series_nav` | Previous / next links | `true` |
| `related` | `true` = by tag, a list of paths, or `false` | `true` |
| `related_limit` | `0` = all | `0` |
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

{% wide() %}
| Surface | `"always"` | `"local"` | `"never"` |
|---|---|---|---|
| Its permalink | yes | yes | yes |
| Its own section's list | yes | yes | no |
| Series | yes | yes | no |
| `sitemap.xml` | yes | yes | no |
| Home page, tag pages, tag-matched related, `atom.xml` | yes | no | no |
| Search index | yes | yes | yes |
{% end %}

`list` hides, it doesn't delete — use Zola's `draft = true` for that. To keep a
post out of search, add Zola's `in_search_index = false` at the top level of its
front matter. A path named in `related` is always shown.
