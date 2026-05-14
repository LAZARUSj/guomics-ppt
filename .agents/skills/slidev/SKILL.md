---
name: slidev
description: Work with this repository's Guomics-branded Slidev group meeting template. Use when Codex needs to edit, extend, explain, repair, preview, or export the Guomics Slidev theme/deck, including slides.md, custom layouts, Vue components, public backgrounds/logos/decorations, PPT-like page structure, image path fixes, and guidance for using this template in a new group meeting presentation.
---

# Guomics Slidev Template

This repository is a Slidev theme and example deck rebuilt from the Guomics group meeting PPT style. Treat it as a finished visual system, not a generic Slidev playground.

## First Steps

1. Inspect `slides.md` to understand the current slide sequence and slot usage.
2. Inspect the relevant `layouts/*.vue` file before changing a slide's structure.
3. Use assets from `public/` with root-relative URLs such as `/logos/guomics-color.png`; do not use `../public/...` or relative paths from `slides.md`.
4. Keep deck frontmatter aligned with the template:

```yaml
---
theme: ./
aspectRatio: 16/9
canvasWidth: 980
fonts:
  sans: Arial
  mono: Fira Code
  provider: none
---
```

## Commands

Use the package scripts already defined in `package.json`.

```bash
bun install
bun run dev -- --port 3030
bun run build
bun run export
```

Verify visual work in the browser at `http://localhost:3030/`. For layout-sensitive changes, inspect several slides at 16:9 desktop size and at least one slide containing images.

## Visual Language

- Use Arial for body text and Arial Black for major headings.
- Use Guomics orange `#F18D00` / `#ff9300` for emphasis and dark blue `#004791` / `#005091` for blue pages.
- Use white content pages with `/backgrounds/bg-1.jpg`.
- Use dark blue divider/publication/summary/thanks pages with `/backgrounds/bg-2.jpg`.
- Use the outline page with `/backgrounds/bg-3.jpg`.
- Use the split blue/orange/white figure page with `/backgrounds/bg-4.jpg`.
- Prefer the existing layouts and components over inline absolute-positioned HTML.
- Keep logos in layout components through `LogoBar`; do not paste logo images directly into slide markdown unless a one-off custom slide requires it.

## Public Resources

All runtime assets live under `public/` and are referenced from markdown/Vue as root paths.

| Folder | Purpose | Example URL |
|---|---|---|
| `public/backgrounds/` | PPT-derived page backgrounds | `/backgrounds/bg-1.jpg` |
| `public/logos/` | Color and white institute/lab logos | `/logos/westlake-university-white.png` |
| `public/decorations/` | Example scientific figures and cropped PPT images | `/decorations/predicted-pairs-venn.png` |

When adding a new image, put it in `public/decorations/` unless it is a logo or background. Use lowercase, hyphenated filenames and reference it with `/decorations/name.png`.

## Layouts

Use slide frontmatter to select one of the template layouts.

| Layout | Use For | Slots / Notes |
|---|---|---|
| `cover` | Opening title slide | Default slot; use `# Title`, `.presenter`, `.website` |
| `outline` | Agenda slide | Default slot with ordered or unordered list |
| `two-figure` | Two figures plus definitions/source text | `::left::`, `::right::`, `::body::`, `::sources::` |
| `comparison` | Two side-by-side figures plus highlight box | `::left::`, `::right::`, `::highlight::` |
| `publications` | Eight-paper/publication overview | Default slot with `PublicationCard` components |
| `data-show` | Main figure pair plus callout | `::left::`, `::right::`, `::highlight::`; optional `leftCaption` frontmatter |
| `triple-data` | One left figure and two stacked right figures | `::left::`, `::right-top::`, `::right-bottom::`, `::highlight::` |
| `full-bleed` | Blue/orange split page with right figure | Default text slot and `::figure::`; use `.text-orange` for emphasized text |
| `summary` | Final key points | Default slot; use `## Summary` and a short bullet list |
| `thanks` | Closing page | Default slot; use `# Thanks!`, `.presenter`, `.website` |

