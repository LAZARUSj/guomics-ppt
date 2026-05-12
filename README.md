# Guomics PPT Skill

Guomics PPT Skill 是一个面向 Guomics / Westlake 相关科研汇报的 PPT 生成技能包。它围绕 SVG 到 PPTX 的工作流组织脚本、模板、图表组件、图标库和品牌规范，用于生成可编辑的 PowerPoint 幻灯片，而不是把整页内容导出成图片。

## 主要能力

- 将 PDF、Word、网页、Markdown 等资料整理为演示文稿输入内容。
- 基于 Guomics 品牌视觉规范生成 16:9 幻灯片。
- 使用 SVG 模板描述页面结构、图表和版式。
- 将 SVG 页面转换为可编辑的 PPTX 形状和元素。
- 支持封面、章节页、目录页、内容页、图文页、图表页和结束页等常用科研汇报页面。

## 目录结构

| Path | Description |
| --- | --- |
| `SKILL.md` | Codex / Claude skill 入口说明和完整工作流 |
| `AGENTS.md` | Agent 执行约束和协作规范 |
| `references/` | 设计规范、执行规范、图像和 SVG 规则 |
| `scripts/` | 内容转换、SVG 处理、质量检查、PPTX 导出等脚本 |
| `templates/layouts/` | Guomics 幻灯片版式模板 |
| `templates/charts/` | 常用图表 SVG 模板 |
| `templates/icons/` | 图标 SVG 组件库 |
| `workflows/` | 独立工作流说明 |

## 基础用法

在支持 Codex / Claude skill 的环境中，将本目录作为 `guomics-ppt` skill 加载。当用户请求创建 Guomics 风格 PPT、科研汇报幻灯片或基于文档生成演示文稿时，按 `SKILL.md` 中定义的串行流程执行。

常用脚本示例：

```bash
python scripts/pdf_to_md.py input.pdf
python scripts/doc_to_md.py input.docx
python scripts/web_to_md.py https://example.com/page
python scripts/svg_quality_checker.py path/to/slide.svg
python scripts/finalize_svg.py path/to/project
python scripts/svg_to_pptx.py path/to/project
```

具体参数和完整说明见 `scripts/README.md`。

## 设计规范

默认使用 Guomics 品牌配色和字体体系：

| Role | Value |
| --- | --- |
| Canvas | `ppt169`, 1280 x 720 |
| Primary | `#004791` |
| Accent | `#F18D00` |
| Body text | `#212121` |
| Background | `#FFFFFF` |
| Main fonts | Arial Black, Arial |

科研图像和图表应遵循 `references/guomics_standards.md` 中的清晰性、可读性、可访问性和 Nature-style artwork 原则。

## Attribution

本项目的部分代码、脚本结构、SVG/PPTX 转换思路、模板组件和工作流设计参考并改编自 [hugohe3/ppt-master](https://github.com/hugohe3/ppt-master)。

`ppt-master` 是 Hugo He 开源的 AI PPTX 生成项目，采用 MIT License。本仓库在其基础上加入了 Guomics 品牌视觉规范、专用模板、科研汇报规范和本地化执行流程。原项目版权归其原作者和贡献者所有；本项目中来自或改编自 `ppt-master` 的部分遵循其原始许可证要求。

## Notes

- 生成的 PPTX 应保持元素可编辑，优先使用原生 PowerPoint 形状、文本和图片。
- 不建议提交运行中生成的临时文件、缓存文件或 `__pycache__`。
- 如果扩展模板或脚本，请同步更新 `SKILL.md`、`scripts/README.md` 或对应索引文件。
