# UX Audit Checklist — Website

Use this file when auditing a **website or web app** (desktop + responsive).
For mobile apps use `checklists/app.md`.
Load only this file to keep context lean — it is self-contained.

---

## How to Use

Work through each section top to bottom. Mark each item:
- ✅ Pass
- ⚠️ Partial / needs improvement
- ❌ Fail
- — Not applicable

Flag every ❌ as an issue. Score it and assign a priority (see scoring at the bottom).

---

## 1. First Impression (Trunk Test)

Drop onto the page cold. Answer each question in under 2 seconds:

- [ ] What site is this? — logo/brand visible top-left, recognisable at any size
- [ ] What page am I on? — page name prominent, in the right place
- [ ] What are the major sections? — primary navigation clear and labelled
- [ ] Where am I in the site? — current section highlighted, breadcrumb present if deep
- [ ] How do I search? — search box visible if the site is content-heavy
- [ ] What is this site for? — purpose clear at a glance, no guessing required
- [ ] What can I do here? — primary action or starting point obvious without scrolling

---

## 2. Content & Copy

- [ ] Plain language — no unexplained jargon or acronyms
- [ ] All abbreviations are spelled out on first use
- [ ] CTAs are contextual, not generic ("Download the guide" not "Submit")
- [ ] All messaging (including error messages) uses consistent tone of voice
- [ ] Empty states tell the user what to do next, not just "no data"
- [ ] Page titles match what the user clicked to get there
- [ ] No happy talk / welcome text that says nothing useful
- [ ] No walls of text — short paragraphs, bullet lists where appropriate
- [ ] No lorem ipsum or placeholder content in production
- [ ] No invented metrics without a source ("10× faster", "saves 5h/week")
- [ ] Tagline describes what the product does in 6–8 words (not a vague motto)
- [ ] Information follows F or Z reading pattern placement

---

## 3. Navigation & Information Architecture

- [ ] Navigation present and consistent on every page (except intentional focus flows)
- [ ] Navigation contains: Site ID, Sections, Utilities, Search
- [ ] Menu labels are conventional — not clever, not marketing-speak
- [ ] Current page/section clearly indicated (highlighted nav item)
- [ ] Every page has a visible, prominent page name that matches what was clicked
- [ ] Breadcrumbs present for deep content — last item bold, not a link
- [ ] Footer has: secondary links, support contact, site map
- [ ] Logo in header links to home on every page
- [ ] No navigation items hidden unless in mobile responsive mode
- [ ] System does not require extra "submit" or "apply" after user completes an action
- [ ] Users can navigate back and forth on any page without losing context
- [ ] Disabled buttons explain why they are inactive
- [ ] Progress indicator present for multi-step flows — shows position AND steps remaining
- [ ] 404 and 503 pages tell the user what to do next (not just "page not found")
- [ ] Company physical address visible (if applicable)
- [ ] Support contact (phone or email) in footer or easily accessible

---

## 4. Visual Design & Typography

- [ ] Visual hierarchy communicates primary / secondary / tertiary within 2 seconds
- [ ] Primary actions are visually distinct from secondary actions
- [ ] Maximum 3 primary colours on any page
- [ ] No more than 2 font families across the site
- [ ] No more than 3 font styles per page
- [ ] Font size in body text is at least 16px
- [ ] Line length is 45–75 characters for paragraphs
- [ ] Headings use negative letter-spacing (−0.02em); body text uses normal
- [ ] Uppercase used only for labels, headers, or acronyms — not for body copy
- [ ] Type hierarchy is consistent across all pages and screens
- [ ] 8px grid — spacing in multiples of 8 (8, 16, 24, 32, 48, 64)
- [ ] Between sections: 48–64px minimum whitespace
- [ ] Inside cards: 24–32px padding
- [ ] Related content is grouped together (proximity)
- [ ] Data uses proximity and alignment to communicate relationships
- [ ] Illustrations and images look like they belong to this product (brand match)
- [ ] No text embedded in images or illustrations
- [ ] Icon set is consistent — one library per project, no mixing
- [ ] Body text line-height ≥ 1.4× font size — dense 1.0–1.2 line-height fails readability
- [ ] Overflowing text is truncated with ellipsis — not abruptly clipped; full content accessible on hover or expand
- [ ] Numeric data in tables and data displays uses tabular-width figures so digits align vertically
- [ ] Single primary accent colour — no competing saturated highlights scattered through the page
- [ ] Semantic colours applied consistently: red = destructive/error, green = success, amber = warning, blue = info
- [ ] Neutral palette uses consistent temperature — all warm or all cool grays (no mixing beige background with blue-gray text)
- [ ] Maximum 5–6 colours in the full palette — no one-off per-page colours
- [ ] Consistent border-radius values across all components — no mixing 4px cards next to 16px modals
- [ ] Micro-animations use consistent easing and duration across all pages — no jarring timing variation between sections
- [ ] Terminology consistent: the same concept uses the same word everywhere ("Settings" not "Preferences" on another page; "Delete" not "Remove")

