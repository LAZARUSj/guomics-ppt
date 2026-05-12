# AGENTS.md

This file serves as the project entry point for general AI agents. Before executing PPT generation tasks, **you MUST first read `skills/guomics-ppt/SKILL.md`** for the complete workflow and rules.

## Project Overview

Guomics PPT is an AI-driven Guomics-branded presentation generation system. Through multi-role collaboration (Strategist → Image_Generator → Executor → Optimizer), it converts source documents (PDF/DOCX/URL/Markdown) into natively editable PPTX with real PowerPoint shapes (DrawingML), following Guomics visual identity (navy `#004791` / orange `#F18D00` / white) and Nature artwork standards.

**Core Pipeline**: `Source Document → Create Project → Template Option → Strategist Eight Confirmations → [Image_Generator] → Executor → Post-processing → Export PPTX`

**Execution Requirements**:

- Before starting a PPT task, read `skills/guomics-ppt/SKILL.md` first
- To create a template independently, read `skills/guomics-ppt/workflows/create-template.md`
- Role-specific rules and technical constraints are in `skills/guomics-ppt/references/`
- ⚠️ **Strict serial execution**: Every Step in the pipeline MUST be executed sequentially — bundling, batching, or parallelizing Steps is FORBIDDEN

## Common Commands

```bash
# Source content conversion
python3 skills/guomics-ppt/scripts/pdf_to_md.py <PDF_file>
python3 skills/guomics-ppt/scripts/doc_to_md.py <DOCX_or_other_file>   # Requires: pandoc (DOCX/EPUB/HTML/LaTeX/RST/etc.)
python3 skills/guomics-ppt/scripts/web_to_md.py <URL>
node skills/guomics-ppt/scripts/web_to_md.cjs <URL>                     # WeChat / high-security sites

# Project management
python3 skills/guomics-ppt/scripts/project_manager.py init <project_name> --format ppt169
python3 skills/guomics-ppt/scripts/project_manager.py import-sources <project_path> <source_files_or_URLs...> --move
python3 skills/guomics-ppt/scripts/project_manager.py validate <project_path>

# Image tools
python3 skills/guomics-ppt/scripts/analyze_images.py <project_path>/images
python3 skills/guomics-ppt/scripts/nano_banana_gen.py "prompt" --aspect_ratio 16:9 --image_size 1K -o <project_path>/images

# SVG quality check
python3 skills/guomics-ppt/scripts/svg_quality_checker.py <project_path>

# Post-processing pipeline (MUST run sequentially, one at a time — NEVER batch)
python3 skills/guomics-ppt/scripts/total_md_split.py <project_path>
# ✅ Confirm no errors before running the next command
python3 skills/guomics-ppt/scripts/finalize_svg.py <project_path>
# ✅ Confirm no errors before running the next command
python3 skills/guomics-ppt/scripts/svg_to_pptx.py <project_path> -s final --only native
# --only native: Guomics only needs the editable DrawingML version — NEVER omit this flag
```

## Core Directories

- `skills/guomics-ppt/SKILL.md` — Main entry point and complete workflow
- `skills/guomics-ppt/workflows/create-template.md` — Standalone template workflow
- `skills/guomics-ppt/references/` — Role definitions and technical specifications
- `skills/guomics-ppt/references/guomics_standards.md` — Guomics Nature artwork rules
- `skills/guomics-ppt/scripts/` — Tool scripts
- `skills/guomics-ppt/templates/` — Layout templates, chart templates, icon library
- `skills/guomics-ppt/templates/layouts/guomics/` — Guomics official layout templates
- `examples/` — Example projects
- `projects/` — User project workspace

## SVG Technical Constraints

**Banned features**: `clipPath` | `mask` | `<style>` | `class` | external CSS | `<foreignObject>` | `textPath` | `@font-face` | `<animate*>` | `<script>` | `marker-end` | `<iframe>` | `<symbol>+<use>` (`id` inside `<defs>` is a legitimate reference and is NOT banned)

**PPT compatibility alternatives**:

| Banned | Alternative |
|--------|-------------|
| `rgba()` | `fill-opacity` / `stroke-opacity` |
| `<g opacity>` | Set opacity on each child element individually |
| `<image opacity>` | Overlay with a mask layer |
| `marker-end` arrows | `<polygon>` triangles |

## Canvas Format Quick Reference

| Format | viewBox | Use Case |
|--------|---------|----------|
| PPT 16:9 (**Guomics default**) | `0 0 1280 720` | Business / scientific presentations |
| PPT 4:3 | `0 0 1024 768` | Traditional projectors, academic talks |
| Xiaohongshu (RED) | `0 0 1242 1660` | Image-text sharing |
| WeChat Moments / Instagram | `0 0 1080 1080` | Square posters |
| Story / TikTok | `0 0 1080 1920` | Vertical stories |
| WeChat Article Header | `0 0 900 383` | WeChat article covers |
| Landscape Banner | `0 0 1920 1080` | Web banners, digital screens |
| Portrait Poster | `0 0 1080 1920` | Phone screens, elevator ads |
| A4 Print | `0 0 1240 1754` | Print posters, flyers |

## Post-processing Notes

- **NEVER** use `cp` as a substitute for `finalize_svg.py`
- **NEVER** export directly from `svg_output/` — MUST export from `svg_final/` (use `-s final`)
- **ALWAYS** pass `--only native` to `svg_to_pptx.py` — Guomics does not need the `_svg.pptx` legacy reference file
- **NEVER** run the three post-processing steps in a single code block or single shell invocation
- After Optimizer optimization, re-run all three post-processing steps in order
