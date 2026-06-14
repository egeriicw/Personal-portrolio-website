# CLAUDE.md

This file provides guidance for AI assistants working in this repository.

## Project Overview

Personal portfolio website built with **Astro** and **Tailwind CSS**. The site is statically generated and deployed to **Netlify** or **AWS** (S3 + CloudFront).

## Tech Stack

| Layer | Technology |
|---|---|
| Framework | [Astro](https://astro.build) |
| Styling | [Tailwind CSS](https://tailwindcss.com) |
| Language | TypeScript |
| Package Manager | npm |
| Deployment | Netlify or AWS (S3 + CloudFront) |

## Project Structure

```
src/
  assets/        # Images and fonts processed by Astro (use <Image /> for optimization)
  components/    # Reusable .astro components (PascalCase filenames)
  content/       # Astro Content Collections — projects, blog posts, etc.
  layouts/       # Page layout wrappers (e.g. BaseLayout.astro)
  pages/         # File-based routing — each .astro file becomes a page
  styles/        # global.css (Tailwind @layer directives, CSS custom properties)
public/          # Static files served as-is: favicon.ico, robots.txt, OG images
astro.config.mjs
tailwind.config.mjs
tsconfig.json
package.json
```

## Development Workflow

```bash
npm install          # Install dependencies
npm run dev          # Start dev server at http://localhost:4321
npm run build        # Build static output to dist/
npm run preview      # Preview production build locally
npm run astro check  # Type-check .astro files
```

## Key Conventions

### Routing
- File-based routing via `src/pages/`. `index.astro` is the home page.
- Dynamic routes use bracket syntax: `src/pages/projects/[slug].astro`

### Components
- Use `.astro` components for all static/layout UI
- Only add React/Svelte/Vue island components when interactivity is required — keep JS footprint minimal (Astro's zero-JS-by-default philosophy)
- Component filenames: `PascalCase.astro` (e.g., `ProjectCard.astro`, `NavBar.astro`)
- Page filenames: `kebab-case.astro` (e.g., `about-me.astro`)

### Styling
- Tailwind utility classes are the primary styling approach
- Global styles and CSS custom properties go in `src/styles/global.css`
- Avoid inline `style` attributes; avoid writing custom CSS unless Tailwind cannot achieve the result
- Use Tailwind's `dark:` variant for dark mode support

### Images
- Always use Astro's `<Image />` component from `astro:assets` for images in `src/assets/` — this enables automatic optimization
- Static files that should not be processed (e.g., favicons, OG images) go in `public/`

### Content Collections
- Use Astro Content Collections (`src/content/`) for structured repeated content like projects or blog posts
- Define schemas with Zod in `src/content/config.ts`

### TypeScript
- Strict mode is enabled; avoid `any`
- Use `.ts` files for utilities and data; `.astro` for components

## Deployment

### Netlify
- Build command: `npm run build`
- Publish directory: `dist`
- Configure in `netlify.toml` at the repo root

### AWS (S3 + CloudFront)
- Output from `npm run build` (`dist/`) is uploaded to an S3 bucket configured for static website hosting
- CloudFront sits in front for CDN and HTTPS
- Redirects/rewrites handled via CloudFront Functions or S3 error document config

## AI Assistant Rules

- Do not add dependencies without checking the existing `package.json` first
- Prefer Astro-native solutions over third-party packages when one exists
- Never commit build artifacts (`dist/`, `.astro/`, `node_modules/`)
- Do not modify `package-lock.json` manually
- Keep pages lightweight — avoid bundling heavy client-side JS unless necessary
- All development happens on feature branches; do not push directly to `main`
