---
name: frontier-ui
description: >
  Frontier Code UI standards based on official Brand Identity guidelines (dark theme, blue/cyan accents, NO glow effects per brand rules).
  Trigger: When creating/modifying UI components, sections, or visual elements.
license: Apache-2.0
metadata:
  author: frontier-code
  version: "2.0"
  scope: [root]
  auto_invoke: "Creating/modifying UI components, sections, or visual elements"
---

## When to Use

- Creating or modifying any UI component (buttons, cards, sections, etc.)
- Designing new page sections
- Adding interactive elements with hover states
- Implementing typography and color schemes
- Creating visual effects (glows, gradients, animations)
- Working with responsive layouts

## Critical Patterns

### Brand Guidelines

**Official Brand Colors** (from Brand Identity Manual - see `docs/Frontiercode/BRAND IDENTITY/`)

- **Primary Blue**: `#0862C8` (PANTONE 2387 C) - Main brand color
- **Primary Cyan**: `#2AD1C9` (PANTONE 3252 C) - Secondary brand color
- **Dark Neutral**: `#0C171A` (PANTONE Black 6 C) - Backgrounds, dark elements
- **Light Neutral**: `#DEE6EC` (PANTONE 656 C) - Light text, backgrounds

**Prohibited by Brand Guidelines:**
- ❌ NO glow effects (brillo/resplandor)
- ❌ NO blur effects
- ❌ NO color palette changes
- ❌ NO logo modifications (rotation, distortion, recoloring)
- ❌ NO adding graphical effects of any type

### Color Palette

**Backgrounds** (Dark Theme)
- Primary: `#0C171A` (brand dark neutral)
- Secondary: Use `dark-900`, `dark-800` as fallbacks
- Accents: `dark-800/50` (semi-transparent)

**Accent Colors** (Use Hex Codes or Custom Tailwind Colors)
- Primary: `#0862C8` (brand blue) - for buttons, links, CTAs
- Secondary: `#2AD1C9` (brand cyan) - for highlights, accents
- Neutral Dark: `#0C171A` - for backgrounds
- Neutral Light: `#DEE6EC` - for text on dark backgrounds

**Tailwind Color Mapping** (predefined in theme.css):
```js
// Available as: text-frontier-blue, bg-frontier-cyan, etc.
--color-frontier-blue: #0862C8,
--color-frontier-cyan: #2AD1C9,
--color-frontier-dark: #0C171A,
--color-frontier-light: #DEE6EC,
```

**Text Colors**
- Primary: `#DEE6EC` (light neutral) on dark backgrounds
- Secondary: `dark-400`
- Muted: `dark-500`

### Gradients

**Text Gradients** (use brand colors)
```astro
<span class="bg-linear-to-r from-frontier-blue to-frontier-cyan bg-clip-text text-transparent">
  Frontier Code
</span>
```

**Background Gradients**
```astro
<!-- Hero background -->
<div class="bg-linear-to-br from-frontier-dark via-dark-900 to-frontier-dark"></div>

<!-- Button gradient -->
<div class="bg-linear-to-r from-frontier-blue to-frontier-cyan"></div>

<!-- Text gradient with brand colors -->
<span class="bg-linear-to-r from-frontier-cyan to-frontier-blue bg-clip-text text-transparent"></span>
```

### Typography

**Official Brand Fonts** (from Brand Identity Manual)
- **MONDA**: Geometric, structured - Use for headings, brand elements
- **NUNITO SANS**: Rounded, organic - Use for body text, UI elements
- Both fonts use **Regular** weight by default

**Font Setup** (add to tailwind.config):
```js
fontFamily: {
  'monda': ['Monda', 'sans-serif'],
  'nunito': ['Nunito Sans', 'sans-serif'],
}
```

**Hero Headings** (Monda, bold)
```astro
<h1 class="font-monda text-5xl sm:text-6xl md:text-7xl lg:text-8xl font-bold">
  Title
</h1>
```

**Subheadings** (Monda, light weight)
```astro
<h2 class="font-monda text-2xl sm:text-3xl md:text-4xl lg:text-5xl font-light text-frontier-light">
  Subtitle
</h2>
```

