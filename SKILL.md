---
name: guomics-ppt
description: >
  Guomics-branded SVG→PPTX presentation generation system. Extends ppt-master with
  Guomics visual identity and Nature artwork standards. Use when user asks to "create
  guomics ppt", "guomics slides", "guomics演示", "做guomics PPT", "制作guomics幻灯片",
  "guomics presentation", or any PPT request in the context of Guomics lab work.
---

# Guomics PPT Skill

> Guomics-branded SVG→PPTX pipeline. Built on ppt-master with Guomics visual identity (navy/orange/white) and Nature artwork principles for scientific presentations.

**Core Pipeline**: `Source Document → Create Project → Template Option → Strategist → [Image_Generator] → Executor → Post-processing → Export`

## Guomics Branding (Always Apply)

> [!IMPORTANT]
> All Guomics presentations MUST follow these overrides regardless of user request:

**Canvas**: Always use `ppt169` (1280×720) — matches Guomics template aspect ratio.

**Color Scheme** (`guomics` in config):
| Role | Hex | Usage |
|------|-----|-------|
| Primary (navy) | `#004791` | Title backgrounds, key headers |
| Accent (orange) | `#F18D00` | Highlights, callouts, emphasis |
| Text dark | `#212121` | Body text |
| Background | `#FFFFFF` | Slide backgrounds |
| Text light | `#FFFFFF` | Text on dark backgrounds |

**Typography**:
| Role | Font | Size |
|------|------|------|
| Title large | Arial Black | 80pt |
| Presentation title | Arial Black | 48pt |
| Section heading | Arial Black | 36–40pt |
| Slide subtitle | Arial Black | 26pt |
| Author/name | Arial | 24pt |
| Body | Arial | 18–20pt |
| Caption | Arial | 14pt |
| Citation/small | Arial | 10–11pt |
| Institution | Arial | 16pt |

**Template reference**: `/home/lazarus/westlake/guomics_ppt/Guomics ppt_template_svg.pptx`

**Nature artwork rules** (see `references/guomics_standards.md`):
- Saturated focal colors → neutral backgrounds (hierarchy)
- Label every element; no ambiguity (clarity)
- No red/green combos; min 7pt text; black type preferred (accessibility)
- Top→bottom, left→right information flow; max 6 panels per figure

---

> [!CAUTION]
> ## 🚨 Global Execution Discipline (MANDATORY)
>
> **This workflow is a strict serial pipeline. The following rules have the highest priority — violating any one of them constitutes execution failure:**
>
> 1. **SERIAL EXECUTION** — Steps MUST be executed in order; the output of each step is the input for the next. Non-BLOCKING adjacent steps may proceed continuously once prerequisites are met, without waiting for the user to say "continue"
> 2. **BLOCKING = HARD STOP** — Steps marked ⛔ BLOCKING require a full stop; the AI MUST wait for an explicit user response before proceeding and MUST NOT make any decisions on behalf of the user
> 3. **NO CROSS-PHASE BUNDLING** — Cross-phase bundling is FORBIDDEN. (Note: the Eight Confirmations in Step 4 are ⛔ BLOCKING — the AI MUST present recommendations and wait for explicit user confirmation before proceeding. Once the user confirms, all subsequent non-BLOCKING steps — design spec output, SVG generation, speaker notes, and post-processing — may proceed automatically without further user confirmation)
> 4. **GATE BEFORE ENTRY** — Each Step has prerequisites (🚧 GATE) listed at the top; these MUST be verified before starting that Step
> 5. **NO SPECULATIVE EXECUTION** — "Pre-preparing" content for subsequent Steps is FORBIDDEN (e.g., writing SVG code during the Strategist phase)

> [!IMPORTANT]
> ## 🌐 Language & Communication Rule
>
> - **Response language**: Always match the language of the user's input and provided source materials. For example, if the user asks in Chinese, respond in Chinese; if the source material is in English, respond in English.
> - **Explicit override**: If the user explicitly requests a specific language (e.g., "请用英文回答" or "Reply in Chinese"), use that language instead.
> - **Template format**: The `design_spec.md` file MUST always follow its original English template structure (section headings, field names), regardless of the conversation language. Content values within the template may be in the user's language.

## Main Pipeline Scripts

