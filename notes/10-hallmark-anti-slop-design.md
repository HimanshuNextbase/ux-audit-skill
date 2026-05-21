# Hallmark: Anti-Slop Design System

Source: https://github.com/Nutlope/hallmark
Files: references/slop-test.md, references/anti-patterns.md, references/macrostructures.md, references/interaction-and-states.md
Note: Duplicates from notes 01–09 filtered out — only unique content saved here.

---

## Pre-Emit Self-Critique (Before Any Gate Sweep)

Before running any slop-gate checks, run this 6-axis internal critique:

| Axis | Question |
|------|----------|
| **Philosophy** | Is there a clear *why* behind every major decision? |
| **Hierarchy** | Can you tell primary / secondary / tertiary in 2 seconds? |
| **Execution** | Are all details in the spec (tokens, variants, states)? |
| **Specificity** | Does this look like *this* brief, or could it be any SaaS? |
| **Restraint** | Is everything earning its place, or is there decoration for decoration's sake? |
| **Variety** | Does this have a different structural fingerprint from the previous output? |

Record the score as a comment: `/* Hallmark · pre-emit critique: P5 H4 E5 S4 R5 V5 */`

**Rule:** Score < 3 on any axis → complete a revision pass before proceeding to gate checks.

---

## 21 Macrostructures (Named Page Shapes)

Every page has an implicit shape. Before emitting, pick a named macrostructure — stamp it in a CSS comment `/* Hallmark · macrostructure: Bento Grid */` — and never use the same shape twice in a single output set.

| # | Name | Character |
|---|------|-----------|
| 01 | **Bento Grid** | Asymmetric tile layout — different-sized cells, mixed content types |
| 02 | **Long Document** | Linear scroll, typographic hierarchy, article-style reading experience |
| 03 | **Marquee Hero** | Large animated text or image band draws first attention |
| 04 | **Stat-Led** | Lead with metrics/numbers above the fold; proof before pitch |
| 05 | **Workbench** | Product UI screenshot or demo embedded as the hero itself |
| 06 | **Conversational FAQ** | Page reads as a dialogue — questions and answers drive the layout |
| 07 | **Manifesto** | Strong opinion or belief statement as the structural center |
| 08 | **Photographic** | Real photography as the dominant visual element throughout |
| 09 | **Quote-Led** | Customer quote or endorsement opens the page |
| 10 | **Specimen** | Showcases the design system, type scale, or component library itself |
| 11 | **Catalogue** | Dense item grid — products, works, or resources with minimal chrome |
| 12 | **Letter** | Written as a personal letter to the reader (founder, team) |
| 13 | **Index-First** | Navigation/index is the hero — browse before explanation |
| 14 | **Narrative Workflow** | Tells a before → after story, step by step |
| 15 | **Split Studio** | Persistent split — content one side, example/demo the other |
| 16 | **Feature Stack** | Long vertical list of features, each taking a full section |
| 17 | **Type Specimen** | Typography itself is the design — minimal visual, maximum font expression |
| 18 | **Portfolio Grid** | Case study or project thumbnails as the primary content |
| 19 | **Map/Diagram** | Visual system diagram, architecture map, or org chart leads |
| 20 | **Ecosystem Index** | Shows integrations, partners, or connected products as a system |
| 21 | **Component Playground** | Interactive component demos are the main content |

**SaaS page sequence** (for Bento Grid / Stat-Led / Workbench / Marquee Hero):
Hero → Logo wall → Features → Testimonials → Pricing → FAQ → Final CTA strip → Footer

---

## Anti-Patterns by Severity

### Critical (Ships as Slop)

These patterns are disqualifying. Presence of any = AI-default output, not intentional design.

