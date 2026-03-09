# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static single-page promotional website for the Salonica Armwrestling Cup 2026 tournament, hosted on Vercel at https://sac2026.vercel.app.

## Architecture

**Two HTML files, no build step, no framework, no package manager.**

- `index.html` — promotional/registration page (hero, categories, fees, seminar, venue, contacts)
- `results.html` — post-event results page (3-tab layout: results by category, athlete standings, team standings)

Tournament data from `tournament_thessaloniki_2026_v9.xlsx` is embedded directly as JS arrays in `results.html` (no fetch needed). Both files share the same header, footer, styles, and i18n system.

Both files use the same inline `tailwind.config`, `<style>` block, and JS patterns. The `results.html` JS renders three tabs dynamically from embedded data arrays using `innerHTML`; the `renderAll()` function is triggered via `setLanguage()` on `DOMContentLoaded`.

**`index.html` sections (anchor links):** `#overview`, `#categories`, `#weighing`, `#fees`, `#contact`

**Assets:**
- `Hero Images/` — hero background images
- `Facility Photos/` — venue photos used in gallery
- `Sponsor Logos/` — partner brand logos
- `Promotional Media/` — poster, share image, seminar instructor photo
- `tournament_thessaloniki_2026_v9.xlsx` — source data for results (already embedded in results.html)

## Internationalization

The site is bilingual (Greek `el` / English `en`):
- All translatable strings use `data-i18n="key"` attributes on HTML elements
- The `translations` JS object holds 140+ keys for both languages
- `setLanguage(lang)` updates all `[data-i18n]` elements and persists choice in `localStorage` under `sac2026-lang`
- Language toggle buttons are in the sticky header (EL / EN)

## Styling

- **Tailwind CSS 3.x** via CDN — use utility classes directly
- Custom color tokens defined in `tailwind.config`:
  - Brand blue: `#0a4a7a` → `brand-blue`
  - Brand gold: `#c9a227` → `brand-gold`
- Custom component classes: `.gold-gradient`, `.blue-gradient`, `.gold-text`, `.card-hover`, `.btn-gold`, `.mobile-menu`, `.responsive-iframe`

## Development

No build step needed. Open `index.html` directly in a browser or use any static file server:

```bash
# Quick local dev server options:
python -m http.server 8000
# or
npx serve .
```

Deployment is automatic via Vercel on push to the connected GitHub repository.
