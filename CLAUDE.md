# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Odyssey Theme — a marketing website theme/starter built with **Astro** (static site generator). Uses Lit web components for interactive elements, MDX for blog content, and CSS variables for theming.

## Commands

```bash
npm run dev        # Start dev server with hot reload
npm run build      # Build static site to /dist
npm run preview    # Preview production build locally
npm run format     # Format code with Prettier (uses tabs)
```

No test or lint scripts exist.

## Architecture

**Astro SSG** with file-based routing — every `.astro`/`.mdx` file in `src/pages/` becomes a route.

### Layout hierarchy
`Base.astro` (root HTML shell) → `Page.astro` (standard pages with header/footer) or `Post.astro` (blog posts)

### Key directories
- `src/config/` — Site-wide configuration: `settings.js` (site metadata), `nav.js` (navigation structure), `footer.js` (footer content/socials)
- `src/components/core/` — Layout primitives: Header, Footer, Nav, Container, ThemeProvider
- `src/components/sections/` — Page building blocks: Hero variants, CTA, TextSection, CustomerQuote
- `src/pages/blog/posts/` — Blog posts as MDX files with frontmatter
- `src/styles/` — Global styles organized as: `reset.css` → `typography.css` → `theme.css` (CSS variables) → `global.css`

### Theming system
CSS variables defined in `src/styles/theme.css` power multiple themes (Classic, Dark, Earth, Ocean, Sand). `ThemeProvider.astro` initializes the theme; `theme-switcher/` is a Lit web component for runtime switching.

### Interactive components
Lit web components (requires `experimentalDecorators` in tsconfig) are used where client-side interactivity is needed. Astro's `@astrojs/lit` integration handles SSR/hydration.

## Import aliases

Configured in `tsconfig.json` with `baseUrl: "src"`:
- `@components/*`, `@layouts/*`, `@styles/*`, `@config`, `@utils/*`, `@pages/*`, `@icons/*`

## Deployment

Built to static files in `dist/`. CI deploys to Deno Deploy on push to main. Netlify config also present (`netlify.toml`).
