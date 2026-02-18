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
- Secondary: Use `slate-900`, `slate-800` as fallbacks
- Accents: `slate-800/50` (semi-transparent)

**Accent Colors** (Use Hex Codes or Custom Tailwind Colors)
- Primary: `#0862C8` (brand blue) - for buttons, links, CTAs
- Secondary: `#2AD1C9` (brand cyan) - for highlights, accents
- Neutral Dark: `#0C171A` - for backgrounds
- Neutral Light: `#DEE6EC` - for text on dark backgrounds

**Tailwind Color Mapping** (configure in tailwind.config):
```js
colors: {
  'frontier-blue': '#0862C8',
  'frontier-cyan': '#2AD1C9',
  'frontier-dark': '#0C171A',
  'frontier-light': '#DEE6EC',
}
```

**Text Colors**
- Primary: `#DEE6EC` (light neutral) on dark backgrounds
- Secondary: `slate-400`
- Muted: `slate-500`

### Gradients

**Text Gradients** (use brand colors)
```astro
<span class="bg-gradient-to-r from-[#0862C8] to-[#2AD1C9] bg-clip-text text-transparent">
  Frontier Code
</span>
```

**Background Gradients**
```astro
<!-- Hero background -->
<div class="bg-gradient-to-br from-[#0C171A] via-slate-900 to-[#0C171A]"></div>

<!-- Button gradient -->
<div class="bg-gradient-to-r from-[#0862C8] to-[#2AD1C9]"></div>

<!-- Text gradient with brand colors -->
<span class="bg-gradient-to-r from-[#2AD1C9] to-[#0862C8] bg-clip-text text-transparent"></span>
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
<h2 class="font-monda text-2xl sm:text-3xl md:text-4xl lg:text-5xl font-light text-[#DEE6EC]">
  Subtitle
</h2>
```

**Body Text** (Nunito Sans)
```astro
<p class="font-nunito text-lg sm:text-xl text-slate-400 leading-relaxed">
  Description text
</p>
```

**Small Labels** (Nunito Sans, mono style)
```astro
<span class="font-nunito px-4 py-2 bg-slate-800/50 border border-[#2AD1C9]/30 rounded-full text-[#2AD1C9] text-sm">
  &lt;Frontier /&gt;
</span>
```

**Status Badges**
```astro
<div class="flex items-center gap-2">
  <div class="w-2 h-2 bg-[#2AD1C9] rounded-full animate-pulse"></div>
  <span class="font-nunito text-slate-500 text-sm">Status</span>
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
class="border-2 border-[#2AD1C9]/50"

<!-- Badge border -->
class="border border-[#2AD1C9]/30"

<!-- Hover state border -->
class="hover:border-[#2AD1C9]"
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
<span class="w-2 h-8 bg-[#2AD1C9] animate-blink"></span>
```

### Transitions

**Standard Transitions**
```astro
class="transition-all duration-300"

<!-- Hover effects -->
class="hover:scale-105"
class="hover:bg-[#2AD1C9]/10"
class="hover:border-[#2AD1C9] hover:text-[#2AD1C9]"

<!-- Opacity transitions -->
class="opacity-0 group-hover:opacity-100 transition-opacity duration-300"
```

### Buttons

**Primary Gradient Button** (brand colors, NO shadows per brand guidelines)
```astro
<a href="#" class="group relative px-8 py-4 bg-gradient-to-r from-[#0862C8] to-[#2AD1C9] text-white font-semibold rounded-lg overflow-hidden transition-all duration-300 hover:scale-105">
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
<a href="#" class="px-8 py-4 border-2 border-[#2AD1C9]/50 text-[#2AD1C9] font-semibold rounded-lg hover:bg-[#2AD1C9]/10 hover:border-[#2AD1C9] hover:text-[#2AD1C9] transition-all duration-300 hover:scale-105">
  Button Text
</a>
```

### Sections

**Hero Section Structure** (NO glow orbs per brand guidelines)
```astro
<section id="hero" class="relative min-h-screen flex items-center justify-center overflow-hidden bg-[#0C171A]">
  <!-- Background layers -->
  <div id="particles" class="absolute inset-0 opacity-20"></div>
  <div class="absolute inset-0 bg-gradient-to-br from-[#0C171A] via-slate-900 to-[#0C171A]"></div>

  <!-- Grid pattern -->
  <div class="absolute inset-0 bg-[linear-gradient(rgba(42,209,201,0.03)_1px,transparent_1px),linear-gradient(90deg,rgba(42,209,201,0.03)_1px,transparent_1px)] bg-[size:50px_50px]"></div>

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
<section id="{id}" class="relative py-16 sm:py-20 lg:py-24 bg-[#0C171A]">
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
  cyan: 'text-[#2AD1C9] border-[#2AD1C9]/30 bg-slate-800/50',
  blue: 'text-[#0862C8] border-[#0862C8]/30 bg-slate-800/50',
  green: 'text-green-400 border-green-500/30 bg-slate-800/50'
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
  cyan: 'bg-[#2AD1C9]',
  blue: 'bg-[#0862C8]',
  green: 'bg-green-500'
};
---
<div class="flex items-center gap-2">
  <div class={`w-2 h-2 ${colors[color]} rounded-full animate-pulse`} style={`animation-delay: ${delay}s;`}></div>
  <span class="text-slate-500 text-sm">{status}</span>
</div>
```

## Decision Tree: Which Style to Apply?

| Situation | Use |
|-----------|-----|
| Primary action | Gradient button `from-[#0862C8] to-[#2AD1C9]` |
| Secondary action | Outline button `border-[#2AD1C9]/50` |
| Headings | Large with text gradient `from-[#2AD1C9] to-[#0862C8]` using MONDA font |
| Subheadings | Light weight `font-light text-[#DEE6EC]` using MONDA font |
| Body text | NUNITO SANS with `leading-relaxed` |
| Labels/badges | Rounded pill `rounded-full` with subtle border |
| Background | Dark `bg-[#0C171A]` with gradient overlay |
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
- White backgrounds for main sections (use `#0C171A`)
- Colors outside brand palette (`#0862C8`, `#2AD1C9`, `#0C171A`, `#DEE6EC`)
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
