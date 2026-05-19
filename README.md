# Hannwi's Tech Blog

Jekyll-based personal technical blog using the [Minimal Mistakes](https://github.com/mmistakes/minimal-mistakes) theme, hosted on GitHub Pages via GitHub Actions.

## Prerequisites

Requires Ruby 3.0+. If using macOS system Ruby (2.6), install via Homebrew and add to PATH:

> ```bash
> brew install ruby
> echo 'export PATH="/opt/homebrew/opt/ruby/bin:$PATH"' >> ~/.zshrc
> source ~/.zshrc
> ```

## How to Apply New Theme

1. Update `Gemfile` to reference the new theme gem:
   ```ruby
   gem "new-theme-name"
   ```
2. Update `_config.yml` to set the theme:
   ```yaml
   theme: new-theme-name
   ```
3. Install the new gem:
   ```bash
   bundle install
   ```
4. Update `_layouts/post.html` to delegate to the new theme's equivalent layout, so individual post files don't need to be touched.
   ```html
   ---
   layout: new-theme-layout-name   # e.g. single, article, default
   ---
   {{ content }}
   ```
   This shim keeps all posts using `layout: post` in their front matter while the actual rendering is handled by the new theme's layout.
   For standalone pages (e.g. `about.md`), update the `layout` field in each file's front matter directly.
5. Update theme-specific pages that use layouts unique to the old theme.  
   For example, `tags.md` uses `layout: tags` which is provided by Minimal Mistakes — the new theme may not have this layout or may name it differently.
   Check the new theme's documentation for equivalent layouts, and update the `layout` field in each affected page accordingly.
6. Remove any local layout/include overrides in `_layouts/` and `_includes/` that were specific to the old theme.
6. Verify the site renders correctly:
   ```bash
   bundle exec jekyll serve
   ```

## Local Development

```bash
# Install gems
#  Install all gems listed in Gemfile and lock versions in Gemfile.lock
#  Run this after first clone or whenever Gemfile changes
bundle install

# Start the Dev local server (http://localhost:4000)
#  If a file has been changed, it immediately applys to the running server.
#  To publish draft posts as well, use option --drafts.
bundle exec jekyll serve

# Build for production — enables production-only features (e.g. Google analytics, Ads, etc.)
# Output is written to _site/; the same command is used by the GitHub Actions deployment workflow
JEKYLL_ENV=production bundle exec jekyll build
```

## Post Front Matter

```yaml
---
layout: post
title: "Post Title"
categories: posts
tags: [tag1, tag2]
date: 2024-01-01
---
```

## Deployment

Pushing to `master` triggers GitHub Actions, which builds and deploys to GitHub Pages automatically.
