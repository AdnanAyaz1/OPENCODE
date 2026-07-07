---
name: premium-landing-pages
description: Use when generating, designing, or building landing pages, hero sections, feature sections, testimonials, CTAs, or any visually-rich marketing page. Triggers on prompts like "create a landing page", "build a hero section", "design a modern page", "make it look premium", "add glassmorphism", "add animations". Produces visually stunning, premium dark-themed pages with glassmorphism, gradient effects, blur animations, and sophisticated micro-interactions — NOT generic flat/square card layouts.
---

# Premium Landing Page Design System

This skill teaches you how to create visually stunning, premium landing pages that look like they were designed by a top-tier design agency. Follow these patterns exactly — they produce pages with depth, atmosphere, and polish that generic AI-generated pages lack.

**Core philosophy:** Every element must feel like it exists in a 3D space with light sources, depth, and atmosphere. Never use flat, opaque backgrounds. Never use plain square cards. Never use default styling.

---

## 1. DESIGN PHILOSOPHY — THE "WHY"

Generic AI pages fail because they:
- Use solid opaque backgrounds (`bg-white`, `bg-gray-100`)
- Use flat square cards with hard borders
- Have no depth, no atmosphere, no light
- Use default fonts at default sizes
- Have zero animation or micro-interaction
- Use random colors with no system

Premium pages succeed because they:
- Use translucent layered surfaces (`bg-white/[0.02]`, `bg-white/[0.06]`)
- Have glassmorphism with asymmetric borders simulating light
- Use gradient glow effects that activate on hover
- Feature blur-deblur entrance animations
- Have ambient background orbs that float and pulse
- Use a strict 3-color accent system
- Employ typography hierarchy with 3 distinct font families
- Use a single consistent easing curve for all animations

---

## 2. COLOR SYSTEM

### Background Layer Stack (bottom to top)
```
Layer 0: Base surface       → #0e1417 (darkest, page background)
Layer 1: Container low      → #161c20
Layer 2: Container          → #1a2024 (cards, modals)
Layer 3: Container high     → #252b2e (elevated elements)
Layer 4: Container highest  → #303639 (borders, dividers)
```

### Text Colors
```
Primary text    → #dee3e7 (on-surface)
Secondary text  → #bbc9cf (on-surface-variant)
Muted text      → #859399 (outline)
```

### 3-Color Accent System
```
Primary (Cyan)    → #00d2ff  — Main accent, links, active states, CTAs
Secondary (Green)  → #1fe19e  — Success, secondary actions, complementary
Tertiary (Amber)   → #ffd79f  — Highlights, badges, warnings, warmth
```

**Rule:** Each feature card uses ONE accent color. Alternate between primary, secondary, and tertiary across cards. Never mix accent colors within a single card.

### Translucent Border Scale
```
Rest state         → border-white/[0.06]   (6% white)
Hover state        → border-white/[0.12]   (12% white)
Active/open state  → border-white/[0.12]
Button borders     → border-white/10 or border-white/15
Glass card top     → border-top: rgba(255,255,255,0.15)
```

### Translucent Background Scale
```
Subtle             → bg-white/[0.02]  (barely visible)
Card default       → bg-white/[0.02]
Card hover         → bg-white/[0.03]  (slight brightening)
Input default      → bg-white/[0.05]
Input focus        → bg-white/[0.04]
Active/selected    → bg-white/[0.04]
```

---

## 3. TYPOGRAPHY SYSTEM

### Three Font Families
| Role | Font | CSS Variable | Usage |
|------|------|-------------|-------|
| **Headings** | Sora | `var(--font-sora)` | All headings, titles, stat numbers |
| **Body** | Plus Jakarta Sans | `var(--font-jakarta)` | Descriptions, paragraphs, form inputs |
| **Labels** | JetBrains Mono | `var(--font-jetbrains-mono)` | Uppercase labels, tags, chips, micro-text |

### Font Application Pattern
```tsx
{/* Headings */}
<h2 className="font-[family-name:var(--font-sora)] text-[36px] md:text-[56px] font-bold text-on-surface leading-[1.05] tracking-tight">
  Heading Text
</h2>

{/* Body */}
<p className="font-[family-name:var(--font-jakarta)] text-on-surface-variant leading-relaxed">
  Body text here
</p>

{/* Labels / Chips */}
<span className="font-[family-name:var(--font-jetbrains-mono)] text-xs uppercase tracking-[0.2em] text-primary">
  LABEL TEXT
</span>
```

### Typography Scale
```
Hero title        → text-4xl md:text-8xl, font-extrabold, uppercase, tracking-tighter, leading-[0.95]
Section heading   → text-[36px] md:text-[56px], font-bold, leading-[1.05], tracking-tight
Sub-heading       → text-[32px] md:text-[48px], font-bold
Body large        → text-lg, leading-relaxed
Body              → text-base or text-sm, leading-relaxed
Caption/Label     → text-xs or text-[10px], uppercase, tracking-[0.2em] or tracking-widest
Micro             → text-[8px] or text-[9px], uppercase, tracking-widest
```

