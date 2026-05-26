# UX Audit Checklist — Mobile App

Use this file when auditing a **mobile app** (iOS, Android, or mobile PWA).
For websites and web apps use `checklists/site.md`.
Load only this file to keep context lean — it is self-contained.

---

## How to Use

Work through each section top to bottom. Mark each item:
- ✅ Pass
- ⚠️ Partial / needs improvement
- ❌ Fail
- — Not applicable

Flag every ❌ as an issue. Score it and assign a priority (see scoring at the bottom).
Test on real device or accurate emulation at 390×844 (iPhone 14) and 360×800 (Android).

---

## 1. First Impression

- [ ] App purpose is clear within 3 seconds of launch
- [ ] Onboarding can be skipped or started from the beginning at any time
- [ ] First screen shows what the user can do, not just branding
- [ ] Sign-in / sign-up options both visible on the entry screen
- [ ] No mandatory account creation before the user can explore (where applicable)

---

## 2. Navigation & Structure

- [ ] Navigation matches the platform convention (iOS: tab bar at bottom; Android: bottom nav or drawer)
- [ ] Bottom nav labels are task-oriented and specific, not generic ("My Bookings" not "Home")
- [ ] Active navigation item clearly highlighted with both colour and icon state change
- [ ] No more than 5 items in bottom navigation
- [ ] Main navigation items always visible — not hidden behind hamburger in primary flow
- [ ] Back navigation works correctly and goes to the logical previous state
- [ ] Deep links go to the correct page, not always to home
- [ ] Current page / section is always clear
- [ ] Progress indicator present for multi-step flows — shows position AND steps remaining
- [ ] Footer / overflow menus contain secondary navigation, not primary actions
- [ ] Sub-page screens replace the bottom tab bar with a back button + page title in the header — global nav does not persist inside deep sub-flows

---

## 3. Touch & Interaction

- [ ] Touch targets minimum 44×44 CSS px — use `::before` pseudo-element overlay if needed to expand without changing visual size
- [ ] Enough spacing between adjacent tap targets (minimum 8px gap)
- [ ] Primary actions reachable with one thumb in natural hold position (lower portion of screen)
- [ ] Swipeable content (galleries, carousels) is obvious and responds immediately
- [ ] No hover-only affordances — every interactive element has an obvious tap affordance
- [ ] Active / pressed state gives immediate visual feedback (scale, colour, or ripple)
- [ ] No accidental triggers from scrolling over interactive elements
- [ ] Gesture-based actions have a visible affordance or discoverable entry point
- [ ] Pull-to-refresh present where content can be updated
- [ ] Swipe to go back works on iOS (when using native navigation)
- [ ] Horizontal swipeable content (carousels, galleries) does not conflict with the system back gesture (iOS edge swipe / Android gesture navigation)
- [ ] Haptic feedback used for destructive actions, toggles, and confirmations where platform supports it

---

## 4. Forms on Mobile

- [ ] Every field has a visible label — no placeholder-only labels
- [ ] Keyboard type matches the input field:
  - [ ] Email → `type="email"` (@ key prominent)
  - [ ] Phone → `type="tel"` (numeric pad)
  - [ ] Number → `type="number"` or `inputmode="numeric"`
  - [ ] URL → `type="url"`
  - [ ] Search → `type="search"`
- [ ] Autocorrect disabled for data entry fields (names, codes, addresses)
- [ ] Auto-capitalise disabled for email and username fields
- [ ] Fields tall enough to be easily tappable (minimum 44px height)
- [ ] Responsive forms are single-column — no side-by-side fields on narrow screens
- [ ] On-screen keyboard does not cover active input fields (page scrolls to keep field visible)
- [ ] Real-time validation for complex fields — not post-submit
- [ ] Error messages are inline, field-specific, and include a correction hint
- [ ] Valid fields preserved after a submit error
- [ ] Button stays disabled until all required fields are filled (2+ field forms)
- [ ] "Done" / "Go" / "Search" soft-keyboard action matches the expected form action

---

## 5. Authentication (Mobile)

- [ ] Password requirements shown BEFORE entry, not after a failed attempt
- [ ] Eye toggle to reveal/hide password
- [ ] Biometric authentication offered (Face ID, fingerprint) where supported
- [ ] Social sign-in available (where applicable)
- [ ] "Remember me" / "Stay signed in" option present
- [ ] Forgot password accessible from the login screen
- [ ] Password confirmation shows match status in real time
- [ ] Login page has a visible heading
- [ ] "Create account" option on login screen

---

## 6. Content & Copy

- [ ] Plain language — no unexplained jargon
- [ ] CTAs are contextual, not generic
- [ ] Empty states tell the user what to do next with an action button
- [ ] Error messages are human-readable and include a fix or next step
- [ ] Loading states communicate what is happening (not just a spinner)
- [ ] No lorem ipsum or placeholder content in production
- [ ] Notification copy is specific ("Your order has shipped" not "Update available")
- [ ] Onboarding copy is brief — no paragraphs of instruction text

