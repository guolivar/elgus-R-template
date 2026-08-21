# GitHub Copilot instructions

This repository holds a data analysis project in R (and Python), built with RStudio. Full
instructions — including what the analysis is about and how to run it — are in
[`AGENTS.md`](../AGENTS.md); the essentials are repeated here.

## Where code and files go

- `data/` — raw data for this analysis, treated as **read-only**.
- `ext/` — external inputs not generated for this analysis; also read-only.
- `R/` — R scripts; `R/functions.R` holds shared function definitions.
- `python/` — Python scripts.
- `docs/` — R Markdown reports and their rendered outputs.
- `output/` — processed data and generated products; figures in `output/plots/`.
- `Docker/` — one subfolder per image, with files copied in rather than linked.
- `secrets/` — credentials and tokens; ignored by git apart from its `README.md`.

Never write generated files into `data/` or `ext/`. Script filenames imply run order —
`01_read.R`, `02_tidy.R`, and so on — and each step reads the previous step's output from
`output/` rather than re-deriving it.

## Style

- R: two-space indent, UTF-8, [tidyverse style guide](https://style.tidyverse.org/),
  `snake_case`, `<-` for assignment, `library()` calls at the top of the script.
- Python: PEP 8, four-space indent, `snake_case`.
- Use paths relative to the project root; no `setwd()`, `install.packages()` or
  `rm(list = ls())` in committed code.
- Reusable R functions go in `R/functions.R` with a short roxygen-style comment block.
- `.Rmd` files in `docs/` present results; the analysis itself belongs in `R/`.
- Match the idioms already used in the project rather than introducing a second style.

## Conventions

- Every folder carries a `README.md` describing its purpose.
- Update the file tree in the root `README.md` when adding files or folders.
- Read credentials from `secrets/` at runtime; never hard-code a key or token in a script,
  and never print one to the console or into a report.
- Never suggest committing data, credentials or rendered outputs.
