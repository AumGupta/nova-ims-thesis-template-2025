# NOVA IMS Thesis Template, lean edition

An optional, lighter LaTeX thesis template for **NOVA Information Management School (NOVA IMS)**, Universidade NOVA de Lisboa, offered **alongside** the NOVAthesis template of the [NOVA IMS thesis template 2025](https://github.com/pdecampossouza/nova-ims-thesis-template-2025). It keeps the NOVA IMS layout (official covers, title page, statement of integrity, copyright page, margins, headings) but runs on a small set of standard packages, so it compiles in a few seconds.

> **Status:** optional alternative, in English only. The reference template is NOVAthesis (`NOVAthesis 2025-2026.zip` in the repository root), which also supports Portuguese, committee pages and document stages. Check with your programme office before submitting with this version.

- Moving from NOVAthesis: [MIGRATION.md](MIGRATION.md)
- Compile times of both templates on the same content: [BENCHMARK.md](BENCHMARK.md)

## Preview

[![Covers: an example programme, the current and proposed Geospatial Technologies covers, and the 2025 back cover](preview/covers.png)](preview/template-preview.pdf)

See the full compiled template in [preview/template-preview.pdf](preview/template-preview.pdf) (example settings, placeholder text) and a doctoral example with the DGI cover (`\covercode{DGI-EN}`, `\degreetype{phd}`) in [preview/dgi-example.pdf](preview/dgi-example.pdf). The `preview` folder is only for viewing on GitHub; it is not needed to compile, and you can delete it in your own project.

## When to use it

Measured on the same generated 6-chapter thesis with 60 references, pdfLaTeX, TeX Live 2023 (details and method in [BENCHMARK.md](BENCHMARK.md)):

| | NOVAthesis | Lean edition | Lean edition, `apa7` |
| --- | --- | --- | --- |
| Full build from a clean folder | 35.4 s | 6.1 s | 18.2 s |
| One more pdfLaTeX pass (recompile after an edit) | 6.7 s | 0.9 s | 3.8 s |
| References | biblatex-apa (APA 7), Biber | apacite, BibTeX | biblatex-apa (APA 7), Biber |
| Languages | English, Portuguese and others | English | English |
| Committee, document stages | yes | no | no |
| Schools included | all NOVAthesis schools | NOVA IMS only | NOVA IMS only |

These are local times on a 2-core machine. Overleaf uses other hardware and a newer TeX Live, and its free plan has a compile time limit, so use them as a comparison, not as Overleaf times.

## Quick start on Overleaf

1. Download this repository as a zip (Code, Download ZIP) and unzip it.
2. Open the `lean-edition` folder, select everything inside it and compress it into a new zip (the zip should contain `main.tex` at its top level).
3. In Overleaf: New Project, Upload Project, choose that zip.
4. Open `thesis-info.tex` and fill in your title, name, student number, programme, supervisors and cover code.
5. Press Recompile. The main document is `main.tex`, the compiler is pdfLaTeX (the Overleaf default).

## Choose your cover

Set the cover in `thesis-info.tex` with `\covercode{...}`, using a folder name from `Figures/Covers`. All covers are the official NOVA IMS artwork (English versions).

| Code | Programme | Specialization |
| --- | --- | --- |
| `DGI-EN` | Doctoral Program in Information Management | |
| `MCSIG-CDG-EN` | Geographic Information Systems and Science | Geospatial Data Science |
| `MCSIG-CSIG-EN` | Geographic Information Systems and Science | Geographic Information Systems and Science |
| `MDDM-DMA-EN` | Data-Driven Marketing | Digital Marketing & Analytics |
| `MDDM-DS4M-EN` | Data-Driven Marketing | Data Science for Marketing |
| `MDDM-MI-EN` | Data-Driven Marketing | Marketing Intelligence |
| `MDDM-MRCRM-EN` | Data-Driven Marketing | Marketing Research & CRM |
| `MDSAA-BA-EN` | Data Science and Advanced Analytics | Business Analytics |
| `MDSAA-DS-EN` | Data Science and Advanced Analytics | Data Science |
| `MEGI-AGI-EN` | Statistics and Information Management | Data Analytics |
| `MEGI-AGR-EN` | Statistics and Information Management | Risk Analysis and Management |
| `MEGI-MRCRM-EN` | Statistics and Information Management | Marketing Research and CRM |
| `MGI-BI-EN` | Information Management | Business Intelligence |
| `MGI-GCBI-EN` | Information Management | Knowledge Management and Business Intelligence |
| `MGI-GSI-EN` | Information Management | Information Systems Management |
| `MGI-GSTI-EN` | Information Management | Information Systems and Technologies Management |
| `MGI-MI-EN` | Information Management | Marketing Intelligence |
| `MGI-TD-EN` | Information Management | Digital Transformation |
| `MGT-EN` | Geospatial Technologies (Erasmus Mundus), current official cover | |
| `MGT-2025-EN` | Geospatial Technologies, **proposal pending institutional confirmation** (2025 NOVA IMS identity) | |

Also set the matching text for the title page, for example:

```latex
\covercode{MDSAA-DS-EN}
\programme{Data Science and Advanced Analytics, with a specialization in Data Science}
\degreetype{msc}   % or phd for the Doctoral Program
```

The back cover follows the cover code: programmes with their own back cover use it, all others use the official 2025 NOVA IMS back cover (`Figures/Covers/back-2025.pdf`).

### Geospatial Technologies: current and proposed cover

Every NOVA IMS programme in the upstream template already has a cover in the identity NOVA IMS introduced in 2025, except Geospatial Technologies, which keeps the earlier Erasmus Mundus design. This template offers both:

- `\covercode{MGT-EN}`: the current official cover artwork and back cover, unchanged. The title is set in bold italic capitals and the author's name sits between two blue bars.
- `\covercode{MGT-2025-EN}`: a proposal in the 2025 identity, **pending confirmation by NOVA IMS**; use `MGT-EN` for submission until it is confirmed. It uses the official vector 2025 cover with the other programme's text removed, typesets "Master's Degree in Geospatial Technologies", adds a row of partner logos, and uses the official 2025 back cover.

The partner logos of the programme (Universitat Jaume I, Universität Münster, Erasmus+) are included in `Figures/Logos`. Switch them on together with the cover:

```latex
\covercode{MGT-2025-EN}
\programme{Geospatial Technologies}
\partnerlogos{Logos/uji,Logos/uni-muenster,Logos/erasmus-plus}
\partnerlogoscale{Logos/uji}{0.8}
```

All logos share one height and are centred in the row. `\partnerlogoscale` resizes a single logo so that the logos look equally prominent (1 = full height).

A missing logo file shows as a labelled empty box, so the document still compiles.

## Project structure

| Path | Purpose |
| --- | --- |
| `main.tex` | Main document and order of all parts. |
| `thesis-info.tex` | Title, author, student number, programme, supervisors, date, keywords, SDGs, cover. |
| `novaims-thesis.cls` | Layout: covers, title page, statement of integrity, Use of Generative AI table, copyright page, headings, margins, references. |
| `FrontMatter/` | Use of Generative AI table, dedication, acknowledgements, Abstract, Resumo, acronyms. |
| `Chapters/` | Chapters 1 to 6 (examples of citations and tables in Chapter 2). |
| `BackMatter/` | Declaration of Generative AI Use (off by default, see Optional pages). |
| `Appendices/` | Appendix A. Copy the file for more appendices. |
| `Bibliography/` | `references.bib` and optional citation key aliases. |
| `Figures/` | Your figures, official covers, partner logos (Geospatial Technologies), SDG icons. |
| `preview/` | Compiled example PDFs and cover overview for this README (not needed to compile). |
| `benchmark/` | Script that compares compile times with NOVAthesis (not needed to compile). |
| `MIGRATION.md`, `BENCHMARK.md` | Migration guide and compile-time comparison. |

## Settings

- **Font:** Arial/Helvetica 12 pt, as set in the NOVA IMS template. For 12 pt Times write `\documentclass[times]{novaims-thesis}`.
- **Page layout:** A4, margins 3 cm (top, bottom) and 3.25 cm (left, right), line spacing 1.15, as in the NOVA IMS template.
- **Citations:** `\citet{key}` gives Author (Year), `\citep{key}` gives (Author, Year). By default references are in APA author-year style with apacite and BibTeX, with "et al." from the first citation and DOIs as links.
- **Full APA 7 (optional):** `\documentclass[apa7]{novaims-thesis}` switches to biblatex with `style=apa` and Biber, the set-up NOVAthesis uses for NOVA IMS. It follows APA 7 completely (for example, up to 20 authors in a reference, where the default lists the first 6, "…" and the last). `\textcite` and `\parencite` are available as well as `\citet` and `\citep`. A full build takes about three times as long (see [BENCHMARK.md](BENCHMARK.md)); Overleaf runs Biber automatically.
- **Sustainable Development Goals:** `\sdgs{4,9}` prints the SDG icons under the abstract. `\sdgs{}` hides them.
- **Front matter:** after the cover, title page and copyright page come the Statement of Integrity (with space for a signature), Use of Generative Artificial Intelligence, Dedication, Acknowledgements, Abstract, Resumo, Index, Index of Tables, Index of Figures and the acronyms. From the Statement of Integrity on, the front matter pages are listed in the Index with roman page numbers, except the dedication. The title page shows the student number under the name (`\studentid{...}`; leave it empty to omit it).
- **Optional pages:** `\genaiusepage{false}` and `\dedicationpage{false}` in `thesis-info.tex` remove the Use of Generative AI table and the dedication. Fill the table in `FrontMatter/genai-use.tex` with one `\genairow{Task}{yes|no}{Tool}` line per task.
- **Generative AI: table or declaration.** The template has two forms of the same information: the Use of Generative Artificial Intelligence table in the front matter (`\genaiusepage`, on by default) and the longer Declaration of Generative AI Use chapter after the conclusion (`BackMatter/genai-declaration.tex`, switched by `\genaideclarationpage`, off by default). Use the form your programme asks for; switch both on only if it asks for both.
- **Supervisors and date:** one centred block per supervisor on the title page, `\supervisor{Name, PhD}{School\\University\\City, Country}` (and `\cosupervisor` in the same way). `\submissiondate[Day]{Month}{Year}` prints the full date; the day is optional.
- **Compile part of the thesis:** use the `\includeonly` line at the top of `main.tex`.
- **Engines:** pdfLaTeX (default), XeLaTeX and LuaLaTeX all work. Locally: `latexmk -pdf main.tex`.

## Differences from the upstream template and known limitations

- Only NOVA IMS. The files and code for other NOVAthesis schools are not included.
- English only. The fixed texts (title page, statement of integrity, copyright) are in English, and only the English covers are included. A Resumo in Portuguese is part of the front matter.
- The official covers use the Borna typeface, which is not included. Text typeset on the covers (title, author, and the programme name on `MGT-2025-EN`) uses Helvetica.
- The default reference style is apacite (based on APA 6) with "et al." set to the APA 7 rule. For full APA 7 use the `apa7` option, which compiles more slowly.
- No document stages (working, provisional, final) and no committee page; see [MIGRATION.md](MIGRATION.md).

## Credits and licence

The layout, front-matter wording and cover artwork come from the NOVA IMS thesis template 2025 by Paulo Vitor de Campos Souza (github.com/pdecampossouza/nova-ims-thesis-template-2025), which adapts the NOVAthesis template by João Lourenço (github.com/joaomlourenco/novathesis). This derived version is distributed under the LaTeX Project Public License 1.3c (see `LICENSE`). Cover artwork and logos remain the property of NOVA IMS and the partner institutions.
