+++
title = "Markdown Showcase"
date = 2026-04-21
description = "A sample post covering common Markdown elements."

[taxonomies]
tags = ["markdown", "syntax", "zola"]

[extra]
# These headings exist only to show what each level looks like, not as real
# sections — left out of the table of contents so they don't derail its
# nesting (a real h1 or h6 appearing where a section boundary is expected
# throws off every heading that follows it).
toc_exclude = ["heading-1", "heading-2", "heading-3", "heading-4", "heading-5", "heading-6", "setext-headings","my-heading","heading-ids", "custom"]
+++

A comprehensive reference for Markdown syntax supported by Zola (pulldown-cmark).

## Headings

```
# Heading 1
## Heading 2
### Heading 3
#### Heading 4
##### Heading 5
###### Heading 6
```

# Heading 1

## Heading 2

### Heading 3

#### Heading 4

##### Heading 5

###### Heading 6

### Setext headings

The first two levels can also be underlined:

```
Heading 1
=========

Heading 2
---------
```

### Heading IDs

Every heading gets an `id` derived from its text, which is what makes anchor
links work. Override it with `{#custom-id}`:

```
#### My Heading                        → id="my-heading"
#### Heading with custom id {#custom}  → id="custom"
```

#### My Heading                      
#### Heading with custom id {#custom}

