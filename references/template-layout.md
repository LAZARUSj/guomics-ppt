# Template Layout Reference — Guomics

Coordinate guide for placing content on each guomics template background.
All coordinates are in **1280×720 px** space (the output SVG canvas).

---

## How to use templates

The 8 guomics templates are clean SVGs (no `<mask>` / `<clipPath>` / glyph paths).
They reference flat image assets (background JPGs + corner logos) under `templates/assets/`.

When generating each output page:

1. **Start from the template** — copy the template SVG (`templates/<NN>_<name>.svg`) and
   replace `{{PLACEHOLDER}}` tokens with the actual content.
2. **Keep the asset references intact** — the `<image href="../assets/...">` lines at the top
   of each template embed the background and logos. `finalize_svg.py` will base64-embed
   them during post-processing.
3. **No pre-render step is needed** — cairosvg/PowerPoint render the templates natively.

> ⚠️ Never add `<mask>` / `<clipPath>` / `<g class>` etc. to output SVGs. See
> `shared-standards.md` § 1 for the full banned-features list.

---

## Template Types — Safe Content Zones

### `templates/01_cover.svg` — Cover slide (white + arc)

| Zone | x | y | Width | Height | Notes |
|------|---|---|-------|--------|-------|
| Orange arc (avoid) | 0–290 | 0–290 | — | — | Top-left corner |
| Navy arc (avoid) | 990–1280 | 430–720 | — | — | Bottom-right corner |
| **Title zone** | 220–1060 | 240–380 | 840 | 140 | Large title, centered |
| **Subtitle zone** | 220–1060 | 390–430 | 840 | 40 | Decorative lines, orange |
| **Author zone** | 300–980 | 420–540 | 680 | 120 | Author, affiliation, date |

**Typical SVG**:
```xml
<!-- Orange divider lines flanking title -->
<rect x="220" y="248" width="840" height="3" fill="#F18D00"/>
<text x="640" y="305" font-family="Arial Black" font-size="48"
      fill="#212121" text-anchor="middle">Main Title</text>
<text x="640" y="360" font-family="Arial Black" font-size="48"
      fill="#212121" text-anchor="middle">Title Line 2</text>
<rect x="220" y="380" width="840" height="3" fill="#F18D00"/>
<text x="640" y="428" font-family="Arial" font-size="22"
      fill="#212121" text-anchor="middle">Author Name</text>
<text x="640" y="460" font-family="Arial" font-size="16"
      fill="#666666" text-anchor="middle">Affiliation · Lab</text>
<text x="640" y="490" font-family="Arial" font-size="16"
      fill="#666666" text-anchor="middle">Date</text>
```

---

### `templates/02_chapter.svg` — Chapter divider (full navy, centered)

Centered layout on full-navy background (`chapter_bg.jpg`). All content is centered and stacked vertically:

| Zone | x | y | Width | Height | Notes |
|------|---|---|-------|--------|-------|
| **Number zone** | 440–840 | 200–270 | 400 | 70 | Large gradient number, centered |
| **Label zone** | 500–780 | 290–320 | 280 | 30 | Section label, centered |
| Orange separator | 560–720 | 332–335 | 160 | 3 | `fill="#F18D00"` |
| **Title zone** | 220–1060 | 370–470 | 840 | 100 | Chapter title + subtitle, stacked |
| Corner branding | 43–175 | 652–699 | — | — | Bottom-left, fixed |

**Typical SVG (Chapter)**:
```xml
<!-- Centered layout on chapter_bg.jpg -->
<text x="640" y="260" font-family="Arial Black" font-size="96"
      fill="url(#numGrad)" text-anchor="middle">01</text>
<text x="640" y="315" font-family="Arial Black" font-size="22"
      fill="#FFFFFF" text-anchor="middle">Part 1</text>
<rect x="560" y="332" width="160" height="3" fill="#F18D00"/>
<text x="640" y="400" font-family="Arial Black" font-size="42"
      fill="url(#titleGrad)" text-anchor="middle">Chapter Title</text>
<text x="640" y="455" font-family="Arial Black" font-size="42"
      fill="url(#titleGrad)" text-anchor="middle">Chapter Subtitle</text>
```

---

### `templates/02_toc.svg` — TOC (white left panel, navy right panel)

