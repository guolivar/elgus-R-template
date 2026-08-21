# R Analysis ... for El Gus

## Purpose

A very tailored version of [Matt Dray's great repo](https://github.com/matt-dray/analysis-template) to begin a simple analytical project with R and RStudio that fits in my workflow.

You should [read this blog post](https://www.rostrum.blog/2019/06/11/r-repo-template/) for a more in-depth explanation of the original repo.

## How to use

[Click here to open the page for copying the repo](https://github.com/guolivar/elgus-R-template/generate).

Feel free to fork or copy this and tweak it for your workflow.

## File tree
See individual `README.md` files in the folders for specific information but in general:
* Docker images go on `Docker/`
* Data go on `data/`
* External data go on `ext/`
* Human readable reports go on `docs/`
* Output data and plots go on `output/`
* **R** scripts go on `R/`
* **Python** scripts go on `python/`
* Credentials go on `secrets/` (never committed)
* **Docker** images go on `Docker/`

```
elgus-R-template/
├── .github/
│   └── copilot-instructions.md
├── data/
│   ├── README.md
├── Docker/
│   ├── README.md
├── docs/
│   ├── README.md
│   └── template-document-example.Rmd
├── ext/
│   └── README.md
├── output/
│   └── README.md
├── python/
│   └── README.md
├── R/
│   ├── functions.R
│   └── README.md
├── secrets/
│   └── README.md
├── AGENTS.md
├── CLAUDE.md
├── elgus-R-template.Rproj
├── GEMINI.md
└── README.md
```

## AI coding agents

`AGENTS.md` gives AI coding assistants a starting point for working on your analysis: the
repository layout, where generated files belong, code style and working practices.
`CLAUDE.md` (Claude Code), `GEMINI.md` (Gemini CLI) and `.github/copilot-instructions.md`
(GitHub Copilot) point at it, so edit `AGENTS.md` to modify their behaviour/approach.

When you start a project from this template, fill in the sections of `AGENTS.md` marked
_TODO_ — what the analysis is about, what the data are, and how to run the scripts. That
project-specific context is what makes an agent actually useful; the rest already matches
this structure and can be left alone.
