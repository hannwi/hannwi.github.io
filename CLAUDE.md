# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is a Jekyll-based personal technical blog hosted on GitHub Pages, using the [Minimal Mistakes](https://github.com/mmistakes/minimal-mistakes) gem theme. Deployment is handled by GitHub Actions on push to `master`.

## Commands

```bash
# Install dependencies
bundle install

# Serve locally with live reload
bundle exec jekyll serve

# Build for production
JEKYLL_ENV=production bundle exec jekyll build
```

> Requires Ruby 3.0+. On macOS with system Ruby 2.6, prefix commands with `PATH="/opt/homebrew/opt/ruby/bin:$PATH"`.

## Architecture

**Content flow:** Markdown files in `_posts/` and `_drafts/` → Jekyll processes with layouts from the `minimal-mistakes-jekyll` gem → static HTML output to `_site/` → deployed via GitHub Actions.

**Key directories:**
- `_posts/` — Published blog posts. Filename format: `YYYY-MM-DD-title.md`
- `_drafts/` — Unpublished drafts (no date in filename). Published when served with `--drafts` flag or when `future: true` is set.
- `_layouts/` — Local layout overrides only. `post.html` is a compatibility shim that wraps the gem's `single` layout.
- `_includes/` — Local partial overrides (currently empty; gem provides all partials).
- `assets/` — Images and static files. SASS is provided by the gem.
- `.github/workflows/deploy.yml` — GitHub Actions workflow for build and deployment.

**Post front matter:**
```yaml
---
layout: post
title: "Post Title"
categories: posts
tags: [tag1, tag2]
---
```

**Page front matter:**
```yaml
---
layout: single
title: "Page Title"
permalink: /path/
---
```

**Site config:** `_config.yml` controls title, URL, theme, plugins, and permalink structure (`/:categories/:title/`).

**Permalink structure:** Posts are served at `/<categories>/<title>/` (slugified).

**Theme customization:** Override any gem layout or include by creating a file with the same path locally (e.g., `_layouts/single.html` overrides the gem's single layout).
