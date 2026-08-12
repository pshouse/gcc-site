# Gaston Community Church — Website

The refreshed website for Gaston Community Church (Gastonia, NC), originally
generated with Claude Design and published as a static site via **GitHub Pages**.

**Live site:** https://gastoncommunitychurch.com (custom domain on GitHub
Pages; `pshouse.github.io/gcc-site` redirects here. DNS is managed at
GoDaddy — apex A records point to GitHub's Pages IPs, `www` is a CNAME to
`pshouse.github.io`.)

**This repo is the source of truth.** The Claude Design export was a one-time
starting point; all ongoing edits are made directly to the files in this repo
(by hand or with Claude Code) and published by pushing to `main`. Do not
re-export from Claude Design — that would overwrite changes made here.

## How it works

The pages are Claude Design `.dc.html` files. `support.js` is a small client-side
runtime that loads React (from unpkg) in the browser, parses each page's template,
and resolves shared components (`<dc-import name="Nav">`, `<dc-import name="Footer">`)
by fetching the sibling files. Because everything renders in the browser, the site
is fully static — no build step and no server code.

- `index.html` — entry point; redirects to `Home.dc.html`.
- `Home.dc.html`, `About.dc.html`, `Ministries.dc.html`, `Events.dc.html`,
  `Media.dc.html`, `Give.dc.html`, `ImNew.dc.html`, `Contact.dc.html`,
  `SmallGroups.dc.html` — pages.
- `Nav.dc.html`, `Footer.dc.html` — shared components imported by the pages.
- `support.js`, `image-slot.js` — Claude Design runtime.
- `assets/` — logos and hero image.
- `.nojekyll` — tells GitHub Pages to serve the files as-is (no Jekyll processing).

> Note: the runtime uses `fetch()` to load sibling pages, so the site must be
> served over HTTP(S). Opening the files directly from disk (`file://`) will not
> render. Use GitHub Pages, or run a local server (see below).

## Preview locally

```bash
python3 -m http.server 8000
```

Then open http://localhost:8000/ in a browser.

## Publishing (GitHub Pages)

This repo is configured to publish from the root of the `main` branch. In the
GitHub repo: **Settings → Pages → Build and deployment → Source: Deploy from a
branch → Branch: `main` / `root`**. Pushing to `main` updates the live site.

## Updating the site

Edit the `.dc.html` files (and `assets/`) directly in this repo, then commit and
push to `main`. GitHub Pages redeploys automatically within a minute or two.
