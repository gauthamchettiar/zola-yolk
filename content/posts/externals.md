+++
title = "Components: Externals"
date = 2026-04-18
description = "Components that lean on a bundled external library: Mermaid diagrams and KaTeX math notation."

[taxonomies]
tags = ["component", "syntax", "zola"]

[extra]
series = "Components"
series_part = 3
+++

## Render

`render` turns one fenced `mermaid` or `math` block into a diagram or formula.
Both libraries ship with the theme and load only on pages that use them.

inline
: math only — render within a sentence. Default `false`.

Needs `enable_mermaid` / `enable_math` (both on by default). With a flag off,
the block shows as plain source.

### Mermaid

{% raw %}
````md
{% <render> %}
```mermaid
graph TD
  A[Write Markdown] --> B{Component?}
  B -->|render| C[Diagram]
  B -->|none| D[Code block]
```
{% </render> %}
````
{% endraw %}

{% <render> %}
```mermaid
graph TD
  A[Write Markdown] --> B{Component?}
  B -->|render| C[Diagram]
  B -->|none| D[Code block]
```
{% </render> %}

### Math

{% raw %}
````md
{% <render> %}
```math
E = mc^2
```
{% </render> %}
````
{% endraw %}

{% <render> %}
```math
E = mc^2
```
{% </render> %}

Inline:

{% raw %}
````md
{% <render inline={true}> %}
```math
E = mc^2
```
{% </render> %}
````
{% endraw %}

Einstein's mass–energy equivalence, {% <render inline={true}> %}
```math
E = mc^2
```
{% </render> %}, sits in the middle of this sentence.
