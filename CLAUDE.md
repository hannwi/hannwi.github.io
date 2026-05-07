# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is a Jekyll-based personal technical blog hosted on GitHub Pages, using the Voyager theme.

## Commands

```bash
# Serve locally with live reload
jekyll serve

# Build for production
JEKYLL_ENV=production jekyll build

# Standard build
jekyll build
```

## Architecture

**Content flow:** Markdown files in `_posts/` and `_drafts/` → Jekyll processes with layouts from `_layouts/` and partials from `_includes/` → static HTML output to `_site/`.

**Key directories:**
- `_posts/` — Published blog posts. Filename format: `YYYY-MM-DD-title.md`
- `_drafts/` — Unpublished drafts (no date in filename). Published when served with `--drafts` flag or when `future: true` is set.
- `_layouts/` — Page templates. `compress.html` wraps others to minify HTML output.
- `_includes/` — Reusable partials (head, header, footer, aside).
- `assets/_sass/` — SASS source; compiled output goes to `assets/css/`.

**Post front matter:**
```yaml
---
layout: post
title: "Post Title"
categories: category1 category2
tags: tag1 tag2
---
```

**Site config:** `_config.yml` controls title, URL, permalink structure (`/:categories/:title/`), and SASS compilation settings.

**Permalink structure:** Posts are served at `/<categories>/<title>/` (slugified).
