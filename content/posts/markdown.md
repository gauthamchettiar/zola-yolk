+++
title = "Markdown Showcase"
date = 2026-04-22
description = "A sample post covering common Markdown elements."

[taxonomies]
tags = ["markdown", "sample", "zola"]
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

 

## Text Formatting

| Syntax | Rendering |
|---|---|
| `**bold**` | **bold** |
| `*italic*` | *italic* |
| `` `code` `` | `code` |
| `~~strikethrough~~` | ~~strikethrough~~ |
| `<ins>inserted</ins>` | <ins>inserted</ins> |
| `<mark>highlight</mark>` | <mark>highlight</mark> |
| `<sub>sub</sub>script` | <sub>sub</sub>script |
| `<sup>super</sup>script` | <sup>super</sup>script |

> `++inserted++`, `==mark==`, `~sub~`, `^sup^` are **not** supported by Zola's renderer — use inline HTML instead (shown above).

 

## Paragraphs and Line Breaks

Leaving a blank line creates a new paragraph.

Two trailing spaces at the end of a line  
creates a line break without a new paragraph.

 

## Lists

### Unordered

```
- First item
- Second item
  - Nested item
```

- First item
- Second item
  - Nested item

### Ordered

```
1. Step one
2. Step two
   1. Nested step
```

1. Step one
2. Step two
   1. Nested step

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

 

## Images

Plain image — `![alt text](path/to/image.jpg)`:

![An ant on a plumeria flower](/images/ant_on_a_flower.jpg)




 

