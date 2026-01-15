# Repository Guidelines

## How to Use This Guide

- Start here for cross-project norms.
- Each component has an `AGENTS.md` file with specific guidelines (e.g., `api/AGENTS.md`, `ui/AGENTS.md`).
- Component docs override this file when guidance conflicts.
- 
## Available Skills

Use these skills for detailed patterns on-demand:

### Generic Skills (Any Project)

| Skill | Description | URL |
|-------|-------------|-----|
| `astro` | Astro v5 patterns, component structure, islands architecture | [SKILL.md](skills/astro/SKILL.md) |
| `typescript` | Const types, flat interfaces, utility types | [SKILL.md](skills/typescript/SKILL.md) |
| `tailwind-4` | cn() utility, no var() in className | [SKILL.md](skills/tailwind-4/SKILL.md) |

### Project-Specific Skills

| Skill | Description | URL |
|-------|-------------|-----|
| `skill-creator` | Create new AI agent skills | [SKILL.md](skills/skill-creator/SKILL.md) |

### Auto-invoke Skills

When performing these actions, ALWAYS invoke the corresponding skill FIRST:

| Action | Skill |
|--------|-------|
| After creating/modifying a skill | `skill-sync` |
| Creating/modifying Astro files (.astro) | `astro` |
| Writing TypeScript types/interfaces | `typescript` |
| Working with Tailwind classes | `tailwind-4` |

## Project Overview

This is an Astro v5 landing page for Frontier Code, a software development company.
- **Framework**: Astro 5.16.6
- **Styling**: Tailwind CSS v4.1.18 via Vite plugin
- **TypeScript**: Strict mode enabled
- **Package Manager**: pnpm
- **Language**: Spanish (UI text and content)
- **Interactive Features**: SweetAlert2 for modals/alerts

## Commands

### Development
```bash
pnpm run dev          # Start dev server at localhost:4321
pnpm run build        # Build production bundle to ./dist/
pnpm run preview      # Preview production build
pnpm run astro ...    # Run Astro CLI commands
```

### Testing & Linting
No test or lint scripts configured yet. To add testing:
- Consider Vitest for unit tests
- Consider Astro's built-in check: `pnpm run astro check`
- No linting setup (no ESLint/Prettier configured)

## Code Structure

```
src/
├── layouts/          # Base HTML layouts (BaseLayout.astro)
├── pages/            # File-based routes (index.astro)
├── components/
│   ├── ui/           # Reusable UI components (Button, Card, Container, Section)
│   ├── layout/       # Page layout components (Header, Footer, MainLayout)
│   ├── sections/     # Page sections (Hero, About, Services, Portfolio, etc.)
│   └── islands/      # Interactive client-side components (MobileMenu, ContactForm)
└── styles/           # Global styles
```
