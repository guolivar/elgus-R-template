# GEMINI.md

Guidance for Gemini CLI when working on this project.

The project instructions live in [AGENTS.md](AGENTS.md) — read that file and follow it.
It describes the analysis, the data, how to run the scripts, the repository layout, code
style, and the checks to run before finishing.

Notes:

- The analysis steps in `R/` (and `python/`) run in filename order and pass intermediate
  products through `output/`. Read the surrounding scripts before changing one.
- `data/` and `ext/` are read-only inputs. Generated files go in `output/` or `docs/`.
- Do not commit or push unless asked.
