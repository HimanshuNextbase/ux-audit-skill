# Example Audit: E-commerce Checkout Flow

**Type:** Composite teaching example (not a live brand audit)
**Product type:** E-commerce
**Scope:** Category → Product → Cart → Checkout → Confirmation
**Input:** Live URL + mobile 390×844

---

## What Is Working

- ✅ Guest checkout exists — lowers barrier to first purchase
- ✅ Order summary visible throughout the checkout flow
- ✅ Primary CTA is consistently placed and visually prominent
- ✅ Trust signals (SSL badge, accepted cards) present at payment step

---

## Findings

### FORM-001: Two-column layout on mobile checkout
- **Priority:** P1 | **Score:** 14
- **What:** Shipping fields are arranged in a two-column grid at 390px width, forcing users to tab across small adjacent fields.
- **Why it matters:** Increases parsing effort and error rate on mobile; conflicts with thumb-input patterns on small screens.
- **Standard:** Baymard checkout usability research; W3C Forms tutorials
- **Fix:** Switch to single-column layout for all core input fields at breakpoints below 600px.

### FORM-002: Card number field rejects spaces
- **Priority:** P1 | **Score:** 13
- **What:** Entering "4111 1111 1111 1111" (with spaces, as printed on the card) triggers a validation error.
- **Why it matters:** Users copy from their physical card. Rejecting the natural format creates friction and distrust at the highest-value moment.
- **Standard:** Baymard form field usability research
- **Fix:** Accept and auto-strip spaces on input; store the normalized value. Display with spaces for readability.

### FORM-003: Error message says "Invalid input" only
- **Priority:** P1 | **Score:** 14
- **What:** Submitting the form with an invalid postal code shows "Invalid input" with no field-specific guidance.
- **Why it matters:** Users cannot self-diagnose or recover without trial and error.
- **Standard:** Nielsen heuristic 9 — Help users recognize, diagnose, and recover from errors; WCAG 3.3.1, 3.3.3
- **Fix:** Use field-specific inline error: "Postal code must be 5 digits (e.g., 94105)." Position inline below the field.

### FORM-004: Valid fields cleared after submit error
- **Priority:** P0 | **Score:** 18
- **What:** After submitting with one invalid field, all previously entered values are wiped.
- **Why it matters:** Forces users to re-enter all data; a leading cause of checkout abandonment. Also violates error recovery requirements.
- **Standard:** Nielsen heuristic 5 — Error prevention; WCAG 3.3.1; Baymard checkout UX
- **Fix:** Preserve all valid field values on submit error. Move focus to the first invalid field. Show inline error on that field only.
- **Acceptance criteria:**
  - Valid fields remain populated after any submit attempt
  - Focus moves programmatically to first invalid field
  - Error is programmatically associated with the field via aria-describedby

### A11Y-001: Form errors not announced to screen readers
- **Priority:** P1 | **Score:** 15
- **What:** Validation errors appear visually but are not announced by screen readers (no aria-live region or role="alert").
- **Why it matters:** Blind or low-vision users completing checkout receive no feedback that their submission failed.
- **Standard:** WCAG 3.3.1 (Level A); WCAG 4.1.3
- **Fix:** Wrap the error summary in `<div role="alert">` or use `aria-live="assertive"`. Also associate each field error via `aria-describedby`.

---

## Quick Wins

| Fix | Time | Impact |
|-----|------|--------|
| Change error text to field-specific messages | 30 min | High — immediate recovery improvement |
| Add `role="alert"` to error summary container | 15 min | High — unblocks screen reader users |
| Accept spaces in card number field | 1 hr | High — removes a major payment friction point |

---

## Roadmap

- **P0 (hotfix):** FORM-004 — preserve valid fields on submit error
- **P1 (this sprint):** FORM-001, FORM-002, FORM-003, A11Y-001
- **P2 (next sprint):** Add Playwright E2E test covering the full guest checkout flow + axe assertion on the checkout page

---

## Key Lesson

> Checkout is where Baymard's research shows the highest abandonment rates. Every friction point here has a direct, measurable revenue cost. P0 and P1 issues in checkout should be treated as production incidents, not design backlog items.
