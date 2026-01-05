# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Frontier Code landing page - An Astro-based static site for a software development company. The site content is primarily in Spanish.

## Development Commands

| Command | Action |
|---------|--------|
| `npm run dev` | Start development server at `localhost:4321` |
| `npm run build` | Build production site to `./dist/` |
| `npm run preview` | Preview production build locally |
| `npm run astro ...` | Run Astro CLI commands |

## Architecture

### Framework & Tooling

- **Astro 5** - Static site generator with island architecture for interactive components
- **TypeScript** - Strict mode enabled via `astro/tsconfigs/strict`
- **Tailwind CSS v4** - Using Vite plugin with `@import "tailwindcss"` syntax

### Directory Structure

```markdown
src/
├── components/
│   ├── islands/        # Interactive components with client-side JS (client:* directives)
│   ├── layout/         # Layout components (Header, Footer, MainLayout)
│   ├── sections/       # Page sections (Hero, About, Services, etc.)
│   └── ui/             # Reusable UI primitives (Button, Card, Container)
├── layouts/            # Astro page layouts
├── pages/              # File-based routing
└── styles/             # Global styles and theme configuration
```

### Component Organization

- **Islands** (`components/islands/`) - Components requiring client-side JavaScript. Use `client:*` directives (e.g., `client:load`, `client:visible`) when these are used.
- **Layouts** (`components/layout/`) - Page structure components. `MainLayout.astro` provides the flex container with header/footer. `BaseLayout.astro` is the root HTML structure.
- **Sections** (`components/sections/`) - Content sections that compose the main page. Each section is self-contained.
- **UI** (`components/ui/`) - Reusable design system components like `Button`, `Card`, `Container`, `Section`.

### Styling System

**Tailwind v4 Theme**: All colors are defined as CSS variables in `src/styles/theme.css` using the `@theme` directive. To change the site's color palette, modify the hex values in this file only - Tailwind will automatically propagate changes.

Available color palettes:

- `primary` - Blue (brand color, primary-600 is main)
- `secondary` - Purple (accents)
- `accent` - Green
- `yellow` - For stars, reviews
- `neutral` - Gray scale

The `Container` component provides consistent horizontal padding and max-width for content sections.

### Component Patterns

All Astro components use TypeScript interfaces for props with default values. Example pattern:

```astro
---
interface Props {
  title: string;
  variant?: 'primary' | 'secondary';
}

const { title, variant = 'primary' } = Astro.props;
---
```

### Island Architecture

Interactive components live in `components/islands/` and are imported with client directives:

- `client:load` - Load immediately on page load
- `client:visible` - Load when component enters viewport
- `client:idle` - Load during browser idle time

Currently implemented islands: `ScrollToTop`, `MobileMenu`, `ContactForm`.

### Routing

Astro uses file-based routing in `src/pages/`. The main page is `index.astro` which composes various section components.