**Body Text** (Nunito Sans)
```astro
<p class="font-nunito text-lg sm:text-xl text-dark-400 leading-relaxed">
  Description text
</p>
```

**Small Labels** (Nunito Sans, mono style)
```astro
<span class="font-nunito px-4 py-2 bg-dark-800/50 border border-frontier-cyan/30 rounded-full text-frontier-cyan text-sm">
  &lt;Frontier /&gt;
</span>
```

**Status Badges**
```astro
<div class="flex items-center gap-2">
  <div class="w-2 h-2 bg-frontier-cyan rounded-full animate-pulse"></div>
  <span class="font-nunito text-dark-500 text-sm">Status</span>
</div>
```

### Spacing

**Vertical Spacing**
- Sections: `py-16 sm:py-20 lg:py-24`
- Margin between elements: `mb-8`, `mb-12`, `mb-16`
- Gap: `gap-2`, `gap-4`, `gap-8`

### Borders

**Subtle Borders** (use brand colors)
```astro
<!-- Outline button/badge -->
class="border-2 border-frontier-cyan/50"

<!-- Badge border -->
class="border border-frontier-cyan/30"

<!-- Hover state border -->
class="hover:border-frontier-cyan"
```

### Rounded Corners

- Buttons/badges: `rounded-lg`
- Circular elements: `rounded-full`

### Animations

**Pulse Animation**
```astro
class="animate-pulse"
<!-- Add delay for staggered effects -->
style="animation-delay: 0.2s;"
```

**Bounce Animation**
```astro
class="animate-bounce"
```

**Custom Blink (Cursor)**
```astro
<style>
  @keyframes blink {
    0%, 50% { opacity: 1; }
    51%, 100% { opacity: 0; }
  }
  .animate-blink {
    animation: blink 1s infinite;
  }
</style>
<span class="w-2 h-8 bg-frontier-cyan animate-blink"></span>
```

### Transitions

**Standard Transitions**
```astro
class="transition-all duration-300"

<!-- Hover effects -->
class="hover:scale-105"
class="hover:bg-frontier-cyan/10"
class="hover:border-frontier-cyan hover:text-frontier-cyan"

<!-- Opacity transitions -->
class="opacity-0 group-hover:opacity-100 transition-opacity duration-300"
```

### Buttons

**Primary Gradient Button** (brand colors, NO shadows per brand guidelines)
```astro
<a href="#" class="group relative px-8 py-4 bg-linear-to-r from-frontier-blue to-frontier-cyan text-white font-semibold rounded-lg overflow-hidden transition-all duration-300 hover:scale-105">
  <span class="relative flex items-center gap-2">
    <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="..." />
    </svg>
    <span>Button Text</span>
  </span>
</a>
```

**Outline Button** (brand colors)
```astro
<a href="#" class="px-8 py-4 border-2 border-frontier-cyan/50 text-frontier-cyan font-semibold rounded-lg hover:bg-frontier-cyan/10 hover:border-frontier-cyan hover:text-frontier-cyan transition-all duration-300 hover:scale-105">
  Button Text
</a>
```

### Sections

**Hero Section Structure** (NO glow orbs per brand guidelines)
```astro
<section id="hero" class="relative min-h-screen flex items-center justify-center overflow-hidden bg-frontier-dark">
  <!-- Background layers -->
  <div id="particles" class="absolute inset-0 opacity-20"></div>
  <div class="absolute inset-0 bg-linear-to-br from-frontier-dark via-dark-900 to-frontier-dark"></div>

  <!-- Grid pattern -->
  <div class="absolute inset-0 bg-[linear-gradient(rgba(42,209,201,0.03)_1px,transparentlinear-gradient(90_1px),deg,rgba(42,209,201,0.03)_1px,transparent_1px)] bg-[size:50px_50px]"></div>

  <!-- Content -->
  <Container>
    <div class="relative z-10 max-w-5xl mx-auto text-center">
      <!-- Content goes here -->
    </div>
  </Container>
</section>
```

**Standard Section**
```astro
<section id="{id}" class="relative py-16 sm:py-20 lg:py-24 bg-frontier-dark">
  <Container>
    <div class="max-w-6xl mx-auto">
      <!-- Section content -->
    </div>
  </Container>
</section>
```

