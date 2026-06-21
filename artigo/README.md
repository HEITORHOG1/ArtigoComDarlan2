# Self-Aware Steel Structures — Elsevier (Automation in Construction) LaTeX project

Conceptual framework + state-of-the-art review manuscript prepared for
**Automation in Construction** (Elsevier, ISSN 0926-5805), using the
`elsarticle` class with **numbered** references.

**Title:** *From Passive Members to Self-Aware Steel Structures: A Digital-Twin and
Machine-Learning Framework for Structural Cognition and Autonomous Health Monitoring.*

## Structure

```
artigo/
├── main.tex                  # master file (frontmatter + \input of all parts)
├── references.bib            # 24 references (10 from Automation in Construction)
├── elsarticle-num.bst        # Elsevier numbered bibliography style
├── secoes/                   # one .tex per section
│   ├── 01-introduction.tex
│   ├── 02-background.tex      # 2.1 SHM · 2.2 data-driven · 2.3 ML · 2.4 dynamics · 2.5 FEM/DT
│   ├── 03-paradigm.tex        # Structural Cognition; L0–L5; Rytter mapping
│   ├── 04-architecture.tex    # five-layer reference architecture
│   ├── 05-methodology.tex     # braced-frame demonstrator; six-step method
│   ├── 06-ml-strategy.tex     # features, novelty, classification, LSTM, validation
│   ├── 07-discussion.tex
│   └── 08-conclusions.tex
├── figs/                     # vector figures (TikZ / pgfplots)
│   ├── fig-architecture.tex  # Fig. 1  five-layer architecture
│   ├── fig-frf.tex           # Fig. 2  schematic frequency-response (stiffness loss)
│   ├── fig-levels.tex        # Fig. 3  six levels of self-awareness
│   ├── fig-testbed.tex       # Fig. 4  demonstrator + digital-twin loop
│   └── fig-mlpipeline.tex    # Fig. 5  ML pipeline mapped to Rytter stages
├── tabelas/                  # booktabs tables
│   ├── tab1-pillars.tex      # Table 1  theoretical foundations
│   ├── tab2-conv-vs-aware.tex# Table 2  conventional SHM vs self-aware
│   ├── tab3-levels.tex       # Table 3  levels ↔ Rytter ↔ technique
│   ├── tab4-sensors.tex      # sensor network
│   ├── tab5-mlmethods.tex    # ML methods ↔ task ↔ level
│   ├── tab6-params.tex       # auditable experimental specification (parameters)
│   └── tab-positioning.tex   # novelty: framework vs. closest works
├── highlights.txt            # 5 highlights (each ≤ 85 characters)
├── graphical-abstract.tex    # standalone graphical abstract (compiles alone)
├── graphical-abstract-body.tex # body \input by main.tex frontmatter
└── cover-letter.tex          # cover letter to the Editor-in-Chief
```

## Compile

```bash
latexmk -pdf -interaction=nonstopmode main.tex            # -> main.pdf
latexmk -pdf graphical-abstract.tex                       # -> graphical-abstract.pdf
latexmk -pdf cover-letter.tex                             # -> cover-letter.pdf
```

(`latexmk` runs pdflatex + bibtex + pdflatex twice automatically. MiKTeX
installs any missing packages on the fly.)

## Before submission — fill in the placeholders

- `[First Author]`, `[Second Author]`, e-mail, ORCID, and the `\affiliation{...}`
  block in `main.tex`; the same names in the CRediT statement and `cover-letter.tex`.
- In `references.bib`, full author names are completed from each item's DOI
  (every DOI is real and resolvable); verify formatting against the journal style.
- Figures 4 and the testbed numbers are **schematic / illustrative** (no measured
  data, as stated in the captions): this is a conceptual framework paper.

## References from the target journal (Automation in Construction)

10 cited: Chiachío et al. 2022; Zou et al. 2026; Li et al. 2025; Mariniello et al.
2025; Parisi et al. 2022; He et al. 2022; Karaaslan et al. 2021; Yu et al. 2024;
Wang & Su 2023; Arya et al. 2021 — well above the 5 required.
