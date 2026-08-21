# AGENTS.md

Instructions for AI coding agents working on this project. This is the canonical file;
`CLAUDE.md`, `GEMINI.md` and `.github/copilot-instructions.md` point here.

> **Fill this in.** The sections below marked _TODO_ describe your specific analysis and
> are the main thing that makes an agent useful here. Everything else already matches the
> repository structure and can be left as-is.

## The project

_TODO — replace with a few sentences: what question this analysis answers, who it is for,
and what the final product is (a report in `docs/`, a dataset in `output/`, a figure set)._


## Layout and where things go

This project follows the [elgus-R-template](https://github.com/matt-dray/analysis-template)
structure. Each folder has a `README.md` with more detail.

| Path      | Contents |
|-----------|----------|
| `data/`   | Raw data for this analysis. **Read-only** — never modify or overwrite files here. |
| `ext/`    | External inputs not generated for this analysis (reference data, models). Also read-only. |
| `R/`      | R scripts. `functions.R` holds shared function definitions. |
| `python/` | Python scripts. |
| `docs/`   | R Markdown reports and their rendered outputs (HTML, PDF, docx). |
| `output/` | Processed data, plots and other generated products. Figures go in `output/plots/`. |
| `Docker/` | One subfolder per image. Files must be **copied** into the image folder, not symlinked. |
| `secrets/` | Credentials and tokens. Ignored by git apart from its `README.md`. |

Rules:

- Never write generated artefacts into `data/` or `ext/`. Everything produced by a script
  goes to `output/`; anything human-readable goes to `docs/`.
- Scripts are grouped by purpose (read, tidy, model, plot...) and the filename implies the
  run order: `01_read.R`, `02_tidy.R`, ... Same convention in `python/`.
- Later steps read the intermediate products of earlier ones from `output/` rather than
  re-deriving them, so any single step can be re-run on its own.
- `.Rmd` files in `docs/` should not carry substantial new analysis — that lives in `R/`
  and is sourced or read from `output/`. Follow Emily Riederer's
  [R Markdown-driven development](https://emilyriederer.netlify.com/post/rmarkdown-driven-development/).

## Code style

R:

- Two spaces for indentation, no tabs, UTF-8 (matches the `.Rproj` settings).
- Follow the [tidyverse style guide](https://style.tidyverse.org/): `snake_case` names,
  `<-` for assignment, spaces around infix operators, lines under ~80 characters.
- Load packages with `library()` at the top of a script. Do not use `install.packages()`,
  `setwd()`, or `rm(list = ls())` in committed code.
- Use paths relative to the project root (the RStudio project working directory), e.g.
  `"data/raw.csv"`. `here::here()` is fine if the project already uses **here**.
- Reusable functions belong in `R/functions.R`, sourced by the scripts that need them.
  Give each a short roxygen-style comment block describing arguments and return value.
- Prefer the idioms already used in the project's scripts (base vs tidyverse, **data.table**
  vs **dplyr**) over introducing a second way of doing the same thing.

Python:

- PEP 8, 4-space indentation, `snake_case`.
- Paths relative to the project root, same as R.

## Working practices

- Read the relevant script in `R/` or `python/` before changing it — the analysis steps are
  sequential and a change early in the chain affects everything downstream.
- Adding a package dependency is a real decision: mention it rather than slipping it in.
- Analysis results are the deliverable. Do not adjust parameters, filters or thresholds to
  make a result look better, and report what the numbers actually show — including when a
  result is null, noisy, or contradicts the expected answer.
- If a script fails or a check could not be run, say so plainly with the error rather than
  implying it passed.
- Read credentials from `secrets/` at runtime (see `secrets/README.md`). Never hard-code a
  key in a script, and never print one to the console or into a knitted report.
- Do not commit data, credentials or rendered outputs. `.gitignore` excludes `.Rhistory`,
  `.RData`, `.Rproj.user/`, caches, `secrets/` and any file matching `_secret*`.
- Do not run `git commit`, `git push`, or create branches unless explicitly asked.
- Keep the file tree in the root `README.md` accurate when adding or removing files.

## Checks

_TODO — replace if the project gains tests or CI._

There is no test suite. Before declaring work done:

- R scripts should at least parse: `Rscript -e 'invisible(parse("R/<file>.R"))'`.
- Re-run the affected script end to end and confirm the expected files appear in `output/`.
- Reports should knit: `Rscript -e 'rmarkdown::render("docs/<file>.Rmd")'`.