| Pattern | Description | Fix |
|---------|-------------|-----|
| **Inter-everywhere** | One font across the entire page — screams template | Add a second typeface for headings or use weight contrast within the family |
| **3-column feature grid** | Every LLM defaults to this; it reads as a placeholder | Vary column widths, mix section heights, use Feature Stack macrostructure instead |
| **Card-in-card** | Bordered container that contains cards — double containment | Pick one containment layer: either the outer border OR the inner cards, not both |
| **Gradient headline** | `background-clip: text` with a gradient fill on headings | Use solid ink — gradient text is a decoration that obscures rather than elevates |
| **Side-stripe card** | Thick colored border on one edge of a card | Use a hairline (1px) or remove the border entirely |
| **Full-viewport centred hero** | `height: 100vh` with everything centered | Let the hero be content height, not a viewport-filling centering exercise |
| **Pure black / pure white** | `#000000` or `#ffffff` as background or text | Tint the neutral toward the anchor hue (e.g., `#0A0A0F`, `#FAFAF8`) |
| **Default-attractor sameness** | Two consecutive outputs using the same macrostructure | Check CSS for existing macrostructure stamp; pick a different one |
| **Specimen fall-through** | Using the Specimen macrostructure when brief didn't ask for editorial | Reserve Specimen for design-system showcases only |
| **The AI nav** | Wordmark left + 4–5 inline links centred + CTA right + sticky white + hairline `border-bottom` | This pattern appears on every brief regardless of context — it's genre-blind. Vary: flush left nav, vertical sidebar, no sticky, dark surface |
| **The AI footer** | 4-column links (Product / Company / Resources / Legal) + social icons + copyright | Pick from a footer routing table matched to the product type; don't emit 4-column by default |
| **Aurora-blob background** | Flowing mesh gradient blobs as background decoration | Use a solid surface or subtle grain texture |
| **Floating-orb decoration** | Ambient 3D spheres in background | Cut them entirely |
| **Sound-on autoplay** | `<video>` without `muted` attribute | Always: `autoplay muted loop playsinline` |
| **Lazy-loaded LCP** | `loading="lazy"` on the hero/LCP image | Use `fetchpriority="high"` and no lazy on above-the-fold images |
| **Invented metrics** | "10× faster", "saves 5 hours/week" with no source | Use a placeholder or ask the client for real data — never fabricate |
| **Re-drawn UI chrome** | Fake browser bar, phone frame, or code-block window built in HTML/CSS | Use a real screenshot or a minimal CSS frame; don't simulate OS chrome |
| **Mid-render token improvisation** | Inline hex/OKLCH values outside the token block | All color values live in the token file; no exceptions during render |
| **Wrap-to-two-lines clickable text** | CTA or nav link that wraps mid-phrase | Shorten the label or add `white-space: nowrap` |
| **Lottie shortcut** | LottieFiles community animation (someone else's work) | Build custom with CSS/SVG animation |
| **Three.js for a still object** | Non-interactive 3D object using Three.js | Use a high-res photo or SVG instead |

---

### Major (Looks AI-Generated)

| Pattern | Description | Fix |
|---------|-------------|-----|
| **Bounce/elastic easing on buttons** | Spring physics on button presses — disruptive, not satisfying | Use `ease-out` or custom `cubic-bezier` — no `spring()` on UI controls |
| **Centred everything** | Every section center-aligned regardless of content type | Bias the layout — wide left margin, reverse alternating sections |
| **Eyebrow on every section** | `01 / EXAMPLES` label before each heading | Eyebrows are **default OFF** — only use when genuinely ordinal. Hard ban: two-column section heads with tag left + header right |
| **Shadow-glow on dark surfaces** | Colored halo/glow around elevated elements on dark backgrounds | Use lightness (lighter surface = elevated) not glow for elevation on dark |
| **Icon-tile feature card** | Rounded rectangle + icon + heading + copy (same for every feature) | Make asymmetric: vary card sizes, or drop the containment and use inline icons |
| **Glassmorphism without purpose** | `backdrop-filter: blur` applied decoratively | Only use glassmorphism when there's a literal layer to see through |
| **Hover-only affordances** | Interactive element only shows clickability on hover | Every hover affordance needs: `:focus-visible` state + tap affordance |
| **Tabular data without tabular-nums** | Number columns with proportional figures — digits don't align | Add `font-variant-numeric: tabular-nums` to all number columns |
| **Animate-on-scroll on everything** | Every section triggers a fade-up or reveal on scroll | Reserve scroll animation for 1–2 key moments; don't animate prose |
| **Mismatched icon sets** | Icons from multiple libraries in one project | Icons are typography — one library per project. Defaults: Lucide (SaaS), Phosphor (weight variants), Heroicons (Tailwind/shadcn projects) |
| **AI-illustration look** | Smooth mesh-blob characters, corporate-doodle style | Commission custom SVG or use CSS illustration; avoid vector stock packs |

---

### Microinteraction Tells

| Pattern | Fix |
|---------|-----|
| `transition-all` | Specify properties explicitly: `transition: color 150ms ease, background 150ms ease` |
| Universal `hover:scale-105` | Pick one transform signal per element type — not the same on everything |
| Bouncy overshoot easings on UI controls | `ease-out` for entrances, `ease-in` for exits; never `spring()` on form controls |
| Animated hover gradients | Gradient direction/color should not animate — only opacity or transform |
| Cursor follower dots | Cut entirely — they break accessibility and add no UX value |
| Auto-rotating carousels with no pause | WCAG 2.2.2 violation — add pause control; default to static or manual-only |
| Celebratory success toasts for trivial saved actions | Silent success — only show toasts for: failures, async completions, and confirmations. Not for saving a preference. |
| Confirmation dialogs for reversible actions | Use optimistic delete + undo toast instead — confirmation dialogs are only for irreversible operations |
| **Tooltip timing: same delay on hover and focus** | Hover delay: 800–1000ms. Focus delay: 0ms (immediate). Never use the same delay for both. |
| **Focus rings that animate in** | Focus rings must appear instantly — never transition `outline` or `box-shadow` on `:focus` gain |
| Toasts that shift layout | Toasts must be `position: fixed` at viewport corner — never flow-positioned |
| Universal scroll-triggered fade-up | One or two key moments max; never every section |
| Spinners that flash for <150ms | Delay-show the spinner 150ms; once visible, keep it visible minimum 300ms to avoid flash |

---

### Minor Tells

| Pattern | Fix |
|---------|-----|
| Straight quotes `'text'` | Use curly quotes `'text'` `"text"` |
| Double-hyphen dashes `--` | Use em dash `—` |
| Three periods `...` | Use ellipsis character `…` |
| Placeholder names Jane Doe / John Smith | Use plausible, diverse names — vary ethnicity, first names |
| Startup-cliché product names (Acme, Nexus, Pulse) | Name concretely — describe what it does |
| `z-index: 9999` | Use a named 6-level scale: 10 (sticky), 20 (dropdown), 30 (modal overlay), 40 (modal), 50 (toast), 60 (tooltip) |
| Every section padded the same | Vary vertical padding — dense sections read differently than spacious ones |
| `width: 100vw` | Use `width: 100%` with container padding — `100vw` causes horizontal scroll when a scrollbar is present |

---

## 8-State Interactive Element Requirement

Every interactive element must have all 8 states designed — not just default and hover:

| State | Implementation |
|-------|---------------|
| **Default** | Base appearance |
| **Hover** | Only apply with `@media (hover: hover)` — don't style hover on touch-primary devices |
| **Focus** | Use `:focus-visible` not `:focus` — keyboard users see it, mouse users don't |
| **Active / Pressed** | `transform: scale(0.97)` or color shift on `active` pseudo-class |
| **Disabled** | `opacity: 0.5` + `cursor: not-allowed` + `aria-disabled="true"` |
| **Loading** | Spinner or skeleton replacing content; `aria-busy="true"` |
| **Error** | Red border + error icon + `aria-invalid="true"` |
| **Success** | Green confirmation + `aria-live="polite"` announcement |

**Hit target expansion without visual change:**
```css
.small-icon-button {
  position: relative;
}
.small-icon-button::before {
  content: '';
  position: absolute;
  inset: -8px;          /* expands tap area 8px in all directions */
  /* no background — invisible expansion */
}
```
Use this to reach 44×44px minimum without changing the visual icon size.

---

## Tooltip Timing Rule (New — Not in Prior Notes)

Tooltip delays must differ by trigger method:

| Trigger | Delay |
|---------|-------|
| Mouse hover | 800–1000ms (long delay prevents flicker as cursor passes through) |
| Keyboard focus | 0ms (immediate — keyboard user is already intentionally on the element) |

Applying the same delay to both fails keyboard users who need instant feedback.

---

## Focus Ring Rule

Focus rings must **never animate in**. The outline or box-shadow on `:focus-visible` must appear instantly at the moment of focus — no `transition` on these properties during focus gain. Animation on focus gain fails users who navigate by keyboard: the ring appears late and creates visual lag that breaks spatial orientation.

```css
/* ❌ Wrong */
.button:focus-visible {
  outline: 2px solid blue;
  transition: outline 200ms ease;  /* never do this */
}

/* ✅ Correct */
.button:focus-visible {
  outline: 2px solid blue;
  /* no transition — instant appearance */
}
```

---

## Icon Set Defaults by Project Type

| Project Type | Icon Library |
|-------------|-------------|
| SaaS / general web | **Lucide** |
| Weight variants needed (thin → bold) | **Phosphor** |
| Tailwind CSS / shadcn/ui projects | **Heroicons** |

Rule: one library per project. Mixing icon sets is as jarring as mixing typefaces.
