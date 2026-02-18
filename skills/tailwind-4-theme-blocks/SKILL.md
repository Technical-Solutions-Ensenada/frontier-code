---
name: tailwind-4-theme-blocks
description: >
  Troubleshoot and fix Tailwind v4 @theme block conflicts and missing custom colors.
  Trigger: When custom Tailwind colors are not working, colors appear as white/black, or multiple @theme blocks exist.
license: Apache-2.0
metadata:
  author: prowler-cloud
  version: "1.0"
  scope: [root, ui]
  auto_invoke: "Multiple @theme blocks detected or custom colors not rendering"
---

## When to Use

Use this skill when:
- Custom colors (e.g., `bg-my-blue`, `text-brand-red`) render as white/black instead of defined values
- Multiple `@theme` blocks exist in different CSS files
- Colors defined in source CSS but don't appear in compiled CSS
- Seeing symptoms: "colors changed to white" or "background is white instead of dark"

## Critical Patterns

### Tailwind v4 @theme Block Rules

**CRITICAL:** Tailwind v4 only processes **ONE** `@theme` block. Multiple blocks cause conflicts.

**How Tailwind v4 Processes @theme Blocks:**

1. Scans all CSS files in the project
2. Finds all `@theme` blocks
3. **Only the last loaded `@theme` block takes effect**
4. Variables from earlier blocks are **completely ignored**

### Problem: Multiple @theme Blocks

```css
/* ❌ WRONG: Multiple @theme blocks */
/* src/styles/theme.css */
@theme {
  --color-my-blue: #0862C8;
  --color-my-cyan: #2AD1C9;
  --color-my-dark: #0C171A;
}

/* src/styles/global.css */
@import "tailwindcss";

@theme {
  --font-monda: 'Monda', sans-serif;
}
```

**Result:**
- `--color-my-blue`, `--color-my-cyan`, `--color-my-dark` are **ignored**
- Only `--font-monda` from global.css is active
- Classes `bg-my-blue`, `text-my-cyan`, `bg-my-dark` **don't exist**
- Tailwind falls back to default values (white for backgrounds, black for text)

### Solution: Single Consolidated @theme Block

```css
/* ✅ CORRECT: Single consolidated @theme block */
/* src/styles/global.css */
@import "tailwindcss";

@theme {
  /* ALL colors and fonts in ONE place */
  --color-my-blue: #0862C8;
  --color-my-cyan: #2AD1C9;
  --color-my-dark: #0C171A;
  --color-my-light: #DEE6EC;
  --font-monda: 'Monda', sans-serif;
}
```

## Detection Patterns

### Symptom: Colors Not Rendering

If you see:
- Backgrounds appearing white when should be dark
- Text appearing black when should be colored
- Custom color classes not working
- Variables in source but missing from compiled CSS

### Diagnosis Commands

```bash
# 1. Check for multiple @theme blocks
grep -r "@theme" src/styles/ --include="*.css"

# Output: Shows all @theme blocks
# src/styles/theme.css:@theme {
# src/styles/global.css:@theme {
# If MORE THAN ONE line appears, you have the problem

# 2. Check if colors exist in compiled CSS
grep -o "your-color-name" dist/_astro/*.css

# Output: If your color appears, it's working
# If no output, the variable is not being processed
```

### Step-by-Step Fix

1. **Identify all `@theme` blocks:**
   ```bash
   grep -r "@theme" src/styles/ --include="*.css"
   ```

2. **Choose the main CSS file** (usually `global.css` or entry point):
   - This is the file imported by your layout/framework
   - Check `src/layouts/BaseLayout.astro` or similar for imports

3. **Consolidate ALL variables** into the main `@theme` block:
   ```css
   @import "tailwindcss";

   @theme {
     /* ALL custom colors */
     --color-brand-primary: #0862C8;
     --color-brand-secondary: #2AD1C9;
     
     /* ALL custom fonts */
     --font-display: 'Monda', sans-serif;
   }
   ```

4. **Delete extra `@theme` blocks** from other CSS files:
   ```bash
   rm src/styles/theme.css
   ```

5. **Import main CSS file** in your layout (if not already):
   ```astro
   <!-- src/layouts/BaseLayout.astro -->
   <style is:global>
     @import "../styles/global.css";
   </style>
   ```

6. **Rebuild and verify:**
   ```bash
   npm run build
   
   # Verify colors in compiled CSS
   grep -o "your-color-name" dist/_astro/*.css
   ```

