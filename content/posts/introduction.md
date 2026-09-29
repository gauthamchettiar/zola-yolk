+++
title = "Introduction"
date = 2026-04-23
description = "What Zola is, what this theme does, and where to find the rest of the demo."

[taxonomies]
tags = ["zola", "theme"]
+++

## What is Zola?

{{ elink(text="Zola", href="https://www.getzola.org/") }} is a static site
generator: Markdown in, plain HTML out. It's a single binary with Sass, syntax
highlighting and search built in.

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

A small, dark, monospace theme where **the page looks a little like its
Markdown**: headings keep their `#`, menu items sit in `[brackets]`, tags are
`#hashtags`.

{% wide() %}
{% row() %}
{% col() %}

### Reading

- A single dark theme — no toggle, no flash of the wrong colours
- Full-text search — the Search menu item, or <kbd>Ctrl</kbd>/<kbd>Cmd</kbd> + <kbd>K</kbd>
- Posts grouped by year, each listed date first, browsable by tag
{% end %}
{% col() %}

### Authoring

- Shortcodes for icons, links, borders, columns and wide content
- Content that can differ between mobile and desktop
- Self-hosted fonts and icons — no third-party requests
{% end %}
{% end %}
{% end %}

## Where to go next

[Markdown Showcase](@/posts/markdown.md)
: Every Markdown element, rendered.

[Shortcode: Elements](@/posts/shortcode.md)
: Icons, links, marks, quotes, callouts, expand.

[Shortcode: Layouts](@/posts/layout.md)
: Borders, alignment, wide blocks, columns, tabs.

[Shortcode: Externals](@/posts/externals.md)
: Mermaid diagrams and KaTeX math.

[UI Showcase](@/posts/showcase.md)
: Screenshots of the theme.

[Configuration](@/posts/configuration.md)
: Every option, site-wide and per post.

[All posts](@/posts/_index.md) · [Tags](/tags)
: The archive and the tag index.

## Making it yours

Colours, fonts and spacing are CSS custom properties in `sass/_tokens.scss`.
