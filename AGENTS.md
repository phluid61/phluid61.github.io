# AGENTS.md

This repository contains the source for a static GitHub Pages user site,
served at [phluid61.github.io](https://phluid61.github.io/). It also acts
as a Jekyll remote theme, providing shared layouts, includes, and navigation
data to child repositories.

## Overview

The site is built with Jekyll (run automatically by GitHub Pages). The
repository defines reusable layouts and includes that child repositories
inherit via the `jekyll-remote-theme` plugin.

## Technology

- Jekyll (GitHub Pages native)
- HTML5, CSS3
- Bootstrap 3 (vendored: `bootstrap.min.css`, `bootstrap.min.js`)
- jQuery (vendored: `jquery.min.js`)
- Custom styles in `site.css` (CSS custom properties for light/dark theming)
- Liquid templates

## Structure

- `_config.yml` — Jekyll site configuration (title, description, url)
- `_data/navigation.yml` — data-driven navbar menu structure
- `_includes/` — reusable template fragments:
  - `head.html` — HTML `<head>` element (meta, CSS links, optional
    `extra_head`)
  - `navbar.html` — site-wide navbar, rendered from navigation data
  - `scripts.html` — closing jQuery and Bootstrap JS tags
- `_layouts/` — page layouts:
  - `default.html` — full page skeleton (head, navbar, page header, content,
    scripts)
- `index.html` — the site homepage (uses `layout: default`)
- `site.css` — custom site styles and CSS custom properties for theming
- `bootstrap.min.css`, `bootstrap.min.js`, `jquery.min.js` — vendored
  dependencies (do not modify)
- `favicon.ico`, `twitter.png`, `google+.png` — static assets

## Layouts

### `default`

The standard page layout. Supports these front matter variables:

- `title` (string) — the HTML `<title>` (defaults to `site.title`)
- `page_heading` (string) — the `<h1>` in the page header (defaults to
  `site.title`)
- `extra_head` (string) — raw HTML injected into `<head>` for per-page
  CSS or JS (e.g. highlight.js)

## Adding navigation items

Edit `_data/navigation.yml`. Each entry is either a simple link or a
dropdown menu. Dropdown items support `divider: true` for separators and
`struck: true` for strikethrough styling.

## Child repositories

Child repos (e.g. `mug`, `ruby-h2`) inherit this theme by adding to their
`_config.yml`:

```yaml
remote_theme: phluid61/phluid61.github.io

plugins:
  - jekyll-remote-theme
```

Their pages use `layout: default` in front matter and only need to provide
page-specific content. The navbar, CSS/JS includes, and page skeleton are
all inherited.

## Colour scheme (light / dark mode)

`site.css` uses CSS custom properties to support automatic light/dark
theming via `@media (prefers-color-scheme: dark)`. Palette variables
(e.g. `--grey-800`) define raw colours; semantic variables (e.g.
`--body-bg`, `--link-colour`) map them to UI roles. The dark-mode media
query overrides only the semantic layer, so a single set of style rules
covers both schemes. Light-mode defaults match Bootstrap 3's own values.

Child repos inherit dark-mode support automatically. When adding custom
styles, prefer the semantic variables (e.g. `background-color:
var(--body-bg)`) so they adapt to both schemes. Hard-coded colours in
`extra_head` or inline styles will need per-page dark-mode overrides.

## Guidelines

- Do not modify vendored files (`bootstrap.min.css`, `bootstrap.min.js`,
  `jquery.min.js`).
- There is no custom CI. GitHub Pages runs Jekyll automatically on push to
  `master`.
- Keep markup consistent with the existing Bootstrap 3 conventions.
- When updating the navbar, edit `_data/navigation.yml` — the change
  propagates to all child repos automatically.