### Gradient Text
Apply gradient to ONE key word per heading:
```tsx
<h2 className="font-[family-name:var(--font-sora)] text-[36px] md:text-[56px] font-bold text-on-surface leading-[1.05] tracking-tight">
  Find Your <span className="gradient-text">Dream</span> Car
</h2>
```

The `.gradient-text` class:
```css
background: linear-gradient(90deg, #00d2ff 0%, #1fe19e 100%);
-webkit-background-clip: text;
-webkit-text-fill-color: transparent;
background-clip: text;
```

---

## 4. GLASSMORPHISM & BLUR EFFECTS

### The Glass Card (`.glass-card`)
```css
.glass-card {
  background: rgba(255, 255, 255, 0.07);
  backdrop-filter: blur(20px);
  border-top: 1px solid rgba(255, 255, 255, 0.15);
  border-left: 1px solid rgba(255, 255, 255, 0.1);
  border-right: 1px solid rgba(255, 255, 255, 0.1);
  border-bottom: 1px solid rgba(255, 255, 255, 0.05);
}
```

**Why asymmetric borders?** They simulate a light source from above. Top edge is brightest (0.15), bottom is dimmest (0.05). This creates a 3D glass illusion.

**When to use glass-card:** Search bars, floating overlays, spec panels, navigation bars, loading states. NOT for main content cards (those use the "Fancy Card" pattern below).

### Glow Orbs
Ambient background decorations — large blurred circles that add atmosphere:
```tsx
{/* Primary glow */}
<div className="absolute w-[600px] h-[600px] bg-primary/[0.04] rounded-full blur-[120px] opacity-15 pointer-events-none" 
     style={{ top: "-200px", left: "-200px" }} />

{/* Secondary glow */}
<div className="absolute w-[500px] h-[500px] bg-secondary/[0.04] rounded-full blur-[120px] opacity-15 pointer-events-none animate-pulse" 
     style={{ top: "20%", right: "-150px" }} />
```

Sizes: `w-40 h-40` (sm), `w-60 h-60` (md), `w-80 h-80` (lg)
Blur: `blur-[80px]` (small), `blur-[100px]` (medium), `blur-[120px]` (large)
Opacity: 4-6% for ambient, 15% for decorative

### Corner Blur Accents (on cards)
Every card gets a decorative corner orb that fades in on hover:
```tsx
<div className="absolute -top-20 -right-20 w-60 h-60 bg-primary/[0.04] rounded-full blur-[80px] opacity-0 group-hover:opacity-100 transition-opacity duration-700" />
```

### Dot Grid Overlay
Subtle texture applied as a fixed full-screen layer:
```tsx
<div className="fixed inset-0 pointer-events-none z-10 opacity-50"
     style={{
       backgroundImage: "radial-gradient(rgba(255,255,255,0.05) 1px, transparent 0)",
       backgroundSize: "32px 32px",
       backgroundPosition: "-19px -19px"
     }} />
```

### Animated Background
For hero sections, use a slowly shifting gradient:
```css
.animated-gradient-bg {
  background: linear-gradient(-45deg, #0e1417, #0a1a2e, #0e1417, #0a2e1a);
  background-size: 400% 400%;
  animation: gradient-shift 15s ease infinite;
}
```

---

## 5. THE "FANCY CARD" PATTERN

This is the signature card design. Every content card in the app follows this EXACT structure:

```tsx
<div className="relative rounded-3xl border border-white/[0.06] overflow-hidden bg-white/[0.02] hover:bg-white/[0.03] hover:border-white/[0.12] transition-all duration-500 group">
  
  {/* Layer 1: Gradient glow on hover */}
  <div className="absolute inset-0 bg-gradient-to-br from-primary/[0.04] via-transparent to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-700" />
  
  {/* Layer 2: Corner accent blur orb */}
  <div className="absolute -top-20 -right-20 w-60 h-60 bg-primary/[0.04] rounded-full blur-[80px] opacity-0 group-hover:opacity-100 transition-opacity duration-700" />
  
  {/* Layer 3: Content (must be relative z-10) */}
  <div className="relative z-10 p-8">
    {/* Card content here */}
  </div>
</div>
```

### Card Color Variants
Change the gradient and orb colors per card:
- **Primary cards:** `from-primary/[0.04]` + `bg-primary/[0.04]`
- **Secondary cards:** `from-secondary/[0.04]` + `bg-secondary/[0.04]`
- **Tertiary cards:** `from-tertiary/[0.04]` + `bg-tertiary/[0.04]`

