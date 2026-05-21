# Example Audit: Mobile PWA

**Type:** Composite teaching example (not a live brand audit)
**Product type:** Mobile Progressive Web App (booking / scheduling)
**Scope:** Install flow → Browse → Book → Offline behavior → Update flow
**Input:** URL + Lighthouse PWA audit + device emulation 390×844

---

## What Is Working

- ✅ App is installable — valid web manifest and service worker registered
- ✅ Key content (browse and read) accessible in weak/offline connectivity
- ✅ Install prompt shown at the right moment (after user demonstrates intent)

---

## Findings

### MOBILE-001: Touch targets too small throughout booking flow
- **Priority:** P1 | **Score:** 14
- **What:** Time slot selector buttons measure 32×28px. Date navigation arrows measure 28×28px. Both fall below the 44×44px minimum.
- **Why it matters:** Error-prone for all users; excludes users with motor disabilities. Booking mistakes cause real support cost.
- **Standard:** Material Design 3 minimum touch target; Apple HIG; WCAG 2.5.5 (AAA) and 2.5.8 (AA, WCAG 2.2)
- **Fix:** Increase visual size OR use `::before` pseudo-element to expand the tap area without changing the visual layout:
  ```css
  .time-slot::before {
    content: '';
    position: absolute;
    inset: -8px; /* expands tap area 8px in all directions */
  }
  ```

### IA-001: Bottom navigation labels are vague
- **Priority:** P1 | **Score:** 12
- **What:** Bottom nav items are labelled "Home", "Explore", "You" — generic labels that don't communicate what each section contains for this specific product.
- **Why it matters:** Slows navigation for new users; increases mis-taps; doesn't tell users what they'll find.
- **Standard:** Nielsen heuristic 6 — Recognition rather than recall; Apple HIG navigation guidelines
- **Fix:** Use task-oriented labels specific to the product: "Find" / "My Bookings" / "Account". Pair each with a matching icon and an active-state indicator.

### TRUST-001: Offline mode silently serves stale data
- **Priority:** P1 | **Score:** 15
- **What:** When offline, the app shows availability data (time slots) from the cache with no indication that the data may be out of date. Users can attempt to book slots that are no longer available.
- **Why it matters:** Creates booking failures that feel like app bugs. Destroys trust. Increases support load.
- **Standard:** web.dev PWA checklist — offline behavior; Nielsen heuristic 1 — Visibility of system status
- **Fix:** Show a banner when serving cached data: "You're offline — availability shown may be outdated. [Retry]". Include a "Last updated: X minutes ago" timestamp. Disable the booking CTA or warn before submitting.

### A11Y-001: Booking form breaks at high zoom / narrow width
- **Priority:** P0 | **Score:** 17
- **What:** At 400% zoom (WCAG reflow test, equivalent to 320px CSS width), the booking form's date picker overflows horizontally. The "Confirm" button is partially obscured.
- **Why it matters:** Excludes users who rely on browser zoom (low vision, older users). WCAG reflow is a Level AA criterion.
- **Standard:** WCAG 1.4.10 Reflow (Level AA)
- **Fix:** Fix the date picker to use a responsive layout with `flex-wrap` or `grid`. Ensure the Confirm button is full-width at narrow viewports. Test at 320px CSS width.

### PWA-001: No update notification after new version available
- **Priority:** P2 | **Score:** 8
- **What:** When a new service worker version is available, the app silently serves the old version. Users on stale versions can encounter feature mismatches with the server.
- **Why it matters:** Creates confusing behavior — users see different features than what's documented. Support calls increase.
- **Standard:** web.dev PWA checklist — handling updates
- **Fix:** Listen for the `waiting` service worker state and show a non-intrusive banner: "A new version is available — [Refresh to update]". On click, call `skipWaiting()` and reload.

---

## Quick Wins

| Fix | Time | Impact |
|-----|------|--------|
| Add `::before` pseudo-element overlay to time slot buttons | 30 min | High — fixes touch target failures without layout changes |
| Add offline banner with "Last updated" timestamp | 1 hr | High — prevents booking failures and trust damage |
| Rename bottom nav labels to task-oriented names | 15 min | Medium — immediate recognition improvement |

---

## Roadmap

- **P0:** A11Y-001 — fix reflow/zoom at 320px
- **P1:** MOBILE-001 (touch targets), IA-001 (nav labels), TRUST-001 (offline state)
- **P2:** PWA-001 (update notification)
- **CI:** Add Lighthouse PWA assertion (`pwa: ["error", { minScore: 0.9 }]`); add reflow test at 320px width in Playwright

---

## Key Lesson

> PWAs that work "well enough" on a fast connection often fail silently offline. Offline UX is not just "show cached content" — it requires communicating data freshness, disabling actions that require connectivity, and providing clear recovery paths. Treat offline states the same as error states: explicit, informative, and recoverable.