| Script | Purpose |
|--------|---------|
| `${SKILL_DIR}/scripts/pdf_to_md.py` | PDF to Markdown |
| `${SKILL_DIR}/scripts/doc_to_md.py` | Documents to Markdown via Pandoc (DOCX, EPUB, HTML, LaTeX, RST, etc.) |
| `${SKILL_DIR}/scripts/web_to_md.py` | Web page to Markdown |
| `${SKILL_DIR}/scripts/web_to_md.cjs` | WeChat / high-security sites to Markdown |
| `${SKILL_DIR}/scripts/project_manager.py` | Project init / validate / manage |
| `${SKILL_DIR}/scripts/analyze_images.py` | Image analysis |
| `${SKILL_DIR}/scripts/nano_banana_gen.py` | AI image generation (Gemini API) |
| `${SKILL_DIR}/scripts/svg_quality_checker.py` | SVG quality check |
| `${SKILL_DIR}/scripts/total_md_split.py` | Speaker notes splitting |
| `${SKILL_DIR}/scripts/finalize_svg.py` | SVG post-processing (unified entry) |
| `${SKILL_DIR}/scripts/svg_to_pptx.py` | Export to PPTX |

For complete tool documentation, see `${SKILL_DIR}/scripts/README.md`.

## Template Index

| Index | Path | Purpose |
|-------|------|---------|
| Layout templates | `${SKILL_DIR}/templates/layouts/layouts_index.json` | Query available page layout templates |
| Chart templates | `${SKILL_DIR}/templates/charts/charts_index.json` | Query available chart SVG templates |
| Icon library | `${SKILL_DIR}/templates/icons/icons_index.json` | Query available icon names and categories |

## Standalone Workflows

| Workflow | Path | Purpose |
|----------|------|---------|
| `create-template` | `workflows/create-template.md` | Standalone template creation workflow |

---

## Workflow

### Step 1: Source Content Processing

🚧 **GATE**: User has provided source material (PDF / DOCX / EPUB / URL / Markdown file / text description / conversation content — any form is acceptable).

When the user provides non-Markdown content, convert immediately:

| User Provides | Command |
|---------------|---------|
| PDF file | `python3 ${SKILL_DIR}/scripts/pdf_to_md.py <file>` |
| DOCX / Word / Office document | `python3 ${SKILL_DIR}/scripts/doc_to_md.py <file>` |
| EPUB / HTML / LaTeX / RST / other | `python3 ${SKILL_DIR}/scripts/doc_to_md.py <file>` |
| Web link | `python3 ${SKILL_DIR}/scripts/web_to_md.py <URL>` |
| WeChat / high-security site | `node ${SKILL_DIR}/scripts/web_to_md.cjs <URL>` |
| Markdown | Read directly |

**✅ Checkpoint — Confirm source content is ready, proceed to Step 2.**

---

### Step 2: Project Initialization

🚧 **GATE**: Step 1 complete; source content is ready (Markdown file, user-provided text, or requirements described in conversation are all valid).

```bash
python3 ${SKILL_DIR}/scripts/project_manager.py init <project_name> --format <format>
```

Format options: `ppt169` (default), `ppt43`, `xhs`, `story`, etc. For the full format list, see `references/canvas-formats.md`.

Import source content (choose based on the situation):

| Situation | Action |
|-----------|--------|
| Has source files (PDF/MD/etc.) | `python3 ${SKILL_DIR}/scripts/project_manager.py import-sources <project_path> <source_files...> --move` |
| User provided text directly in conversation | No import needed — content is already in conversation context; subsequent steps can reference it directly |

> ⚠️ **MUST use `--move`**: All source files (original PDF / MD / images) MUST be **moved** (not copied) into `sources/` for archiving.
> - Markdown files generated in Step 1, original PDFs, original MDs — **all** must be moved into the project via `import-sources --move`
> - Intermediate artifacts (e.g., `_files/` directories) are handled automatically by `import-sources`
> - After execution, source files no longer exist at their original location

**✅ Checkpoint — Confirm project structure created successfully, `sources/` contains all source files, converted materials are ready. Proceed to Step 3.**

---

### Step 3: Template Selection

🚧 **GATE**: Step 2 complete; project directory structure is ready.

⛔ **BLOCKING**: If the user has not yet clearly expressed whether to use a template, you MUST present options and **wait for an explicit user response** before proceeding. If the user has previously stated "no template" or specified a particular template, skip this prompt and proceed directly.

