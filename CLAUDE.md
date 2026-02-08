# CLAUDE.md

## ONE-PAGE RULE (MANDATORY)

The résumé MUST be exactly one page at all times. This rule is non-negotiable and applies after every change. After adding or modifying any content, verify the compiled PDF is still one page. If it spills onto a second page:

1. First, try compacting: reduce bullet points, shorten descriptions, remove unnecessary content.
2. As a last resort, remove the earliest (oldest) experience entry from `experience.tex`.

Never commit a résumé that exceeds one page.

## Project Overview

LaTeX resume for Joel Bandi. Compiles to PDF using XeLaTeX inside Docker. No CI/CD, no tests, no deployment pipeline — just source `.tex` files that produce `resume.pdf`.

## Tech Stack

- **LaTeX** (XeLaTeX) with custom document class (`base.cls`)
- **Docker** for builds (`aergus/latex` image)
- **Fonts:** Lato (TTF) and Raleway (OTF) in `fonts/`

## File Structure

```
resume.tex        # Main document — imports all sections
base.cls          # Custom LaTeX class (layout, commands, fonts, colors)
title.tex         # Name and contact info
experience.tex    # Work experience (reverse chronological)
education.tex     # Education (currently commented out in resume.tex)
skills.tex        # Technical skills by category
links.tex         # Professional links (not currently imported)
index.html        # Browser PDF viewer wrapper
resume.pdf        # Compiled output (tracked in git)
makefile          # Single target: `make up` → docker-compose up
docker-compose.yml
fonts/            # Lato and Raleway font files
```

## Build

```sh
docker-compose up
# or
make up
```

This runs `xelatex resume.tex` inside the Docker container and outputs `resume.pdf`.

## Key LaTeX Commands (defined in base.cls)

| Command | Purpose |
|---|---|
| `\namesection{first}{last}{contact}` | Page header with name and contact links |
| `\runsubsection{title}` | Company/institution name |
| `\descript{text}` | Job title or degree |
| `\location{text}` | Date range and location |
| `\sectionsep` | Vertical spacing between entries |
| `\tightemize` | Compact bullet list environment |
| `\lastupdated` | Auto "Last Updated" date in top-right |

## Conventions

- **Modular sections:** Each resume section lives in its own `.tex` file and is imported via `\input{}` in `resume.tex`. Comment out the `\input` line to hide a section.
- **Reverse chronological order** for experience entries.
- **Entry pattern:** `\runsubsection` → `\descript` → `\location` → `\tightemize` bullets → `\sectionsep`.
- **Colors** are defined as hex values in `base.cls`: primary `#2b2b2b`, headings `#6A6A6A`, subheadings `#333333`, date `#666666`.
- `resume.pdf` is committed to git so the latest version is always available without building.

## Dev Workflow

1. **Make changes** to the `.tex` source files.
2. **Run `make up`** to compile the PDF via Docker.
3. **Inspect `resume.pdf`** and confirm everything looks correct (layout, spacing, content).

Always run `make up` and verify the output before committing or opening a PR. Since `resume.pdf` is tracked in git, every commit should include a freshly compiled PDF that matches the source.

## Adding a New Experience Entry

```latex
\runsubsection{Company Name}
\descript{| Job Title}
\location{Start – End | City, State}
\begin{tightemize}
    \item Achievement or responsibility
\end{tightemize}
\sectionsep
```

Add it at the top of `experience.tex` (most recent first).
