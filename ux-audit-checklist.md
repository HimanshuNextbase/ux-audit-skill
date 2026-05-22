# 🔍 UX Audit Checklist

> **A practical, standalone checklist for auditing the user experience of any web or mobile application.**
>
> Use this document to systematically evaluate your product's UX. Each item is a pass/fail checkpoint with a clear threshold. Work through each category, check off passing items, and use the scoring section at the end to calculate an overall grade.

### How to Use

1. Go screen-by-screen through your app
2. For each category, evaluate every item — check `[x]` for pass, leave `[ ]` for fail
3. Note severity: 🔴 **Critical** (must fix before launch) · 🟡 **Warning** (fix soon) · 🔵 **Info** (polish item)
4. Calculate your score at the end

---

## 🧭 1. Navigation

_Does the user always know where they are, where they can go, and how to get back?_

| # | Severity | Check | Pass/Fail |
|---|----------|-------|-----------|
| 1.1 | 🔴 | **Consistent nav items across screens** — The same navigation elements (tab bar, sidebar, top nav) appear on every screen where expected. No items randomly appear/disappear. | `[ ]` |
| 1.2 | 🔴 | **Active state is visually distinct** — The currently active nav item is clearly distinguishable from inactive items via color fill, weight change, or underline — not just a subtle opacity shift. | `[ ]` |
| 1.3 | 🔴 | **Back navigation always works** — Every sub-page has a clear back affordance (← arrow or system gesture). The user is never stranded on a screen with no way to return. | `[ ]` |
| 1.4 | 🟡 | **Icon + label pairing** — Nav icons are paired with text labels. No icon-only navigation unless the icon is universally understood (e.g., home, search, profile). | `[ ]` |
| 1.5 | 🟡 | **Tab bar is fixed at bottom (mobile)** — On mobile, the primary tab bar is anchored to the bottom of the screen within the thumb zone — not hidden behind a hamburger menu. | `[ ]` |
| 1.6 | 🟡 | **Nav icon sizes are consistent** — All navigation icons use the same dimensions (e.g., 24×24px or 28×28px). No icon is visually larger/smaller than its siblings. | `[ ]` |
| 1.7 | 🟡 | **Breadcrumbs or context indicators on deep pages** — Pages ≥2 levels deep show breadcrumbs, a screen title, or a clear parent indicator so the user knows their location. | `[ ]` |
| 1.8 | 🟡 | **Sub-page nav doesn't conflict with global nav** — When a sub-page has its own tabs/segments, they are visually distinct from the global navigation (different style, position, or treatment). | `[ ]` |
| 1.9 | 🔵 | **Swipe-back gesture works (mobile)** — On iOS, edge-swipe-back is not blocked by custom gestures. On Android, the system back button/gesture navigates as expected. | `[ ]` |
| 1.10 | 🔵 | **Current page title is visible** — Every screen has a visible title in the header/toolbar that describes what the user is looking at. | `[ ]` |
| 1.11 | 🔵 | **No dead-end screens** — Every screen leads somewhere or provides a clear next action. No screen is a pure dead end with zero affordances. | `[ ]` |
| 1.12 | 🔵 | **Deep links resolve correctly** — Shared URLs or notification taps open the correct screen — not the home page or a broken state. | `[ ]` |

---

## 📐 2. Layout & Spacing

_Is the spatial system consistent, comfortable to read, and easy to interact with?_