**⚡ Early-exit**: If the user has already stated "no template" / "不使用模板" / "自由设计" (or equivalent) at any prior point in the conversation, **do NOT query `layouts_index.json`** — skip directly to Step 4. This avoids unnecessary token consumption.

**Template recommendation flow** (only when the user has NOT yet decided):
Query `${SKILL_DIR}/templates/layouts/layouts_index.json` to list available templates and their style descriptions.
**When presenting options, you MUST provide a professional recommendation based on the current PPT topic and content** (recommend a specific template or free design, with reasoning), then ask the user:

> 💡 **AI Recommendation**: Based on your content topic (brief summary), I recommend **[specific template / free design]** because...
>
> Which approach would you prefer?
> **A) Use an existing template** (please specify template name or style preference)
> **B) No template** — free design

After the user confirms option A, copy template files and generate clean backgrounds:
```bash
cp ${SKILL_DIR}/templates/layouts/<template_name>/*.svg <project_path>/templates/
cp ${SKILL_DIR}/templates/layouts/<template_name>/design_spec.md <project_path>/templates/
# Copy the assets/ directory (background JPGs + corner logos) to the PROJECT ROOT
# (parallel to templates/, svg_output/, images/) so both template and output SVGs
# can resolve "../assets/<file>" relative paths.
cp -r ${SKILL_DIR}/templates/layouts/<template_name>/assets <project_path>/assets
```

The templates reference assets via relative paths (`<image href="../assets/cover_bg.jpg"/>`),
which `finalize_svg.py` will base64-embed during post-processing. No pre-rendering step is needed.

After the user confirms option B, proceed directly to Step 4.

> To create a new template, Read `references/template-designer.md`

**✅ Checkpoint — User has responded with template selection, template files copied (if option A). Proceed to Step 4.**

---

### Step 4: Strategist Phase (MANDATORY — cannot be skipped)

🚧 **GATE**: Step 3 complete; user has confirmed template selection.

First, read the role definitions:
```
Read references/strategist.md
Read references/shared-standards.md
```

**Must complete the Eight Confirmations** (refer to `templates/design_spec_reference.md` for the template structure):

⛔ **BLOCKING**: The Eight Confirmations MUST be presented to the user as a bundled set of recommendations, and you MUST **wait for the user to confirm or modify** before outputting the Design Specification & Content Outline. This is one of only two core confirmation points in the workflow (the other is template selection). Once confirmed, all subsequent script execution and slide generation should proceed fully automatically.

1. Canvas format
2. Page count range
3. Target audience
4. Style objective
5. Color scheme
6. Icon usage approach
7. Typography plan
8. Image usage approach

If the user has provided images, run the analysis script **before outputting the design spec** (do NOT directly read/open image files — use the script output only):
```bash
python3 ${SKILL_DIR}/scripts/analyze_images.py <project_path>/images
```

> ⚠️ **Image handling rule**: The AI must NEVER directly read, open, or view image files (`.jpg`, `.png`, etc.). All image information must come from the `analyze_images.py` script output or the Design Specification's Image Resource List.

**Output**: `<project_path>/design_spec.md`

**✅ Checkpoint — Phase deliverables complete, auto-proceed to next step**:
```markdown
## ✅ Strategist Phase Complete
- [x] Eight Confirmations completed (user confirmed)
- [x] Design Specification & Content Outline generated
- [ ] **Next**: Auto-proceed to [Image_Generator / Executor] phase
```

---

### Step 5: Image_Generator Phase (Conditional)

🚧 **GATE**: Step 4 complete; Design Specification & Content Outline generated and user confirmed.

> **Trigger condition**: Image approach includes "AI generation". If not triggered, skip directly to Step 6 (Step 6 GATE must still be satisfied).

Read `references/image-generator.md`

1. Extract all images with status "pending generation" from the design spec
2. Generate prompt document → `<project_path>/images/image_prompts.md`
3. Generate images (CLI tool recommended):
   ```bash
   python3 ${SKILL_DIR}/scripts/nano_banana_gen.py "prompt" --aspect_ratio 16:9 --image_size 1K -o <project_path>/images
   ```

