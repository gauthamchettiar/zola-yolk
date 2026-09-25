+++
title = "Shortcodes"
date = 2026-04-17
description = "Everything the theme's shortcodes can do, across three posts: the ones that insert content, the ones that arrange it, and the ones that lean on a bundled library."

[taxonomies]
tags = ["shortcode", "zola"]

[extra]
# The overview of a series is a way in to the three parts, not a post that
# stands on its own — it belongs in the series, not in the site's recents.
list = "local"
series = "Shortcodes"
series_part = 0
+++

Zola calls a reusable snippet you can drop into a post a
{{ elink(text="shortcode", href="https://www.getzola.org/documentation/content/shortcodes/") }}.
This theme ships around thirty of them, and they split cleanly into three
groups — one post each.

## What's in each part

Every shortcode here is a thin wrapper over a macro, so all of them are
callable from Markdown *and* from a template with identical output. Which post
covers a shortcode depends only on what it does to your page:

- **[Elements](@/posts/shortcode.md)** — shortcodes that *insert* something
  that wasn't there: icons, external links, marks, coloured text, quotes,
  callouts and blocks that appear in only one theme or one screen size.
- **[Layouts](@/posts/layout.md)** — shortcodes that *arrange* what you already
  wrote: borders, alignment, wide blocks, columns, tabbed code.
- **[Externals](@/posts/externals.md)** — the two that need a library beyond
  Zola itself: Mermaid diagrams and KaTeX math. Both libraries ship inside the
  theme, and each is behind a flag so a site that uses neither pays nothing for
  them.

## Where to start

Read them in order if you're new to the theme — each post assumes only what the
one before it showed. If you're after one specific shortcode, the theme's
[README](https://github.com/gauthamchettiar/zola-yolk) lists every one with its
parameters, and links straight to the part that demonstrates it.