Example content slide:

```md
---
layout: comparison
title: CCprofiler Comparison
subtitle: Write here your subtitle
---

::left::

![Complexes](/decorations/complexes-ccprofiler.png)

Complexes identified from CCprofiler

::right::

![Interactions](/decorations/interactions-ccprofiler.png)

Interactions identified from CCprofiler

::highlight::

Complex sizes were balanced across reference databases.
```

Example data slide:

```md
---
layout: data-show
title: Predicted Protein Pairs
subtitle: Write here your subtitle
leftCaption: "Predicted protein pairs (FDR<20%)"
---

::left::

![Predicted protein pairs](/decorations/predicted-pairs-venn.png)

::right::

![GO pathway analysis](/decorations/photo-portrait-2.png)

::highlight::

FTC238 identified the greatest number of protein interactions.
```

## Components

The components are globally available in Slidev markdown.

### `LogoBar`

Render template logos with the correct color, grouping, and position.

```vue
<LogoBar variant="color" set="pair" position="top-right" size="content" />
<LogoBar variant="white" set="full" position="top-center" size="thanks" />
```

Props:

| Prop | Values | Notes |
|---|---|---|
| `variant` | `color`, `white` | Use color logos on white pages and white logos on blue pages |
| `set` | `full`, `pair` | `full` = four logos; `pair` = Westlake University + Westlake Laboratory |
| `position` | `top-center`, `top-right`, `bottom-left`, `bottom-right` | Absolute positions tuned to PPT layout |
| `size` | `cover`, `content`, `footer`, `thanks` | Use `content` for normal white slides |
| `logos` | array of paths | Optional custom logo override |

### `SubtitleBar`

Render the PPT-style slide heading area.

```vue
<SubtitleBar>Write here your subtitle</SubtitleBar>
<SubtitleBar dark :rule="false">Publications</SubtitleBar>
```

Use `dark` on blue pages. Set `:rule="false"` when the heading should not have the horizontal line.

### `HighlightBar`

Render the pale-blue callout block used near the bottom of data/comparison slides.

```vue
<HighlightBar align="left">
  <p>Key result goes here.</p>
</HighlightBar>
```

Props: `color`, `textColor`, `align`. Most slides should use the defaults.

### `PublicationCard`

Render one publication tile in the publications grid.

```vue
<PublicationCard
  image="/decorations/photo-square-2.png"
  caption="Protein restriction reprograms the multi-organ proteomic landscape..."
/>
```

Use this only inside the `publications` layout unless adding a deliberate custom publication grid.

### `SlideNumber`

Render the current Slidev page number.

```vue
<SlideNumber />
<SlideNumber color="#000000" position="bottom-left" />
```

Most layout components already include it where needed.

### `CornerMarkers`

Legacy utility for small corner markers. Prefer background images and existing layouts for normal template work.

## Creating Your Own Group Meeting Deck

1. Copy this repository or start from its `slides.md`.
2. Replace the cover title, presenter, institution lines, and website.
3. Keep the first frontmatter block and choose existing layouts for new slides.
4. Put new figures under `public/decorations/`.
5. Reference images with root paths like `/decorations/my-figure.png`.
6. Run `bun run dev -- --port 3030` and review the slides visually.
7. Run `bun run build` before sharing or exporting.

When a figure is missing, check filename case, folder location, and whether the markdown path starts with `/`.

## Editing Rules

- Preserve user content in `slides.md`; adjust layout components only when the template cannot support the needed slide type.
- Keep geometry changes scoped to the relevant layout component.
- Avoid global CSS overrides unless they are truly shared across all slides.
- Avoid adding new brand colors or decorative systems; extend the PPT-derived visual language.
- If adding a new layout, name it by purpose, document its slots here, and include the correct background/logo/slide-number pattern.

## Generic Slidev References

This skill keeps the upstream Slidev reference files in `references/`. Load them only when needed for core syntax, animation, export, hosting, code highlighting, diagrams, or other generic Slidev behavior.