### Card Size Variants
| Type | Padding | Corner Orb | Border Radius |
|------|---------|-----------|---------------|
| Large feature | `p-8` or `p-12` | `w-60 h-60 blur-[80px]` | `rounded-3xl` |
| Medium card | `p-6` to `p-8` | `w-48 h-48 blur-[60px]` | `rounded-3xl` |
| Small card | `p-5` | `w-32 h-32 blur-[50px]` | `rounded-2xl` |
| Inner item | `p-4` | none | `rounded-xl` or `rounded-lg` |

### Card Hover Effects
- Background: `bg-white/[0.02]` → `bg-white/[0.03]`
- Border: `border-white/[0.06]` → `border-white/[0.12]`
- Gradient glow: `opacity-0` → `opacity-100` (duration-700)
- Corner orb: `opacity-0` → `opacity-100` (duration-700)
- Image inside: `scale-100` → `scale-105` (duration-700)

---

## 6. ANIMATION PATTERNS (Framer Motion)

### The Universal Easing Curve
Use this EXACT easing for 95% of all animations:
```ts
ease: [0.22, 1, 0.36, 1]
```
This is a custom cubic-bezier — fast start, smooth deceleration. It produces a premium "snap-in" feel.

### Section Header Entrance
```tsx
<motion.div
  initial={{ opacity: 0, y: 30 }}
  whileInView={{ opacity: 1, y: 0 }}
  viewport={{ once: true, margin: "-100px" }}
  transition={{ duration: 0.6, ease: [0.22, 1, 0.36, 1] }}
  className="mb-16"
>
  {/* Section label */}
  <div className="flex items-center gap-3 mb-6">
    <div className="h-px w-12 gradient-bg" />
    <span className="font-[family-name:var(--font-jetbrains-mono)] text-xs uppercase tracking-[0.2em] text-primary">
      Section Label
    </span>
  </div>
  
  {/* Section heading */}
  <h2 className="font-[family-name:var(--font-sora)] text-[36px] md:text-[56px] font-bold text-on-surface leading-[1.05] tracking-tight">
    Heading with <span className="gradient-text">gradient word</span>
  </h2>
</motion.div>
```

### Blur-Deblur Card Entrance (Premium Signature)
```tsx
// Stagger container
const containerVariants = {
  hidden: { opacity: 0 },
  visible: {
    opacity: 1,
    transition: { staggerChildren: 0.18, delayChildren: 0.1 },
  },
};

// Each card/item
const itemVariants = {
  hidden: { opacity: 0, y: 30, scale: 0.98, filter: "blur(4px)" },
  visible: {
    opacity: 1, y: 0, scale: 1, filter: "blur(0px)",
    transition: { duration: 0.65, ease: [0.22, 1, 0.36, 1] },
  },
};

// Usage
<motion.div variants={containerVariants} initial="hidden" whileInView="visible" viewport={{ once: true, margin: "-100px" }}>
  {items.map((item, i) => (
    <motion.div key={i} variants={itemVariants}>
      {/* Card content */}
    </motion.div>
  ))}
</motion.div>
```

### Hero Reveal Sequence
```tsx
// Staggered cascade with blur entrance
const heroSequence = [
  { delay: 0.15, duration: 0.9, initial: { opacity: 0, y: 30, filter: "blur(8px)" } },
  { delay: 0.35, duration: 0.7, initial: { opacity: 0, y: 20 } },
  { delay: 0.55, duration: 0.7, initial: { opacity: 0, y: 30, scale: 0.97 } },
];
```

### Underline Reveal Animation
```tsx
<motion.span
  className="absolute -bottom-1 left-0 h-[3px] gradient-bg rounded-full"
  initial={{ width: 0 }}
  whileInView={{ width: "100%" }}
  viewport={{ once: true }}
  transition={{ duration: 0.8, delay: 0.5, ease: [0.22, 1, 0.36, 1] }}
/>
```

### Slide Transition (Testimonials/Carousels)
```tsx
const variants = {
  enter: (direction: number) => ({
    x: direction > 0 ? 80 : -80, opacity: 0, filter: "blur(4px)",
  }),
  center: { x: 0, opacity: 1, filter: "blur(0px)" },
  exit: (direction: number) => ({
    x: direction < 0 ? 80 : -80, opacity: 0, filter: "blur(4px)",
  }),
};
// Transition: { duration: 0.5, ease: [0.22, 1, 0.36, 1] }
```

### Accordion (CSS Grid Trick)
```tsx
{/* Smooth height animation using CSS grid */}
<div
  className="grid transition-[grid-template-rows] duration-300 ease-[cubic-bezier(0.22,1,0.36,1)]"
  style={{ gridTemplateRows: isOpen ? "1fr" : "0fr" }}
>
  <div className="overflow-hidden">
    {/* Accordion content */}
  </div>
</div>

{/* Chevron rotation */}
<motion.span
  animate={{ rotate: isOpen ? 180 : 0 }}
  transition={{ duration: 0.2, ease: "easeInOut" }}
/>
```

