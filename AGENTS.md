# Repository Guidelines

## Project Structure & Module Organization

This repository contains OpenBioMaps documentation rather than application code. Official, language-specific Sphinx projects live under `official_docs/<language>/` (`en`, `hu`, `ro`, `ru`, and partially populated `es`, `fr`, and `pt`). Each project keeps its pages in `.rst` or `.md` files, navigation in `index.rst`, settings in `conf.py`, images in `images/`, and theme resources in `_static/` and `_templates/`. Community-maintained manuals and their supporting images belong in `user_contributed_docs/`. Do not commit generated `official_docs/*/_build/` content.

## Build, Test, and Development Commands

Run commands from the language directory you changed:

```bash
cd official_docs/en
make html
make linkcheck
make clean
```

`make html` renders the site into `_build/html`; open that output locally to review navigation, formatting, and images. `make linkcheck` validates external and internal links. `make clean` removes generated output. For a language directory without a Makefile, use `sphinx-build -b html official_docs/es official_docs/es/_build/html`. The build requires Sphinx plus the extensions configured in `conf.py`, notably `m2r2` and `sphinxcontrib.srclinks`.

## Writing Style & Naming Conventions

Write concise, task-oriented documentation in the target directory's language. Follow surrounding reStructuredText or Markdown style; preserve heading hierarchy and use relative links and image paths. Name new topic files with lowercase `snake_case` (for example, `data_access.rst`) and add them to the relevant `index.rst` toctree. Use four spaces for Python changes in `conf.py` and extension modules. Keep translations structurally aligned with the English documentation where practical.

## Testing Guidelines

There is no separate automated test suite. Treat a warning-free Sphinx build and link check as the validation baseline. Build every language affected by a shared template, extension, or asset change. Manually inspect rendered pages after navigation, CSS, image, or cross-reference edits.

## Commit & Pull Request Guidelines

Recent history favors short, imperative subjects such as `Update docker.md`; make subjects more specific when possible, for example `Document email queue setup`. Keep each commit focused on one documentation concern. Pull requests should identify affected languages and pages, summarize user-visible changes, and report build/link-check results. Link the relevant issue and include screenshots when rendered layout or styling changes.
