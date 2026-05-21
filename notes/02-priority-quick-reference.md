# Priority Quick Reference — UX Rule Categories

---

## Rule Priority Table

| Priority | Category | Impact | Key Checks | Anti-Patterns |
|----------|----------|--------|------------|---------------|
| 1 | Accessibility | CRITICAL | Contrast 4.5:1, Alt text, Keyboard nav, Aria-labels | Removing focus rings, Icon-only buttons without labels |
| 2 | Touch & Interaction | CRITICAL | Min 44×44px, 8px+ spacing, Loading feedback | Hover-only interactions, Instant state changes (0ms) |
| 3 | Performance | HIGH | WebP/AVIF, Lazy loading, Reserve space (CLS < 0.1) | Layout thrashing, Cumulative Layout Shift |
| 4 | Style Selection | HIGH | Match product type, Consistency, SVG icons (no emoji) | Mixing flat & skeuomorphic, Emoji as icons |
| 5 | Layout & Responsive | HIGH | Mobile-first breakpoints, Viewport meta, No horizontal scroll | Horizontal scroll, Fixed px containers, Disable zoom |
| 6 | Typography & Color | MEDIUM | Base 16px, Line-height 1.5, Semantic color tokens | Text < 12px body, Gray-on-gray, Raw hex in components |
| 7 | Animation | MEDIUM | Duration 150–300ms, Motion conveys meaning | Decorative-only animation, Animating width/height |
| 8 | Forms & Feedback | MEDIUM | Visible labels, Error near field, Progressive disclosure | Placeholder-only label, Errors only at top |
| 9 | Navigation Patterns | HIGH | Predictable back, Bottom nav ≤5, Deep linking | Overloaded nav, Broken back behavior |
| 10 | Charts & Data | LOW | Legends, Tooltips, Accessible colors | Color alone to convey meaning |

---

## 1. Accessibility (CRITICAL)

- `color-contrast` — Min 4.5:1 normal text, 3:1 large text
- `focus-states` — Visible focus rings 2–4px on all interactive elements
- `alt-text` — Descriptive alt text for meaningful images
- `aria-labels` — aria-label for icon-only buttons
- `keyboard-nav` — Tab order matches visual order; full keyboard support
- `form-labels` — Use `<label>` with `for` attribute or wrap input
- `skip-links` — Skip to main content for keyboard users
- `heading-hierarchy` — Sequential h1→h6, no level skip
- `color-not-only` — Don't convey info by color alone (add icon/text)
- `dynamic-type` — Support system text scaling; avoid truncation as text grows
- `reduced-motion` — Respect `prefers-reduced-motion`
- `voiceover-sr` — Meaningful accessibilityLabel/accessibilityHint
- `escape-routes` — Provide cancel/back in modals and multi-step flows
- `keyboard-shortcuts` — Preserve system and a11y shortcuts

---

## 2. Touch & Interaction (CRITICAL)

- `touch-target-size` — Min 44×44pt (Apple) / 48×48dp (Material)
- `touch-spacing` — Min 8px gap between touch targets
- `hover-vs-tap` — Use click/tap for primary; don't rely on hover alone
- `loading-buttons` — Disable button during async; show spinner
- `error-feedback` — Clear error messages near the problem
- `cursor-pointer` — Add cursor-pointer to clickable elements (Web)
- `gesture-conflicts` — Avoid horizontal swipe on main content
- `tap-delay` — Use `touch-action: manipulation`
- `press-feedback` — Visual feedback on press within 80–150ms
- `haptic-feedback` — Use for confirmations; avoid overuse
- `safe-area-awareness` — Keep targets away from notch and gesture bar
- `swipe-clarity` — Swipe actions must show clear affordance

---

## 3. Performance (HIGH)

- `image-optimization` — WebP/AVIF, responsive images (srcset/sizes), lazy load
- `image-dimension` — Declare width/height or use aspect-ratio (prevents CLS)
- `font-loading` — `font-display: swap` to avoid FOIT
- `critical-css` — Inline critical CSS or early-load stylesheet
- `lazy-loading` — Lazy load non-hero components
- `bundle-splitting` — Split code by route/feature
- `third-party-scripts` — Load async/defer; remove unnecessary ones
- `content-jumping` — Reserve space for async content
- `virtualize-lists` — Virtualize lists with 50+ items
- `main-thread-budget` — Keep per-frame work under ~16ms for 60fps
- `input-latency` — Keep input latency under ~100ms
- `tap-feedback-speed` — Visual feedback within 100ms of tap
- `debounce-throttle` — Debounce/throttle high-frequency events

---

## 4. Style Selection (HIGH)

- `style-match` — Match style to product type
- `consistency` — Same style across all pages
- `no-emoji-icons` — Use SVG icons (Heroicons, Lucide), not emojis
- `color-palette-from-product` — Choose palette from product/industry
- `effects-match-style` — Shadows, blur, radius aligned with chosen style
- `platform-adaptive` — Respect iOS HIG vs Material idioms
- `state-clarity` — Hover/pressed/disabled states visually distinct
- `elevation-consistent` — Consistent elevation/shadow scale
- `dark-mode-pairing` — Design light/dark together
- `icon-style-consistent` — One icon set / visual language throughout
- `primary-action` — One primary CTA per screen

