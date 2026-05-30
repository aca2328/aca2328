# CLAUDE.md

This file documents the codebase structure, development conventions, and workflows for AI assistants working in this repository.

## Project Overview

Personal portfolio website for Antoine Camerlo (Systems Engineer), hosted on GitHub Pages. Built with Jekyll and the [epidrome/cover-card](https://github.com/epidrome/cover-card) remote theme.

**Live site:** https://aca2328.github.io  
**Deployment branch:** `gh-pages` (GitHub Pages serves this branch directly)

## Repository Structure

```
aca2328/
├── _config.yml          # Jekyll site configuration, theme, plugins, social links
├── _includes/
│   └── head.html        # HTML <head>: meta tags, OpenGraph, Twitter Card, JSON-LD, CSS
├── _layouts/
│   └── default.html     # Master layout; includes Font Awesome and jekyll-seo-tag
├── assets/css/
│   ├── main.css         # Core styles: CSS variables, typography, layout, utilities
│   └── accessibility.css# WCAG styles: focus indicators, reduced-motion, high-contrast, dark mode
├── index.md             # Home page (hero section + about section)
├── 404.html             # Custom error page
├── robots.txt           # SEO crawler config
├── Gemfile              # Ruby dependencies (github-pages + plugins)
├── aca.jpg              # Avatar image
├── background.jpg       # Hero background image
└── favicon.ico          # Site favicon
```

## Technology Stack

- **Static site generator:** Jekyll (via `github-pages` gem)
- **Theme:** `epidrome/cover-card@main` (remote theme)
- **Plugins:** jekyll-seo-tag, jekyll-sitemap, jekyll-feed, jekyll-paginate, jekyll-gist, jekyll-redirect-from, jekyll-image-optim
- **CSS:** Vanilla CSS with custom properties (no preprocessor)
- **Icons:** Font Awesome (loaded in `_layouts/default.html`)
- **Templates:** Liquid templating (Jekyll built-in)

## Development Commands

```bash
# Install Ruby dependencies
bundle install

# Build the site to _site/
jekyll build

# Serve locally with live reload (http://localhost:4000)
jekyll serve

# Build with drafts and future posts
jekyll serve --drafts --future
```

The `_site/` directory is generated output — it is gitignored and should never be committed.

## Configuration

### `_config.yml`

All site-wide settings live here. Key sections:

| Section | Purpose |
|---|---|
| `remote_theme` | Theme source (`epidrome/cover-card@main`) |
| `title` / `description` | Site identity shown in SEO and theme |
| `avatar` / `background` / `favicon` | Image asset paths |
| `github-user`, `twitter`, `linkedin`, `email` | Social profile values |
| `social-links-order` | Display order of social icons |
| `social-links` | URL patterns for each social network |
| `seo` | OpenGraph title, description, image, Twitter card config |
| `sitemap` | Crawl frequency, priority, exclusions |
| `feed` | RSS feed path and post limit |
| `plugins` | Active Jekyll plugins |

To add a new social profile, uncomment the relevant key (e.g. `instagram: 'myhandle'`) and ensure it appears in `social-links-order`.

### Adding Pages

Create a new `.md` or `.html` file at the root with Jekyll front matter:

```yaml
---
layout: default
title: "Page Title"
description: "Page description for SEO"
---
```

## CSS Conventions

### CSS Custom Properties (`main.css:1-14`)

All colours and design tokens are declared in `:root`:

```css
--text-color: #333
--primary-color: #005fcc    /* blue — links, focus rings, buttons */
--accent-color: #ff6b6b     /* red — highlights */
--light-gray / --medium-gray / --dark-gray
--success-color / --warning-color / --error-color
```

Always use these variables; never hardcode colour values.

### Utility Classes

Bootstrap-style spacing utilities are available in `main.css`:

- `.mt-{1-5}` / `.mb-{1-5}` — margin top/bottom (0.5rem to 3rem)
- `.p-{1-5}` — padding (0.5rem to 3rem)
- `.text-center` — centered text
- `.container` — centred max-width wrapper (1200px)
- `.btn`, `.btn-primary`, `.btn-secondary` — button styles
- `.skip-link` — visually hidden skip-to-content (revealed on focus)
- `.no-print` — hidden in print media
- `.lazy-load` — placeholder for lazily loaded images
- `.sr-only` (in `accessibility.css`) — screen-reader-only text

### Accessibility (`accessibility.css`)

- Focus indicators: 3px solid outline with 2px offset, colour from `--primary-color`
- `prefers-reduced-motion`: disables transitions/animations
- `prefers-color-scheme: dark`: dark background variants
- `prefers-contrast: more`: high-contrast overrides
- Never remove `:focus` styles; never use `outline: none` without a visible replacement

## Jekyll Templates

### Liquid Variables

Key site variables available in all templates:

| Variable | Source |
|---|---|
| `site.title` | `_config.yml` → `title` |
| `site.description` | `_config.yml` → `description` |
| `site.github-user` | `_config.yml` → `github-user` |
| `site.twitter` | `_config.yml` → `twitter` |
| `site.linkedin` | `_config.yml` → `linkedin` |
| `site.email` | `_config.yml` → `email` |
| `site.avatar` | `_config.yml` → `avatar` |
| `site.background` | `_config.yml` → `background` |
| `page.title` | Page front matter |
| `page.description` | Page front matter |

### `_includes/head.html`

Included by the remote theme's layout. Contains:
- Standard meta tags with Liquid fallbacks (`page.X | default: site.X`)
- OpenGraph and Twitter Card tags
- JSON-LD `Person` schema markup
- Preload hints for `avatar` and `background` images
- Links to `/assets/css/main.css` and `/assets/css/accessibility.css`
- Skip-to-content link (`<a class="skip-link" href="#main-content">`)

The main content area in `index.md` wraps everything in `<div id="main-content">` — this ID is the target of the skip link and must be preserved.

## Git Workflow

- **Default branch:** `gh-pages` — GitHub Pages deploys from here automatically on every push
- **Feature branches:** branch off `gh-pages`, open a PR back to `gh-pages`
- There are no CI checks; deployment is instant on merge to `gh-pages`
- `_site/`, `.sass-cache/`, `.jekyll-cache/`, `.jekyll-metadata`, `Gemfile.lock`, `.DS_Store` are all gitignored

## SEO & Metadata

- `robots.txt` allows all crawlers, points to `/sitemap.xml`, sets a 2s crawl delay
- The sitemap is generated automatically by `jekyll-sitemap`; `/404.html` and `/assets/` are excluded
- Canonical URLs are set via `<link rel="canonical">` in `head.html`
- JSON-LD `Person` schema in `head.html` links GitHub, Twitter, and LinkedIn profiles

## Image Assets

| File | Size | Usage |
|---|---|---|
| `aca.jpg` | 45 KB | Avatar / profile photo |
| `background.jpg` | 335 KB | Hero background |
| `favicon.ico` | 6.4 KB | Browser tab icon |

Images are preloaded in `head.html`. When replacing images, keep the same filenames or update both `_config.yml` and `_includes/head.html`.

## No Test Suite

This is a static site — there is no automated test framework. Validate changes by running `jekyll serve` and reviewing the site locally at `http://localhost:4000` before pushing to `gh-pages`.
