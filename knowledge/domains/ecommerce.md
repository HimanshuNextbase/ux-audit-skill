# Domain Module — E-Commerce

Load this when: the product is an online store, marketplace buyer-side, or D2C brand.

---

## Top 7 Failure Patterns (check these first)

### 1. Checkout friction kills conversion
The most common conversion killer. Audit the full checkout as a cold-start user.
- Guest checkout missing or buried → P1 FLOW
- Checkout requires account creation before showing price total → P1 FLOW
- Address form has no autocomplete (`autocomplete` attributes missing) → P1 FORM
- Payment methods fewer than 3 (no UPI/PayTM in India, no GPay/Apple Pay globally) → P1 TRUST
- No progress indicator in multi-step checkout → P2 NOTIFY
- Order confirmation doesn't show estimated delivery → P2 NOTIFY

### 2. Trust signals absent at highest-anxiety moments
Users abandon carts not because of price, but because they don't trust the site.
- No security badge / SSL visual confirmation near payment → P1 TRUST
- No return/refund policy visible on product page or cart → P1 TRUST
- No customer reviews on product page (or reviews are clearly fake — round stars, generic text) → P1 TRUST
- Shipping cost hidden until checkout (revealed at last step) → P0 TRUST — dark pattern

### 3. Product page evidence gaps
- Only 1-2 product images, no zoom, no alternate angles → P2 VISUAL
- No size guide for apparel/footwear → P1 CONTENT
- Stock status absent ("In stock" vs "Only 2 left" vs "Out of stock") → P2 CONTENT
- No delivery estimate on product page (user finds out at checkout) → P1 TRUST
- Price without tax/duty shown (actual cost revealed late) → P1 TRUST

### 4. Search and filter failure
- Search returns no results for common terms (test with category name, not product name) → P1 FLOW
- No filter options on category pages with 20+ products → P2 IA
- Filters don't show count of matching products → P3 IA
- Sort options missing (price low-high, newest, most popular) → P2 IA
- Search bar not in persistent header → P2 IA

### 5. Cart and wishlist UX
- Adding to cart doesn't give clear feedback (no count update, no animation) → P1 NOTIFY
- Cart clears on session end with no recovery (no persistent cart / no email recovery) → P1 NOTIFY
- No wishlist / save-for-later option → P3 UX-OPP
- Cart doesn't show product thumbnail, color, size → P2 VISUAL

### 6. Mobile checkout is unusable
E-commerce conversion on mobile is 60-70% of traffic but checkout is often desktop-only UX.
- Input fields too small for touch — test all checkout fields at 390px → P1 MOBILE
- Payment form doesn't trigger numeric keyboard for card number field → P1 FORM
- CTA button ("Place Order") not thumb-reachable (buried below fold on mobile) → P1 MOBILE
- Apple Pay / Google Pay not offered on mobile despite being supported → P1 FLOW

### 7. Empty and error states abandoned
- Empty search results show "0 results" with no next step → P1 CONTENT
- Out-of-stock product page with no "notify me" or similar alternatives → P2 UX-OPP
- Payment failure gives generic error with no actionable next step → P1 CONTENT
- Failed order gives no reference number, no email confirmation → P0 NOTIFY

---

## PSYCH Focus Points (apply these in the PSYCH section)

| Commitment moment | The user's real fear | What to check |
|-------------------|---------------------|---------------|
| Entering card details | "Will this site steal my card?" | Security badge, HTTPS indicator, trust copy |
| Placing the order | "What if it doesn't arrive / is wrong?" | Return policy visibility, delivery guarantee |
| Signing up | "Will they spam me?" | Email field label copy, newsletter opt-in vs opt-out |
| Seeing the total with tax | "This is more than I expected" | Price transparency from product page onward |

**Reciprocity test:** Does the site give the user value before asking for their email or account? (Free shipping threshold shown? Discount code for signing up?) If no value exchange before the ask → PSYCH finding.

**Loss aversion check:** Does the site use real scarcity ("3 left in stock" from inventory, not fake countdown timers)? Fake urgency = TRUST finding + PSYCH finding combined.

---

## What Good Looks Like

- Checkout in 3 steps max: cart → shipping → payment. Order review inline, not a separate step.
- Guest checkout as prominent as "Create Account" — not hidden or secondary.
- Free shipping threshold visible on every page (sticky banner or cart sidebar).
- Product page shows: delivery estimate, return window, trust badge, and at least 4 images.
- Mobile checkout uses browser autofill for address and platform-native payment (Apple Pay/GPay).

---

## Domain-Specific "What If" Tests

Run these in addition to the standard what-if table:

| Test | How | Pass condition |
|------|-----|----------------|
| Apply invalid discount code | Enter `FAKE2024` at cart | Inline error immediately — not a page reload |
| Add max quantity | Try to add 999 of an item | Stock-aware error or max enforced with message |
| Change shipping country mid-checkout | Switch country on address form | Price and delivery estimate update dynamically |
| Payment declined (use test card 4000000000000002) | Enter Stripe test declined card | User-friendly "card declined" with specific reason |
| Return to cart after 1 hour | Add items, leave, return | Cart preserved with items |

---

## Priority Codes to Check First

`TRUST` → `FLOW` (checkout) → `FORM` (checkout fields) → `MOBILE` (checkout at 390px) → `CONTENT` (empty states)