### Spring Bounce (Icons/Stars)
```tsx
<motion.div
  initial={{ scale: 0 }}
  whileInView={{ scale: 1 }}
  transition={{ duration: 0.5, delay: 0.5, type: "spring", stiffness: 200 }}
/>
```

### Viewport Margin Guide
| Context | Margin | Purpose |
|---------|--------|---------|
| Section headers | `-100px` | Trigger before fully visible |
| Cards in grid | `-50px` | Trigger slightly before visible |
| Small items (FAQ, chips) | `-30px` | Rapid succession trigger |
| Reusable AnimatedSection | `-60px` | Default balanced trigger |

### Duration Scale
| Element | Duration |
|---------|----------|
| Micro (chevron rotate) | 200ms |
| Small (underline reveal) | 300ms |
| Card entrance | 500-650ms |
| Glow/hover effects | 700ms |
| Ambient backgrounds | 15s (infinite) |

---

## 7. SECTION LAYOUT PATTERNS

### Standard Section Structure
```tsx
<SectionContainer>
  <div className="relative z-10 max-w-[1440px] mx-auto">
    
    {/* Background decorations (orbs, etc.) - positioned absolute */}
    
    {/* Section header */}
    <motion.div
      initial={{ opacity: 0, y: 30 }}
      whileInView={{ opacity: 1, y: 0 }}
      viewport={{ once: true, margin: "-100px" }}
      transition={{ duration: 0.6, ease: [0.22, 1, 0.36, 1] }}
      className="mb-16"
    >
      <div className="flex items-center gap-3 mb-6">
        <div className="h-px w-12 gradient-bg" />
        <span className="font-[family-name:var(--font-jetbrains-mono)] text-xs uppercase tracking-[0.2em] text-primary">
          Label
        </span>
      </div>
      <h2 className="font-[family-name:var(--font-sora)] text-[36px] md:text-[56px] font-bold text-on-surface leading-[1.05] tracking-tight">
        Heading with <span className="gradient-text">gradient word</span>
      </h2>
    </motion.div>
    
    {/* Content grid */}
    <motion.div variants={containerVariants} initial="hidden" whileInView="visible" viewport={{ once: true, margin: "-100px" }}>
      {/* Cards */}
    </motion.div>
  </div>
</SectionContainer>
```

### SectionContainer Defaults
```tsx
<section className="relative z-20 py-[64px] md:py-[128px] px-5 md:px-16 max-w-[1440px] mx-auto">
```
- Mobile: 64px vertical, 20px horizontal padding
- Desktop: 128px vertical, 64px horizontal padding
- Max width: 1440px centered
- z-index: 20

### Section Label Pattern (The Horizontal Line + Mono Text)
Every section starts with this:
```tsx
<div className="flex items-center gap-3 mb-6">
  <div className="h-px w-12 gradient-bg" />
  <span className="font-[family-name:var(--font-jetbrains-mono)] text-xs uppercase tracking-[0.2em] text-primary">
    Label
  </span>
</div>
```

For centered sections (like FAQ):
```tsx
<div className="flex items-center justify-center gap-3 mb-6">
  <div className="h-px w-12 gradient-bg" />
  <span className="font-[family-name:var(--font-jetbrains-mono)] text-xs uppercase tracking-[0.2em] text-primary">
    Label
  </span>
  <div className="h-px w-12 gradient-bg" />
</div>
```

### Grid Systems
| Layout | Classes |
|--------|---------|
| 2-column (50/50) | `grid grid-cols-1 lg:grid-cols-2 gap-16` |
| 3-column | `grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-5` |
| 4-column stats | `grid grid-cols-2 md:grid-cols-4 gap-6` |
| Bento (1 large + 2 small) | `grid grid-cols-1 md:grid-cols-2 gap-5` with `md:row-span-2` on large card |
| Single centered | `max-w-3xl mx-auto` or `max-w-5xl mx-auto` |

---

## 8. HERO SECTION PATTERN

The hero is the most complex section. Layer stack (bottom to top):

```
z-0:   animated-gradient-bg (slowly shifting dark gradient)
z-0:   Background image with gradient overlay
z-0:   3x GlowOrbs (ambient light sources)
z-10:  DotGrid overlay (subtle texture)
z-15:  Radial readability gradient (darkens edges for text legibility)
z-20:  Content container (title, subtitle, search, stats)
```

