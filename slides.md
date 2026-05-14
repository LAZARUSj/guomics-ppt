---
theme: ./
title: Guomics Group Meeting Template
author: Your Name
aspectRatio: 16/9
canvasWidth: 980
layout: cover
fonts:
  sans: Arial
  mono: Fira Code
  provider: none
---

# This is your Presentation Title

<p class="presenter">Your Name</p>

Guomics Laboratory for Proteome Complexity Science, Westlake University

Westlake Center for Intelligent Proteomics, Westlake Laboratory

<div class="website">guomics.com</div>

---
layout: outline
title: Outline
---

1. Add Title
2. Add Title
3. Add Title
4. Add Title
5. Add Title
6. Add Title

---
layout: two-figure
title: Protein Interaction Basics
subtitle: Write here your subtitle
---

::left::

![Prefoldin complex](/decorations/prefoldin-complex.png)

Prefoldin complex

::right::

![Alzheimer disease-related PPIs](/decorations/photo-portrait-1.png)

Alzheimer disease-related PPIs

::body::

**Protein-Protein Interactions (PPIs)** - direct physical interactions between two or more proteins

**Protein Complexes** - a stable or transient assembly of multiple proteins that come together to perform a specific biological function

::sources::

https://www.researchgate.net/figure/Figures-A-to-C-is-the-prefoldin-complex-formation-process-A-Scattered-prefoldin_fig1_345363768
https://www.researchgate.net/publication/344673028_Systems_biology_and_bioinformatics_approach_to_identify_gene_signatures_pathways_and_therapeutic_targets_of_Alzheimer's_disease

---
layout: comparison
title: CCprofiler Comparison
subtitle: Write here your subtitle
---

::left::

![Complexes identified from CCprofiler](/decorations/complexes-ccprofiler.png)

Complexes identified from CCprofiler

::right::

![Interactions identified from CCprofiler](/decorations/interactions-ccprofiler.png)

Interactions identified from CCprofiler

::highlight::

Complex sizes was balanced for CORUM, Complex Portal, and hu.MAP

hu.MAP shows an advantage in identifying medium-sized complexes.

iRefIndex should be cross-referenced with experimentally validated databases

---
layout: publications
title: Publications
subtitle: Write here your subtitle
---

<PublicationCard image="/decorations/photo-square-2.png" caption="Protein restriction reprograms the multi-organ proteomic landscape of mouse aging Lu, et al. Cell. 2025" />

<PublicationCard image="/decorations/figure-detail-1.png" caption="Spatial distribution of the proteome in human body and cancers Yue, et al. 2nd revision. Nature" />

<PublicationCard image="/decorations/photo-square-3.png" caption="Large-scale metaproteomics of human gut microbiota reveals microbial functions in metabolic diseases and aging Liang, et al. Cell Metabolism. 2026" />

<PublicationCard image="/decorations/figure-detail-2.png" caption="A spatially resolved human brain proteome atlas for decoding brain function and disease. Xiao, et al. Under review." />

<PublicationCard image="/decorations/photo-landscape-1.png" caption="Longitudinal serum proteome mapping reveals biomarkers for healthy ageing and related cardiometabolic diseases Tang, et al. Nature Metabolism. 2025" />

<PublicationCard image="/decorations/photo-square-4.png" caption="Proteomic landscape of epithelial ovarian cancer Qian, et al. Nature Comms. 2024" />

<PublicationCard image="/decorations/photo-square-5.png" caption="Population serum proteomics uncovers a prognostic protein classifier for metabolic syndrome Cai, et al. Cell Rep Med. 2023" />

<PublicationCard image="/decorations/photo-square-6.png" caption="The pan-cancer proteome atlas, a mass spectrometry-based landscape for discovering tumor biology, biomarkers, and therapeutic targets Knol, et al. Cancer Cell. 2025" />

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

FTC238 identified the greatest number of protein interactions

The enriched GO pathway of the protein pairs was similar among the three cell lines

---
layout: triple-data
title: Activated PPIs
subtitle: Write here your subtitle
---

::left::

![Predicted protein pairs](/decorations/predicted-pairs-fdr5.png)

Predicted protein pairs (FDR&lt;5%)

::right-top::

![FTC238 vs Nthy-ori 3-1](/decorations/ftc238-volcano.png)

::right-bottom::

![TPC-1 vs Nthy-ori 3-1](/decorations/tpc1-volcano.png)

::highlight::

Nthy-ori 3-1 as control and analyzed the activated PPIs in FTC238 and TPC-1

2138 downregulated and 952 upregulated protein pairs between FTC238 vs Nthy-ori 3-1

1286 downregulated and 479 upregulated protein pairs between TPC-1 vs Nthy-ori 3-1

---
layout: full-bleed
title: Novel Protein Interactions
subtitle: Novel protein interactions
---

PFAS is a key enzyme in the de novo purine biosynthesis pathway

HK1 catalyzes the first step of glycolysis, converting glucose to glucose-6-phosphate

TGM2 is a multifunctional enzyme involved in protein crosslinking, cell adhesion, and extracellular matrix remodeling

<span class="text-orange">Highlight the metabolic and survival adaptations TPC-1 employ and represent potential therapeutic targets for disrupting tumor progression</span>

::figure::

![Novel protein interactions](/decorations/photo-portrait-3.png)

---
layout: summary
---

## Summary

- Robotic platform increased **throughput** by fourfold of sample preparation
- Multi-database strategy of **PrInCE** increased near ninefold for predicted protein interactions

---
layout: thanks
---

# Thanks!

<p class="presenter">Your Name</p>

Guomics Laboratory for Proteome Complexity Science, Westlake University

Westlake Center for Intelligent Proteomics, Westlake Laboratory

<div class="website">guomics.com</div>