| Zone | x | y | Width | Height | Notes |
|------|---|---|-------|--------|-------|
| White left panel | 0–270 | 0–720 | 270 | 720 | Text: navy `#004791` |
| Transition curve | 270–330 | — | — | — | Avoid placing text here |
| **Navy right panel** | 330–1280 | 0–720 | 950 | 720 | Text: white `#FFFFFF` |
| Left content zone | 55–240 | 200–540 | 185 | 340 | Section label + line |
| Right content zone | 360–1100 | 130–620 | 740 | 490 | Numbered items (safe from branding) |
| Separator lines | 380–1100 | — | 720 | 1 | `fill-opacity="0.15"`, ends before branding |

**Typical SVG (TOC)**:
```xml
<!-- Left: section type label -->
<text x="160" y="295" font-family="Arial Black" font-size="40"
      fill="#004791" text-anchor="middle">Outline</text>
<rect x="90" y="310" width="145" height="3" fill="#F18D00"/>

<!-- Right: numbered items -->
<text x="385" y="195" font-family="Arial Black" font-size="18" fill="#F18D00">01</text>
<text x="420" y="195" font-family="Arial" font-size="18" fill="#FFFFFF">Item One</text>
<rect x="380" y="203" width="800" height="1" fill="#FFFFFF" fill-opacity="0.2"/>
<!-- Repeat for items 2–6, spacing: 85px -->
```

---

### `templates/03_content.svg` — Content + right figure (white bg)

| Zone | x | y | Width | Height | Notes |
|------|---|---|-------|--------|-------|
| **Title zone** | 60–1220 | 40–75 | 1160 | 35 | Slide title |
| Orange separator | 60–1220 | 76–79 | 1160 | 3 | `fill="#F18D00"` |
| **Left text zone** | 60–630 | 88–660 | 570 | 572 | Bullets, text |
| **Right figure zone** | 650–1215 | 88–660 | 565 | 572 | Image or placeholder |
| Page number | 1180–1215 | 695–710 | 35 | 15 | Bottom right |

**Typical bullet spacing** (4 bullets + sub-bullets, baseline y values):
| Bullet | Main y | Sub y |
|--------|--------|-------|
| 1 | 130 | 158 |
| 2 | 270 | 298 |
| 3 | 410 | 438 |
| 4 | 550 | 578 |

**Bullet element** (orange dot style):
```xml
<circle cx="68" cy="124" r="5" fill="#F18D00"/>
<text x="88" y="130" font-family="Arial" font-size="18" fill="#212121">Main bullet text</text>
<text x="98" y="158" font-family="Arial" font-size="15" fill="#666666">Sub-bullet text</text>
```

**Bullet element** (icon style — use 28×28, top y = baseline − 22):
```xml
<!-- Icon top-left y = text_baseline_y - 22 = 130 - 22 = 108 -->
<use data-icon="checkmark" x="60" y="108" width="28" height="28" fill="#004791"/>
<text x="90" y="130" font-family="Arial" font-size="18" fill="#212121">Main bullet text</text>
<text x="100" y="158" font-family="Arial" font-size="15" fill="#666666">Sub-bullet text</text>
```

| Bullet | Main baseline y | Icon top y (baseline−22) |
|--------|----------------|--------------------------|
| 1 | 130 | 108 |
| 2 | 270 | 248 |
| 3 | 410 | 388 |
| 4 | 550 | 528 |

**Figure placeholder**:
```xml
<rect x="650" y="88" width="565" height="572" fill="#F5F7FA" stroke="#E0E0E0" stroke-width="1"/>
<text x="932" y="378" font-family="Arial" font-size="14" fill="#666666" text-anchor="middle">Figure placeholder</text>
```

**Figure image** (adjust dimensions to match image ratio):
```xml
<image href="../images/FILENAME.jpg" x="650" y="88" width="565" height="572"
       preserveAspectRatio="xMidYMid meet"/>
<text x="932" y="672" font-family="Arial" font-size="11" fill="#666666" text-anchor="middle">Caption text</text>
```

---

### `templates/03_text_panel.svg` — Text + right figure (navy left 2/3, white right 1/3)

