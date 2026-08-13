+++
title = "Introduction"
date = 2026-04-23
description = "What Zola is, what this theme does, and where to find the rest of the demo."

[taxonomies]
tags = ["zola", "theme"]
+++

The short version of what you are looking at: *the generator underneath, the
theme on top, and where the rest of the demo lives*.

## What is Zola?

{{ elink(text="Zola", href="https://www.getzola.org/") }} is a static site
generator. You write Markdown, it produces plain HTML files that any web server
can hand out as-is — no database, no runtime, nothing to keep patched.

It ships as a **single binary** with no dependencies: no Node, no Ruby, no
`node_modules`. Syntax highlighting, Sass compilation, search indexing and
internal-link checking are all built in, so this site needs no build pipeline
beyond one command.

{% row(gap="sm") %}
{% border(size="sm") %}
`zola serve`

Live-reloading preview.
{% end %}
{% border(size="sm") %}
`zola build`

The whole site into `public/`.
{% end %}
{% border(size="sm") %}
`zola check`

Validates every link.
{% end %}
{% end %}

## What is zola-yolk?

A deliberately small theme built around one idea: **the page should look a
little like the Markdown that produced it**. Headings keep their `#` prefixes,
menu items sit in `[brackets]`, and a post's metadata reads like a config block —
look just under the title of this page.

Everything is monospace, the palette is seven colours, and the whole stylesheet
is a few hundred lines split across four files.

{% wide() %}
{% row() %}
{% col() %}

### Reading

- Light and dark themes that follow your system and remember your choice
- Full-text search — press <kbd>Ctrl</kbd>/<kbd>Cmd</kbd> + <kbd>K</kbd>
- Posts grouped by year, browsable by tag
{% end %}
{% col() %}

### Authoring

- Shortcodes for icons, links, borders, columns and wide content
- Content that can differ between light and dark mode
- Self-hosted fonts and icons — no third-party requests
{% end %}
{% end %}
{% end %}

## Where to go next

[Markdown Showcase](@/posts/markdown.md)
: Every element the renderer supports, rendered live — plus what it deliberately does *not* support, and which features are off by default.

[Shortcode: Elements](@/posts/shortcode.md)
: Shortcodes that insert content — `icon`, `elink` and the theme-conditional `lmode` / `dmode`.

[Shortcode: Layouts](@/posts/layout.md)
: Shortcodes that arrange it — `border`, `wide`, and `row` / `col` with table-style proportional spans.

[Shortcode: Externals](@/posts/externals.md)
: Shortcodes that lean on a bundled external library — Mermaid diagrams and KaTeX math, both on by default.

[UI Showcase](@/posts/showcase.md)
: Screenshots of the theme in both modes.

[All posts](@/posts/_index.md) · [Tags](/tags)
: The archive, grouped by year, and the tag index.

## Making it yours

Colours, fonts and spacing are CSS custom properties in one file,
`sass/_tokens.scss`. Each colour declares its light and dark value on a single
line, so restyling the theme means editing that file and nothing else.

The rest of the stylesheet is split by role — bare element styles, page layout,
and the handful of components that genuinely need a class. Most of the theme is
styled by element rather than by class, so semantic markup picks up the right
styling on its own.
