# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

Single-file static portfolio site for cosplayer @ciufflegend, hosted on GitHub Pages at `https://ciufflegend.github.io`. No build step, no framework, no dependencies.

## Deploying

```bash
git add -p
git commit -m "..."
git push  # GitHub Pages auto-deploys from master branch
```

## Architecture

Everything lives in `index.html` — styles, markup, and JS in one file. `photos/` holds 105 JPEG thumbnails (previews pulled from Immich, ~40 MB total).

The JS at the bottom of `index.html` builds the page dynamically from two hardcoded data structures:
- `named` — array of named cosplay characters (JAX, Lest, Stolas, Andrealphus), each with a list of photo IDs, cover ID, fandom, and photographer credit. Renders as the "Characters" card grid.
- `galleryIds` / `stolitzIds` — flat arrays of photo IDs for the masonry gallery and the Stolitz Wedding section respectively.

Photos are referenced as `photos/<uuid>.jpg`. To add a new photo: download the Immich preview thumbnail to `photos/`, add the ID to the relevant array in the JS data, commit and push.

## Photo source

Photos originate from an Immich instance at `192.168.1.162:2283` (local network only). The API key and Immich URLs are intentionally absent from the current codebase — photos are static files committed to the repo. To refresh or add photos, temporarily use the Immich API with a read-only asset key.

## Lightbox

A single shared lightbox (`#lightbox`) handles all three sections. `openLightbox(images, index)` takes an array of `{id, caption}` objects. Keyboard: `←`/`→` to navigate, `Esc` to close.