| # | Severity | Check | Pass/Fail |
|---|----------|-------|-----------|
| 2.1 | 🔴 | **Touch targets ≥ 44×44 pt (iOS) / 48×48 dp (Android)** — Every interactive element (button, link, icon-button, checkbox) meets the minimum touch target size. Measure the tappable area, not just the visible element. | `[ ]` |
| 2.2 | 🔴 | **Content respects safe areas** — No content is clipped by the status bar, notch, dynamic island, or home indicator. Content does not render behind system UI. | `[ ]` |
| 2.3 | 🔴 | **No overlapping elements** — No text, buttons, or images overlap each other on any screen at any supported screen size. | `[ ]` |
| 2.4 | 🟡 | **Spacing scale is consistent** — The app uses a defined spacing scale (e.g., 4/8/12/16/24/32px). Spot-check: measure 10 random gaps — all should map to the scale (±1px tolerance). | `[ ]` |
| 2.5 | 🟡 | **Primary CTA is in thumb zone (mobile)** — The most important action on each screen is placed in the lower 2/3 of the screen, reachable with a natural thumb arc. | `[ ]` |
| 2.6 | 🟡 | **Related content is grouped via whitespace** — Logically related items (e.g., form fields in a section) have tighter spacing between them than between unrelated sections. Gestalt proximity principle applied. | `[ ]` |
| 2.7 | 🟡 | **Horizontal margins are ≥ 16px** — Content has at least 16px padding from the screen edges. No text or interactive elements touch the edge of the viewport. | `[ ]` |
| 2.8 | 🟡 | **Form field padding is sufficient** — Input fields have ≥ 12px internal padding. Text inside fields does not touch the border. | `[ ]` |
| 2.9 | 🟡 | **No excessive whitespace** — No section has padding > 48px (mobile) or > 64px (desktop) that creates a "lost in space" feeling. Content density is balanced. | `[ ]` |
| 2.10 | 🟡 | **Consistent card/container padding** — All cards/containers on the same screen use identical internal padding. No card has 16px padding next to one with 24px. | `[ ]` |
| 2.11 | 🔵 | **Scroll content starts below header** — Content does not start hidden behind a transparent or overlapping header. Initial scroll position shows the first content item fully. | `[ ]` |
| 2.12 | 🔵 | **Bottom padding accounts for tab bar** — The last scrollable item has enough bottom padding that it's fully visible above the tab bar or bottom nav. | `[ ]` |
| 2.13 | 🔵 | **Grid alignment is consistent** — Elements that should be aligned (e.g., left edges of labels, card grids) are pixel-aligned on the same axis. | `[ ]` |

---

## 🔤 3. Typography

_Is text readable, hierarchical, and consistently styled?_

| # | Severity | Check | Pass/Fail |
|---|----------|-------|-----------|
| 3.1 | 🔴 | **Minimum body text size ≥ 14px (mobile) / 16px (web)** — No body text is smaller than this threshold. Captions/footnotes may be 12px but are not used for primary content. | `[ ]` |
| 3.2 | 🔴 | **Text hierarchy has ≥ 4 distinct levels** — The app uses at least 4 clearly distinguishable type levels (e.g., H1=28px bold, H2=22px semibold, Body=16px regular, Caption=12px). Each level differs in size AND/OR weight. | `[ ]` |
| 3.3 | 🟡 | **Line height ≥ 1.4 for body text** — Body paragraphs have line-height of at least 1.4× the font size (ideal: 1.5×). Dense text walls with 1.0–1.2 line-height fail. | `[ ]` |
| 3.4 | 🟡 | **Single font family (or deliberate pairing)** — The app uses one font family, or at most two with a clear purpose (e.g., sans-serif for UI + monospace for code). No accidental font mixing. | `[ ]` |
| 3.5 | 🟡 | **Weight differentiation is clear** — Bold/semibold is used for emphasis or headings; regular for body. There is a visible weight difference — not two weights that look identical (e.g., 400 vs 450). | `[ ]` |
| 3.6 | 🟡 | **Body text line length ≤ 75 characters** — On wide screens, body text blocks are constrained to ≤ 75 characters per line (ideal: 50–65). Text does not stretch edge-to-edge on desktop. | `[ ]` |
| 3.7 | 🟡 | **Text alignment is consistent** — Body text is left-aligned (LTR) or right-aligned (RTL). No center-aligned body paragraphs. Center alignment is reserved for short headings or CTAs only. | `[ ]` |
| 3.8 | 🔵 | **No orphaned words** — Headings don't have a single word dangling on the last line. If they do, the layout adjusts or the copy is rewritten. | `[ ]` |
| 3.9 | 🔵 | **Truncation uses ellipsis** — Text that overflows its container is truncated with `…` (not clipped abruptly). Tapping/hovering reveals the full text. | `[ ]` |
| 3.10 | 🔵 | **Numbers use tabular/monospace figures** — Numeric data in tables, prices, or counters uses tabular-width figures so digits align vertically. | `[ ]` |

