# AGENTS.md

This repository contains the source for a static GitHub Pages user site,
served at [phluid61.github.io](https://phluid61.github.io/).

## Overview

This is a simple, hand-authored static site. There is no build step, no
static site generator, and no CI pipeline. Files are served directly by
GitHub Pages from the `master` branch.

## Technology

- HTML5
- CSS3
- Bootstrap 3 (vendored: `bootstrap.min.css`, `bootstrap.min.js`)
- jQuery (vendored: `jquery.min.js`)
- Custom styles in `site.css`

## Structure

- `index.html` — the site homepage
- `site.css` — custom site styles
- `bootstrap.min.css`, `bootstrap.min.js`, `jquery.min.js` — vendored dependencies (do not modify)
- `favicon.ico`, `twitter.png`, `google+.png` — static assets

Subpaths (e.g. `/internet-drafts/`, `/mug/`, `/ruby-h2/`) are defined in
separate repositories and are not part of this repository.

## Guidelines

- Do not modify vendored files (`bootstrap.min.css`, `bootstrap.min.js`,
  `jquery.min.js`).
- There is no build or test step. Changes take effect once pushed to
  `master`.
- Keep markup consistent with the existing Bootstrap 3 conventions used in
  `index.html`.