That heading is reachable at `[Custom Heading](#custom)` ->  [Custom Heading](#custom)

## Text Formatting

| Syntax | Rendering |
|---|---|
| `**bold**`, `__bold__` | **bold** |
| `*italic*`, `__italic__` | *italic* |
| `***bold italic***`, `___bold italic___` | ***bold italic*** |
| `` `code` `` | `code` |
| `~~strikethrough~~` | ~~strikethrough~~ |
| `\*escaped\*` | \*escaped\* |
| `&copy;` | &copy; |
| `<ins>inserted</ins>` | <ins>inserted</ins> |
| `<mark>highlight</mark>` | <mark>highlight</mark> |
| `<sub>sub</sub>script` | <sub>sub</sub>script |
| `<sup>super</sup>script` | <sup>super</sup>script |

{% tip() %}
Backslash-escape any Markdown character to render it literally — `\*`, `\_`,
`\#`, `\[`, `` \` ``. HTML entities such as `&copy;`, `&amp;` and `&#169;` pass
straight through.
{% end %}

{% warning() %}
`++inserted++`, `==mark==`, `~sub~`, `^sup^` are **not** supported by Zola's renderer — use inline HTML instead (shown above).
{% end %}

## Paragraphs and Line Breaks

Leaving a blank line creates a new paragraph.

Two trailing spaces at the end of a line  
creates a line break without a new paragraph.

A trailing backslash does the same thing and is easier to spot in a diff\
because trailing whitespace is invisible.

## Lists

### Unordered

```
- First item
- Second item
  + Nested item
```

- First item
- Second item
  + Nested item

### Ordered

```
1. Step one
2. Step two
   1. Nested step
```

1. Step one
2. Step two
   1. Nested step

### Markers and numbering

`-`, `*` and `+` all start an unordered list. Ordered lists accept `.` or `)`,
and start from whatever number you give:

```
9. starts at nine
10. keeps counting
```

9. starts at nine
10. keeps counting

### Loose and tight lists

Items separated by a blank line are a *loose* list — each item is wrapped in a
`<p>`, which adds vertical spacing. Without blank lines the list is *tight*.

### Task list

```
- [x] Write content
- [x] Pick a theme
- [ ] Deploy to production
```

- [x] Write content
- [x] Pick a theme
- [ ] Deploy to production

### Definition list

```
Term
: Definition
```

Zola
: A fast static site generator written in Rust.

pulldown-cmark
: The CommonMark-compliant Markdown parser used by Zola.

## Horizontal Rule

Created with `---`, `***`, or `___`:

---

## Blockquote

```
> The best way to predict the future is to invent it.
> — Alan Kay
```

> The best way to predict the future is to invent it.  
> — Alan Kay

{% tip() %} 
Blockquotes nest, and can hold any other block — lists, code, headings.
{% end %}

{% note(title="") %}
There is an alternate [shortcode version](/posts/shortcode/#quotes) that supports author, cite and colours.  

{% end %}

## Footnote

Zola is a static site generator[^1] written in Rust[^2].

[^1]: A static site generator pre-builds all pages into plain HTML files.
[^2]: Rust is a systems programming language focused on safety and performance.

## Code

Inline — wrap in backticks: `` `let x = 42;` `` → `let x = 42;`

Plain block — wrap in triple backticks:

````
```
plain text block
no syntax highlighting
```
````

```
plain text block
no syntax highlighting
```

Syntax-highlighted block — add language name after opening backticks:

````
```rust
fn main() {
    println!("Hello, Zola!");
}
```
````

```rust
fn main() {
    println!("Hello, Zola!");
}
```

{% tip() %}
- Tildes work as fences too, which is handy when the code itself contains
backticks - just use `~~~` instead of ```.
- Indenting by four spaces also makes a code block, with no language
{% end %}

## Table

```
| Column A | Column B | Column C |
|----------|----------|----------|
| Alpha    | Beta     | Gamma    |
```

| Column A | Column B | Column C |
|----------|----------|----------|
| Alpha    | Beta     | Gamma    |
| Delta    | Epsilon  | Zeta     |

Add colons to the separator row to align a column:

```
| Left | Center | Right |
|:-----|:------:|------:|
| a    | b      | c     |
```

| Left | Center | Right |
|:-----|:------:|------:|
| a    | b      | c     |

## Links

<u>Simple Links</u>:  
Syntax : `<https://www.getzola.org>`  
Look &nbsp; : &nbsp;<https://www.getzola.org>

<u>Custom Link Text</u>:  
Syntax : `[Visit Zola](https://www.getzola.org)`  
Look &nbsp; : &nbsp;[Visit Zola](https://www.getzola.org)

<u>Custom Link Text (with title)</u>:  
Syntax : `[Visit Zola](https://www.getzola.org "Official Zola website")`  
Look &nbsp; : &nbsp;[Visit Zola](https://www.getzola.org "Official Zola website") (hover on link to see text)

<u>Anchor Link</u>  
Syntax : `[Back to top](#headings)`  
Look &nbsp; : &nbsp;[Back to top](#headings)

<u>Email Link</u>  
Syntax : `<someone@example.com>`  
Look &nbsp; : &nbsp;<someone@example.com>

<u>Reference Link</u> — define the target once, reuse it anywhere:

```
Read the [Zola docs][docs] and the [docs][] again.

[docs]: https://www.getzola.org "Official Zola website"
```

Read the [Zola docs][docs] and the [docs][] again.

[docs]: https://www.getzola.org "Official Zola website"

<u>Internal Link</u> — Zola resolves `@/` paths to the page's permalink and
`zola check` fails the build if the target does not exist, so these cannot rot:

```
[Supported Shortcodes](@/posts/shortcode.md)
```

Look &nbsp; : &nbsp;[Supported Shortcodes](@/posts/shortcode.md)

{% warning() %}
A bare URL such as `https://example.com` is **not** auto-linked — wrap it in `<>` angle brackets or use `[text](url)`.
{% end %}

## Images

Plain image — `![alt text](path/to/image.jpg)`:

![An ant on a plumeria flower](/images/ant_on_a_flower.jpg)

Images take an optional title, and support the same reference syntax as links:

```
![alt text](path/to/image.jpg "Title shown on hover")
![alt text][img-ref]

[img-ref]: path/to/image.jpg "Title"
```

## Raw HTML

Inline HTML works anywhere (the formatting table above relies on it). Block-level
HTML is passed straight through, but note that **Markdown inside a raw HTML block
is not parsed** — `**this**` stays literal:

```html
<div align="center">
  <strong>Use HTML tags, not Markdown, inside a block.</strong>
</div>
```

<div align="center">
  <strong>Use HTML tags, not Markdown, inside a block.</strong>
</div>

### Off by default

These work, but only once enabled under `[markdown]` in `config.toml` 

{% wide() %}
| Setting | Effect | Accepted values |
|---|---|---|
| `render_emoji` | `:smile:` renders as an emoji | `true`, `false` (default) |
| `smart_punctuation` | straight quotes become curly, `--` becomes an en dash | `true`, `false` (default) |
| `insert_anchor_links` | adds a clickable anchor beside every heading; `"heading"` wraps the heading text itself instead of adding a separate mark | `"left"`, `"right"`, `"heading"`, `"none"` (default) |
| `github_alerts` | `> [!NOTE]` and friends render as styled callout blockquotes | `true`, `false` (default) |
| `lazy_async_image` | adds `loading="lazy" decoding="async"` to every image | `true`, `false` (default) |
| `external_links_target_blank` | external links open in a new tab with `rel="noopener"` | `true`, `false` (default) |
| `external_links_no_follow` | adds `rel="nofollow"` to external links | `true`, `false` (default) |
| `external_links_no_referrer` | adds `rel="noreferrer"` to external links | `true`, `false` (default) |
| `external_links_class` | adds a class attribute to external links | any string, unset by default |
{% end %}

Zola already tells external links apart from internal ones — every link whose
host isn't the site's own gets `rel="external"` — so nothing above is needed
just to detect them, only to change what happens once they're detected.


### Not supported

These are common elsewhere but do nothing here — use inline HTML instead:

| Syntax | Instead use |
|---|---|
| `^superscript^` | `<sup>` |
| `~subscript~` | `<sub>` |
| `==highlight==` | `<mark>` |
| `++inserted++` | `<ins>` |
| `https://bare-url.com` | `<https://bare-url.com>` |
| `$E = mc^2$` (math) | — |
| `[[Wikilink]]` | `[text](@/path.md)` |