---

## 5. Interactive States (Every Element)

Every interactive element must have all 8 states:

- [ ] **Default** — base appearance
- [ ] **Hover** — only applied via `@media (hover: hover)`
- [ ] **Focus** — via `:focus-visible`, never removed without replacement
- [ ] **Active / Pressed** — visual feedback on click/press
- [ ] **Disabled** — visually distinct + `aria-disabled="true"` + `cursor: not-allowed`
- [ ] **Loading** — spinner or skeleton; `aria-busy="true"`
- [ ] **Error** — red/error colour + icon + `aria-invalid="true"`
- [ ] **Success** — confirmation visual + `aria-live="polite"` announcement

---

## 6. Feedback & System Status

- [ ] All clickable elements have a hover state indicating they are clickable
- [ ] Loading > 3 seconds → loader shows remaining time hint, not just a spinner
- [ ] Spinners: delay-show 150ms; once visible, stay visible minimum 300ms
- [ ] Toasts are fixed-position at viewport corner — never shift page layout
- [ ] Toasts only shown for: failures, async completions, confirmations — NOT trivial saves
- [ ] Confirmation dialogs only for irreversible actions — reversible deletes use optimistic delete + undo toast
- [ ] Alert messages (snack bars, toasts, banners) are consistent and visually distinct from page content
- [ ] Errors: user can return to exact error point without losing progress
- [ ] Confirmation on form submission is visually distinct
- [ ] After an error, users can restart the process OR return to the error without losing progress
- [ ] Async action buttons show a loading spinner and disable themselves to prevent duplicate submissions
- [ ] Quick actions (toggle, like, save) update UI optimistically without waiting for server response — failures revert with explanation
- [ ] Long-running requests > 10s show a progress indicator or allow cancellation — page never appears frozen with no feedback
- [ ] Session expiry during active use is communicated — user redirected to sign-in, not shown a broken page or cryptic API error

---

## 7. Forms & Input

- [ ] Every field has a visible label — no placeholder-only labels
- [ ] Labels are outside fields, not floating inside
- [ ] Field width matches expected input length
- [ ] Real-time validation for complex fields (password, email, username) — not post-submit
- [ ] Error messages are inline, field-specific, and include a correction hint
- [ ] Valid fields preserved after a submit error — focus moves to first invalid field
- [ ] Forms grouped by intent and context
- [ ] Minimum required fields only — no unnecessary fields
- [ ] Long dropdowns avoided
- [ ] Complex fields (date, time) reduce number of clicks
- [ ] Button stays disabled until all required fields are filled (2+ field forms)
- [ ] Browser auto-fill supported
- [ ] Field label always visible in the filled state (not replaced by value)
- [ ] Incorrect data type blocked at field level (numbers blocked in name field)
- [ ] Button hierarchy clear (primary vs secondary vs tertiary)
- [ ] Radio buttons for single-select choices only
- [ ] Checkboxes for multi-select choices only
- [ ] Text links visually different from body copy

---

## 8. Authentication

- [ ] Password requirements shown BEFORE entry, not after a failed attempt
- [ ] Eye toggle to reveal/hide password
- [ ] Browser password generation supported
- [ ] "Remember me" checkbox present on login screen
- [ ] Forgot password link visible on login screen
- [ ] Social sign-in available (where applicable)
- [ ] "Create account" option on login page
- [ ] Login / sign-in heading visible on login page
- [ ] Product logo present on login page
- [ ] "I agree" to T&C located next to the registration button
- [ ] Password confirmation field shows match status in real time
- [ ] Tab order through login form makes sense

