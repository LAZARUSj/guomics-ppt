# Executor Common Guidelines

> Style-specific content is in the corresponding `executor-{style}.md`. Technical constraints are in shared-standards.md.

---

## 1. Template Adherence Rules

If template files exist in the project's `templates/` directory, the template structure must be followed:

| Page Type | Template SVG | Adherence Rules |
|-----------|--------------|-----------------|
| Cover | `templates/01_cover.svg` | Place title, author, date in center safe zone |
| TOC | `templates/02_toc.svg` | Section label left panel, items right navy panel |
| Chapter | `templates/02_chapter.svg` | Centered layout: number, label, separator, title stacked vertically |
| Content | `templates/03_content.svg` | Title bar at top, bullets left 50%, figure right 50% |
| Text+Figure | `templates/03_text_panel.svg` | Bullets on navy left 2/3, figure on white right 1/3 |
| Figure Grid | `templates/04_figure_grid.svg` | Multi-panel grid inside orange frame |
| Full Navy Text | `templates/05_text_fullblue.svg` | Title + bullets in white text on navy |
| Ending | `templates/07_ending.svg` | Contact info only; "Thanks!" and logos are in background |

**How to use a template**: copy the template SVG to `svg_output/`, then replace each
`{{PLACEHOLDER}}` token with the real content. The `<image href="../assets/...">` lines
at the top of each template embed the background and corner logos — keep those verbatim.

**Background reference syntax** (already present in each template — do NOT re-add):
```xml
<image href="../assets/cover_bg.jpg" x="0" y="0"
       width="1280" height="720" preserveAspectRatio="none"/>
```

**Layout coordinates**: See `references/template-layout.md` for exact safe zones, bullet spacing,
and copy-paste SVG snippets for each template type.

### Page-Template Mapping Declaration (Required Output)

Before generating each page, you must explicitly output which template (or "free design") is used:

```
📝 **Template mapping**: `templates/01_cover.svg` (or "None (free design)")
🎯 **Adherence rules / layout strategy**: [specific description]
```

- **Content pages**: Templates only define header and footer; the content area is freely laid out by the Executor
- **No template**: Generate entirely per the Design Specification & Content Outline

---

## 2. Design Parameter Confirmation (Mandatory Step)

> Before generating the first SVG page, you **must review the key design parameters from the Design Specification & Content Outline** to ensure all subsequent generation strictly follows the spec.

Must output confirmation including: canvas dimensions, body font size, color scheme (primary/secondary/accent HEX values), font plan.

**Why is this step mandatory?** Prevents the "spec says one thing, execution does another" disconnect.

---

## 3. Execution Guidelines

- **Absolute spec adherence**: Strictly follow the color, layout, canvas format, and typography parameters in the spec
- **Follow template structure**: If templates exist, inherit the template's visual framework
- **Phased batch generation** (recommended):
  1. **Visual Construction Phase**: Generate all SVG pages continuously, ensuring high consistency in design style and layout coordinates (Visual Consistency)
  2. **Logic Construction Phase**: After all SVGs are finalized, batch-generate speaker notes to ensure narrative coherence (Narrative Continuity)
- **Technical specifications**: See [shared-standards.md](shared-standards.md) for SVG technical constraints and PPT compatibility rules

### SVG File Naming Convention

File naming format: `<number>_<page_name>.svg`

- **Chinese content** → Chinese naming: `01_封面.svg`, `02_目录.svg`, `03_核心优势.svg`
- **English content** → English naming: `01_cover.svg`, `02_agenda.svg`, `03_key_benefits.svg`
- **Number rules**: Two-digit numbers, starting from 01
- **Page name**: Concise and descriptive, matching the page title in the Design Specification & Content Outline

---

## 4. Icon Usage

Four approaches: **A: Emoji** (`<text>🚀</text>`) | **B: AI-generated** (SVG basic shapes) | **C: Built-in library** (`templates/icons/` 640+ icons, recommended) | **D: Custom** (user-specified)

**Built-in icons — Placeholder method (recommended)**:

```xml
<use data-icon="chart-bar" x="100" y="200" width="48" height="48" fill="#005587"/>
```

> No need to manually run `embed_icons.py`; `finalize_svg.py` post-processing tool will auto-embed icons.

**Icon sizing guidelines** (for 1280×720 canvas, 18px body text):