### Hero Background Composition
```tsx
<section className="relative min-h-screen overflow-hidden">
  {/* Animated gradient base */}
  <div className="absolute inset-0 animated-gradient-bg" />
  
  {/* Background image */}
  <div className="absolute inset-0">
    <Image src="/hero-image.png" fill className="object-cover object-center" priority />
    <div className="absolute inset-0 bg-gradient-to-bl from-[#0e1417]/40 via-[#0e1417]/10 to-[#0e1417]/70" />
  </div>
  
  {/* Ambient glow orbs */}
  <GlowOrb color="primary" size="lg" position={{ top: "-200px", left: "-200px" }} />
  <GlowOrb color="secondary" size="md" position={{ top: "20%", right: "-150px" }} />
  <GlowOrb color="primary" size="sm" position={{ bottom: "10%", left: "30%" }} />
  
  {/* Dot grid texture */}
  <div className="absolute inset-0 dot-grid pointer-events-none z-10 opacity-50" />
  
  {/* Radial readability overlay */}
  <div className="absolute inset-0 z-15 bg-[radial-gradient(ellipse_at_center,rgba(10,14,24,0.85)_0%,rgba(10,14,24,0.5)_50%,transparent_80%)]" />
  
  {/* Content */}
  <div className="relative z-20 min-h-screen flex flex-col justify-center px-5 md:px-20 pt-20">
    {/* Title, subtitle, search bar, stats */}
  </div>
</section>
```

### Hero Title
```tsx
<h1 className="font-[family-name:var(--font-sora)] text-4xl md:text-8xl font-extrabold text-white mb-8 leading-[0.95] tracking-tighter uppercase">
  FIND YOUR <span className="gradient-text">DREAM</span> RIDE
</h1>
```

### Hero Stats Bar
```tsx
<div className="grid grid-cols-2 md:grid-cols-3 gap-8 md:gap-16 mt-12 pt-10 border-t border-white/[0.06]">
  <div>
    <div className="font-[family-name:var(--font-sora)] text-3xl md:text-4xl font-bold text-primary">
      <CountingNumber value={500} suffix="+" />
    </div>
    <div className="font-[family-name:var(--font-jetbrains-mono)] text-[10px] text-on-surface-variant uppercase tracking-[0.2em] mt-1">
      Premium Cars
    </div>
  </div>
  {/* More stat items... */}
</div>
```

### Search Bar (Glass Card Style)
```tsx
<div className="glass-card rounded-none p-2.5 flex items-center shadow-2xl max-w-5xl mx-auto">
  <div className="flex items-center gap-3 px-4 flex-1">
    <Search className="w-5 h-5 text-on-surface-variant" />
    <input 
      className="flex-1 bg-transparent text-on-surface font-[family-name:var(--font-jakarta)] text-base outline-none placeholder:text-on-surface-variant/50"
      placeholder="Search by brand, model, or keyword..."
    />
  </div>
  <button className="gradient-bg text-on-primary-fixed px-12 py-7 font-bold text-lg hover:brightness-110 transition-all shadow-lg shadow-primary/20">
    Search
  </button>
</div>
```

---

## 9. NAVIGATION / HEADER PATTERN

```tsx
<header className={`fixed top-0 left-0 right-0 z-50 transition-all duration-500 ${
  scrolled ? "bg-surface/80 backdrop-blur-2xl border-b border-white/10" : "bg-transparent"
}`}>
  <div className="max-w-[1440px] mx-auto px-5 md:px-16 h-20 flex items-center justify-between">
    {/* Logo */}
    <Link href="/" className="font-[family-name:var(--font-sora)] text-xl font-bold text-on-surface">
      Brand<span className="text-primary">Name</span>
    </Link>
    
    {/* Nav links (desktop) */}
    <nav className="hidden lg:flex items-center gap-8">
      <Link href="/link" className="font-[family-name:var(--font-jakarta)] text-base text-on-surface-variant hover:text-on-surface transition-colors">
        Link Text
      </Link>
    </nav>
    
    {/* Auth buttons */}
    <div className="flex items-center gap-4">
      <button className="bg-white/5 px-8 py-2.5 rounded-full font-semibold text-on-surface hover:bg-white/10 border border-white/10 backdrop-blur-md transition-all">
        Sign In
      </button>
      <button className="gradient-bg px-8 py-2.5 rounded-full font-bold text-on-primary-fixed hover:brightness-110 shadow-lg shadow-primary/20 transition-all">
        Get Started
      </button>
    </div>
  </div>
</header>
```

---

## 10. FOOTER PATTERN

