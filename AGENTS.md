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

`site.css` uses CSS custom properties (variables) to support automatic
light/dark theming via `@media (prefers-color-scheme: dark)`. The browser
switches modes based on the user's OS or browser setting — no JavaScript is
required.

### How it works

- **Palette variables** (e.g. `--grey-800`, `--blue-400`) define raw colour
  values. These do not change between modes.
- **Semantic variables** (e.g. `--body-bg`, `--link-colour`,
  `--code-bg`) map palette values to UI roles. The dark-mode media query
  overrides only these semantic variables.
- **Style rules** reference semantic variables, so a single set of rules
  supports both schemes.
- `color-scheme: light dark` (CSS) and
  `<meta name="color-scheme" content="light dark">` (HTML) tell the browser
  to render native controls (scrollbars, form widgets) in the appropriate
  mode.

### Light-mode defaults

The semantic variables default to Bootstrap 3's own colour values, so the
light-mode appearance is unchanged from the original theme.

### Covered components

The variables and overrides cover: body, links, typography, page header,
code/pre/kbd, tables, dropdowns, panels, wells, list groups, forms, modals,
and the close button. The `.navbar-inverse` is already dark-themed and
requires no per-mode changes.

### Child repo considerations

- Child repos inherit the dark-mode support automatically through the
  remote theme.
- If a child page injects hard-coded light-background colours via
  `extra_head` or inline styles, those will need per-page dark-mode
  overrides.
- Prefer using the semantic variables from `site.css` when adding custom
  styles (e.g. `background-color: var(--body-bg)`) so they adapt
  automatically.

## Guidelines

- Do not modify vendored files (`bootstrap.min.css`, `bootstrap.min.js`,
  `jquery.min.js`).
- There is no custom CI. GitHub Pages runs Jekyll automatically on push to
  `master`.
- Keep markup consistent with the existing Bootstrap 3 conventions.
- When updating the navbar, edit `_data/navigation.yml` — the change
  propagates to all child repos automatically.