### Container Pattern

```astro
<div class="relative z-10 max-w-5xl mx-auto text-center">
  <!-- Centered content -->
</div>

<div class="max-w-6xl mx-auto">
  <!-- Full-width container -->
</div>

<div class="max-w-3xl mx-auto leading-relaxed">
  <!-- Text content -->
</div>
```

### Responsive Design

**Always use mobile-first responsive utilities:**
```astro
<!-- Spacing -->
class="py-16 sm:py-20 lg:py-24"

<!-- Typography -->
class="text-5xl sm:text-6xl md:text-7xl lg:text-8xl"

<!-- Layout -->
class="flex flex-col sm:flex-row gap-4 justify-center"
```

### Icons

```astro
<svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="..." />
</svg>
```

## Code Examples

### Complete Badge Component
```astro
---
const { label = '', color = 'cyan' } = Astro.props;
const colors = {
  cyan: 'text-frontier-cyan border-frontier-cyan/30 bg-dark-800/50',
  blue: 'text-frontier-blue border-frontier-blue/30 bg-dark-800/50',
  green: 'text-green-400 border-green-500/30 bg-dark-800/50'
};
---
<span class={`px-4 py-2 rounded-full text-sm border ${colors[color]}`}>
  {label}
</span>
```

### Status Indicator with Delay
```astro
---
const { status = '', color = 'cyan', delay = 0 } = Astro.props;
const colors = {
  cyan: 'bg-frontier-cyan',
  blue: 'bg-frontier-blue',
  green: 'bg-green-500'
};
---
<div class="flex items-center gap-2">
  <div class={`w-2 h-2 ${colors[color]} rounded-full animate-pulse`} style={`animation-delay: ${delay}s;`}></div>
  <span class="text-dark-500 text-sm">{status}</span>
</div>
```

## Decision Tree: Which Style to Apply?

| Situation | Use |
|-----------|-----|
| Primary action | Gradient button `from-frontier-blue to-frontier-cyan` |
| Secondary action | Outline button `border-frontier-cyan/50` |
| Headings | Large with text gradient `from-frontier-cyan to-frontier-blue` using MONDA font |
| Subheadings | Light weight `font-light text-frontier-light` using MONDA font |
| Body text | NUNITO SANS with `leading-relaxed` |
| Labels/badges | Rounded pill `rounded-full` with subtle border |
| Background | Dark `bg-frontier-dark` with gradient overlay |
| Hover effects | `hover:scale-105` with color transitions (NO shadows per brand guidelines) |
| Grid patterns | `bg-[linear-gradient(...)] bg-[size:50px_50px]` |

## Anti-Patterns

❌ **PROHIBITED by Brand Guidelines:**
- Glow effects (brillo/resplandor) - including text-shadow with blur
- Blur effects (blur-3xl, blur effects on backgrounds)
- Logo modifications (rotation, distortion, recoloring)
- Using purple color (not in brand palette)
- Adding graphical effects of any type

❌ **Don't use:**
- White backgrounds for main sections (use `frontier-dark`)
- Colors outside brand palette (`frontier-blue`, `frontier-cyan`, `frontier-dark`, `frontier-light`)
- Sharp corners on buttons/badges (use rounded-lg/rounded-full)
- Text without spacing (add `leading-relaxed`)
- Missing responsive utilities (always add `sm:` `md:` `lg:`)

## Commands

No specific commands - UI is purely declarative through Tailwind classes.

## Resources

- **Brand Identity Manual**: `docs/Frontiercode/BRAND IDENTITY/` (10 PNG pages with official guidelines)
- **Examples**: Hero section at `src/components/sections/Hero.astro`
- **Color Reference**: 
  - Primary Blue: `#0862C8` (PANTONE 2387 C)
  - Primary Cyan: `#2AD1C9` (PANTONE 3252 C)
  - Dark Neutral: `#0C171A` (PANTONE Black 6 C)
  - Light Neutral: `#DEE6EC` (PANTONE 656 C)
- **Typography**: MONDA (headings), NUNITO SANS (body text)
- **Animation Library**: Tailwind built-in + custom `@keyframes` for blinking
- **Brand Guidelines Source**: Official Frontiercode Brand Identity document
