# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/).
From 2022-02-28 onwards, versioning is done using [Calendar Versioning](https://calver.org/).

## [2026-10-19]

### Added

- References show the DOI (`IEEEtranN-doi.bst`). [#18](https://github.com/latextemplates/ieee-enhanced/issues/18)
- A section written in plain Markdown (`content-markdown.md`; LuaLaTeX).
- VS Code: [markdownlint](https://marketplace.visualstudio.com/items?itemName=DavidAnson.vscode-markdownlint) recommended, configured by `.markdownlint.yml`.
- VS Code: LTeX+ knows the words of the aspell word lists (`.vscode/ltex.dictionary.<language>.txt`).
- `make dictionaries` merges the word lists of aspell, LTeX+, and TeXtidote.
- CI: after a push that changes a word list, the workflow `Dictionaries` runs `make dictionaries` and commits the merged word lists.
- CI: [typos](https://github.com/crate-ci/typos) checks the spelling, also in comments (configured in `.typos.toml`).

### Changed

- References: repeated author names are written out instead of a dash, as in the current [IEEE Reference Guide](https://journals.ieeeauthorcenter.ieee.org/wp-content/uploads/sites/7/IEEE_Reference_Guide.pdf).
- Citation ranges are written out (`[1], [2], [3]` instead of `[1]–[3]`), as the [IEEE Reference Guide](https://journals.ieeeauthorcenter.ieee.org/wp-content/uploads/sites/7/IEEE_Reference_Guide.pdf) (V 3.28.2025) now asks for.
- References in the text as the [IEEE Editorial Style Manual](https://journals.ieeeauthorcenter.ieee.org/your-role-in-article-production/ieee-editorial-style-manual/) asks for: "Fig. 1" (also at the beginning of a sentence), "(1)" for equations ("Equation (1)" at the beginning of a sentence).
- Captions read "Fig. 1." (babel had changed them to "Figure 1.").
- `paper.tex` keeps the caption style of the document class, as `paper-basic-listings.tex` does (the `caption` package is no longer loaded).
- The example tables are tables (caption "TABLE I" above) instead of figures.
- Lines in minted listings are labeled with `\label` and referenced with `\zcref` like everything else (`\labelline` and `\refline` removed).
- Markdown example: "a whole section" instead of "a longer part".
- CI: aspell, textlint, and TeXtidote also check the Markdown files.
- CI and `make spellcheck`: aspell and TeXtidote run in the [Docker image by DANTE e.V.](https://hub.docker.com/r/danteev/texlive).
- README.md: FAQ on adding words (e.g., names of tools) to the spell checkers.
- README.md: how to run the `make` targets in Docker without a local `make`.
- README.md: "Disabled features" is a subsection of "Benefits".
- README.md: differences to the IEEEtran package on CTAN.
- README.md: markdownlint findings fixed.

### Removed

- `paper.spell.good`: word list of a former spell check, no longer used.

### Fixed

- Typos fixed, mostly in comments; German comments in the English files translated.

## [2026-10-16]

### Added

- [TeXtidote](https://github.com/sylvainhalle/textidote) checks spelling, grammar, and style (configuration `.textidote`, `make spellcheck-textidote`), for English documents in CI.
- VS Code: [JabRef 4 VSCode](https://marketplace.visualstudio.com/items?itemName=jabref.jabref-4-vscode) recommended.

### Changed

- `paper.tex` uses minted; the variant using the listings package is `paper-basic-listings.tex`.
- README.md: minted FAQs merged and moved up.
- `make spellcheck` runs all spell checkers (`make aspell` is now `make spellcheck-aspell`).
- GitHub workflows: actions pinned to commit SHAs.

### Fixed

- Example texts: spelling and grammar fixed.
- Makefile: `.PHONY` lists all targets; `make spellcheck-aspell` and `make showundef` work.

## [2026-10-15]

### Added

- The LaTeX hints show how to color table rows and cells (`\rowcolor`, `\cellcolor`). [scientific-thesis-template#87](https://github.com/latextemplates/scientific-thesis-template/pull/87)
- `make log` shows the relevant messages of the LaTeX log (texlogsieve).
- `paper.tex` shows how to produce a self-archiving version (`authorarchive`, commented out).

### Changed

- `make format` (and thus CI) indents all main files (`paper*.tex`), not only `MASTER_TEX`.
- VS Code: the recommended extension is `james-yu.latex-workshop` (`manhen.latex-workshop-2` was removed from the stores).
- VS Code: the background of the PDF viewer follows the light or dark theme.
- Dependabot groups all GitHub Actions updates into one weekly PR.
- `check.yml` pins all GitHub Actions to commit SHAs.
- README.md: sections reordered.
- README.md: on Overleaf, select TeX Live 2026.
- README.md: passages in another language are an FAQ.
- README.md: links the decision records of the template generator.
- README.md: "Usage with docker" merged into "Docker-based (recommended)".
- Embedding the `.bib` file into the PDF is opt-in.
- `.latexmkrc` replaces `_latexmkrc`; it works on Overleaf, too.
- `make` runs the LaTeX tools in the Docker image (`make LOCAL=1` runs them locally).
- `vscode.settings.json` contains the Docker settings of LaTeX Workshop and does not build on save.
- README.md: compilation hints consolidated in "LaTeX compilation".
- minted compiles without `--shell-escape`.

### Fixed

- The README links the `figures/` directory, and `.dockerignore` excludes the generated `figures/*.pdf_tex` files. [generator-latex-template#586](https://github.com/latextemplates/generator-latex-template/pull/586)
- The `.markdown.in` file of the markdown package is ignored by git and removed by `latexmk -c`.
- README.md: the download link points to this repository.
- textlint ignores expl3 function names, Markdown reference IDs, and the name of the markdown package.
- `make view` opens the PDF on Linux and macOS.
- README.md: the self-archiving FAQ points to the example in `paper.tex`.
- `vscode.settings.json`: the recipes run `lualatex` (resp. `pdflatex`) with the right bibliography tool.

## [2026-10-14]

### Added

- The LaTeX hints show how to write text in Markdown using the [markdown](https://ctan.org/pkg/markdown) package - easing the start for LaTeX newcomers. The example is shown when compiling with LuaLaTeX; with pdfLaTeX, a hint is shown instead. The package's cache directory (`_markdown_*/`) is ignored by git. Markdown references such as `<#tbl:markdown>` typeset the type name and the number ("Table 1").
- The header of the main file states in which lines `\begin{document}` and the first heading are, so the content is found without scrolling through the long preamble.

### Changed

- The README uses the TeX Live image of the Island of TeX directly (also in the VS Code setting `latex-workshop.docker.image.latex`) - building an own image `ltg` is no longer needed. The commands to compile in the container are copy-and-paste ready for Windows (PowerShell and Command Prompt), Linux, and macOS.
- The README's tool hints distinguish a Docker-based setup (recommended) from a traditional installation: the [TeX Live image by the Island of TeX](https://gitlab.com/islandoftex/images/texlive) works the same on Windows, macOS, and Linux and makes `minted` work without a separate Python setup. The "Usage with docker" section and the VS Code hints (LaTeX Workshop can compile in the container) are linked from there.

## [2026-10-08]

### Added

- The `Check` workflow has a `textlint` job that reports weakening words (e.g., "clearly", "just") in the English `.tex` files as annotations, without failing the build ("only" is allowed). Configure it in `.textlintrc.json`; the README shows how to run it locally.
- A commented-out `\pagestyle{plain}` after `\maketitle` adds page numbers for submissions, reviews, and non-IEEE use; keep it off for the IEEE camera-ready version. The README explains how to use the template for a term paper at Technische Hochschule Ulm (THU).
- The figure examples show how to include a JPEG photo (`figures/ulm-minster.jpg`, CC0 from Wikimedia Commons).
- The "Related Work" section points to [ScienceOS](https://www.scienceos.ai/) (EU-hosted) for searching related work and to writing hints in [Student Thesis Projects](https://vdf.ch/product/student-thesis-projects-en.html) and [Writing for Computer Science](https://doi.org/10.1007/978-1-4471-6639-9); each title is a clickable link, and its URL is also given in a footnote.

### Changed

- Cross-references use [zref-clever](https://ctan.org/pkg/zref-clever) instead of [cleveref](https://ctan.org/pkg/cleveref), because zref-clever works with tagged (accessible) PDFs: write `\zcref{...}` instead of `\cref` and, at the start of a sentence, `\Zcref{...}` (short for `\zcref[S]{...}`) instead of `\Cref`.
- `_latexmkrc` is organized in sections and lists commented-out alternatives for continuous preview (`-pvc`), the job name, and the PDF viewer (e.g., evince).
- The example and paper-structure texts avoid words that textlint's `write-good` rule flags (`Finally`, `rarely`, `a few`, `just`), so a fresh paper has no textlint annotations. A sentence-initial `Finally,` is allowed in `.textlintrc.json`, because it marks a sequence rather than weakening a statement.
- The paragraph example links Andrew Stacey's *Document Revision System* by title with the URL in a footnote, and the hyphenation example shows the short `\verb` snippets `\allowbreak{}` and `"=` instead of whole words, so that neither runs out of a narrow column.

### Fixed

- The sub-figure examples no longer overlap the "Corresponding LaTeX code" box in the `minted` variant: their `figure*` is placed at the top of the page (`[!t]`, as in IEEEtran's `bare_conf.tex`) instead of the bottom, and the code boxes break across columns and pages instead of overflowing when the floats of a page leave the columns too little room.
- The two columns of the last page are balanced by the [flushend](https://ctan.org/pkg/flushend) package, also when the text ends in the first column. Before, the `balance` package was loaded but never used, and a `\balance` added by hand failed with "You have called `\balance` in second column" whenever the text reached the second column. The README explains how to switch balancing off or do it by hand with `\IEEEtriggeratref`. [#24](https://github.com/latextemplates/ieee-enhanced/issues/24)
- The "Corresponding LaTeX code" listing of the diagonal-table example (`diagbox`) no longer runs out of the column: the table has a short first cell, so latexindent's column alignment pads the rows less.
- Long code lines without spaces (e.g., `\includegraphics[width=.4\linewidth]{example-image-a}`) in the "Corresponding LaTeX code" boxes of the `listings` variant are wrapped instead of running out of the box.
- Fixed typos in the example and writing-hint texts.
- `latexmk -pv` opens the PDF on Linux and macOS: the SumatraPDF viewer is only configured on Windows.

## [2026-07-30]

### Added

- The Overleaf note now states the template is based on TeX Live 2025 (was 2024), matching Overleaf's current TeX Live.
- The README now links the [latex-snippets site](https://latextemplates.github.io/latex-snippets/) near the top, so you can inspect the source snippets this template is assembled from.
- Soft-wrapped lines in code listings now show a gray hook arrow (↪) at the start of each continuation line, so they are distinguishable from real line breaks; the arrow is not copied when you select the code from the PDF.
- The "Examples" section with the rendered example-PDF links now appears right below the title, before "Usage", so you see the output first.
- Opt-in rectangular ("block") paragraphs: uncomment `\rectangularparagraphstrue` in the preamble to stretch every paragraph's last line to the full column width (off by default; see the comment in `paper.tex` for the copy-fitting trade-off).
- LuaLaTeX builds avoid a lone short word as the last line of a paragraph (`impnattypo` with its `lastparline` feature; pdfLaTeX builds are unaffected). [lncs-enhanced#16](https://github.com/latextemplates/lncs-enhanced/issues/16)
- The compiled PDF now embeds `paper.bib`, so the reference data can be extracted from the PDF (e.g., with JabRef).

### Fixed

- arXiv uploads no longer fail with "! I can't find file `clmr28t10+20`": `paper.tex` now starts with `\ifdefined\pdfoutput\pdfoutput=1\fi`, which makes arXiv use `pdflatex` instead of DVI-producing `latex`. See the README section "Final submission". [lncs-enhanced#44](https://github.com/latextemplates/lncs-enhanced/issues/44)

## [2026-06-30]

### Added

- Inline acronym typesetting with `\initialism` (and the ready-made `\OMG`, `\BPEL`, `\BPMN`, `\UML`) now works — the required `lccaps` package is now loaded — demonstrated by a new example in the "LaTeX Hints" chapter.

## [2026-06-25]

### Added

- New example sections in the "LaTeX Hints" chapter: Formulas and Equations, Figures with TikZ, and Plots with pgfplots.

## [2025-04-11]

### Added

- Added support to use `lualatex-dev`.
- Added more words to personal aspell dictionary.
- Added support for TeXLive 2025.

### Fixed

- Fixed utf-8 marking in generated `.aspell-en.pws`.

## Removed

- Removed support for TeXLive 2023.

## [2025-03-04]

### Changed

- Switched from `paper-conference*` to `paper-*` as keeping `-conference` increases maintenance effort.

## [2025-02-12]

### Fixed

- `pdflatex` run works again if both lualatex and pdflatex are used.

## [2025-01-31]

### Changed

- Renamed to `ieee-enhanced` to show that this an enhanced version of the existing template [IEEEtran](https://ctan.org/pkg/ieeetran)
- Removed `paper.tex` (because it is a duplicate of `paper-conference.tex`)

### Added

- Added `commands.tex` to collects all LaTeX macros / commands for a better overview on available (custom) LaTeX commands.

## [2025-01-25]

### Added

- Added [TeXcount](https://app.uio.no/ifi/texcount/index.html) to GitHub workflow summary.
- GitHub workflow job summary for `latexmk` generated using [texlogsieve](https://ctan.org/pkg/texlogsieve).

### Changed

- Refined `README.md`
- Refined `.gitignore`

## [2025-01-20]

### Added

- Added `.aspell.en.pws` and `.aspell.conf` to ignore some LaTeX commands at aspell.
- Added `latexindent` to GitHub actions (`check.yml`).
- When using lualatex: Added support for [spelling](https://www.ctan.org/pkg/spelling) package (which highlights bad spellings in red - if `.spell.bad` containing misspelled words exists)

### Fixed

- Fixed tag for iot Docker image.

### Changed

- Refined `Makefile`

## [2025-01-14]

### Changed

- Compilation with both lualatex and pdflatex is possible. Defaults to lualatex.
- Nicer gray scale for `minted` listings.
- `Dockerfile` switched to [Island of TeX's docker image](https://gitlab.com/islandoftex/images/texlive#tex-live-docker-image) to enable easy addition of new LaTeX packages.

## [2022-06-06]

### Added

- Magic comment for [LTeX](https://github.com/valentjn/vscode-ltex#ltex-extension-for-vs-code-grammarspell-checker-using-languagetool-with-support-for-latex-markdown-and-others) (because of [vscode-ltex#632](https://github.com/valentjn/vscode-ltex/issues/632))

### Changed

- `_latexmkrc` is available instead of `latexmkrc` to ease usage at overleaf. [lncs#40](https://github.com/latextemplates/lncs-enhanced/issues/40)

### Fixed

- Fixed reference to examples in IEEE template
- Fixed line break in introduction

## [2022-02-28]

### Added

- Added package [mindflow](https://www.ctan.org/pkg/mindflow), which supports quickly noting down thoughts with a) a proper rendering of LaTeX and b) a proper differentiation from the main text

### Removed

- Removed `paper-conference-compsoc.tex` as the option `compsoc` is not in use any more.
- Removed `paper-9pt-technote.tex` as that format is not used at all.

### Changed

- Now generated using the [latex template generator](https://www.npmjs.com/package/generator-latex-template).
- Updated to TeXLive 2021
- Switch from [balance](https://ctan.org/pkg/balance) to [pbalance](https://ctan.org/pkg/pbalance), because the latter works better in edge cases.

### Fixed

- Examples now also work on overleaf. `\currfile` now correctly returns `main.tex`/`paper.tex` instead of `output.tex`.

## [1.5.0] – 2020-03-29

### Fixed

- Fixed compatibility with recent babel versions: using `main=english` as package parameter.

## [1.4.0] – 2018-03-07

### Added

- Added "aboveskip" and "belowskip" hints.
- Added example Java listing using minted.
- Added example XML listing using listings.

### Changed

- Changed minted style from friendly to bw.

## [1.3.0] – 2018-03-06

### Added

- Added optional tweak to reduce spacing between bibitems
- Added `crefname` for `lstlisting` to ensure cleveref works

### Changed

- Removed `chngcntr`, because lsitings package counts right in the case of IEEE.
- Separated minted support to separate file `paper-conference-minted.tex`.

## [1.2.0] – 2018-02-07

### Changed

- Ligatures are disabled for monospaced font. E.g., \texttt{--} stays `--` and is not converted to an en dash.

## [1.1.0] – 2018-02-03

### Fixed

- Title of `paper-conference.tex` does not show "Computer Society" any more.

### Added

- One more lipsum paragraph on first page and separate Lorem Ipsum section.
- Enforce version V1.8b (2015/08/26) of [IEEEtrans.cls](https://www.michaelshell.org/tex/ieeetran/).

### Changed

- Removed `tracking=smallcaps` option in microtype to have letters in `\textsc{BPMN}` standing closer together.
- Instead of package [cite](https://www.ctan.org/pkg/cite) the more comprehensive package [natbib](https://www.ctan.org/pkg/natbib) is used. Thereby, `\citet{ref}` is enabled.

### Removed

- Removed wrong `\allowbreak{}` example.

## [1.0.0] – 2018-01-30

First release using semantic versioning.

[Unreleased]: https://github.com/latextemplates/ieee-enhanced/compare/2026-10-19...HEAD
[2026-10-19]: https://github.com/latextemplates/ieee-enhanced/compare/2026-10-16...2026-10-19
[2026-10-16]: https://github.com/latextemplates/ieee-enhanced/compare/2026-10-15...2026-10-16
[2026-10-15]: https://github.com/latextemplates/ieee-enhanced/compare/2026-10-14...2026-10-15
[2026-10-14]: https://github.com/latextemplates/ieee-enhanced/compare/2026-10-08...2026-10-14
[2026-10-08]: https://github.com/latextemplates/ieee-enhanced/compare/2026-07-30...2026-10-08
[2026-07-30]: https://github.com/latextemplates/ieee-enhanced/compare/2026-06-30...2026-07-30
[2026-06-30]: https://github.com/latextemplates/ieee-enhanced/compare/2026-06-25...2026-06-30
[2026-06-25]: https://github.com/latextemplates/ieee-enhanced/compare/2025-04-11...2026-06-25
[2025-04-11]: https://github.com/latextemplates/ieee-enhanced/compare/2025-03-04...2025-04-11
[2025-03-04]: https://github.com/latextemplates/ieee-enhanced/compare/2025-02-12...2025-03-04
[2025-02-12]: https://github.com/latextemplates/ieee-enhanced/compare/2025-01-31...2025-02-12
[2025-01-31]: https://github.com/latextemplates/ieee-enhanced/compare/2025-01-25...2025-01-31
[2025-01-25]: https://github.com/latextemplates/ieee-enhanced/compare/2025-01-20...2025-01-25
[2025-01-20]: https://github.com/latextemplates/ieee-enhanced/compare/2025-01-14...2025-01-20
[2025-01-14]: https://github.com/latextemplates/ieee-enhanced/compare/2022-06-06...2025-01-14
[2022-06-06]: https://github.com/latextemplates/ieee-enhanced/compare/2022-02-28...2022-06-06
[2022-02-28]: https://github.com/latextemplates/ieee-enhanced/compare/1.5.0...2022-02-28
[1.5.0]: https://github.com/latextemplates/ieee-enhanced/compare/1.4.0...1.5.0
[1.4.0]: https://github.com/latextemplates/ieee-enhanced/compare/1.3.0...1.4.0
[1.3.0]: https://github.com/latextemplates/ieee-enhanced/compare/1.2.0...1.3.0
[1.2.0]: https://github.com/latextemplates/ieee-enhanced/compare/1.1.0...1.2.0
[1.1.0]: https://github.com/latextemplates/ieee-enhanced/compare/1.0.0...1.1.0
[1.0.0]: https://github.com/latextemplates/ieee-enhanced/releases/tag/1.0.0

<!-- markdownlint-disable-file MD024 MD033 -->
