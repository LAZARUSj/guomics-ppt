# Guomics PPT Standards

## 1. Guomics Visual Identity

### Color Palette

Extracted from `Guomics ppt_template.pptx`:

| Name | Hex | RGB | Usage |
|------|-----|-----|-------|
| Navy (primary) | `#004791` | 0, 71, 145 | Title backgrounds, key headers, borders |
| Orange/Gold (accent) | `#F18D00` | 241, 141, 0 | Highlights, callouts, emphasis text, icons |
| Near-black (text) | `#212121` | 33, 33, 33 | Body text, captions |
| White (background) | `#FFFFFF` | 255, 255, 255 | Slide background, text on dark |
| Light gray (alt bg) | `#F5F7FA` | 245, 247, 250 | Section dividers, alternate backgrounds |

**Key rule**: Navy for structure/authority → Orange for focal emphasis → White/gray for breathing room.

### Typography

All slides use two fonts only:

| Font | Weight | Usage |
|------|--------|-------|
| **Arial Black** | Heavy | Titles, section headings, closing text |
| **Arial** | Regular | Body, captions, citations, affiliations |

Font size scale (from template analysis):

| Role | Font | Size |
|------|------|------|
| Closing title ("Thanks!") | Arial Black | 80pt |
| Presentation main title | Arial Black | 48pt |
| Section title (Summary, etc.) | Arial Black | 40pt |
| Slide heading (Outline, etc.) | Arial Black | 36pt |
| Slide subtitle / section label | Arial Black | 26pt |
| Author name | Arial | 24pt |
| Body large (summary bullets) | Arial | 20pt |
| Standard body text | Arial | 18pt |
| Institution / affiliation | Arial | 16pt |
| Figure caption / label | Arial | 14pt |
| Citations, URLs, footnotes | Arial | 10–11pt |

### Slide Layout Conventions

The template defines these slide types (in order):

| Slide | Type | Key Elements |
|-------|------|-------------|
| 0 | **Title** | Large title (Arial Black 48pt), author, affiliation, website, decorative group |
| 1 | **Outline** | Section heading (Arial Black 36pt), numbered content list |
| 2–3 | **Content + Figures** | Subtitle (Arial Black 26pt), images, descriptive text |
| 4 | **Publication Gallery** | Grid of paper entries (title + citation, 10.5pt) |
| 5–7 | **Research Results** | Subtitle (26pt), figures, analytical text |
| 8 | **Summary** | Large heading (40pt), bullet points (20pt) |
| 9 | **Closing** | "Thanks!" (80pt), author info, institution, website |

**Canvas**: Always `ppt169` (1280×720 px). Never use other formats for Guomics slides.

---

## 2. Nature Artwork Guidelines

*Source: nature-artworkguide.pdf — applies to conceptual/summary figures in Guomics presentations.*

### Core Principles

#### Hierarchy
- Most important elements → most saturated colors; background elements → neutral tones
- Use `#F18D00` (orange) as the focal accent; `#004791` (navy) for structural elements
- Add depth/detail to focal areas; simplify background elements
- Maintain consistent color palette within a figure set

#### Clarity
- **Label every element** — no ambiguity, explain all in labels or legend
- Label the first instance of every object type
- Use figure parts (a, b, c…) and subheadings for structure
- Remove unnecessary elements; do not use icons for decoration only
- Do not rely solely on color for definition — add text labels where possible

#### Visual Editing
Ask before finalizing each figure:
- What are the essential elements? Can anything be removed?
- Is there unnecessary repetition or decoration?
- Can redundant steps be merged? Can multiple arrows be simplified to one?

#### Accessibility
- **No red/green combinations** — fails color blindness checks
- Minimum text size: **7pt** in draft figures; standard body text 8pt
- Use primarily **black type** rather than colored text
- Check contrast ratios; ensure adequate contrast for all text
- Use Guomics palette (tested for hierarchy and accessibility)

### Layout Rules

- **Information flow**: Top→bottom, left→right (viewers look top-left first)
- **No circular layouts** unless showing a recognized cycle (cell cycle, life cycle)
- **Max 6 panels** per full-page figure
- **Lists**: Group into ≤5 items per group; long flat lists impede comprehension
- **Brevity**: Cut all unnecessary info; overcrowded figures cause cognitive overload

### Do / Don't Quick Reference

| DO | DON'T |
|----|-------|
| Use color for grouping/relationships | Use too many colors randomly |
| Label every object at first instance | Use italic or color for emphasis (use bold) |
| Keep labels on separate layers from photos | Flatten labels into photos |
| Provide axes with units on all graphs | Reproduce publication trend graphs |
| Use bold 8pt for headings | Use excessive abbreviations |
| Ensure min 7pt text throughout | Cram too many panels into one figure |
| Use `#F18D00` for focal accent elements | Use red/green combinations |
| Keep figures focused — show process/action | Create "faux figures" (decorated tables) |

### Common Mistakes to Avoid

1. **Faux figures** — tables with decorative icons that show no process; use a real bullet list instead
2. **Overcrowded figures** — too much info in small space → cognitive overload; give images space
3. **Too many colors** — palette should reflect hierarchy, not randomness
4. **Unlabeled elements** — every shape, arrow, and object needs a label or legend entry
5. **Circular layouts without focal point** — use only for recognized cycle diagrams
6. **Flat photo labels** — keep text labels on separate SVG layer, not merged into image
