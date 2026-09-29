# zola-yolk 🟡

A minimal, dark, monospace Zola theme with full-text search, series, related
posts and a set of shortcodes. [Live demo](https://zola-yolk.gauthamchettiar.com).

![screenshot](/static/images/screenshots/home-dark.webp)

## Features

- Dark only, monospace (IBM Plex Mono), self-hosted fonts and icons
- Search dialog (menu item or <kbd>Ctrl</kbd>/<kbd>Cmd</kbd>+<kbd>K</kbd>)
- Date-first listings, table of contents, tags at the foot of each post
- [Series](#series) and [related posts](#related-posts)
- Every shortcode is also a template macro

Browser support: Chrome 123+, Safari 17.5+, Firefox 120+.

## Installation

```sh
cd your-zola-site
git submodule add https://github.com/gauthamchettiar/zola-yolk.git themes/zola-yolk
cp themes/zola-yolk/example_zola.toml zola.toml
cp -r themes/zola-yolk/example_content/. content/
```

Then fill in the `CHANGE ME` values in `zola.toml`. `example_content/` provides
the Posts, Series and Tags pages the menu links to.

## Configuration

See [`example_zola.toml`](example_zola.toml) for a commented config, and the
demo's [Configuration](content/posts/configuration.md) page for every option.
Options under `[extra]` in a post override the site's.

## Customizing

Colours, fonts and spacing are CSS custom properties in `sass/_tokens.scss`.
The rest of the styles: `_base.scss` (elements), `_layout.scss` (header, nav),
`_components.scss` (everything with a class).

## Series

```toml
[extra]
series = "Shortcodes"
series_part = 2   # 0 = the series' overview page
```

A post in a series gets a "Part 2 of 3 from series “Shortcodes”" line under
its date and previous / next links under it. The series name links to the
overview page, or to the series' entry on the listing page.

- Change the text with `series_label_text` (site or post) or
  `[extra.series_label_texts]` (per series); `{part}`, `{count}` and
  `{series}` are filled in.
- Turn pieces off with `series_label = false` / `series_nav = false`.
- Listing page: a section with `template = "series.html"` (see
  `content/series/_index.md`); set `series_page` if it isn't `series`.

## Related posts

Listed under each post: posts sharing its tags, most shared first. Set
`related` to a list of paths to pick them by hand, or `false` to hide them;
`related_limit` caps the count.

## Fonts

Fonts are self-hosted. Use `scripts/py-ssg-tools` to sync Google Fonts into `static/fonts/`:

```sh
cd scripts/py-ssg-tools
uv run pst sync fonts --name "IBM Plex Mono" --dest ../../static/fonts/google --weights 400,700 --subset latin
```

Then add a `[[extra.fonts]]` table (`source`, `name`, optional `preload`).

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

Each shortcode has a matching macro — inline ones in `macros/widgets.html`,
block ones in `macros/blocks.html` (taking `content` as HTML). The demo's
[Shortcodes](content/posts/shortcodes.md) posts show every one.

Colours: `white`, `red`, `orange`, `yellow`, `lime`, `green`, `cyan`, `blue`,
`purple`, `pink`, `muted`.

| Shortcode | Parameters |
|---|---|
| `elink(text, href)` | `new_tab`, `show_icon` (both `true`) |
| `mark(text)` | `color` (`yellow`), `decoration` (`highlight` \| `border`) |
| `color(text)` | `color` (`yellow`) |
| `shimmer(text)` | `type` (`text` \| `background`), `style` (`cycle` \| `wave`) |
| `quote` | `author`, `cite`, `url`, `color` (`pink`) |
| `admonition` | `title`, `icon` (`circle-info`), `color` (`yellow`) |
| `note` `warning` `danger` `info` `tip` | `title` — admonition presets |
| `expand` | `title` (`Details`), `state` (`collapsed` \| `expanded`), `style` (`simple` \| `border`) |
| `border` | `size` (`sm` `md` `lg` `xl`), `color` (`white`), `style` (`solid` `dashed` `dotted` `double`) |
| `img(src)` | `alt`, `eager`, `sizes` — sets width/height and a srcset |
| `align` | `align` (`left` \| `center` \| `right`); presets `center`, `left`, `right` |
| `wide` | `size` (`sm` `md` `lg` `xl`) |
| `row` / `col` | `gap` (`sm` `md` `lg`), `span` (width share) |
| `tabs(titles)` | `group` — one tab per fenced code block; same group switches together |
| `render` | `inline` — one ` ```mermaid ` or ` ```math ` block (needs `enable_mermaid` / `enable_math`) |
| `mobile` / `desktop` | shown below / above `48rem` |

Block shortcodes wrap their body: `{% border() %}…{% end %}`.

## License

MIT
