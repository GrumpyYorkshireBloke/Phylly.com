# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Hugo static blog using the PaperMod theme, hosted on GitHub Pages at https://phylly.com.

## Commands

- `hugo server --buildDrafts` — local dev server with drafts visible (http://localhost:1313)
- `hugo --gc --minify` — production build (outputs to `public/`)
- `hugo new content posts/my-post.md` — create a new post

## Deployment

Pushes to `main` trigger `.github/workflows/deploy.yml`, which builds with Hugo 0.146.0 (extended) and deploys to GitHub Pages. No manual deploy step needed.

## Architecture

- `hugo.toml` — site config (title, theme, menus, params)
- `content/posts/` — blog posts in Markdown with YAML front matter
- `content/archives.md` — archive page (uses PaperMod's `archives` layout)
- `content/search.md` — search page (requires JSON output, already configured)
- `themes/PaperMod/` — theme as a git submodule; do not edit files here
- `static/CNAME` — custom domain file for GitHub Pages; must contain `phylly.com`

## Post Front Matter

```yaml
---
title: "Post Title"
date: 2026-01-01
draft: false
tags: ["tag1", "tag2"]
summary: "Short description for list pages"
---
```

Set `draft: true` to hide a post from production builds. Drafts are visible with `hugo server --buildDrafts`.

## Theme Customization

PaperMod is a git submodule — override templates by placing files in the repo's `layouts/` directory (mirrors the theme's `layouts/` structure). Same for `assets/css/extended/` for custom CSS.
