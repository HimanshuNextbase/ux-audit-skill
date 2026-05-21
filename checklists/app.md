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
- [ ] Keyboard does not cover active input fields (scroll into view on focus)
- [ ] Real-time validation for complex fields — not post-submit
- [ ] Error messages are inline, field-specific, and include a correction hint
- [ ] Valid fields preserved after a submit error — focus moves to first invalid field
- [ ] Button stays disabled until all required fields are filled (2+ field forms)
- [ ] Tab / Next key advances to the next field in logical order
- [ ] "Done" / "Go" / "Search" action on keyboard matches the expected form action

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

---

## 8. Interactive States

Every interactive element must have all 8 states:

- [ ] **Default** — base appearance
- [ ] **Hover** — only via `@media (hover: hover)` (tablets with keyboard / pointer)
- [ ] **Focus** — via `:focus-visible` for keyboard/switch users
- [ ] **Active / Pressed** — immediate visual feedback
- [ ] **Disabled** — visually distinct + `aria-disabled="true"` + explains why when tapped
- [ ] **Loading** — skeleton or spinner with `aria-busy="true"`
- [ ] **Error** — error colour + icon + `aria-invalid="true"`
- [ ] **Success** — confirmation visual + `aria-live="polite"` announcement

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
- [ ] Decorative images are hidden from screen readers (`alt=""` / `accessibilityHidden`)
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

**Major:**
- [ ] Universal `hover:scale-105` on all list items (applies to pointer interactions)
- [ ] `transition-all` instead of specific properties
- [ ] Celebratory toast for a trivial save
- [ ] Confirmation dialog for a reversible delete
- [ ] Auto-rotating carousel with no pause control
- [ ] Bounce / elastic easing on UI controls
- [ ] Animate-on-scroll on every list item

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

**P0 override:** Force P0 if the issue blocks sign-in, payment, core task completion, or keyboard/switch-access navigation on a critical journey — regardless of numeric score.

---

## Report Output

Use `templates/full-report.md` for the complete report.
Use `templates/executive-scorecard.md` for a leadership snapshot.
Use `templates/issue-entry.json` for individual tickets.
