# Compile-time comparison

This page compares the NOVAthesis template (the reference template in this repository, `NOVAthesis 2025-2026.zip`) with the lean edition, using the **same thesis content** in both. The numbers are local measurements; they show the relative cost of each template, not the exact time on Overleaf.

## Content used

The script [`benchmark/run_benchmark.py`](benchmark/run_benchmark.py) generates the same synthetic thesis for every variant, so no real thesis text is stored here:

- 6 chapters, each with 4 sections, 12 paragraphs, 1 table, 1 figure and 1 equation
- about 155 citations in `\textcite` and `\parencite` form, to 60 journal articles in one `.bib` file (1 to 9 authors each, with DOIs)
- 12 acronyms used with `\gls{...}`, and an acronym list
- abstract, acknowledgements and one appendix

Settings per variant:

| Variant | Template and settings | References | Acronyms |
| --- | --- | --- | --- |
| `novathesis` | NOVAthesis from the zip, `\imsDegree{mgt}`, `docstatus=provisional` (submission version), English, Portuguese and English abstracts | biblatex `style=apa`, Biber (NOVA IMS default) | glossaries package, `\newacronym` |
| `lean` | lean edition, `\covercode{MGT-EN}`, default options | apacite, BibTeX | plain acronym list |
| `lean-apa7` | lean edition, `\documentclass[apa7]{novaims-thesis}` | biblatex `style=apa`, Biber | plain acronym list |

In the lean variants `\textcite` and `\parencite` map to `\citet` and `\citep` (the `apa7` option provides them directly) and `\gls{X}` prints `X`.

## Results

Median of 3 runs per variant, measured on 22 November 2026.

| Variant | Full build from a clean folder | One more pdfLaTeX pass | Pages |
| --- | --- | --- | --- |
| `novathesis` | 35.4 s | 6.7 s | 48 |
| `lean` | 6.1 s | 0.9 s | 53 |
| `lean-apa7` | 18.2 s | 3.8 s | 53 |

- **Full build:** `latexmk -pdf` in an empty folder, including all pdfLaTeX passes, BibTeX or Biber, and (for NOVAthesis) the glossary run.
- **One more pass:** a single `pdflatex` run on the finished build. This is close to what happens on each recompile after a small edit.
- The page counts differ because the two templates set the front matter differently (for example, NOVAthesis adds page back-references to each reference and page numbers to the acronym list). All citations and cross-references resolved in every variant.

Raw values: [`benchmark/results.csv`](benchmark/results.csv) and [`benchmark/results.md`](benchmark/results.md).

## Environment

| | |
| --- | --- |
| Engine | pdfLaTeX: pdfTeX 3.141592653-2.6-1.40.25 |
| Distribution | TeX Live 2023/Debian |
| Biber | 2.19 |
| BibTeX | 0.99d |
| latexmk | 4.83 |
| CPU | Intel Xeon @ 2.10 GHz, 2 cores |
| OS | Linux (x86_64) |

## Reading the numbers

- On this content the lean edition with the default references needs about one sixth of the full build time of NOVAthesis and about one seventh of the time per pass.
- Most of the difference in the `lean-apa7` variant comes from biblatex and Biber: the same lean layout with biblatex-apa takes about three times as long as with apacite. This is why `apa7` is an option and not the default.
- Overleaf runs on other hardware and a newer TeX Live, and its free plan has a compile time limit (10 s at the time of writing). Treat these numbers as relative. When this was tested on a free Overleaf account, the NOVAthesis project as downloaded stopped with `File 'xfor.sty' not found`, so it was not timed there.

## Run it yourself

From the repository root, with a TeX Live installation that has `latexmk`, `biber` and `pdfinfo`:

```bash
python3 lean-edition/benchmark/run_benchmark.py --runs 3
```

The script builds each variant in `lean-edition/benchmark/runs/` (ignored by git) and rewrites `results.csv` and `results.md`.