---

## 7. Visual Design & Typography

- [ ] Body text minimum 16px
- [ ] Fonts used in text content are at least 14px minimum (captions / metadata)
- [ ] Font styles limited to 3 or fewer per screen
- [ ] Sufficient contrast between text and background (4.5:1 for normal text, 3:1 for large)
- [ ] Colour is never the sole indicator of meaning — icon or text always accompanies colour
- [ ] Visual hierarchy clear within 2 seconds — primary / secondary / tertiary
- [ ] Primary actions visually distinct from secondary actions
- [ ] Images and product photos are high resolution and not blurry at device pixel ratio
- [ ] Text on images is readable (sufficient contrast + not relying on image for legibility)
- [ ] Icon set is consistent — one library across the app, no mixing styles
- [ ] All icons represent what they actually do (no generic icons for specific actions)
- [ ] Body text line-height ≥ 1.4× font size — dense 1.0–1.2 line-height fails readability
- [ ] Overflowing text is truncated with ellipsis — not abruptly clipped; full text accessible on tap or expand
- [ ] Numeric data in tables, prices, and counters uses tabular-width figures so digits align vertically
- [ ] Maximum 5–6 distinct colours in the palette — no one-off per-screen colours that don't exist elsewhere
- [ ] Single primary accent colour for interactive elements — no competing saturated highlights scattered across the app
- [ ] Semantic colour rule applied consistently: red = destructive/error, green = success, amber = warning, blue = info
- [ ] Neutral palette uses consistent temperature — all warm grays or all cool grays (no mixing beige with blue-gray)
- [ ] Border-radius values consistent throughout — cards, sheets, and buttons use the same defined set of radii
- [ ] Micro-animations use consistent easing and duration (150–300ms) — no jarring timing differences between screens
- [ ] Terminology is consistent: the same action uses the same word everywhere (not "Delete" on one screen and "Remove" on another)

---

## 8. Interactive States

Every interactive element must have all 8 states:

- [ ] **Default** — base appearance
- [ ] **Hover** — only via `@media (hover: hover)` (tablets with pointer)
- [ ] **Focus** — visible focus indicator via `:focus-visible`
- [ ] **Active / Pressed** — immediate visual feedback
- [ ] **Disabled** — visually distinct + `cursor: not-allowed` + explains why when tapped
- [ ] **Loading** — skeleton or spinner visible
- [ ] **Error** — error colour + icon + inline error message
- [ ] **Success** — confirmation visual shown

---

## 9. Feedback & System Status

- [ ] Loading > 3 seconds → loader shows remaining time hint, not just a spinner
- [ ] Spinners: delay-show 150ms; once visible, stay visible minimum 300ms
- [ ] Toasts are fixed-position — never shift page layout
- [ ] Toasts only shown for: failures, async completions, confirmations — NOT trivial saves
- [ ] Confirmation dialogs only for irreversible actions — reversible deletes use optimistic delete + undo toast
- [ ] After an error, user can return to exact error point without losing progress
- [ ] Network errors are clearly communicated with a retry option
- [ ] All async operations have a visible loading state
- [ ] Async action buttons show a loading spinner and disable themselves to prevent duplicate submissions
- [ ] Quick actions (toggle, save, reaction) update UI optimistically without waiting for server response — failures revert with explanation
- [ ] Long-running requests > 10s show a progress indicator or allow cancellation — app never appears frozen with no feedback
- [ ] Session expiry during active use is communicated — user redirected to sign-in, not shown a broken UI or cryptic API error

---

## 10. Accessibility (Mobile)

### Contrast & Colour
- [ ] Text contrast minimum 4.5:1; UI elements 3:1
- [ ] App usable with system large-text enabled
- [ ] App usable with system colour-invert / high-contrast modes
- [ ] Colour is never the sole indicator of meaning

### Touch & Motor
- [ ] All touch targets minimum 44×44px
- [ ] Spacing between adjacent targets minimum 8px
- [ ] No time-limited interactions that can't be extended
- [ ] No motion-triggered actions without an accessible alternative

### Semantics (iOS VoiceOver / Android TalkBack)
- [ ] All interactive elements have accessible names (labels, content descriptions)
- [ ] Icons and image buttons have descriptive labels
- [ ] Custom controls have correct accessibility roles
- [ ] Decorative images do not clutter the visual layout or compete with primary content
- [ ] Reading order matches visual order
- [ ] Dynamic content changes announced via accessibility live regions
- [ ] Modal/sheet focus is trapped while open; dismissed on back gesture or close button

### Zoom & Reflow
- [ ] Zooming is allowed (meta viewport must not disable user-scalable)
- [ ] Text scales correctly when OS large-text setting is active
- [ ] No content clipped or hidden when text size increases
- [ ] Content usable at 320px CSS width (landscape narrow / zoomed in)