| Use case | Recommended size | Notes |
|----------|-----------------|-------|
| Bullet-point icon (replaces dot) | `width="28" height="28"` | Top-left y = text_baseline − 22 |
| Section decoration | `width="36" height="36"` | |
| Large feature icon | `width="48" height="48"` | |

> ⚠️ Icon paths do not always fill their full viewBox — the rendered size may be smaller than declared. Use at least 28px for bullet icons to ensure legibility.

**Common icons**: `chart-bar` `arrow-trend-up` `users` `cog` `circle-checkmark` `target` `clock` `file` `dollar` `lightbulb`

> ⚠️ **Icon validation rule**: If the Design Specification includes an icon inventory list, Executor may **only** use icons from that approved list. Using icon names not in the index is FORBIDDEN — verify against `templates/icons/icons_index.json` if uncertain.

Full index: `templates/icons/README.md`

---

## 5. Chart Reference

When the Design Spec includes a **VII. Chart Reference List**, read the referenced SVG templates from `templates/charts/` to understand common chart patterns.

**Adaptation rules**:
- **Must preserve**: Chart type (bar/line/pie etc.) as specified in the Design Spec
- **Must adapt**: Data values, labels, colors (match the project's color scheme), and dimensions to fit the page layout
- **May adjust**: Axis ranges, grid lines, legend position, spacing — as long as the chart remains accurate and readable
- **Must NOT**: Change chart type without Design Spec justification, or remove data points specified in the outline

> Chart templates: `templates/charts/` (33 types). Index: `templates/charts/charts_index.json`

---

## 5b. Conceptual Diagram Generation (示意图)

> Content pages (03_content, 03_text_panel, 05_text_fullblue, 04_figure_grid) only fix the
> header and footer; the **content area is free for the Executor to construct**. Use the
> patterns below to build conceptual diagrams, flow charts, process illustrations, and
> logical relationship maps directly with raw SVG shapes.

### Pattern 1: Horizontal Process Flow

```
[Step 1] ──→ [Step 2] ──→ [Step 3] ──→ [Step 4] ──→ [Result]
```

**For 03_content (white bg) / 05_text_fullblue (navy bg) — full-width flow:**

```xml
<!-- Step nodes: rounded rects connected by arrows -->
<rect x="60" y="350" width="240" height="80" rx="6" fill="#004791" fill-opacity="0.08" stroke="#004791" stroke-width="1.5"/>
<text x="180" y="385" font-family="Arial Black" font-size="16" fill="#004791" text-anchor="middle">Step 1</text>
<text x="180" y="408" font-family="Arial" font-size="13" fill="#666666" text-anchor="middle">Description</text>

<!-- Arrow connector (orange) -->
<line x1="300" y1="390" x2="350" y2="390" stroke="#F18D00" stroke-width="2"/>
<polygon points="350,385 360,390 350,395" fill="#F18D00"/>

<!-- Repeat for steps 2-4, spacing 300px each -->
```

**Navy-bg variant**: card fill `#003566` fill-opacity `0.5`, stroke `#1A5A8A`, text `#FFFFFF`.

### Pattern 2: MECE Decomposition Tree

```
Main Concept ──┬── Branch A (key driver)
               ├── Branch B (key driver)
               ├── Branch C (key driver)
               └── Branch D (key driver)
```

```xml
<!-- Trunk node (left, emphasized) -->
<rect x="60" y="280" width="280" height="90" rx="8" fill="#004791"/>
<text x="200" y="318" font-family="Arial Black" font-size="20" fill="#FFFFFF" text-anchor="middle">Core Concept</text>
<text x="200" y="342" font-family="Arial" font-size="14" fill="#AACCEE" text-anchor="middle">Main trunk</text>

<!-- Branch lines from right edge of trunk -->
<line x1="340" y1="290" x2="420" y2="180" stroke="#F18D00" stroke-width="2"/>
<line x1="340" y1="310" x2="420" y2="285" stroke="#F18D00" stroke-width="2"/>
<line x1="340" y1="330" x2="420" y2="390" stroke="#F18D00" stroke-width="2"/>
<line x1="340" y1="350" x2="420" y2="495" stroke="#F18D00" stroke-width="2"/>

<!-- Branch nodes -->
<rect x="420" y="145" width="320" height="55" rx="6" fill="#F8FAFC" stroke="#E0E4E8" stroke-width="1"/>
<text x="580" y="178" font-family="Arial Black" font-size="16" fill="#212121" text-anchor="middle">Branch A</text>

<!-- Repeat for branches B-D, y spacing ~105px -->
```

**Navy-bg variant**: Branch nodes use `fill="#003566" fill-opacity="0.6" stroke="#1A5A8A"`, text `#FFFFFF`.

### Pattern 3: Center-Radiating (Ecosystem / Core Concept)

```
         [Node 2]
            │
    [Node 1]──★──[Node 3]
            │
         [Node 4]
```

```xml
<!-- Center node -->
<circle cx="400" cy="380" r="60" fill="#004791"/>
<text x="400" y="375" font-family="Arial Black" font-size="16" fill="#FFFFFF" text-anchor="middle">Core</text>
<text x="400" y="395" font-family="Arial" font-size="12" fill="#AACCEE" text-anchor="middle">Platform</text>

<!-- Satellite nodes at 0°, 90°, 180°, 270° (or 45° offsets for 6 nodes) -->
<circle cx="400" cy="200" r="45" fill="#FFFFFF" stroke="#F18D00" stroke-width="2"/>
<text x="400" y="205" font-family="Arial Black" font-size="14" fill="#212121" text-anchor="middle">Node A</text>
<!-- Connecting line -->
<line x1="400" y1="320" x2="400" y2="245" stroke="#F18D00" stroke-width="1.5" stroke-dasharray="6,3"/>

<!-- For 6-node: use angles 30°, 90°, 150°, 210°, 270°, 330° -->
```

### Pattern 4: Comparison / Parallel Columns

```
┌──────────┐  ┌──────────┐  ┌──────────┐
│  Item A  │  │  Item B  │  │  Item C  │
│  · pt 1  │  │  · pt 1  │  │  · pt 1  │
│  · pt 2  │  │  · pt 2  │  │  · pt 2  │
└──────────┘  └──────────┘  └──────────┘
```

For 03_content (3-column, 370px each, gap 25px):
```xml
<rect x="60" y="120" width="370" height="480" rx="8" fill="#F8FAFC" stroke="#E0E4E8" stroke-width="1"/>
<rect x="60" y="120" width="370" height="4" fill="#F18D00" rx="2"/>
<text x="245" y="170" font-family="Arial Black" font-size="20" fill="#004791" text-anchor="middle">Item A</text>
<!-- Bullets inside card -->
<circle cx="90" cy="220" r="4" fill="#F18D00"/>
<text x="105" y="226" font-family="Arial" font-size="15" fill="#212121">Point 1</text>
```

### Pattern 5: Vertical Timeline / Cascade

```
2020 ── Milestone A ─────────────────
          2022 ── Milestone B ─────────
                    2024 ── Milestone C
```

```xml
<!-- Vertical spine -->
<line x1="200" y1="120" x2="200" y2="600" stroke="#004791" stroke-opacity="0.2" stroke-width="2"/>

<!-- Timeline nodes (alternate left/right) -->
<circle cx="200" cy="160" r="8" fill="#F18D00"/>
<text x="160" y="148" font-family="Arial Black" font-size="14" fill="#F18D00" text-anchor="end">2020</text>
<rect x="240" y="135" width="450" height="50" rx="6" fill="#F0F4F8"/>
<text x="260" y="166" font-family="Arial" font-size="16" fill="#212121">Milestone A description</text>
```

### Pattern 6: Layer Stack (Architecture / Framework)

```
┌─────────────────────────────────────┐
│           Application Layer         │
├─────────────────────────────────────┤
│           Platform Layer            │
├─────────────────────────────────────┤
│         Infrastructure Layer        │
└─────────────────────────────────────┘
```

```xml
<rect x="100" y="200" width="700" height="70" rx="4" fill="#004791" fill-opacity="0.12" stroke="#004791" stroke-width="1"/>
<text x="130" y="242" font-family="Arial Black" font-size="16" fill="#004791">Application Layer</text>
<text x="750" y="242" font-family="Arial" font-size="12" fill="#666666" text-anchor="end">User-facing</text>

<rect x="100" y="280" width="700" height="70" rx="4" fill="#F18D00" fill-opacity="0.08" stroke="#F18D00" stroke-width="1"/>
<text x="130" y="322" font-family="Arial Black" font-size="16" fill="#004791">Platform Layer</text>

<rect x="100" y="360" width="700" height="70" rx="4" fill="#004791" fill-opacity="0.06" stroke="#004791" stroke-width="0.5"/>
<text x="130" y="402" font-family="Arial Black" font-size="16" fill="#004791">Infrastructure Layer</text>
```

### Diagram Construction Rules

| Rule | Detail |
|------|--------|
| **Color discipline** | Structure lines → navy `#004791` (opacity 0.2–0.5); emphasis/highlights → orange `#F18D00`; node backgrounds → navy tints or `#F8FAFC` |
| **Line hierarchy** | Primary connections: 2–2.5px solid; secondary: 1–1.5px dashed; decorative: 0.5–1px |
| **Node shapes** | Core/trunk → filled navy `#004791`; branches → white or light fill + border; emphasis → orange accent |
| **Text in nodes** | Title: Arial Black 14–20px; description: Arial 12–14px; navy-bg nodes → white text; white-bg nodes → dark text |
| **Spacing** | Min 40px between connected nodes; min 20px between parallel nodes; text padding inside rects: 20–30px |
| **Within templates** | Template defines header (title + orange separator) and footer; diagram occupies the content zone below the separator |
| **Avoid** | Complex arrow paths with many bends; overlapping lines; more than 3 levels of hierarchy in one diagram |

---

## 6. Image Handling

Handle images based on their status in the Design Specification's "Image Resource List":

| Status | Source | Handling |
|--------|--------|----------|
| **Existing** | User-provided | Reference images directly from `../images/` directory |
| **AI-generated** | Generated by Image_Generator | Images already in `../images/`, reference directly |
| **Placeholder** | Not yet prepared | Use dashed border placeholder |

**Reference**: `<image href="../images/xxx.png" ... preserveAspectRatio="xMidYMid slice"/>`

**Placeholder**: Dashed border `<rect stroke-dasharray="8,4" .../>` + description text

---

## 7. Font Usage

Apply corresponding fonts for different text roles based on the font plan in the Design Specification & Content Outline:

| Role | Chinese Recommended | English Recommended |
|------|--------------------|--------------------|
| Title font | Microsoft YaHei / KaiTi / SimHei | Arial / Georgia |
| Body font | Microsoft YaHei / SimSun | Calibri / Times |
| Emphasis font | SimHei | Arial Black / Consolas |
| Annotation font | Microsoft YaHei / SimSun | Arial / Times |

See `references/design-guidelines.md` for details.

---

## 8. Speaker Notes Generation Framework

### Task 1. Generate Complete Speaker Notes Document

After **all SVG pages are generated and finalized**, enter the "Logic Construction Phase" and generate the complete speaker notes document in `notes/total.md`.

**Why not generate page-by-page?** Batch-writing notes allows planning transitions like a script, ensuring coherent presentation logic.

**Format**: Each page starts with `# <number>_<page_title>`, separated by `---` between pages. Each page includes: script text (2-5 sentences), `Key points: ① ② ③`, `Duration: X minutes`. Except for the first page, each page's text starts with a `[Transition]` phrase.

**Basic stage direction markers** (common to all styles):

| Marker | Purpose |
|--------|---------|
| `[Pause]` | Whitespace after key content, letting the audience absorb |
| `[Transition]` | Standalone paragraph at the start of each page's text, bridging from the previous page |

> Each style may extend with additional markers (`[Interactive]`/`[Data]`/`[Scan Room]`/`[Benchmark]` etc.), see `executor-{style}.md`.

**Requirements**:

- Notes should be conversational and flow naturally
- Highlight each page's core information and presentation key points
- Users can manually edit and override in the `notes/` directory

### Task 2. Split Into Per-Page Note Files

Automatically split `notes/total.md` into individual speaker note files in the `notes/` directory.

**File naming convention**:

- **Recommended**: Match SVG names (e.g., `01_cover.svg` → `notes/01_cover.md`)
- **Compatible**: Also supports `slide01.md` format (backward compatibility)

---

## 9. Next Steps After Completion

> **Auto-continuation**: After Visual Construction Phase (all SVG pages) and Logic Construction Phase (all notes) are complete, the Executor proceeds directly to the post-processing pipeline.

**Post-processing & Export** (see [shared-standards.md](shared-standards.md)):

```bash
# 1. Split speaker notes
python3 scripts/total_md_split.py <project_path>

# 2. SVG post-processing (auto-embed icons, images, etc.)
python3 scripts/finalize_svg.py <project_path>

# 3. Export PPTX
python3 scripts/svg_to_pptx.py <project_path> -s final
# Default: generates native shapes (.pptx) + SVG reference (_svg.pptx)
```