---

---

## 10. Performance (Visual Indicators)

- [ ] Page feels responsive within 2.5 seconds (LCP target)
- [ ] No visible layout shift during page load (CLS target ≤ 0.1)
- [ ] Interactions respond immediately — no perceptible lag (INP target ≤ 200ms)
- [ ] Hero / LCP image is NOT lazy-loaded — uses `fetchpriority="high"`
- [ ] Images sized appropriately for their display dimensions
- [ ] Skeleton loading used for content-heavy areas, not spinners only
- [ ] Chart areas have reserved dimensions — no shift when data loads
- [ ] No `width: 100vw` (causes horizontal scroll when scrollbar present — use `100%` with container padding)

### Core Web Vitals Targets
| Metric | Good | Needs Work | Poor |
|--------|------|-----------|------|
| LCP | ≤ 2.5s | 2.5–4s | > 4s |
| INP | ≤ 200ms | 200–500ms | > 500ms |
| CLS | ≤ 0.1 | 0.1–0.25 | > 0.25 |
| TTFB | ≤ 800ms | 800ms–1.8s | > 1.8s |

---

## 11. SEO Basics

- [ ] Every page has a unique, descriptive title tag (under 60 characters)
- [ ] Every page has a unique meta description (under 160 characters)
- [ ] No `noindex` on revenue or conversion pages
- [ ] Images have descriptive alt text (also benefits SEO)
- [ ] Canonical tags present where needed (pagination, duplicate content)
- [ ] Structured data valid — no critical errors (use Rich Results Test)
- [ ] SSL certificate present and enforced site-wide

---

## 12. Security & Trust Baseline

- [ ] HTTPS enforced site-wide — no mixed-content warnings
- [ ] SSL certificate valid and not expiring soon
- [ ] Cookie consent option present
- [ ] Location access requests explicit user permission
- [ ] Contact access requests explicit user permission
- [ ] Prices clearly shown — no hidden fees
- [ ] Privacy policy easily findable
- [ ] Security headers reviewed (use MDN HTTP Observatory or ZAP baseline)

---

## 13. Anti-Slop Detection (AI-Generated UI Tells)

Flag any of the following:

**Critical — ships as slop:**
- [ ] Purple / indigo-to-pink gradient hero
- [ ] The AI nav: wordmark + 4–5 centred links + CTA right + sticky white + hairline border-bottom
- [ ] The AI footer: 4-column Product / Company / Resources / Legal layout
- [ ] 3-column feature grid (no varied widths or heights)
- [ ] Full-viewport centred hero (`height: 100vh`, everything centred)
- [ ] Card-in-card (bordered container containing bordered cards)
- [ ] Gradient headline (`background-clip: text` with gradient fill)
- [ ] Pure `#000000` or `#ffffff` — untinted neutrals
- [ ] Invented metrics without evidence
- [ ] Generic emoji as feature icons (✨🚀⚡🔥🎯)
- [ ] Inter as the only typeface
- [ ] Aurora-blob or floating-orb background decorations
- [ ] Re-drawn UI chrome (fake browser bar or phone frame in HTML/CSS)
- [ ] `loading="lazy"` on the hero / LCP image
- [ ] AI-generated photography — people/places imagery shows six fingers, melted text, or uncanny smoothness

**Major — looks AI-generated:**
- [ ] `transition-all` instead of specific properties
- [ ] Universal `hover:scale-105` on all cards
- [ ] Eyebrow label on every section (`01 / FEATURES` etc.)
- [ ] Glassmorphism without a literal layer to see through
- [ ] Bounce / elastic easing on UI controls
- [ ] Celebratory toast for a trivial save operation
- [ ] Confirmation dialog for a reversible action
- [ ] Auto-rotating carousel with no pause control
- [ ] Animate-on-scroll on every section
- [ ] No signature design element — site is indistinguishable from generic template output (no unique colour, shape language, or interaction pattern specific to this product)

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

**P0 override:** Force P0 if the issue blocks sign-in, payment/billing, legal consent, or keyboard-only completion on a critical journey — regardless of numeric score.

---

## Report Output

Use `templates/full-report.md` for the complete report.
Use `templates/executive-scorecard.md` for a leadership snapshot.
Use `templates/issue-entry.json` for individual tickets.
