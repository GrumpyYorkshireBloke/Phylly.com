---
title: "I Built This Blog With Claude Code (And Barely Typed a Command)"
date: 2026-02-05
draft: false
tags: ["claude-code", "hugo", "meta"]
summary: "How I went from an empty server to a live blog at phylly.com using Claude Code — token permission errors and all."
---

I wanted a blog. I didn't want to spend an evening fighting with static site generators, GitHub settings, and DNS records. So I opened up [Claude Code](https://claude.ai/code) and told it what I wanted: a Hugo blog on phylly.com.

Here's what happened.

## The Setup

I started with a bare Ubuntu server and an empty projects folder. No Hugo installed, no git repo, nothing. I told Claude I wanted a Hugo blog with the PaperMod theme, hosted on GitHub Pages, with my domain phylly.com pointing to it.

It asked me three questions — where to host, where my domain was registered, and which theme I wanted — then got to work.

## What Claude Did

Within a couple of minutes it had:

- Installed Hugo (and then upgraded it when PaperMod turned out to need a newer version)
- Scaffolded the site with PaperMod as a git submodule
- Configured `hugo.toml` with search, archives, tags, and dark mode support
- Written a GitHub Actions workflow for automatic deployments
- Added a CNAME file for the custom domain
- Built the site to make sure it actually worked

I didn't write any of that. I just watched it happen in my terminal.

## The Token Saga

This is where it got entertaining. I gave Claude a GitHub personal access token so it could create the repo and push. What followed was a series of permission errors:

1. **Can't create repos** — token didn't have the right scope. I created the repo manually instead.
2. **Can't push** — token was missing Contents write permission. Back to the token settings.
3. **Can't push workflows** — GitHub won't let you push a `.github/workflows/` file without the Workflows scope. Another round trip to token settings.
4. **Can't configure Pages** — that required manual setup in the repo settings too.

Three token revisions and a few manual clicks later, the site was deployed. Claude handled each error gracefully, told me exactly which permission to add, and picked up where it left off.

## The DNS

My domain is on Porkbun. Claude gave me the exact DNS records to add — four A records pointing to GitHub's IPs and a CNAME for www. I added them, Claude verified they'd propagated, and then nudged me to enable HTTPS once the certificate was ready.

## The Result

About fifteen minutes after I started, phylly.com was live with HTTPS, automatic deploys on push, and a clean PaperMod theme. Claude even generated a `CLAUDE.md` file so that future sessions would already know how the project is set up.

The whole experience felt less like using a tool and more like pair programming with someone who knows the Hugo and GitHub Pages docs better than I do. The only things I did manually were the parts where my token didn't have the right permissions — which, honestly, is fair enough.

Now I just need to write things worth reading.