---

## 🎨 4. Color & Contrast

_Are colors accessible, intentional, and consistently applied?_

| # | Severity | Check | Pass/Fail |
|---|----------|-------|-----------|
| 4.1 | 🔴 | **Text contrast ratio ≥ 4.5:1 (WCAG AA)** — All body text meets WCAG AA contrast ratio against its background. Use a contrast checker tool on every text color/background pair. | `[ ]` |
| 4.2 | 🔴 | **Large text contrast ratio ≥ 3:1** — Text ≥ 18px (or 14px bold) meets at least 3:1 contrast ratio against its background. | `[ ]` |
| 4.3 | 🔴 | **Color is not the only indicator** — Information conveyed by color (e.g., error states, success, categories) also uses a secondary indicator: icon, text label, pattern, or shape. | `[ ]` |
| 4.4 | 🟡 | **Single accent color discipline** — The app uses one primary accent color for interactive elements (buttons, links, toggles). A second accent color is used sparingly if at all. No rainbow of random highlight colors. | `[ ]` |
| 4.5 | 🟡 | **Active vs inactive states use distinct colors** — Active/selected items use the accent color; inactive items use a muted neutral. The difference is ≥ 3:1 contrast between the two states. | `[ ]` |
| 4.6 | 🟡 | **Neutral palette is cohesive** — Background, card, and text colors share the same temperature (all warm grays or all cool grays). No mixing warm beige backgrounds with cool blue-gray text. | `[ ]` |
| 4.7 | 🟡 | **Buttons use dark text on light backgrounds** — Primary action buttons with light/medium fill colors use dark text (not white text on a medium-blue that barely passes contrast). | `[ ]` |
| 4.8 | 🟡 | **Semantic colors are correct** — Red = destructive/error, green = success/positive, yellow/amber = warning, blue = info. No green "delete" buttons or red "success" states. | `[ ]` |
| 4.9 | 🔵 | **Dark mode colors are not just inverted** — If dark mode exists, it uses adjusted colors (not pure #000 background or inverted brand colors). Shadows become glows or are removed. Contrast is re-verified. | `[ ]` |
| 4.10 | 🔵 | **Maximum 5–6 colors in the palette** — The full color palette (excluding grays) contains ≤ 6 intentional colors. Spot-check: are there any one-off colors used on a single screen? | `[ ]` |

---

## 🧩 5. Components

_Are UI components well-crafted, consistent, and behaving as users expect?_

| # | Severity | Check | Pass/Fail |
|---|----------|-------|-----------|
| 5.1 | 🔴 | **Buttons look tappable** — Buttons have visible affordances: fill color, border, or shadow. They don't look like plain text. The user can distinguish buttons from labels at a glance. | `[ ]` |
| 5.2 | 🔴 | **Interactive elements have active/pressed states** — Buttons, cards, and tappable items show a visual response on press (opacity change, scale, color shift). No "dead" feeling on tap. | `[ ]` |
| 5.3 | 🔴 | **Empty states have content** — Screens that can be empty (lists, search results, inbox) show a helpful empty state with: illustration/icon + message + suggested action (CTA). Never a blank white screen. | `[ ]` |
| 5.4 | 🔴 | **Selection flows end with a CTA** — When the user selects items (filters, options, multi-select), there is a clear "Apply" / "Done" / "Save" button. Selections don't apply silently with no confirmation. | `[ ]` |
| 5.5 | 🟡 | **Cards have a single primary action** — Each card has one clear tappable target. If the entire card is tappable, nested buttons inside are avoided or visually subordinated. | `[ ]` |
| 5.6 | 🟡 | **Settings screens use consistent layout** — All settings/preferences use the same list pattern: label left, control right (toggle, chevron, value). No mixing of random layouts within settings. | `[ ]` |
| 5.7 | 🟡 | **Icon-only buttons in tight spaces** — When space is limited (toolbars, table rows), icon-only buttons are used. When space allows, icon + label is preferred. This choice is consistent, not random. | `[ ]` |
| 5.8 | 🟡 | **Checkmarks/selection indicators match design system** — All selection states (checkboxes, radio buttons, selected list items) use the same visual style: same accent color, same size, same shape. | `[ ]` |
| 5.9 | 🟡 | **Modals/dialogs have clear dismiss affordance** — Every modal has an X button, a "Cancel" option, or tap-outside-to-dismiss. The user is never trapped in a modal. | `[ ]` |
| 5.10 | 🟡 | **Form inputs show their state** — Inputs visually distinguish between: default, focused, filled, error, and disabled states. At minimum, focused and error must be distinct. | `[ ]` |
| 5.11 | 🟡 | **Destructive actions require confirmation** — Delete, remove, or irreversible actions show a confirmation dialog or use a two-step pattern (e.g., swipe then tap). No single-tap permanent deletion. | `[ ]` |
| 5.12 | 🔵 | **Toggles reflect current state** — Toggle switches clearly show on/off state with color and position. The label describes what happens when the toggle is ON, not what it controls ambiguously. | `[ ]` |
| 5.13 | 🔵 | **Segmented controls are ≤ 5 options** — Tab-style segmented controls have no more than 5 options. If more, a dropdown, filter chip group, or full-page selector is used instead. | `[ ]` |
| 5.14 | 🔵 | **Loading indicators match the component** — Skeleton screens for content areas, spinners for buttons, progress bars for multi-step flows. The loading indicator fits the context. | `[ ]` |

---

## 📱 6. Mobile Patterns

_Does the app follow platform conventions and feel native?_

| # | Severity | Check | Pass/Fail |
|---|----------|-------|-----------|
| 6.1 | 🔴 | **Bottom sheet for contextual actions (not full modals)** — Quick actions, filters, and option menus use bottom sheets that partially cover the screen — not full-screen modals that lose context. | `[ ]` |
| 6.2 | 🔴 | **Keyboard does not cover input fields** — When the keyboard opens, the active input field scrolls into view above the keyboard. No typing blind into an obscured field. | `[ ]` |
| 6.3 | 🔴 | **No horizontal scroll on vertical pages** — Vertical scroll pages do not accidentally allow horizontal scrolling. Content fits within the viewport width. | `[ ]` |
| 6.4 | 🟡 | **Pull-to-refresh on list/feed screens** — List screens support pull-to-refresh as a standard reload mechanism. The gesture feels native (not a custom implementation with odd physics). | `[ ]` |
| 6.5 | 🟡 | **Gesture conflicts are avoided** — Custom swipe gestures don't conflict with system gestures (edge-swipe back on iOS, system navigation on Android). Horizontal carousels don't block page-back. | `[ ]` |
| 6.6 | 🟡 | **Platform conventions respected** — iOS apps use iOS-style components (rounded rects, SF Symbols, sheet presentations). Android apps use Material patterns. No Android-style UI on iOS or vice versa. | `[ ]` |
| 6.7 | 🟡 | **Editor/canvas screens maximize content area** — On editor, drawing, or media creation screens, the canvas takes ≥ 75% of screen height. Chrome (toolbars, headers) is minimal and can be dismissed. | `[ ]` |
| 6.8 | 🟡 | **Long lists use lazy loading** — Lists with > 20 items load progressively (infinite scroll or pagination) rather than loading everything at once and freezing the UI. | `[ ]` |
| 6.9 | 🟡 | **Input types match content** — Phone fields show numeric keyboard, email fields show email keyboard, URL fields show URL keyboard. No QWERTY for phone number entry. | `[ ]` |
| 6.10 | 🔵 | **Haptic feedback on key actions** — Destructive actions, toggles, and confirmations provide haptic feedback (on supported devices). Subtle, not excessive. | `[ ]` |
| 6.11 | 🔵 | **Landscape mode handled or locked** — The app either supports landscape gracefully or locks to portrait. No broken layouts on rotation. | `[ ]` |
| 6.12 | 🔵 | **Large screen / tablet support** — On iPads and tablets, the UI adapts (split view, wider margins, multi-column) rather than just stretching the phone layout. | `[ ]` |

---

## 🔗 7. Cross-Screen Consistency

_Does the entire app feel like one cohesive product?_

| # | Severity | Check | Pass/Fail |
|---|----------|-------|-----------|
| 7.1 | 🔴 | **Same color palette across all screens** — Spot-check 5+ screens: all use the same background, text, and accent colors. No screen uses a one-off color that doesn't exist elsewhere. | `[ ]` |
| 7.2 | 🔴 | **No screen looks like a different app** — Every screen is recognizably part of the same product. No screen has a completely different visual language (different fonts, colors, layout patterns). | `[ ]` |
| 7.3 | 🟡 | **Consistent border-radius** — All rounded corners use the same radius values (e.g., 8px for cards, 12px for modals, full-round for avatars). No mixing 4px and 16px radii randomly. | `[ ]` |
| 7.4 | 🟡 | **Shadow/elevation system is consistent** — If shadows are used, they follow a consistent elevation system (e.g., cards = 2dp, modals = 8dp, dropdowns = 4dp). No random shadow values. | `[ ]` |
| 7.5 | 🟡 | **Icon style is uniform** — All icons use the same style: all outlined, all filled, or all a specific icon set. No mixing outlined icons with filled ones on the same screen. | `[ ]` |
| 7.6 | 🟡 | **State patterns are reused** — Loading, error, and empty states use the same visual pattern everywhere. The loading spinner on screen A is identical to screen B. | `[ ]` |
| 7.7 | 🟡 | **Button hierarchy is consistent** — Primary buttons look the same everywhere. Secondary buttons look the same everywhere. The visual hierarchy (primary > secondary > tertiary) is maintained across all screens. | `[ ]` |
| 7.8 | 🔵 | **Animation style is uniform** — Transitions and micro-animations use the same easing curves and durations throughout. No screen has jarring or noticeably different animation timing. | `[ ]` |
| 7.9 | 🔵 | **Terminology is consistent** — The same concept uses the same word everywhere. Not "Settings" on one screen and "Preferences" on another; not "Delete" and "Remove" for the same action. | `[ ]` |
| 7.10 | 🔵 | **Header/toolbar pattern is consistent** — All screens use the same header structure: title position (left vs center), icon placement (left = back, right = actions). No screen breaks the pattern. | `[ ]` |

---

## ⚠️ 8. States & Error Handling

_Does the app handle every state gracefully — not just the happy path?_

| # | Severity | Check | Pass/Fail |
|---|----------|-------|-----------|
| 8.1 | 🔴 | **Loading states for async data** — Every screen/section that loads data shows a loading indicator (skeleton, spinner, or shimmer) while fetching. No blank screen that suddenly pops in content. | `[ ]` |
| 8.2 | 🔴 | **Error states show message + retry** — When data fails to load, the user sees: what went wrong (in plain language) + a retry button. No white screens, no cryptic error codes, no silent failures. | `[ ]` |
| 8.3 | 🔴 | **Form validation shows inline errors** — Invalid fields show an error message directly below the field (not just a toast or a generic top-of-form error). The message explains how to fix it. | `[ ]` |
| 8.4 | 🔴 | **Disabled buttons are visually distinct** — Disabled/inactive buttons are clearly grayed out or reduced opacity (≤ 0.5). The user can tell at a glance that a button is not interactive. | `[ ]` |
| 8.5 | 🟡 | **Empty states provide guidance** — Empty lists/screens show: what this screen is for + how to populate it (CTA or instructions). Not just "No items" with no context. | `[ ]` |
| 8.6 | 🟡 | **Offline state is handled** — When the device loses connectivity, the app shows a clear offline indicator and either serves cached content or explains the limitation. No silent broken state. | `[ ]` |
| 8.7 | 🟡 | **Optimistic UI for fast actions** — Quick actions (like, save, toggle) update the UI immediately without waiting for server response. Failures revert the state with an explanation. | `[ ]` |
| 8.8 | 🟡 | **Button loading states prevent double-tap** — Buttons that trigger async actions show a loading spinner and disable themselves to prevent duplicate submissions. | `[ ]` |
| 8.9 | 🔵 | **Success feedback is provided** — After completing an action (save, submit, send), the user receives confirmation: a success toast, screen transition, or visual feedback. No "did it work?" ambiguity. | `[ ]` |
| 8.10 | 🔵 | **Timeout handling exists** — Long-running requests (> 10s) show progress or allow cancellation. The app doesn't appear frozen with no feedback. | `[ ]` |
| 8.11 | 🔵 | **Session expiry is handled** — If authentication expires during use, the user is informed and redirected to login — not shown cryptic API errors or a broken UI. | `[ ]` |

---

## ♿ 9. Accessibility

_Can everyone use this product, regardless of ability?_

| # | Severity | Check | Pass/Fail |
|---|----------|-------|-----------|
| 9.1 | 🔴 | **All text meets WCAG AA contrast (4.5:1)** — Run an automated contrast check on every screen. All text passes 4.5:1 (normal text) or 3:1 (large text, ≥18px / 14px bold). | `[ ]` |
| 9.2 | 🔴 | **Interactive elements have accessible labels** — All buttons, icons, inputs, and images have meaningful `aria-label`, `alt` text, or `accessibilityLabel`. Screen readers announce something useful, not "button" or "image". | `[ ]` |
| 9.3 | 🔴 | **Touch targets ≥ 44×44 pt** — Every tappable element meets the minimum touch target size. This includes close buttons, icon buttons, and inline links. | `[ ]` |
| 9.4 | 🔴 | **Keyboard navigation works (web)** — All interactive elements are reachable and operable via Tab, Shift+Tab, Enter, and Escape. No keyboard traps. Focus order follows visual order. | `[ ]` |
| 9.5 | 🟡 | **Focus indicators are visible** — Focused elements show a clear ring/outline (not just browser default if it's invisible on the background). Focus is never invisible. | `[ ]` |
| 9.6 | 🟡 | **Heading hierarchy is logical** — Screen readers encounter headings in order (H1 → H2 → H3). No skipped levels. Each screen has exactly one H1. | `[ ]` |
| 9.7 | 🟡 | **Reduced motion is respected** — If the user has enabled "Reduce Motion" (OS setting), animations are minimized or removed. No infinite loops, parallax, or auto-playing motion. Check `prefers-reduced-motion`. | `[ ]` |
| 9.8 | 🟡 | **Form errors are announced** — Screen readers announce error messages when they appear. Errors are associated with their fields via `aria-describedby` or equivalent. | `[ ]` |
| 9.9 | 🔵 | **Text is resizable up to 200%** — Content remains usable when the user increases text size to 200% (via browser zoom or OS accessibility setting). No text is clipped or overlapping. | `[ ]` |
| 9.10 | 🔵 | **Media has alternatives** — Videos have captions. Audio has transcripts. Images that convey information have descriptive alt text. Decorative images use `alt=""`. | `[ ]` |
| 9.11 | 🔵 | **Skip navigation link exists (web)** — Web apps have a "Skip to main content" link that appears on Tab focus, allowing keyboard users to bypass repetitive navigation. | `[ ]` |

---

## ✨ 10. Visual Polish

_Does the app look intentional, refined, and professionally crafted?_

| # | Severity | Check | Pass/Fail |
|---|----------|-------|-----------|
| 10.1 | 🟡 | **No AI-generated aesthetic** — The design doesn't look like a default ChatGPT/Midjourney output: no gratuitous glassmorphism, no unnecessary gradients, no "hero image with vague 3D blobs." The design has a clear human point of view. | `[ ]` |
| 10.2 | 🟡 | **Shadows are subtle and purposeful** — Box shadows are used for elevation (cards above backgrounds, modals above content). Shadows are soft (large blur, low opacity). No harsh drop-shadows or colored shadows unless intentional. | `[ ]` |
| 10.3 | 🟡 | **Photography is authentic (if used)** — Images of people, products, or places look real — not AI-generated (check for six fingers, melted text, uncanny smoothness). Stock photos are high-quality and relevant. | `[ ]` |
| 10.4 | 🟡 | **Single icon family throughout** — The app uses one icon set (e.g., Lucide, SF Symbols, Material Icons, Phosphor). All icons share the same stroke weight, style, and visual density. | `[ ]` |
| 10.5 | 🟡 | **No gratuitous visual effects** — No glassmorphism, excessive gradients, parallax, or floating particles unless they serve the brand identity. Effects that exist purely for decoration are absent. | `[ ]` |
| 10.6 | 🟡 | **Visual rhythm is established** — Repeating elements (list items, cards, sections) have consistent height, spacing, and alignment that create a visual rhythm. Scanning the page feels ordered, not chaotic. | `[ ]` |
| 10.7 | 🔵 | **App has a signature design element** — There is at least one distinctive visual element (unique color, shape language, illustration style, interaction pattern) that makes this app recognizable vs. a generic template. | `[ ]` |
| 10.8 | 🔵 | **Illustrations/icons match brand tone** — Custom illustrations or decorative elements share the same style: same line weight, same color palette, same level of detail. No mixing cute cartoons with serious business icons. | `[ ]` |
| 10.9 | 🔵 | **Borders and dividers are minimal** — Sections are separated primarily by spacing and background color — not heavy 1px borders on every element. Dividers, when used, are subtle (light gray, ≤ 0.5px visual weight). | `[ ]` |
| 10.10 | 🔵 | **Microinteractions add delight** — Small animations (button hover, page transitions, success checkmarks) exist and feel polished. They are fast (150–300ms) and don't slow the user down. | `[ ]` |

---

## 📊 Scoring

### How to Calculate Your Score

**1. Count your results per severity level:**

| Severity | Total Items | Passed (✓) | Failed (✗) |
|----------|-------------|-------------|-------------|
| 🔴 Critical | ___ | ___ | ___ |
| 🟡 Warning | ___ | ___ | ___ |
| 🔵 Info | ___ | ___ | ___ |

**2. Calculate weighted score:**

Each severity level carries a different weight:

| Severity | Weight per item | Max impact |
|----------|----------------|------------|
| 🔴 Critical | **3 points** | High — these break usability |
| 🟡 Warning | **2 points** | Medium — these hurt usability |
| 🔵 Info | **1 point** | Low — these are polish items |

**3. Formula:**

```
Earned Points = (🔴 passed × 3) + (🟡 passed × 2) + (🔵 passed × 1)
Max Points    = (🔴 total × 3) + (🟡 total × 2) + (🔵 total × 1)
Score         = (Earned Points / Max Points) × 100
```

### Reference Totals (this checklist)

| Severity | Count |
|----------|-------|
| 🔴 Critical | 28 |
| 🟡 Warning | 48 |
| 🔵 Info | 27 |

**Maximum possible points: (28 × 3) + (48 × 2) + (27 × 1) = 84 + 96 + 27 = 207**

### Grade Thresholds

| Score | Grade | Meaning |
|-------|-------|---------|
| **90–100%** | 🏆 **A — Excellent** | Ship-ready. Minor polish only. |
| **80–89%** | ✅ **B — Good** | Solid foundation. Address remaining warnings. |
| **70–79%** | 🟡 **C — Needs Work** | Usable but inconsistent. Prioritize critical fails. |
| **60–69%** | 🟠 **D — Poor** | Significant UX issues. Requires a focused sprint. |
| **Below 60%** | 🔴 **F — Failing** | Fundamental problems. Redesign or rebuild needed. |

### Priority Rules

1. **Fix ALL 🔴 Critical failures first** — these directly harm usability and accessibility
2. **Then 🟡 Warnings** — these create friction and inconsistency
3. **Then 🔵 Info items** — these separate good from great
4. **Any 🔴 failure in Accessibility (Section 9) is a launch blocker** regardless of overall score

---

_Last updated: 2026-05-21 · Version 1.0_
_Use this checklist alongside real user testing — no checklist replaces watching humans use your product._
