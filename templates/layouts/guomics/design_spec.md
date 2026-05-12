# Guomics Lab Style Template - Design Specification

> For scientific presentations from Guomics Lab (Westlake University). Suitable for academic talks, lab meetings, conference presentations, and research reports on proteomics, metabolomics, and systems biology.

---

## I. Template Overview

| Property | Description |
|----------|-------------|
| **Template Name** | guomics |
| **Use Cases** | Academic presentations, conference talks, lab meeting reports, research seminars, proteomics/metabolomics study presentations |
| **Design Tone** | Clean, professional, scientific, accessible |
| **Theme Mode** | Light (white background, navy + orange accents) |

---

## II. Canvas Specification

| Property | Value |
|----------|-------|
| **Format** | Standard 16:9 |
| **Dimensions** | 1280 × 720 px |
| **viewBox** | `0 0 1280 720` |
| **Safe Margins** | 60px left/right, 77px top (below separator line), 40px bottom |
| **Content Area** | x: 60–1220, y: 90–680 |
| **Title Area** | y: 90–140 |

---

## III. Color Scheme

| Role | Hex | Usage |
|------|-----|-------|
| **Guomics Orange** | `#F18D00` | Corner triangle, accent lines, bullet icons, emphasis |
| **Guomics Navy** | `#004791` | Corner triangle, left accent bars, section numbers, headings |
| **Text Dark** | `#212121` | Primary body text, slide titles |
| **Text Muted** | `#666666` | Sub-bullets, captions, affiliations |
| **Background** | `#FFFFFF` | Slide background |
| **Background Alt** | `#F5F7FA` | Figure placeholders, card backgrounds |
| **Border** | `#E0E0E0` | Figure borders, dividers |

---

## IV. Typography

| Role | Font | Size | Weight |
|------|------|------|--------|
| **Closing title** ("Thanks!") | Arial Black | 80pt | 900 |
| **Main presentation title** | Arial Black | 48pt | 900 |
| **Section heading** (Summary, etc.) | Arial Black | 40pt | 900 |
| **Slide heading** (Outline, etc.) | Arial Black | 36pt | 900 |
| **Slide subtitle / section label** | Arial Black | 26pt | 900 |
| **Author name** | Arial | 24pt | 400 |
| **Body large** (key bullets) | Arial | 20pt | 400 |
| **Body standard** | Arial | 18pt | 400 |
| **Sub-body / notes** | Arial | 15–16pt | 400 |
| **Institution / affiliation** | Arial | 16pt | 400 |
| **Caption / figure label** | Arial | 11–14pt | 400 |
| **Citations, footnotes, page nums** | Arial | 11pt | 400 |

---

## V. Background System (4 Types)

The new template uses **rounded arc corners** (not triangles) and the **Westlake University official logo**. Reference the pre-built layout SVGs in this directory — they contain the exact background images extracted from `Guomics ppt_template_svg.pptx`.

| Type | File | Description | Used for |
|------|------|-------------|----------|
| **White+Arc** | `01_cover.svg`, `03_content.svg` | White bg, orange rounded arc top-left, navy arc bottom-right | Cover, content slides |
| **Navy Right Panel** | `02_toc.svg`, `02_chapter.svg` | White left 1/3, navy rounded rect right 2/3, orange accent | TOC, section separator |
| **Navy Left Panel** | `03_text_panel.svg` | Navy left 2/3, white rounded rect right 1/3, orange junction | Text+figure layout |
| **Full Navy+Orange Frame** | `04_figure_grid.svg`, `05_text_fullblue.svg` | Full-slide navy, orange rounded border frame | Figure grid, full-text |

**Westlake University logo** is embedded in the layout SVG backgrounds — do NOT add separate "Guomics" wordmark or "guomics.com" footer text. The logo placement is already defined in the template backgrounds.

> ⚠️ The layout SVGs use embedded raster backgrounds from the official PPTX template. Do not attempt to recreate the rounded arc shapes manually — use the provided layout files as visual references for the executor.

---

## VI. Slide Types

| File | Placeholders | Use case |
|------|-------------|----------|
| `01_cover.svg` | `{{TITLE}}` `{{TITLE_LINE2}}` `{{AUTHOR_NAME}}` `{{AFFILIATION_1}}` `{{AFFILIATION_2}}` `{{DATE}}` | Cover / Title |
| `02_toc.svg` | `{{SECTION_TITLE}}` `{{ITEM_1}}`–`{{ITEM_6}}` | Outline / Table of Contents |
| `02_chapter.svg` | `{{SECTION_TITLE}}` `{{ITEM_1}}`–`{{ITEM_6}}` | Section separator (same background as TOC) |
| `03_content.svg` | `{{SLIDE_TITLE}}` `{{BULLET_1}}`–`{{BULLET_4}}` + `_SUB` `{{FIGURE_CAPTION}}` `{{FIGURE_LABEL}}` `{{PAGE_NUM}}` | Content + right figure (white bg) |
| `03_text_panel.svg` | `{{SLIDE_TITLE}}` `{{BULLET_1}}`–`{{BULLET_4}}` + `_SUB` `{{FIGURE_CAPTION}}` `{{FIGURE_LABEL}}` `{{PAGE_NUM}}` | Content + right figure (navy left panel) |
| `04_figure_grid.svg` | `{{SLIDE_TITLE}}` `{{FIGURE_LABEL}}`×8 `{{PAGE_NUM}}` | Multi-figure grid (8 panels, full navy bg) |
| `05_text_fullblue.svg` | `{{SLIDE_TITLE}}` `{{BULLET_1}}`–`{{BULLET_4}}` + `_SUB` | Text-only on full navy background |
| `07_ending.svg` | `{{AUTHOR_NAME}}` `{{INSTITUTION_1}}` `{{INSTITUTION_2}}` `{{CONTACT_EMAIL}}` | Closing / Thanks slide |

---

## VII. Structural Rules

- **Westlake University logo**: Already embedded in background images — do NOT add separately
- **"guomics.com"**: Remove from executor output; `07_ending.svg` has it baked into the background
- **Orange bullet icons**: `<circle r="4" fill="#F18D00"/>` for each bullet point
- **Section numbers**: Use `#004791` bold for numbered items (01, 02, 03…)
- **Figure placeholders**: `#F5F7FA` background rect with border `#E0E0E0`
- **Page numbers**: Bottom-right, 11pt Arial, color per background (navy `#004791` on white, white `#FFFFFF` on navy)

---

## VIII. Nature Artwork Rules (Scientific Figures)

See `references/guomics_standards.md` for full guidelines. Key rules:
- Saturated focal colors → neutral backgrounds
- Label every element; max 6 panels per figure
- No red/green combinations; min 7pt text
- Top→bottom, left→right information flow
- Use `#F18D00` for focal highlights; `#004791` for structural elements

---

## IX. DO / DON'T

| DO | DON'T |
|----|-------|
| Use the provided layout SVG files as visual background reference | Redraw the rounded arc corners manually |
| Use Arial Black for all headings | Use other heavy fonts |
| Use orange bullets (`#F18D00`) for body lists | Use generic black bullets |
| Cite publications below figures (11pt, `#888888`) | Leave figures without captions |
| Keep figure captions outside the figure area | Flatten labels into images |
| Match text color to background (white on navy, dark on white) | Use same text color regardless of background |
