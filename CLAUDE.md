# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Personal academic website built with Jekyll using the [al-folio](https://github.com/alshedivat/al-folio) theme. The site includes pages for blog posts, publications, projects, books, CV, and more. This will be a personal website for Leonard Hinckeldey and RL researcher and PhD student at the university of edinburgh. The plan is to have a landing page with a short bio, links to github, scholar, twitter etc. Some recent news (scrollable element that has the 5 newest items shown). some selected publications. Now for the news and publications we also want to have some separate tabs i.e. selected publications is a subset of all the publications shown on the publications page. Lastly we also want a CV tab where the CV ca be downloaded as a PDF or viewed neatly on the website. We want dark mode and light mode.  

## Development Commands

### Local development with Docker (recommended)
```bash
docker compose up          # Serves at http://localhost:8080 with live reload
docker compose up --build  # Rebuild the image before starting
```

### Local development without Docker
```bash
bundle install             # Install Ruby dependencies
bundle exec jekyll serve   # Serve locally (default port 4000)
```

### Formatting
```bash
npx prettier --check .     # Check formatting (Liquid, HTML, JS, CSS, YAML, JSON)
npx prettier --write .     # Auto-fix formatting
```

Prettier is configured with `@shopify/prettier-plugin-liquid`, 150 char print width, and ES5 trailing commas.

### Pre-commit hooks
Uses `pre-commit` with hooks for trailing whitespace, end-of-file fixing, YAML validation, and large file checks.

## Architecture

### Jekyll Structure
- **`_config.yml`** — Central configuration: site metadata, theme settings, collections, plugin config, scholar settings, social links. Most site-wide behavior is controlled here.
- **`_layouts/`** — Page templates (Liquid): `default`, `page`, `post`, `bib`, `distill`, `cv`, `about`, `profiles`, etc.
- **`_includes/`** — Reusable Liquid partials: `header`, `footer`, `head`, `scripts`, `social`, `figure`, `video`, `audio`, citation/bib components, CV/resume sub-templates.
- **`_pages/`** — Top-level site pages as Markdown files (about, blog, cv, publications, projects, books, etc.).
- **`_posts/`** — Blog posts in Markdown with YAML front matter.
- **`_bibliography/papers.bib`** — BibTeX file for publications, processed by `jekyll-scholar`.
- **`_data/`** — YAML data files: `cv.yml`, `coauthors.yml`, `repositories.yml`, `socials.yml`, `venues.yml`, `citations.yml`.
- **`_plugins/`** — Custom Ruby plugins for the build: citation fetching (Google Scholar, InspireHEP), cache busting, accent removal, external posts, file existence checks, custom BibTeX field hiding.
- **`_sass/`** — SCSS partials (`_base`, `_layout`, `_themes`, `_variables`, `_cv`, `_distill`, `_tabs`, `_typograms`) plus vendored Font Awesome and Tabler Icons.

### Assets
- **`assets/js/`** — Client-side JavaScript: theme toggling, search (ninja-keys based), chart/map/diagram setup scripts (Chart.js, ECharts, Leaflet, Mermaid, Vega, Plotly, MathJax), image zoom, code copy, etc.
- **`assets/css/`** — `main.scss` entry point plus vendored CSS (Bootstrap, MDB, Academicons, Jupyter themes).
- **`_scripts/`** — Liquid-templated JS for analytics and comments setup (Giscus, Google Analytics, Cronitor, OpenPanel, PhotoSwipe, search index).

### Build & Deploy
- **`Dockerfile`** / **`docker-compose.yml`** — Docker-based dev environment (Ruby, Node, ImageMagick, nbconvert). Serves on port 8080 with live reload on port 35729.
- **`.github/workflows/deploy.yml`** — GitHub Pages deployment via GitHub Actions.
- **`bin/`** — Helper scripts: `entry_point.sh` (Docker entrypoint with config-change watcher), `deploy`, `cibuild`, `update_scholar_citations.py`.

### Key Conventions
- Pages use Liquid templates (`.liquid` extension for layouts/includes) with Markdown content files.
- Publications are managed via BibTeX (`_bibliography/papers.bib`) and rendered by jekyll-scholar with custom citation plugins.
- Collections defined in `_config.yml`: `books`, `news`, `projects` (each with `output: true`).
- The `_data/` directory drives dynamic content (CV entries, social links, repo cards, coauthor highlighting).