---

## 5. Layout & Responsive (HIGH)

- `viewport-meta` — `width=device-width initial-scale=1` (never disable zoom)
- `mobile-first` — Design mobile-first, scale up
- `breakpoint-consistency` — 375 / 768 / 1024 / 1440
- `readable-font-size` — Min 16px body text on mobile
- `line-length-control` — Mobile 35–60 chars; desktop 60–75 chars
- `horizontal-scroll` — No horizontal scroll on mobile
- `spacing-scale` — 4pt/8dp incremental spacing system
- `container-width` — Consistent max-width on desktop
- `z-index-management` — Define z-index scale (0 / 10 / 20 / 40 / 100 / 1000)
- `fixed-element-offset` — Fixed navbar/bottom bar reserves safe padding
- `viewport-units` — Prefer `min-h-dvh` over `100vh` on mobile
- `visual-hierarchy` — Size, spacing, contrast — not color alone

---

## 6. Typography & Color (MEDIUM)

- `line-height` — 1.5–1.75 for body text
- `line-length` — 65–75 chars per line
- `font-scale` — Consistent type scale (12 / 14 / 16 / 18 / 24 / 32)
- `weight-hierarchy` — Bold headings (600–700), Regular body (400), Medium labels (500)
- `color-semantic` — Define semantic tokens (primary, error, surface) not raw hex
- `color-dark-mode` — Desaturated/lighter tonal variants; test contrast separately
- `color-accessible-pairs` — Meet 4.5:1 (AA) or 7:1 (AAA)
- `truncation-strategy` — Prefer wrapping; when truncating use ellipsis + expand
- `whitespace-balance` — Use whitespace intentionally to group/separate

---

## 7. Animation (MEDIUM)

- `duration-timing` — 150–300ms micro-interactions; complex ≤400ms
- `transform-performance` — Only `transform`/`opacity`; avoid width/height/top/left
- `loading-states` — Skeleton when loading > 300ms
- `easing` — `ease-out` entering, `ease-in` exiting
- `motion-meaning` — Every animation expresses cause-effect, not decoration
- `spring-physics` — Prefer spring/physics curves over linear
- `exit-faster-than-enter` — Exit ~60–70% of enter duration
- `stagger-sequence` — Stagger list items 30–50ms per item
- `interruptible` — Animations must be interruptible by user
- `no-blocking-animation` — Never block user input during animation
- `scale-feedback` — Subtle scale (0.95–1.05) on press for cards/buttons

---

## 8. Forms & Feedback (MEDIUM)

- `input-labels` — Visible label per input (not placeholder-only)
- `error-placement` — Error below the related field
- `submit-feedback` — Loading → success/error
- `required-indicators` — Mark required fields (asterisk)
- `empty-states` — Helpful message + action when no content
- `toast-dismiss` — Auto-dismiss in 3–5s
- `confirmation-dialogs` — Confirm before destructive actions
- `inline-validation` — Validate on blur, not keystroke
- `input-type-keyboard` — Semantic input types for correct mobile keyboard
- `error-clarity` — State cause + how to fix (not just "Invalid input")
- `focus-management` — After submit error, auto-focus first invalid field
- `touch-friendly-input` — Mobile input height ≥44px
- `destructive-emphasis` — Destructive actions use red; separated from primary

---

## 9. Navigation Patterns (HIGH)

- `bottom-nav-limit` — Max 5 items; icons + labels
- `back-behavior` — Predictable and consistent; preserve scroll/state
- `deep-linking` — All key screens reachable via deep link/URL
- `tab-bar-ios` — iOS: bottom Tab Bar for top-level navigation
- `nav-label-icon` — Navigation items must have both icon and text label
- `nav-state-active` — Current location visually highlighted
- `modal-escape` — Clear close/dismiss affordance; swipe-down on mobile
- `state-preservation` — Navigating back restores scroll position, filters, inputs
- `bottom-nav-top-level` — Bottom nav is for top-level screens only
- `adaptive-navigation` — Large screens ≥1024px prefer sidebar
- `back-stack-integrity` — Never silently reset the navigation stack
- `focus-on-route-change` — After page transition, move focus to main content

---

## 10. Charts & Data (LOW)

- `chart-type` — Match chart type to data (trend→line, comparison→bar, proportion→pie)
- `color-guidance` — Accessible palettes; avoid red/green-only for colorblind users
- `legend-visible` — Always show legend near the chart
- `tooltip-on-interact` — Tooltips on hover (Web) or tap (mobile)
- `axis-labels` — Label axes with units; readable scale
- `responsive-chart` — Charts reflow or simplify on small screens
- `empty-data-state` — "No data yet" + guidance, not blank chart
- `large-dataset` — 1000+ points: aggregate/sample; drill-down for detail
- `touch-target-chart` — Interactive elements ≥44pt tap area
- `no-pie-overuse` — Avoid pie/donut for >5 categories