| Zone | x | y | Width | Height | Notes |
|------|---|---|-------|--------|-------|
| **Navy left panel** | 0–855 | 0–720 | 855 | 720 | Text: white `#FFFFFF` |
| Transition zone | 820–900 | — | — | — | Orange junction, avoid |
| **White right panel** | 870–1280 | 0–720 | 410 | 720 | Figures |
| Title zone | 60–800 | 40–75 | 740 | 35 | White text |
| Left bullets zone | 60–800 | 88–650 | 740 | 562 | White text, orange dots |
| Right figure zone | 875–1225 | 88–650 | 350 | 562 | Images |

**Typical SVG**:
```xml
<text x="63" y="60" font-family="Arial Black" font-size="28" fill="#FFFFFF">Slide Title</text>
<rect x="60" y="72" width="740" height="3" fill="#F18D00"/>
<!-- Bullets with white text, same structure as 03_content but fill="#FFFFFF" -->
<circle cx="68" cy="124" r="5" fill="#F18D00"/>
<text x="88" y="130" font-family="Arial" font-size="18" fill="#FFFFFF">Bullet text</text>
<text x="98" y="158" font-family="Arial" font-size="15" fill="#AACCEE">Sub-bullet</text>
<!-- Right figure -->
<image href="../images/FILENAME.jpg" x="875" y="88" width="350" height="300"
       preserveAspectRatio="xMidYMid meet"/>
```

---

### `templates/05_text_fullblue.svg` — Full-text, full navy background

| Zone | x | y | Width | Height | Notes |
|------|---|---|-------|--------|-------|
| **Title zone** | 60–1220 | 40–75 | 1160 | 35 | White text |
| Orange separator | 60–1220 | 76–79 | 1160 | 3 | `fill="#F18D00"` |
| **Content zone** | 60–1220 | 88–660 | 1160 | 572 | White text, 2-column ok |
| Page number | 1180–1215 | 695–710 | 35 | 15 | White `#FFFFFF` |

**Use the same bullet spacing as `templates/03_content.svg` but with white text.**

---

### `templates/04_figure_grid.svg` — Multi-figure grid (full navy + orange frame)

| Zone | x | y | Width | Height | Notes |
|------|---|---|-------|--------|-------|
| **Title zone** | 55–1225 | 30–65 | 1170 | 35 | White text |
| Orange frame separator | 55–1225 | 68–71 | 1170 | 3 | `fill="#F18D00"` |
| **Figure grid zone** | 55–1225 | 78–680 | 1170 | 602 | 8 panels (4×2 or 2×4) |

**8-panel grid layout** (4 columns × 2 rows):
```
Col 1: x=55,   w=275
Col 2: x=345,  w=275
Col 3: x=635,  w=275
Col 4: x=925,  w=275
Row 1: y=78,   h=280
Row 2: y=378,  h=280
Gap: 15px
```

---

### `templates/07_ending.svg` — Ending / Thanks slide

The background already contains:
- "Thanks!" in large orange text (y≈230)
- Institution logos at top (y≈20–80)
- "guomics.com" at bottom

**Only add contact information** in the center area:

| Zone | x | y | Width | Height | Notes |
|------|---|---|-------|--------|-------|
| **Author name** | center | 390–410 | — | — | Font 24–26px, white |
| **Institution** | center | 428–448 | — | — | Font 16–18px, muted |
| **Contact email** | center | 462–480 | — | — | Font 14–16px, muted |

```xml
<text x="640" y="400" font-family="Arial Black" font-size="24"
      fill="#FFFFFF" text-anchor="middle">Author / Lab Name</text>
<text x="640" y="438" font-family="Arial" font-size="17"
      fill="#AACCEE" text-anchor="middle">Institution · Department</text>
<text x="640" y="470" font-family="Arial" font-size="15"
      fill="#AACCEE" text-anchor="middle">email@domain.com</text>
```

---

## Common Mistakes

| Mistake | Effect | Fix |
|---------|--------|-----|
| Adding `<mask>` / `<clipPath>` to an output SVG | Banned features break PPTX export | Stick to `<rect>`, `<text>`, `<image>`, `<path>`, `<circle>` |
| Modifying the asset `<image href="../assets/...">` lines from the template | Background or logos disappear | Keep those lines verbatim |
| Place content in transition curve zone (toc/chapter x≈270–330) | Text overlaps the arc curve | Stay within safe zones |
| White text on white-panel slides | Invisible text | Match text color to background: dark on white, white on navy |
| Image href points to `../images/bg/` | Wrong directory (legacy bandaid path no longer exists) | Content images → `../images/`, template assets → `../assets/` |
