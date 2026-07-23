# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

Marketing site for McKenney Electric Co, a Charlotte, NC electrical contractor. Single-page Astro site styled with Tailwind CSS v4, deployed to GitHub Pages at the custom domain `mckenneyelectric.co`.

## Commands

```
npm run dev       # start dev server at localhost:4321
npm run build     # type-check + build static site to dist/
npm run preview   # serve the built dist/ locally
```

When starting the dev server in an agent session, use background mode:

```
astro dev --background
```

Manage it with `astro dev stop`, `astro dev status`, and `astro dev logs`.

There is no test suite or linter configured.

## Architecture

- **Single page**: everything renders from `src/pages/index.astro`, which composes section components from `src/components/` in order: `Nav` → `Hero` → `Services` → `About` → `Contact` → `Footer`. There is no routing/multi-page structure — new sections are added as components and slotted into `index.astro`, linked via in-page anchors (`#services`, `#about`, `#contact`).
- **Layout**: `src/layouts/Layout.astro` holds the `<html>` shell, meta tags, and imports `src/styles/global.css`. Page-specific `title`/`description` can be passed as props.
- **Design tokens**: brand colors and fonts are defined once as CSS custom properties in `src/styles/global.css` under `@theme` (Tailwind v4's CSS-based config, not a `tailwind.config.js`) — `--color-volt` (brand yellow), `--color-ink` (near-black), `--color-cream` (off-white), plus `--font-display` (Anton), `--font-script` (Kaushan Script), `--font-body` (Oswald). Fonts are self-hosted via `@fontsource/*` packages, imported in `global.css`.
- **Logo**: there is no logo image file. `src/components/Logo.astro` renders the wordmark as styled text (Anton + Kaushan Script) plus `src/components/Bolt.astro`, an inline SVG lightning bolt used as an icon throughout. This keeps the logo crisp and recolorable across yellow/black/cream backgrounds instead of depending on a raster export.
- **Images**: `public/images/` holds web-optimized copies (resized/compressed via macOS `sips`) of source photography. The retro yellow-duotone hero photo effect is done in CSS (`grayscale` filter + a `mix-blend-multiply` yellow overlay div), not a pre-baked image. `public/images/matt-cutout.png` is a transparency-cut PNG (not a plain rectangular photo) — layouts using it rely on the irregular alpha edge for a die-cut look.
- **Raw design source** (`Images/` at repo root — original `.ai`/`.psd`/full-res files) is gitignored; it's reference material only and isn't read by the site or build.
- **Contact form**: `src/components/Contact.astro` posts to Formspree. The endpoint ID is a placeholder (`FORMSPREE_ID` constant at the top of the file) — replace it with a real form ID from formspree.io before the form will actually deliver mail.
- **Deployment**: `.github/workflows/deploy.yml` builds with `npm ci && npm run build` and publishes `dist/` via `actions/deploy-pages`, triggered on push to `main`. `public/CNAME` (containing `mckenneyelectric.co`) and `site` in `astro.config.mjs` are both set for the custom domain — keep them in sync if the domain ever changes.
