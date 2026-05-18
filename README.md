# Hannwi's Technical Blog

Jekyll-based personal technical blog using the [Minimal Mistakes](https://github.com/mmistakes/minimal-mistakes) theme, hosted on GitHub Pages via GitHub Actions.

## Prerequisites

Requires Ruby 3.0+. If using macOS system Ruby (2.6), install via Homebrew and add to PATH:

> ```bash
> brew install ruby
> echo 'export PATH="/opt/homebrew/opt/ruby/bin:$PATH"' >> ~/.zshrc
> source ~/.zshrc
> ```

## Local Development

```bash
# Install dependencies (first time)
bundle install

# Serve locally with live reload
bundle exec jekyll serve

# Build for production
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