```tsx
<footer className="mt-[120px] bg-surface-container-lowest border-t border-white/10">
  <div className="max-w-[1440px] mx-auto py-16 px-5 md:px-16">
    <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-12 mb-16">
      {/* Logo column */}
      <div>
        <Link href="/" className="font-[family-name:var(--font-sora)] text-xl font-bold text-on-surface">
          Brand<span className="text-primary">Name</span>
        </Link>
        <p className="mt-4 text-on-surface-variant text-sm leading-relaxed">
          Tagline or description text.
        </p>
      </div>
      
      {/* Link columns */}
      <div>
        <h4 className="font-[family-name:var(--font-sora)] text-sm font-bold text-on-surface uppercase tracking-wider mb-6">
          Column Title
        </h4>
        <ul className="space-y-3">
          <li>
            <Link href="/link" className="text-on-surface-variant hover:text-white transition-colors font-[family-name:var(--font-jakarta)] text-sm">
              Link Text
            </Link>
          </li>
        </ul>
      </div>
    </div>
    
    {/* Bottom bar */}
    <div className="border-t border-white/5 pt-8 flex flex-col md:flex-row justify-between items-center gap-4">
      <p className="text-on-surface-variant text-sm">&copy; 2026 Brand. All rights reserved.</p>
      <div className="flex items-center gap-4">
        {/* Social icons: w-10 h-10 rounded-full bg-white/5 border border-white/10 hover:bg-primary/20 hover:text-primary */}
      </div>
    </div>
  </div>
</footer>
```

---

## 11. BUTTON PATTERNS

### Primary CTA (Gradient)
```tsx
<button className="gradient-bg text-on-primary-fixed px-8 py-3 rounded-full font-bold hover:brightness-110 transition-all duration-300 shadow-lg shadow-primary/20">
  Get Started
</button>
```

### Ghost Button
```tsx
<button className="bg-white/5 border border-white/10 backdrop-blur-md text-on-surface px-8 py-3 rounded-full font-semibold hover:bg-white/10 transition-all duration-300">
  Learn More
</button>
```

### Outline Button (Card Action)
```tsx
<button className="border border-primary/30 text-primary px-6 py-2 rounded-full text-sm font-semibold group-hover:bg-primary group-hover:text-black group-hover:border-primary transition-all duration-300">
  View Details
</button>
```

### Secondary Outline Button
```tsx
<button className="border border-white/15 px-8 py-3 rounded-full text-on-surface font-semibold hover:bg-white hover:text-black transition-all duration-300">
  View All
</button>
```

---

## 12. INPUT PATTERNS

### Styled Input
```tsx
<input className="w-full px-4 py-3 rounded-xl border bg-white/[0.02] text-on-surface font-[family-name:var(--font-jakarta)] text-sm placeholder:text-on-surface-variant/30 focus:border-primary/50 hover:bg-white/[0.04] focus:bg-white/[0.04] transition-all duration-300 outline-none border-white/[0.06]" />
```

### Email Input (Newsletter)
```tsx
<input className="flex-1 bg-white/[0.05] border border-white/[0.08] rounded-xl px-6 py-4 text-on-surface font-[family-name:var(--font-jakarta)] placeholder:text-on-surface-variant/30 focus:ring-1 focus:ring-primary focus:border-primary hover:border-white/[0.15] transition-all duration-300 outline-none" />
```

---

## 13. SPEC PILL / CHIP PATTERN

```tsx
<span className="inline-flex items-center gap-2 px-4 py-1.5 rounded-full border backdrop-blur-md font-[family-name:var(--font-jetbrains-mono)] text-[10px] tracking-[0.2em] uppercase border-primary/20 bg-primary/5 text-primary">
  <Icon className="w-3 h-3" />
  Label Text
</span>
```

Variants:
- Default: `border-primary/20 bg-primary/5 text-primary`
- Secondary: `border-secondary/30 bg-secondary/10 text-secondary`
- Tertiary: `border-tertiary/30 bg-tertiary/10 text-tertiary`

---

## 14. TESTIMONIALS / CAROUSEL PATTERN

### Two-Column Layout
```tsx
<div className="flex flex-col lg:flex-row gap-16 items-center">
  {/* Left: Controls + Quote */}
  <div className="flex-1">
    <AnimatePresence mode="wait" custom={direction}>
      <motion.div
        key={current}
        custom={direction}
        variants={slideVariants}
        initial="enter"
        animate="center"
        exit="exit"
        transition={{ duration: 0.5, ease: [0.22, 1, 0.36, 1] }}
      >
        {/* Quote content */}
      </motion.div>
    </AnimatePresence>
    
    {/* Navigation dots */}
    <div className="flex items-center gap-2 mt-8">
      {items.map((_, i) => (
        <div className={`h-2 rounded-full transition-all duration-300 ${
          i === current ? "bg-primary w-8 shadow-lg shadow-primary/30" : "bg-white/20 w-2"
        }`} />
      ))}
    </div>
  </div>
  
  {/* Right: Image + floating rating */}
  <div className="flex-1 relative">
    <div className="relative rounded-3xl overflow-hidden aspect-[4/5]">
      <Image src={image} fill className="object-cover" />
    </div>
    
    {/* Floating rating card */}
    <motion.div
      initial={{ opacity: 0, y: 20, scale: 0.9 }}
      whileInView={{ opacity: 1, y: 0, scale: 1 }}
      transition={{ duration: 0.6, delay: 0.6, ease: [0.22, 1, 0.36, 1] }}
      className="absolute -bottom-8 -right-8 glass-card rounded-xl p-6 backdrop-blur-xl"
    >
      {/* Rating content */}
    </motion.div>
  </div>
</div>
```

