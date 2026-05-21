# Example Audit: SaaS Dashboard

**Type:** Composite teaching example (not a live brand audit)
**Product type:** SaaS web app
**Scope:** Sign-in → Dashboard → Create report → Share → Settings
**Input:** URL + credentials + frontend repo

---

## What Is Working

- ✅ Global search is prominent and keyboard-accessible (Cmd+K shortcut works)
- ✅ Saved filters persist across sessions — supports power-user workflows
- ✅ Data density is appropriate on large screens; information-rich without feeling cluttered
- ✅ Active nav item is clearly highlighted

---

## Findings

### A11Y-001: Keyboard focus disappears inside modal
- **Priority:** P0 | **Score:** 18
- **What:** Opening the "Create Report" modal moves focus in, but Tab then escapes the modal onto background content. Escape does not close the modal.
- **Why it matters:** Keyboard-only and assistive technology users cannot complete the primary workflow.
- **Standard:** WCAG 2.1.2 (No Keyboard Trap); WAI-ARIA APG Modal Dialog Pattern
- **Fix:** Implement APG-compliant modal: trap focus within the modal while open, return focus to the trigger element on close, Escape key closes.
- **Code fix:** Use a focus-trap library or implement manually — query all focusable elements within the modal, intercept Tab/Shift+Tab, and cycle within.

### PERF-001: Charts cause layout shift during loading
- **Priority:** P1 | **Score:** 14
- **What:** Dashboard charts render after data loads, causing the page to shift by ~180px. CLS measured at 0.34 (fails Core Web Vitals threshold of 0.1).
- **Why it matters:** Causes mis-clicks, disorientation, and fails Google's CLS threshold — affecting search ranking for the marketing pages that share the domain.
- **Standard:** Core Web Vitals CLS ≤ 0.1
- **Fix:** Reserve chart dimensions with `min-height` matching the final rendered height. Use a skeleton loader (grey placeholder bars) while data loads.

### A11Y-002: Status chips fail contrast
- **Priority:** P1 | **Score:** 13
- **What:** "Active" chip uses #4CAF50 on #F1F8E9 = 2.1:1 contrast ratio. Fails WCAG AA (4.5:1 for text).
- **Why it matters:** Users with low vision or colour deficiency cannot distinguish status states — and colour is the only differentiator (no icon or pattern).
- **Standard:** WCAG 1.4.3; WCAG 1.4.1 (use of colour)
- **Fix:** Darken text or background to reach 4.5:1. Add a secondary non-colour indicator (icon or text prefix: "● Active").

### IA-001: Icon-only sidebar navigation
- **Priority:** P1 | **Score:** 12
- **What:** The left sidebar collapses to icons only with no persistent labels and no tooltips on focus.
- **Why it matters:** Recognition is slower than recall — users must hover each icon to learn what it does. No label on focus means keyboard users get no context.
- **Standard:** Nielsen heuristic 6 — Recognition rather than recall
- **Fix:** Add persistent text labels (even small ones at 11px). At minimum, add immediate tooltips on `:focus-visible` (0ms delay, unlike hover which waits 800–1000ms).

### CONTENT-001: Empty state says "No data" only
- **Priority:** P2 | **Score:** 9
- **What:** The Reports page with no reports shows "No data available" with no further guidance.
- **Why it matters:** Dead end for new users — they don't know what to do next.
- **Standard:** Nielsen heuristic 1 — Visibility of system status; Krug — empty states should tell users what to do
- **Fix:** Add explanation ("You haven't created any reports yet"), a primary action button ("Create your first report"), and a link to documentation.

---

## Quick Wins

| Fix | Time | Impact |
|-----|------|--------|
| Add focus-trap to modal (use existing library already in dependencies) | 1 hr | Critical — unblocks keyboard users |
| Add `role="status"` + icon to status chips | 30 min | High — removes colour-only reliance |
| Add `:focus-visible` tooltip (0ms delay) to sidebar icons | 45 min | Medium — keyboard nav clarity |

---

## Roadmap

- **P0:** A11Y-001 — modal focus trap
- **P1:** PERF-001 (reserve chart dimensions), A11Y-002 (status chip contrast), IA-001 (sidebar labels)
- **P2:** CONTENT-001 (empty states across all list views)
- **CI:** Add `@axe-core/playwright` assertion on the dashboard and modal flows; add LHCI CLS budget of 0.1

---

## Key Lesson

> A SaaS dashboard that keyboard users cannot navigate is not accessible — and WCAG keyboard compliance is a legal requirement in most jurisdictions. The modal focus trap is a P0 regardless of its numeric score because it blocks a primary journey for an entire class of users.
