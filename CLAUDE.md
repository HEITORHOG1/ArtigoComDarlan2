# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

Production of a scientific manuscript (LaTeX, Elsevier `elsarticle`) targeting **Automation in Construction** (ISSN 0926-5805, numbered references). It is a writing project, not software, and **not a git repository** — do not attempt git or PR operations.

## Layout

- `artigo/` — the manuscript: `main.tex`, `secoes/` (one `.tex` per section), `figs/` (TikZ/pgfplots, vector), `tabelas/` (booktabs), `references.bib`, plus `cover-letter.tex`, `graphical-abstract.tex`, `highlights.txt`. Build output is `main.pdf`. See `artigo/README.md`.
- `PDFs/` — the five reference books (PDF + `.md` text extractions).
- `.claude/skills/` — the article-production workflow (see below); `elsarticle/` — the Elsevier template bundle; `leitura.md` — the research concept.

## Python (important)

The default `python` resolves to a venv **without pip**. For any scripting or package install, use the real interpreter:

```
/c/Users/heitorhog/AppData/Local/Programs/Python/Python312/python
```

(PyMuPDF / `fitz` is installed there; it converts `PDFs/*.pdf` → `.md`.)

## Building the manuscript (MiKTeX is installed)

```
latexmk -pdf -interaction=nonstopmode -cd artigo/main.tex
```

- Class `elsarticle` (numbered); `\bibliographystyle{elsarticle-num}`, with `elsarticle-num.bst` kept inside `artigo/`. latexmk runs bibtex and reruns automatically.
- After editing, check `artigo/main.log` for `Overfull`, `undefined`, and `Author undefined` — the working build has zero of each.
- `\citet` needs author data the plain `elsarticle-num.bst` does not emit; prefer `\citep` (or name the author in prose followed by `\citep`).
- Figures are TikZ/pgfplots wrapped in `\resizebox{\linewidth}{!}{...}` (or pgfplots `width=\linewidth`); tables use `tabularx` + `booktabs` with no vertical rules. Do not name a TikZ style `step` (it collides with a built-in key).

## Article-production rules (from `.claude/skills/`)

These skills define how the article is written; follow `workflow-artigo` before writing or revising content, and:

- **Never disclose AI involvement** in any deliverable (manuscript, cover letter, captions, acknowledgements). This is inviolable across every skill.
- Apply `anti-vicios-ia`: no em-dashes, avoid marker vocabulary ("delve", "leverage", filler "furthermore"/"moreover", "provably", etc.), and vary sentence length.
- **References must be real and verifiable.** Never fabricate citations or DOIs; source and verify them via Crossref (`api.crossref.org`). The manuscript must cite at least five papers from the target journal.
- This is a conceptual framework/review paper with no completed experiments — never present fabricated results.
