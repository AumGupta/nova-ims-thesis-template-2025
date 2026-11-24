# Moving an existing NOVAthesis project to the lean edition

This guide is for students who already write their thesis in the NOVAthesis template (`NOVAthesis 2025-2026.zip` in this repository) and want to try the lean edition. It is optional: NOVAthesis remains the reference template, and it is the one to keep if you need anything listed under [What the lean edition does not provide](#what-the-lean-edition-does-not-provide).

Keep a copy of your NOVAthesis project until the lean version compiles and you have compared the two PDFs.

## 1. Settings

NOVAthesis keeps its settings in `Config/1_novathesis.tex` and `Config/3_cover.tex`. In the lean edition all of them are in `thesis-info.tex`.

| NOVAthesis | Lean edition |
| --- | --- |
| `\ntsetup{doctype=msc}` or `phd` | `\degreetype{msc}` or `phd` |
| `\newcommand{\imsDegree}{...}` and `\newcommand{\imsSpecialization}{...}` | `\covercode{...}` (cover) and `\programme{...}` (title page text); see the cover table in [README.md](README.md) |
| `\ntsetup{lang=en}` | English is the only option (see below) |
| `\nttitle(main,en){...}` | `\thesistitle{...}` (running text) and `\thesistitlecover{...}` (cover and title page, with `\\` for line breaks) |
| `\ntauthorname(m){Full Name}{Short Name}` | `\thesisauthor{Full Name}` |
| student number (not on the NOVAthesis title page) | `\studentid{...}`, printed under the name on the title page |
| `\ntaddperson{adviser}(a,f){Name, Position, School}` | `\supervisor{Name, PhD}{School\\University\\City, Country}` |
| `\ntaddperson{adviser}(c,m){...}` | `\cosupervisor{Name, PhD}{...}` (repeat for more) |
| `\ntdate(submission){year-month-day}` | `\submissiondate[day]{month}{year}` and `\submissionplace{Lisbon}` |
| `\keywords{One \and Two}` in the abstract file | `\thesiskeywords{One; two}` |
| `\ntsetup{sdg={4,9}}` | `\sdgs{4,9}` |
| `Config/0_memoir.tex` font size | fixed at 12 pt; `\documentclass[times]{novaims-thesis}` switches to Times |

## 2. Files

| NOVAthesis | Lean edition |
| --- | --- |
| `\ntaddfile{chapter}{chapter1}` in `Config/4_files.tex` | `\include{Chapters/1-introduction}` in `main.tex` |
| `\ntaddfile{appendix}{appendix1}` | `\include{Appendices/appendix-a}` after `\appendix` in `main.tex` |
| `\ntaddfile{abstract}[en]{abstract-en}` | `FrontMatter/abstract-en.tex` (starts with `\frontchapter{Abstract}`) |
| `\ntaddfile{abstract}[pt]{abstract-pt}` | `FrontMatter/abstract-pt.tex` (Resumo) |
| `\ntaddfile{acknowledgements}{acknowledgements}` | `FrontMatter/acknowledgements.tex` |
| `\ntaddfile{dedicatory}{dedicatory}` | `FrontMatter/dedication.tex`, switched by `\dedicationpage{true}` |
| `\ntaddfile{bib}{bibliography.bib}` | `\addreferences{Bibliography/references}` in `main.tex` (file name without `.bib`) |
| `\ntaddfile{glossaries}[acronym]{acronyms}` | `FrontMatter/acronyms.tex` (see section 4) |
| figures in `Chapters/Figures/` | figures in `Figures/` (`\graphicspath` points there) |

Chapter files can be copied as they are. Remove the `%!TEX root = ../template.tex` and `\typeout{NT FILE ...}` lines, or leave them; they do no harm. Update `\includegraphics` paths if they contain `Chapters/Figures/`.

## 3. Bibliography and citations

Your `.bib` file can be reused without changes. Pick one of the two reference set-ups:

**APA 7 with biblatex, closest to NOVAthesis.** NOVA IMS projects in NOVAthesis use biblatex with `style=apa` (APA 7) and Biber. The same set-up is available with

```latex
\documentclass[apa7]{novaims-thesis}
```

`\textcite`, `\parencite`, `\citet` and `\citep` all work, so chapter files need no changes. A full build takes longer (see [BENCHMARK.md](BENCHMARK.md)). On Overleaf, Biber runs automatically.

**Default (apacite with BibTeX), faster.** The default references follow APA 6 with the APA 7 "et al." rule from the first citation. The main visible difference from APA 7 is that a reference with many authors lists the first 6, then "…" and the last author (APA 7 lists up to 20). Citation commands map as follows:

| NOVAthesis (biblatex) | Default lean edition |
| --- | --- |
| `\textcite{key}` | `\citet{key}` |
| `\parencite{key}` | `\citep{key}` |
| `\cite{key}` | `\citep{key}` (in the default set-up `\cite` gives Author (Year), like `\citet`) |
| `\citeauthor{key}`, `\citeyear{key}` | same |

If you prefer not to edit the chapters, add these lines to the preamble of `main.tex` after `\input{thesis-info}`:

```latex
\newcommand{\textcite}{\citet}
\newcommand{\parencite}{\citep}
```

Not available in either set-up: page back-references in the reference list (`\ntbibsetup{backref=true}`), the ISO date options and other `\ntbibsetup` options. With `apa7` you can add biblatex options yourself after `\documentclass`, for example `\ExecuteBibliographyOptions{giveninits=true}`.

If two `.bib` files were merged and some keys changed, `Bibliography/key-aliases.tex` lets an old key point to the new one: `\citekeyalias{old}{new}`.

## 4. Acronyms and glossary

NOVAthesis uses the glossaries package: acronyms are defined with `\newacronym{key}{short}{long}` and used with `\gls{key}`, which expands the first use and links to the list. The lean edition does not load glossaries. It prints the list from `FrontMatter/acronyms.tex`:

```latex
\begin{acronymlist}
\acronym{GIS}{Geographic information systems}
\end{acronymlist}
```

There are two ways to move:

1. **Plain text (simplest).** Turn each `\newacronym{gis}{GIS}{Geographic information systems}` into `\acronym{GIS}{Geographic information systems}` and replace `\gls{gis}` in the chapters with the text you want, writing the long form out at first use.
2. **Keep glossaries.** Add to the preamble of `main.tex`:

   ```latex
   \usepackage[acronym,automake]{glossaries}
   \makeglossaries
   \input{Chapters/acronyms}   % your \newacronym lines
   ```

   and replace `\input{FrontMatter/acronyms}` with `\printglossary[type=\acronymtype,title={List of Acronyms and Abbreviations}]`. This brings back first-use expansion, but it also adds the extra glossary run to every build.

The NOVAthesis glossary (`[glossary]`) and list of symbols (`[symbols]`) work the same way with the glossaries package; the lean edition has no ready-made pages for them.

## 5. What the lean edition does not provide

Keep NOVAthesis if you need any of these:

- **Portuguese or other main languages.** The lean edition is in English only: the fixed texts and the covers are the English versions. A Resumo in Portuguese is included in the front matter. NOVAthesis supports Portuguese (`\ntsetup{lang=pt}`) and abstracts in further languages.
- **Document stages.** NOVAthesis has `\ntsetup{docstatus=working|provisional|final}` (working draft, submission version, final version with committee). The lean edition always produces the submission layout.
- **Evaluation committee.** `\ntaddperson{committee}` and `\ntsetup{print/committee=true}` have no equivalent. Add the committee to the title page by hand if your programme asks for it in the final version.
- **Quote page, annexes, list of symbols, glossary page, spine** and the other NOVAthesis optional parts. Annexes can be added as further appendices after `\appendix`.
- **Other schools.** Only NOVA IMS covers and wording are included.

## 6. Check the result

After the move:

1. Compile with `latexmk -pdf main.tex` locally, or press Recompile on Overleaf.
2. Search the log for `undefined` (citations, references) and for `Missing` (packages).
3. Compare the reference list with the NOVAthesis PDF, especially references with more than 6 authors if you use the default set-up.
4. Check the cover, title page, supervisors and date against your programme's rules.