## Common Scenarios

### Scenario 1: Separate theme.css File

**Problem:**
```
src/
├── styles/
│   ├── global.css    (has @theme with fonts)
│   └── theme.css     (has @theme with colors) ← NOT imported
```

**Solution:**
1. Delete `theme.css`
2. Move all variables from `theme.css` to `global.css`'s `@theme` block

### Scenario 2: Multiple @theme Blocks in Same File

**Problem:**
```css
@theme {
  --color-1: #0862C8;
}
@theme {
  --color-2: #2AD1C9;  /* This overwrites the first one */
}
```

**Solution:** Consolidate into one block

### Scenario 3: @theme in Component Files

**Problem:**
```astro
<!-- Component.astro -->
<style>
  @theme {
    --color-component-specific: #0862C8;
  }
</style>
```

**Solution:** Move all variables to main CSS file's `@theme` block

## Code Examples

### Correct Single @theme Block

```css
/* src/styles/global.css */
@import url('https://fonts.googleapis.com/css2?family=Monda:wght@300;400;500;600;700&family=Nunito+Sans:wght@300;400;500;600;700&display=swap');
@import "tailwindcss";

@theme {
  /* ============================================ */
  /* BRAND COLORS - Custom Colors               */
  /* ============================================ */
  --color-brand-blue: #0862C8;
  --color-brand-cyan: #2AD1C9;
  --color-brand-dark: #0C171A;
  --color-brand-light: #DEE6EC;

  /* ============================================ */
  /* FONTS - Brand Typography                    */
  /* ============================================ */
  --font-display: 'Monda', sans-serif;
  --font-body: 'Nunito Sans', sans-serif;
}
```

### Layout Import Pattern

```astro
---
// src/layouts/BaseLayout.astro
---

<!DOCTYPE html>
<html lang="es">
  <head>
    <style is:global>
      @import "../styles/global.css";

      * {
        scroll-behavior: smooth;
      }

      body {
        @apply bg-brand-dark text-brand-light;
      }
    </style>
  </head>
  <body class="antialiased">
    <slot />
  </body>
</html>
```

### Hero Component Using Custom Colors

```astro
---
// src/components/sections/Hero.astro
import Container from '../ui/Container.astro';
import imagotipoColor from '../../assets/IMAGOTIPO/SVG/IMAGOTIPO - DOS TONOS CLARO DEGRADADO.svg';
---

<section class="relative min-h-screen flex items-center justify-center overflow-hidden bg-brand-dark">
  <Container>
    <div class="relative z-10 max-w-5xl mx-auto text-center">
      <div class="mb-8">
        <img src={imagotipoColor.src} alt="Brand Logo" class="w-64 sm:w-80 mx-auto" />
      </div>
      
      <p class="font-display text-5xl font-light text-brand-light">
        Text with <span class="text-transparent bg-gradient-to-r from-brand-cyan to-brand-blue bg-clip-text">gradient</span>
      </p>
      
      <div class="flex items-center gap-2">
        <div class="w-2 h-2 bg-brand-cyan rounded-full animate-pulse"></div>
        <span>Badge with brand color</span>
      </div>
    </div>
  </Container>
</section>
```

## Anti-Patterns

❌ **DON'T:**
- Create multiple `@theme` blocks across files
- Define colors in component `<style>` blocks
- Leave `@theme` blocks in files that aren't imported
- Mix hex codes with custom color variables
- Assume Tailwind v3 behavior (tailwind.config.js)

❌ **NEVER:**
```css
/* Multiple @theme blocks */
@theme { --color-1: #0862C8; }
@theme { --color-2: #2AD1C9; }

/* @theme in components */
<style>
  @theme { --color-local: #2AD1C9; }
</style>
```

## Commands

```bash
# Check for multiple @theme blocks
grep -r "@theme" src/styles/ --include="*.css"

# Remove extra theme files
rm src/styles/theme.css

# Rebuild project
npm run build

# Verify colors in compiled CSS
grep -o "your-custom-color" dist/_astro/*.css

# Count occurrences (should match usage count)
grep -c "your-custom-color" dist/_astro/*.css
```

## Resources

- **Tailwind v4 Documentation**: https://tailwindcss.com/docs/theme
- **Tailwind v4 Theme Variables**: @theme directive documentation
- **Official Theme Reference**: Default theme variable reference
- **CSS @import MDN**: https://developer.mozilla.org/en-US/docs/Web/CSS/@import
