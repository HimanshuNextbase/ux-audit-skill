# Design System Generation Workflow

Source: https://github.com/nextlevelbuilder/ui-ux-pro-max-skill
Files: `skill-content.md`, `README.md`

---

## How the Design System Generator Works

```
1. USER REQUEST
   "Build a landing page for my beauty spa"
         ↓
2. MULTI-DOMAIN SEARCH (5 parallel searches)
   • Product type matching (161 categories)
   • Style recommendations (67 styles)
   • Color palette selection (161 palettes)
   • Landing page patterns (24 patterns)
   • Typography pairing (57 font combinations)
         ↓
3. REASONING ENGINE
   • Match product → UI category rules
   • Apply style priorities (BM25 ranking)
   • Filter anti-patterns for industry
   • Process decision rules (JSON conditions)
         ↓
4. COMPLETE DESIGN SYSTEM OUTPUT
   Pattern + Style + Colors + Typography + Effects
   + Anti-patterns to avoid + Pre-delivery checklist
```

---

## Skill Workflow: Step by Step

### Step 1: Analyze User Requirements
Extract:
- **Product type** — Entertainment, Tool, Productivity, or hybrid
- **Target audience** — age group, usage context (commute, leisure, work)
- **Style keywords** — playful, vibrant, minimal, dark mode, content-first, immersive
- **Stack** — React, Next.js, Vue, Tailwind, SwiftUI, Flutter, etc.

### Step 2: Generate Design System (ALWAYS FIRST)
```bash
python3 skills/ui-ux-pro-max/scripts/search.py "<product_type> <industry> <keywords>" --design-system [-p "Project Name"]
```
Output: pattern + style + colors + typography + effects + anti-patterns

### Step 2b: Persist Design System (Master + Overrides Pattern)
```bash
python3 skills/ui-ux-pro-max/scripts/search.py "<query>" --design-system --persist -p "Project Name"
# Optional: page-specific override
python3 skills/ui-ux-pro-max/scripts/search.py "<query>" --design-system --persist -p "Project Name" --page "dashboard"
```

Creates:
```
design-system/
├── MASTER.md           ← Global Source of Truth
└── pages/
    └── dashboard.md    ← Page-specific overrides only
```

**Hierarchical retrieval:**
1. Check `design-system/pages/<page-name>.md` first
2. If exists → page rules override Master
3. If not → use `MASTER.md` exclusively

### Step 3: Domain Searches (as needed)

| Need | Domain Flag | Example |
|------|-------------|---------|
| Product type patterns | `--domain product` | `"entertainment social"` |
| More style options | `--domain style` | `"glassmorphism dark"` |
| Color palettes | `--domain color` | `"entertainment vibrant"` |
| Font pairings | `--domain typography` | `"playful modern"` |
| Chart recommendations | `--domain chart` | `"real-time dashboard"` |
| UX best practices | `--domain ux` | `"animation accessibility"` |
| Landing structure | `--domain landing` | `"hero social-proof"` |

### Step 4: Stack-Specific Guidelines
```bash
python3 skills/ui-ux-pro-max/scripts/search.py "<keyword>" --stack <stack-name>
```

Supported stacks: `react`, `nextjs`, `vue`, `nuxtjs`, `nuxt-ui`, `astro`, `svelte`, `html-tailwind`, `shadcn`, `swiftui`, `react-native`, `flutter`, `jetpack-compose`, `angular`, `laravel`

---

## Example Design System Output (Beauty Spa)

```
TARGET: Serenity Spa - RECOMMENDED DESIGN SYSTEM

PATTERN: Hero-Centric + Social Proof
  Conversion: Emotion-driven with trust elements
  CTA: Above fold, repeated after testimonials
  Sections: 1. Hero → 2. Services → 3. Testimonials → 4. Booking → 5. Contact

STYLE: Soft UI Evolution
  Keywords: Soft shadows, subtle depth, calming, premium feel, organic shapes
  Best For: Wellness, beauty, lifestyle brands, premium services
  Performance: Excellent | Accessibility: WCAG AA

COLORS:
  Primary:    #E8B4B8 (Soft Pink)
  Secondary:  #A8D5BA (Sage Green)
  CTA:        #D4AF37 (Gold)
  Background: #FFF5F5 (Warm White)
  Text:       #2D3436 (Charcoal)
  Notes: Calming palette with gold accents for luxury feel

TYPOGRAPHY: Cormorant Garamond / Montserrat
  Mood: Elegant, calming, sophisticated
  Best For: Luxury brands, wellness, beauty, editorial

KEY EFFECTS:
  Soft shadows + Smooth transitions (200–300ms) + Gentle hover states

AVOID (Anti-patterns):
  Bright neon colors + Harsh animations + Dark mode + AI purple/pink gradients

PRE-DELIVERY CHECKLIST:
  [ ] No emojis as icons (use SVG: Heroicons/Lucide)
  [ ] cursor-pointer on all clickable elements
  [ ] Hover states with smooth transitions (150–300ms)
  [ ] Light mode: text contrast 4.5:1 minimum
  [ ] Focus states visible for keyboard nav
  [ ] prefers-reduced-motion respected
  [ ] Responsive: 375px, 768px, 1024px, 1440px
```

---

## When to Use This Skill

### Must Use
- Designing new pages (Landing, Dashboard, Admin, SaaS, Mobile App)
- Creating or refactoring UI components (buttons, modals, forms, tables, charts)
- Choosing color schemes, typography, spacing, or layout systems
- Reviewing UI code for UX, accessibility, or visual consistency
- Implementing navigation, animations, or responsive behavior
- Making product-level design decisions (style, hierarchy, brand expression)

### Recommended
- UI looks "not professional enough" but reason is unclear
- Receiving usability/experience feedback
- Pre-launch UI quality optimization
- Cross-platform design alignment (Web / iOS / Android)
- Building design systems or reusable component libraries

### Skip
- Pure backend logic
- API or database design only
- Infrastructure / DevOps
- Non-visual scripts or automation

**Rule of thumb:** If the task changes how something **looks, feels, moves, or is interacted with** → use this skill.

---

## Tip: Query Strategy

- Use **multi-dimensional keywords** — combine product + industry + tone + density:
  - `"entertainment social vibrant content-dense"` not just `"app"`
- Try different keywords for same need: `"playful neon"` → `"vibrant dark"` → `"content-first minimal"`
- Use `--design-system` first for full recommendations, then `--domain` to deep-dive
- Always add `--stack <stack>` for implementation-specific guidance

## Tip: Common Sticking Points

| Problem | What to Do |
|---------|------------|
| Can't decide style/color | Re-run `--design-system` with different keywords |
| Dark mode contrast issues | `--domain ux` → `color-dark-mode` + `color-accessible-pairs` |
| Animations feel unnatural | `spring-physics` + `easing` + `exit-faster-than-enter` |
| Form UX is poor | `inline-validation` + `error-clarity` + `focus-management` |
| Navigation feels confusing | `nav-hierarchy` + `bottom-nav-limit` + `back-behavior` |
| Layout breaks on small screens | `mobile-first` + `breakpoint-consistency` |
| Performance / jank | `virtualize-lists` + `main-thread-budget` + `debounce-throttle` |
