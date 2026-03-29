# Latex-Template-report

A clean, ready-to-use LaTeX report template aimed at university assignments and technical reports. It comes pre-configured with common packages for math, code listings, figures, bibliography (IEEE style), headers/footers, and PDF appendix support.

---

## Table of Contents

- [Features](#features)
- [File Structure](#file-structure)
- [Prerequisites](#prerequisites)
- [Getting Started](#getting-started)
  - [Overleaf](#use-in-overleaf)
  - [VS Code](#use-in-vs-code)
- [Customisation](#customisation)
- [Usage Guide](#usage-guide)
  - [Adding Images](#adding-images)
  - [Adding Code Listings](#adding-code-listings)
  - [Adding a PDF Appendix](#adding-a-pdf-appendix)
  - [Adding Bibliography Entries](#adding-bibliography-entries)
- [Included Packages](#included-packages)

---

## Features

- A4 paper with 1-inch margins
- Automatic table of contents
- IEEE-style bibliography via BibLaTeX + Biber
- Syntax-highlighted code listings
- Header with subject code, subject name, assignment number, and author
- Appendix chapters for source code and PDF attachments
- Timezone-aware date (defaults to `Australia/Brisbane`)

---

## File Structure

```
.
├── main.tex        # Main LaTeX source file
├── main.bib        # BibTeX bibliography database
├── latexmkrc       # latexmk configuration (sets timezone)
├── Image/          # Put your images here (create this folder)
└── PDF/            # Put your PDF appendices here (create this folder)
```

> **Note:** The `Image/` and `PDF/` folders are not tracked by Git. Create them manually before compiling.

---

## Prerequisites

### Overleaf
No local installation needed — Overleaf handles compilation in the cloud.

### VS Code (local)
| Requirement | Purpose |
|---|---|
| [TeX Live](https://www.tug.org/texlive/) (full installation recommended) | LaTeX compiler and packages |
| [LaTeX Workshop](https://marketplace.visualstudio.com/items?itemName=James-Yu.latex-workshop) VS Code extension | Build, preview, and IntelliSense |
| Biber (included with TeX Live) | Bibliography backend |

---

## Getting Started

### Use in [Overleaf](https://www.overleaf.com/project)

1. Create a new **blank** project in Overleaf (not from a template).
2. Upload or paste the contents of `main.tex` and `main.bib` into the editor.
3. Upload `latexmkrc` so Overleaf picks up the timezone setting.
4. Create a folder called `Image` for images.
5. Create a folder called `PDF` for PDF appendices.
6. Set the compiler to **LuaLaTeX** or **pdfLaTeX** and the bibliography tool to **Biber** in *Menu → Settings*.
7. Click **Compile** — you're ready to go!

### Use in VS Code

1. Install [TeX Live](https://www.tug.org/texlive/) and the [LaTeX Workshop](https://marketplace.visualstudio.com/items?itemName=James-Yu.latex-workshop) extension.
2. Clone or download this repository.
3. Create the `Image/` and `PDF/` folders inside the project root.
4. Open `main.tex` in VS Code and press `Ctrl+Alt+B` (or use the LaTeX Workshop sidebar) to build.
5. The compiled `main.pdf` will appear in the project root.

> **Tip:** LaTeX Workshop automatically runs `latexmk`, which reads `latexmkrc` and handles multiple compilation passes and Biber for you.

---

## Customisation

All personal and assignment details are defined near the top of `main.tex`. Change these six lines to match your details:

```latex
\def\myname{John Document}        % Your full name
\def\mySTDNum{n1123456789}        % Your student number
\def\subjectCode{EGB240}          % Subject/course code
\def\subjectName{Signal Analysis} % Subject/course name
\def\AssignmentNum{Assignment 1}  % Assignment label (e.g. "Lab Report 2")
\def\taskName{Problem Solving Task 1} % Full assignment title
```

These values are automatically used in the page header and on the title page.

To change the timezone for the date, edit `latexmkrc`:

```perl
$ENV{'TZ'}='Australia/Brisbane';  # Replace with your timezone
```

See the [PHP timezone list](https://www.php.net/manual/en/timezones.php) for valid timezone strings.

---

## Usage Guide

### Adding Images

1. Place your image file (e.g. `diagram.png`) inside the `Image/` folder.
2. In `main.tex`, use:

```latex
\begin{figure}[H]
    \centering
    \includegraphics[width=0.8\textwidth]{diagram}
    \caption{Your caption here.}
    \label{fig:diagram}
\end{figure}
```

For side-by-side figures, use the `subcaption` package (already included):

```latex
\begin{figure}[H]
    \centering
    \begin{subfigure}{0.45\textwidth}
        \includegraphics[width=\textwidth]{imageA}
        \caption{Left figure.}
    \end{subfigure}
    \hfill
    \begin{subfigure}{0.45\textwidth}
        \includegraphics[width=\textwidth]{imageB}
        \caption{Right figure.}
    \end{subfigure}
    \caption{Combined figure.}
\end{figure}
```

### Adding Code Listings

The template includes a pre-styled `lstlisting` environment. Use `\lstinputlisting` to pull in an external file:

```latex
\lstinputlisting[language=Python]{myScript.py}
```

Or embed code directly:

```latex
\begin{lstlisting}[language=Matlab, caption=My script]
x = 0:0.1:2*pi;
plot(x, sin(x));
\end{lstlisting}
```

Supported languages include `C`, `C++`, `Java`, `Python`, `Matlab`/`Octave`, `Bash`, and many more.

### Adding a PDF Appendix

1. Place your PDF (e.g. `datasheet.pdf`) inside the `PDF/` folder.
2. In the appendix section of `main.tex`, add:

```latex
\chapter{Datasheet}
\includepdf[pages={1-}]{PDF/datasheet.pdf}
```

Use `pages={1-5}` to include only specific pages, or `pages={-}` for all pages.

### Adding Bibliography Entries

1. Add your reference to `main.bib` (use [ZBib](https://zbib.org/) or [Google Scholar](https://scholar.google.com/) to generate BibTeX entries automatically).
2. Cite it in `main.tex` with `\cite{key}`, where `key` matches the identifier in your `.bib` entry.
3. The references section is printed automatically via `\printbibliography`.

Example `.bib` entry:

```bibtex
@article{doe_example_2024,
    author  = {Doe, Jane},
    title   = {An Example Article},
    journal = {Journal of Examples},
    year    = {2024},
    volume  = {1},
    pages   = {1--10},
}
```

---

## Included Packages

| Package | Purpose |
|---|---|
| `geometry` | Page size and margins |
| `graphicx` | Inserting images |
| `subcaption` | Side-by-side figure captions |
| `appendix` | Appendix chapters |
| `amsmath` | Mathematical equations |
| `pdfpages` | Importing PDF files |
| `fancyhdr` | Custom headers and footers |
| `verbatim` | Verbatim text blocks |
| `color` | Custom colours |
| `babel` / `csquotes` | Language and quotation support |
| `datetime2` | Date/time formatting with timezone support |
| `ragged2e` | Text alignment (useful in tables) |
| `dirtytalk` | Smart quotation marks (`\say{}`) |
| `listings` | Syntax-highlighted code listings |
| `multirow` | Multi-row cells in tables |
| `float` | `[H]` float placement for figures/tables |
| `wrapfig` | Text-wrapped figures |
| `hyperref` | Clickable cross-references and links |
| `biblatex` (IEEE) + Biber | Reference management and bibliography |
| `ulem` | Underline and decorative rules |

---

## License

This project is licensed under the terms of the [LICENSE](LICENSE) file included in this repository.
