# Emergency Locksmith Guide

Static directory site (Python + Markdown) for **24-hour and emergency locksmiths** only: home, car, and business lockouts, rekeying after a break-in, costs, and avoiding scams. Brand: Black Swan Sibyl. Built the same way as the sister sites (`/workspace/shred-directory`, `/workspace/directory-site`). **Not deployed yet.**

## Commands
```bash
python3 build.py            # build into dist/ (drafts excluded)
python3 serve.py            # build and preview at http://127.0.0.1:8000
python3 build.py --drafts   # include draft: true pages
```
The first run creates a local `.venv` and installs `requirements.txt` (PyYAML, Markdown). `make build` / `make serve` do the same.

## Layout
- `build.py` reads `content/pages/*.md` (YAML front matter + Markdown) and writes `dist/<slug>/index.html`, the homepage, `sitemap.xml`, and `robots.txt`. Markdown tables are enabled.
- `content/home.md` is the homepage intro. `config.yml` holds site name, tagline, `base_url`, `base_path`, and `affiliate_disclosure`.
- `static/` is copied into `dist/` as-is (`css/style.css`, and `CNAME` once a domain is chosen).
- `content/backlog.md` is the ranked list of future nightly pages.
- `data/` and `tools/` are gitignored (private earnings/outreach notes and the Telegram helper).

## Add a page
1. Pick the next idea in `content/backlog.md`. Mark it done there.
2. Create `content/pages/<slug>.md` (lowercase, hyphens):
```markdown
---
title: "Page title"
slug: page-slug
description: "One or two sentences used as the meta description and homepage blurb."
last_updated: 2026-11-18
draft: false
listings:
  - name: Business name
    url: https://example.com
    affiliate_url: https://example.com/?ref=x   # optional
    summary: What it is. Only facts you checked.
    category: Optional label
---

Body in Markdown.
```
3. Quote any front matter value that contains a colon. Run `python3 build.py` and check `dist/`.

## Content rules
- Real, sourced information only. Link the source next to every price, hour, or rule, and say "call to confirm".
- Never invent businesses, phone numbers, licence numbers, or prices. Leave listings out until a business's own site or a public record has been checked.
- Before adding any `affiliate_url`, fill `affiliate_disclosure` in `config.yml`.
- Stay in the niche: 24-hour/emergency locksmiths.

## Publishing (not done yet)
Sister sites deploy by pushing to a GitHub repo under `christieMogulReport`; `.github/workflows/pages.yml` (copied here) builds and publishes to GitHub Pages, and `static/CNAME` holds the custom domain (`<niche>.christiejustice.com`). To publish this site: create the repo, set `base_url` in `config.yml`, add `static/CNAME`, push to `main`, and enable Pages with the "GitHub Actions" source. Needs Christie's go-ahead first.