---

## 11. Orientation & Responsive

- [ ] App responds correctly to both portrait and landscape orientation
- [ ] Important elements reachable in both orientations
- [ ] No content cut off or inaccessible in landscape mode
- [ ] Design matches screenshots in the app store / Play Store
- [ ] Content respects safe areas — nothing rendered behind notch, Dynamic Island, status bar, or home indicator
- [ ] First scrollable item is fully visible below the header — content doesn't start hidden behind a transparent overlapping header
- [ ] Scrollable content has sufficient bottom padding to clear the tab bar so the last item is fully visible
- [ ] On editor, canvas, or media screens the content area occupies ≥ 75% of viewport height — chrome (toolbars, headers) is minimal

---

## 12. Performance (Mobile)

- [ ] App launches within 3 seconds on a mid-range device
- [ ] Scrolling is smooth — no jank (60fps target)
- [ ] Images are appropriately compressed for mobile bandwidth
- [ ] No layout shift during content load
- [ ] Tap responses are immediate (< 100ms perceived)
- [ ] Large lists use virtualisation / lazy loading (not rendered all at once)

### Core Web Vitals (for web-based apps / PWAs)
| Metric | Good | Needs Work |
|--------|------|-----------|
| LCP | ≤ 2.5s | > 2.5s |
| INP | ≤ 200ms | > 200ms |
| CLS | ≤ 0.1 | > 0.1 |
| TTFB | ≤ 800ms | > 800ms |

---

## 13. PWA / Offline Behavior (if applicable)

- [ ] App is installable — valid manifest + service worker
- [ ] Offline mode is clearly communicated (banner or indicator showing stale data state)
- [ ] Last-updated timestamp shown when serving cached data
- [ ] Booking / transaction actions disabled or warned before attempting while offline
- [ ] Retry / refresh option provided when offline
- [ ] Update notification shown when a new version is available
- [ ] Stale content does not silently mislead users (e.g., stale availability data)

---

## 14. Permissions & Privacy

- [ ] Location access requested in context and with explanation — not on launch
- [ ] Camera / microphone access requested only when needed for the task
- [ ] Contacts access requests explicit permission
- [ ] Push notification permission requested after the user has seen value — not on first launch
- [ ] Cookie / tracking consent present (web-based apps)
- [ ] Prices and costs clearly shown — no hidden fees

---

## 15. Help & Support

- [ ] Users can find account deletion or subscription cancellation easily
- [ ] FAQ is divided into categories and searchable
- [ ] Help opens without losing the user's current state (new tab or overlay)
- [ ] Error pages tell the user what to do next
- [ ] Support contact easily accessible from settings or footer

---

## 16. Anti-Slop Detection (AI-Generated UI Tells)

Flag any of the following:

**Critical:**
- [ ] Generic emoji as navigation icons (✨🚀⚡🔥)
- [ ] Placeholder names in user-facing content (Jane Doe, John Smith)
- [ ] Invented metrics without evidence
- [ ] Re-drawn device chrome (fake iOS status bar or phone frame in UI)
- [ ] `loading="lazy"` on above-fold / LCP images
- [ ] Sound-on autoplay (video/audio without `muted` attribute)
- [ ] AI-generated photography — people/places imagery shows six fingers, melted text, or uncanny smoothness

**Major:**
- [ ] Universal `hover:scale-105` on all list items (applies to pointer interactions)
- [ ] `transition-all` instead of specific properties
- [ ] Celebratory toast for a trivial save
- [ ] Confirmation dialog for a reversible delete
- [ ] Auto-rotating carousel with no pause control
- [ ] Bounce / elastic easing on UI controls
- [ ] Animate-on-scroll on every list item
- [ ] No signature design element — UI is indistinguishable from generic template output (no unique colour, shape language, or interaction pattern)

---

## Scoring Quick Reference

Score each flagged issue across 5 factors (0–4 each, max 20):

| Factor | 0 | 2 | 4 |
|--------|---|---|---|
| User impact | Cosmetic | Slows task | Task failure / exclusion |
| Business criticality | Peripheral | Important flow | Revenue / sign-in / legal |
| Reach | Edge case | Many users | Most sessions / sitewide |
| Recoverability | Easy self-recovery | Hard to recover | Dead end / data loss |
| Compliance risk | None | Significant | Legal / security exposure |

**Bands:** P0 = 17–20 (or override) · P1 = 13–16 · P2 = 8–12 · P3 = 1–7

**P0 override:** Force P0 if the issue blocks sign-in, payment, or core task completion on a critical journey — regardless of numeric score.

---

## Report Output

Use `templates/full-report.md` for the complete report.
Use `templates/executive-scorecard.md` for a leadership snapshot.
Use `templates/issue-entry.json` for individual tickets.