**✅ Checkpoint — Confirm all images are ready, proceed to Step 6**:
```markdown
## ✅ Image_Generator Phase Complete
- [x] Prompt document created
- [x] All images saved to images/
```

---

### Step 6: Executor Phase

🚧 **GATE**: Step 4 (and Step 5 if triggered) complete; all prerequisite deliverables are ready.

Read the role definition based on the selected style:
```
Read references/executor-base.md          # REQUIRED: common guidelines
Read references/executor-general.md       # General flexible style
Read references/executor-consultant.md    # Consulting style
Read references/executor-consultant-top.md # Top consulting style (MBB level)
```

> Only need to read executor-base + one style file.

**Design Parameter Confirmation (Mandatory)**: Before generating the first SVG, the Executor MUST review and output key design parameters from the Design Specification (canvas dimensions, color scheme, font plan, body font size) to ensure spec adherence. See executor-base.md Section 2 for details.

**Visual Construction Phase**:
- Batch-generate SVG pages → `<project_path>/svg_output/`

**Logic Construction Phase**:
- Generate speaker notes → `<project_path>/notes/total.md`

**✅ Checkpoint — Confirm all SVGs and notes are fully generated. Proceed directly to Step 7 post-processing**:
```markdown
## ✅ Executor Phase Complete
- [x] All SVGs generated to svg_output/
- [x] Speaker notes generated at notes/total.md
```

---

### Step 7: Post-processing & Export

🚧 **GATE**: Step 6 complete; all SVGs generated to `svg_output/`; speaker notes `notes/total.md` generated.

> ⚠️ The following three sub-steps MUST be **executed individually one at a time**. Each command must complete and be confirmed successful before running the next.
> ❌ **NEVER** put all three commands in a single code block or single shell invocation.

**Step 7.1** — Split speaker notes:
```bash
python3 ${SKILL_DIR}/scripts/total_md_split.py <project_path>
```

**Step 7.2** — SVG post-processing (icon embedding / image crop & embed / text flattening / rounded rect to path):
```bash
python3 ${SKILL_DIR}/scripts/finalize_svg.py <project_path>
```

**Step 7.3** — Export PPTX (Guomics: editable version only):
```bash
python3 ${SKILL_DIR}/scripts/svg_to_pptx.py <project_path> -s final --only native
# --only native: outputs ONE editable file (native DrawingML shapes, fully editable in PowerPoint)
# DO NOT omit --only native — Guomics presentations only need the editable version
```

> ❌ **NEVER** use `cp` as a substitute for `finalize_svg.py` — it performs multiple critical processing steps
> ❌ **NEVER** export directly from `svg_output/` — MUST use `-s final` to export from `svg_final/`
> ❌ **NEVER** omit `--only native` — Guomics does not need the `_svg.pptx` legacy reference file

---

### Step 8: Optimizer Phase (Optional)

🚧 **GATE**: Step 7 complete.

> **Trigger condition**: User requests optimization, or design quality needs improvement

Read `references/optimizer-crap.md`

1. Optimizer analyzes and optimizes the specified SVG files in `svg_output/`
2. Optimized files are saved with `yh_` prefix in `svg_output/`
3. After all optimizations are complete, **MUST re-run the entire post-processing pipeline** (Step 7.1 → 7.2 → 7.3), following the same sequential execution rules as Step 7

> ⚠️ Do NOT skip re-processing — optimized SVGs still need icon embedding, image processing, and PPTX export.

---

## Role Switching Protocol

Before switching roles, you **MUST first read** the corresponding reference file — skipping is FORBIDDEN. Output marker:

```markdown
## [Role Switch: <Role Name>]
📖 Reading role definition: references/<filename>.md
📋 Current task: <brief description>
```

---

## Reference Resources

| Resource | Path |
|----------|------|
| Shared technical constraints | `references/shared-standards.md` |
| Canvas format specification | `references/canvas-formats.md` |
| Design guidelines | `references/design-guidelines.md` |
| Image layout specification | `references/image-layout-spec.md` |
| SVG image embedding | `references/svg-image-embedding.md` |
| **Template layout coordinates** | `references/template-layout.md` |

---

## Notes

- Always use `--only native` for the svg_to_pptx.py export command — Guomics only needs the editable version
- If Optimizer optimization was performed, re-run post-processing and export with `--only native`
- Local preview: `python3 -m http.server -d <project_path>/svg_final 8000`
