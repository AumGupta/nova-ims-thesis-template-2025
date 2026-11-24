# Benchmark results

Median of 3 runs per variant. Engine: pdfLaTeX.

| Variant | Full build (s) | One pass (s) | Pages | latexmk OK |
| --- | --- | --- | --- | --- |
| novathesis | 35.4 | 6.7 | 48 | yes |
| lean | 6.1 | 0.9 | 53 | yes |
| lean-apa7 | 18.2 | 3.8 | 53 | yes |

## Environment

- pdfTeX: pdfTeX 3.141592653-2.6-1.40.25 (TeX Live 2023/Debian)
- Biber: biber version: 2.19
- BibTeX: BibTeX 0.99d (TeX Live 2023/Debian)
- latexmk: Latexmk, John Collins, 31 Jan. 2024. Version 4.83
- OS: Linux-6.18.44-fc-v726-x86_64-with-glibc2.39
- CPU: Intel(R) Xeon(R) Processor @ 2.10GHz
- CPU cores: 2