---

## 15. FAQ / ACCORDION PATTERN

```tsx
<div className="max-w-3xl mx-auto space-y-3">
  {items.map((item, index) => (
    <motion.div
      key={index}
      initial={{ opacity: 0, y: 20 }}
      whileInView={{ opacity: 1, y: 0 }}
      viewport={{ once: true, margin: "-30px" }}
      transition={{ duration: 0.45, delay: index * 0.08, ease: [0.22, 1, 0.36, 1] }}
    >
      <div className={`rounded-2xl border transition-all duration-300 ${
        isOpen 
          ? "border-white/[0.12] bg-white/[0.04]" 
          : "border-white/[0.06] bg-white/[0.02] hover:bg-white/[0.03] hover:border-white/[0.10]"
      }`}>
        <button
          onClick={() => toggle(index)}
          className="w-full flex items-center justify-between p-6 text-left"
        >
          <span className={`font-[family-name:var(--font-sora)] text-lg font-semibold transition-colors ${
            isOpen ? "text-primary" : "text-on-surface hover:text-primary"
          }`}>
            {item.question}
          </span>
          <motion.span animate={{ rotate: isOpen ? 180 : 0 }} transition={{ duration: 0.2 }}>
            <ChevronDown className="w-5 h-5 text-on-surface-variant" />
          </motion.span>
        </button>
        
        <div className="grid transition-[grid-template-rows] duration-300 ease-[cubic-bezier(0.22,1,0.36,1)]"
             style={{ gridTemplateRows: isOpen ? "1fr" : "0fr" }}>
          <div className="overflow-hidden">
            <p className="px-6 pb-6 text-on-surface-variant text-sm leading-relaxed">
              {item.answer}
            </p>
          </div>
        </div>
      </div>
    </motion.div>
  ))}
</div>
```

---

## 16. NEWSLETTER CTA PATTERN

```tsx
<div className="max-w-5xl mx-auto rounded-3xl border border-white/[0.06] overflow-hidden bg-white/[0.02] hover:border-white/[0.10] transition-all duration-500">
  {/* Top accent line */}
  <div className="h-px w-full bg-gradient-to-r from-transparent via-primary/40 to-transparent" />
  
  {/* Background glows */}
  <div className="absolute top-0 right-0 w-72 h-72 bg-primary/[0.04] rounded-full blur-[100px] pointer-events-none" />
  <div className="absolute bottom-0 left-0 w-72 h-72 bg-secondary/[0.04] rounded-full blur-[100px] pointer-events-none" />
  
  {/* Gradient overlay */}
  <div className="absolute inset-0 bg-gradient-to-br from-primary/[0.06] via-transparent to-secondary/[0.04] opacity-60 hover:opacity-100 transition-opacity duration-700 pointer-events-none" />
  
  {/* Content */}
  <div className="relative z-10 p-12 md:p-20 text-center">
    <div className="flex items-center justify-center gap-3 mb-6">
      <div className="h-px w-12 gradient-bg" />
      <span className="font-[family-name:var(--font-jetbrains-mono)] text-xs uppercase tracking-[0.2em] text-primary">
        Stay Updated
      </span>
      <div className="h-px w-12 gradient-bg" />
    </div>
    
    <h2 className="font-[family-name:var(--font-sora)] text-[36px] md:text-[48px] font-bold text-on-surface leading-[1.05] tracking-tight mb-6">
      Join Our <span className="gradient-text">Inner Circle</span>
    </h2>
    
    <p className="text-on-surface-variant text-lg max-w-2xl mx-auto mb-10 leading-relaxed">
      Description text here.
    </p>
    
    {/* Form */}
    <div className="flex flex-col sm:flex-row gap-4 max-w-xl mx-auto">
      <input className="flex-1 bg-white/[0.05] border border-white/[0.08] rounded-xl px-6 py-4 text-on-surface placeholder:text-on-surface-variant/30 focus:ring-1 focus:ring-primary focus:border-primary transition-all duration-300 outline-none" />
      <button className="gradient-bg rounded-xl px-8 py-4 font-bold shadow-lg shadow-primary/20 hover:brightness-110 transition-all">
        Subscribe
      </button>
    </div>
  </div>
</div>
```

---

## 17. RESPONSIVE DESIGN RULES

