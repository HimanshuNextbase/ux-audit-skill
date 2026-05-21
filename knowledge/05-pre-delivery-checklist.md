# Pre-Delivery UI/UX Checklist

---

## Quick Pre-Delivery Checks (Web)

- [ ] No emojis used as icons (use SVG: Heroicons/Lucide)
- [ ] `cursor-pointer` on all clickable elements
- [ ] Hover states with smooth transitions (150–300ms)
- [ ] Light mode: text contrast 4.5:1 minimum
- [ ] Focus states visible for keyboard nav
- [ ] `prefers-reduced-motion` respected
- [ ] Responsive: test at 375px, 768px, 1024px, 1440px

---

## Full Pre-Delivery Checklist (App UI — iOS/Android/React Native/Flutter)

### Visual Quality
- [ ] No emojis used as icons (use SVG instead)
- [ ] All icons from a consistent icon family and style (stroke width, corner radius)
- [ ] Official brand assets used with correct proportions and clear space
- [ ] Pressed-state visuals do NOT shift layout bounds or cause jitter
- [ ] Semantic theme tokens used consistently (no ad-hoc hardcoded hex per-screen)

### Interaction
- [ ] All tappable elements provide clear pressed feedback (ripple/opacity/elevation)
- [ ] Touch targets meet minimum size (≥44×44pt iOS, ≥48×48dp Android)
- [ ] Micro-interaction timing stays in 150–300ms range with native-feeling easing
- [ ] Disabled states are visually clear and non-interactive
- [ ] Screen reader focus order matches visual order; interactive labels are descriptive
- [ ] Gesture regions avoid nested/conflicting interactions (tap/drag/back-swipe conflicts)

### Light/Dark Mode
- [ ] Primary text contrast ≥4.5:1 in both light and dark mode
- [ ] Secondary text contrast ≥3:1 in both light and dark mode
- [ ] Dividers/borders distinguishable in both modes
- [ ] Modal/drawer scrim opacity strong enough (typically 40–60% black)
- [ ] Both themes tested before delivery (not inferred from single theme)

### Layout
- [ ] Safe areas respected for headers, tab bars, and bottom CTA bars
- [ ] Scroll content not hidden behind fixed/sticky bars
- [ ] Verified on small phone, large phone, and tablet (portrait + landscape)
- [ ] Horizontal insets/gutters adapt correctly by device size and orientation
- [ ] 4/8dp spacing rhythm maintained across component, section, and page levels
- [ ] Long-form text measure remains readable on larger devices

### Accessibility
- [ ] All meaningful images/icons have accessibility labels
- [ ] Form fields have labels, hints, and clear error messages
- [ ] Color is NOT the only indicator (add icon/text too)
- [ ] Reduced motion and dynamic text size supported without layout breakage
- [ ] Accessibility traits/roles/states (selected, disabled, expanded) announced correctly

---

## Design System Output Checklist (from `--design-system` command)

Before delivering any design, the system auto-generates these checks:

- [ ] Recommended Pattern selected (e.g., Hero-Centric + Social Proof)
- [ ] Style matched to product type (e.g., Soft UI Evolution)
- [ ] Color palette defined with named values (Primary, Secondary, CTA, Background, Text)
- [ ] Typography pair selected (heading / body font)
- [ ] Key effects specified (hover states, transition timing)
- [ ] Anti-patterns listed and avoided
- [ ] Pre-delivery checklist reviewed

---

## Common Issues That Make UI Look Unprofessional

### Icons & Visual Elements
| Issue | Fix |
|-------|-----|
| Emoji as structural icons | Use Phosphor / Heroicons / Lucide SVG icons |
| Raster PNG icons that blur | Use SVG or platform vector icons |
| Layout-shifting press states | Use color/opacity transitions; no layout bound changes |
| Wrong brand logos | Use official brand assets following their guidelines |
| Inconsistent icon sizes | Define design tokens (icon-sm, icon-md=24pt, icon-lg) |
| Mixed stroke widths | Use consistent stroke (1.5px or 2px) throughout |
| Mixed filled/outline at same level | One icon style per hierarchy level |
| Small icons without expanded tap area | Minimum 44×44pt; use hitSlop if needed |
| Misaligned icons | Align to text baseline; consistent padding |
| Low-contrast icons | WCAG 4.5:1 for small, 3:1 minimum for larger glyphs |

### Layout & Spacing
| Issue | Fix |
|-------|-----|
| Fixed UI under notch/status bar | Respect top/bottom safe areas |
| Tappable content in gesture areas | Add spacing for status/navigation bars |
| Inconsistent widths between screens | Consistent content width per device class |
| Random spacing increments | Use consistent 4/8dp spacing system |
| Edge-to-edge text on tablets | Keep readable text measure; max-width for long-form |
| Same gutter on all device sizes | Adaptive gutters by breakpoint |
| Scroll content hidden behind fixed bars | Add bottom/top content insets |

### Interaction
| Issue | Fix |
|-------|-----|
| No visual response on tap | Provide pressed feedback within 80–150ms |
| Instant transitions (0ms) | 150–300ms with platform-native easing |
| Unlabeled controls | Ensure screen reader focus order + descriptive labels |
| Controls that look tappable but do nothing | Use disabled semantics + reduced emphasis |
| Tiny tap targets | ≥44×44pt (iOS) or ≥48×48dp (Android) |
| Overlapping gestures | One primary gesture per region |
| Generic containers as primary controls | Use native primitives with proper accessibility roles |