| Element | Mobile | Tablet | Desktop |
|---------|--------|--------|---------|
| Section padding | `py-[64px] px-5` | `py-[96px] px-8` | `py-[128px] px-16` |
| Hero title | `text-4xl` | `text-6xl` | `text-8xl` |
| Section heading | `text-[32px]` | `text-[40px]` | `text-[48px]` or `text-[56px]` |
| Card grid | Single column | 2 columns | 3-4 columns |
| Testimonials | Stacked | Stacked | Two-column row |
| Stats bar | 2 columns | 3 columns | 4 columns |
| Navigation | Hamburger menu | Hamburger | Full nav links |
| Newsletter | Stacked inputs | Stacked | Side-by-side |
| Footer | Single column | 2 columns | 4 columns |
| Card padding | `p-5` | `p-6` | `p-8` |

---

## 18. BEM-like CLASS NAMING CONVENTION

This project uses Tailwind utility classes exclusively. No custom class names except:
- `.gradient-text` — gradient text fill
- `.gradient-bg` — gradient background
- `.gradient-title` — gradient text + font-weight 800
- `.glass-card` — glassmorphism panel
- `.glow-orb` — ambient blur circle
- `.dot-grid` — background texture pattern
- `.nav-scrolled` — header scroll state
- `.animated-gradient-bg` — hero background animation
- `.card-glow` — hover glow pseudo-element
- `.gradient-shimmer` — animated gradient shimmer
- `.moving-orb` — floating orb animation
- `.pulse-orb` — pulsing orb animation
- `.spec-pill` — spec badge style

---

## 19. ICON SYSTEM

Always use `lucide-react`:
```tsx
import { ArrowUpRight, Star, ChevronDown, Search, Mail, MapPin, Phone } from "lucide-react";
```

Icon sizing:
- Inline with text: `w-4 h-4` or `w-5 h-5`
- In circular containers: `w-5 h-5` inside `w-10 h-10` or `w-12 h-12`
- Standalone: `w-6 h-6` or `w-8 h-8`

Icon container hover:
```tsx
<div className="w-12 h-12 rounded-full bg-white/5 border border-white/10 flex items-center justify-center group-hover:scale-110 group-hover:border-primary/20 transition-all duration-500">
  <Icon className="w-5 h-5 text-on-surface-variant group-hover:text-primary transition-colors" />
</div>
```

---

## 20. "DO NOT" RULES — COMMON MISTAKES

1. **DON'T** use `bg-white`, `bg-gray-100`, `bg-gray-800` or any solid opaque backgrounds for cards
2. **DON'T** use `border-gray-200` or `border-gray-700` — use `border-white/[0.06]`
3. **DON'T** use flat square cards without the Fancy Card pattern
4. **DON'T** skip the blur entrance animation (`filter: "blur(4px)"` → `blur(0px)`)
5. **DON'T** use `transition-all duration-200` — use `duration-500` to `duration-700` for cards
6. **DON'T** use random colors — stick to the 3-accent system (cyan/green/amber)
7. **DON'T** skip the section label (gradient line + mono text) above headings
8. **DON'T** use `font-sans` or default fonts — always specify `font-[family-name:var(--font-sora)]` etc.
9. **DON'T** forget `viewport={{ once: true }}` on scroll animations
10. **DON'T** use `ease: "easeOut"` — use `ease: [0.22, 1, 0.36, 1]`
11. **DON'T** make all cards the same accent color — alternate primary/secondary/tertiary
12. **DON'T** use `className` for gradient text — use the `.gradient-text` class
13. **DON'T** forget `relative z-10` on content layers inside cards (above the absolute glow layers)
14. **DON'T** use `shadow-lg` with arbitrary colors — use `shadow-lg shadow-primary/20` for glow shadows
15. **DON'T** create pages without ambient glow orbs in the background

---

## 21. FULL PAGE CHECKLIST

When generating a landing page, ensure every section has:

- [ ] Dark surface background (#0e1417 or equivalent)
- [ ] Ambient glow orbs (at least 2-3 per major section)
- [ ] Section label (gradient line + mono uppercase text)
- [ ] Heading with gradient-text on one key word
- [ ] Cards using the Fancy Card pattern (translucent bg, hover glow, corner orb)
- [ ] Stagger animation with blur-deblur entrance
- [ ] `viewport={{ once: true }}` on all scroll animations
- [ ] Consistent easing curve `[0.22, 1, 0.36, 1]`
- [ ] Proper typography hierarchy (Sora headings, Jakarta body, JetBrains Mono labels)
- [ ] Responsive grid layouts (single col → multi col)
- [ ] Hover states on all interactive elements
- [ ] Translucent borders that brighten on hover
- [ ] Dot grid overlay on hero or major sections
- [ ] Gradient accent line below section labels
- [ ] Proper spacing (64px/128px section padding)
