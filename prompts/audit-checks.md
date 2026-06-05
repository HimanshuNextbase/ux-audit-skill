# UX Audit Checks — Subagent Reference

This file is loaded by Lane A, Lane B, and Lane C subagents INSTEAD of the full system.md.
It contains: Step 2 checklist, Step 3 anti-slop, Step 3.5 advisory, Step 4 scoring, and reference tables.
The main agent does NOT need to load this file — it is only for auditing subagents.

---

## Step 2 — Lane Reference (Used by Subagents)

Subagents load and follow these sections. Main agent does not run these directly.

### Lane A: URL / Screenshot (Rendered Experience)

Work through each category below. Flag every issue with its taxonomy code.

#### IA — Information Architecture
- Navigation present and consistent on every page
- Current page is clearly indicated (breadcrumb, highlighted nav item)
- Menu labels are conventional, not clever or jargon-heavy
- Search is present and visible if site is content-heavy
- Footer has secondary links, support contact, site map
- Logo in header links to home on every page

#### CONTENT — Copy & Language
- Plain language — no unexplained jargon or acronyms
- CTAs are contextual ("Download the guide" not "Submit")
- All error messages use the product's tone of voice
- Empty states tell the user what to do next, not just "no data"
- Page titles match what the user clicked to get there
- Tagline communicates what the product does in 6–8 words (not a vague motto)

#### FORM — Forms & Input
- Every field has a visible label (never placeholder-only)
- Field width matches expected input length
- Real-time validation for complex fields (password, username, email) — not post-submit
- Error messages are inline, specific, and include correction hints
- Valid fields are preserved after a submit error; focus moves to first invalid field
- Forms are grouped by intent and context, single-column on mobile
- Minimum required fields only — no unnecessary fields
- Complex fields (date, time) reduce clicks as much as possible
- Long dropdowns are avoided
- Button stays disabled until all required fields are filled (2+ field forms)
- Auto-fill from browser is supported

#### AUTH — Login & Registration
- Password requirements shown BEFORE entry, not after failure
- Eye toggle to reveal password
- Browser password generation supported
- "Remember me" checkbox present
- Forgot password link on login screen
- Social sign-in available
- "Create account" option on login page
- T&C "I agree" located next to the register button
- Password confirmation field shows match status in real time
- Login page has a login/sign-in heading

#### VISUAL — Design & Interaction
- Visual hierarchy communicates primary / secondary / tertiary within 2 seconds
- Primary actions are visually distinct from secondary actions
- Maximum 3 primary colors on any page
- No more than 2 font families; no more than 3 font styles per page
- All interactive elements have all 8 states: default / hover (hover media only) / focus (:focus-visible) / active / disabled / loading / error / success
- Loading > 3 seconds → loader shows remaining time hint (not just a spinner)
- Spinners: delay-show 150ms; once shown, visible minimum 300ms to prevent flash
- Toasts are fixed-position (never shift layout); only shown for failures, async completions, and confirmations — NOT for trivial saves
- Confirmation dialogs only for irreversible actions; reversible deletes use optimistic delete + undo toast
- Tooltip delay: 800–1000ms on hover; 0ms on focus
- No `transition-all`; specify properties explicitly
- No universal `hover:scale-105` on all cards
- No animate-on-scroll on every section (use for 1–2 key moments only)
- `tabular-nums` applied to all numeric columns
- Color is never the sole indicator of meaning (always add text or icon)
- Hierarchy, content, or functionality conveyed by more than color alone
- On any page, user can see relevant info without scrolling

#### NAVIGATION & SYSTEM
- When user completes an action, system does not require extra "submit" or "apply" step
- Disabled buttons explain why they are disabled
- Progress indicators for multi-step flows show current position AND steps remaining
- After an error, user can return to the exact error point without losing progress
- 404 and 503 pages tell the user what to do next
- SSL certificate present
- Prices clearly shown; no hidden fees

#### MOBILE
- Body text minimum 16px
- Touch targets minimum 44×44 CSS px (use `::before` pseudo-element overlay to expand without changing visual size)
- Keyboard type matches input field type (email → email keyboard, phone → tel, number → numeric)
- Autocorrect disabled for data entry fields (names, codes, addresses)
- Key elements reachable with one hand (primary actions in thumb zone)
- Responsive to both horizontal and vertical orientation
- No hover-only affordances (every hover state needs a focus and tap equivalent)

#### PERFORMANCE (Visual Indicators)
- No visible layout shift during page load (CLS)
- Page feels responsive within 2.5 seconds (LCP)
- Interactions respond within 200ms (INP)
- Images are appropriately sized for their display size
- Hero/LCP image not lazy-loaded (`fetchpriority="high"`, no `loading="lazy"` above fold)
- Skeleton loading used for content areas, not just spinners
- Chart areas have reserved dimensions to prevent layout shift

**Image format check — run this before recommending AVIF/WebP. Never recommend a format without verifying what is currently served:**
```js
(async () => {
  const imgs = [...document.querySelectorAll('img')].slice(0, 8).map(img => ({
    src: img.src.split('?')[0].slice(-50),
    format: img.src.split('?')[0].split('.').pop().toLowerCase(),
    loading: img.loading,
    fetchpriority: img.fetchPriority || img.getAttribute('fetchpriority'),
    width: img.naturalWidth,
    height: img.naturalHeight,
  }));
  console.log(JSON.stringify(imgs));
})();
```
If images are already WebP/AVIF → note that in the finding, don't recommend the switch. Only file a PERF image-format finding if images are actually served as JPEG/PNG when WebP/AVIF would be better.

**PERF priority thresholds — use these when scoring, not just "P2 for any perf issue":**
| Metric | P1 threshold | P2 threshold | P3 |
|--------|-------------|-------------|-----|
| LCP | > 4 s | 2.5–4 s | borderline 2.3–2.5 s |
| TTI | > 10 s | 5–10 s | 3–5 s |
| TBT | > 600 ms | 300–600 ms | 200–300 ms |
| CLS | > 0.25 | 0.1–0.25 | 0.05–0.1 |
| INP | > 500 ms | 200–500 ms | borderline |

LCP > 4s = P1 regardless of product type. TTI > 10s (e.g. 18s) = P1 for any consumer product — users leave. Score these correctly; do not downgrade to P2 because "it's a performance issue."

#### SEO
- Every page has a unique, descriptive title tag and meta description
- No indexing blocks on revenue/conversion pages
- Structured data valid (no critical errors)
- Search Console performance data reviewed if available
- **H1 presence check — always run this:**
  ```js
  console.log(JSON.stringify({
    h1: [...document.querySelectorAll('h1')].map(h=>h.textContent.trim().slice(0,60)),
    h2: [...document.querySelectorAll('h2')].map(h=>h.textContent.trim().slice(0,40)).slice(0,5),
    h3: [...document.querySelectorAll('h3')].map(h=>h.textContent.trim().slice(0,40)).slice(0,5),
  }));
  ```
  **Priority guidance for missing H1:**
  - Major ecommerce homepage (high organic traffic, brand-level) → **P1** (SEO penalty risk at scale)
  - SaaS marketing homepage → **P1** if no H1 at all
  - Inner content/product pages → P2
  - Single-page app where H1 is dynamically set → verify before filing; check rendered DOM, not source

  Note: Lighthouse SEO score does NOT catch missing H1 — it only checks title/meta. Always check heading structure manually.

#### TRUST (Security Baseline)
- HTTPS enforced site-wide
- No mixed content warnings
- Cookie consent option present
- Location access requested in context with permission
- Contact access requests permission
- Security headers reviewed (use MDN HTTP Observatory)
- **Claim vs. reality consistency** — Check every trust claim on marketing/pricing pages against what the actual product does:
  - "100% anonymous" / "private" / "no data stored" → does signup require email, phone, or tracking pixels? If yes, this is a P1 broken promise.
  - "Free" / "no credit card required" CTAs → what is actually free? Limited credits? Limited features only? Ambiguity = trust drain.
  - "Cancel anytime" → is there a self-serve cancel option? If support ticket required, that's deceptive.
  - Flag each contradiction as a separate finding: `TRUST — "[claim]" on [page] contradicts [actual behavior] at [step]`
- **Brand name consistency** — Check whether the product name is consistent across: site header, modal dialogs, iOS/Android app name, email sender name, billing descriptor. A different name in a modal ("Download BiBi Chat" on a site called "VirtualGF") reads as a scam to users and must be flagged as a P1 trust issue.
- **Adult/NSFW-adjacent products** — If the product shows suggestive imagery or adult content on public pages:
  - Is there an age gate on the landing page (not just the signup form)?
  - Does signup have explicit 18+ confirmation checkbox adjacent to Create Account?
  - File both as separate findings if absent — the landing page gate and the signup gate are independent requirements.


#### PWA (if applicable)
- Installable (manifest + service worker)
- Offline mode communicates stale data with sync state and last-updated timestamp
- Update prompt shown after new version is available
- No stale-cache confusion

#### FLOW — Journey Evaluation (run per journey, not per page)

Score each mapped journey on 4 independent axes. These are not interchangeable — a flow can pass 3 and fail 1 and that 1 matters.

| Axis | Pass condition | Failure example |
|------|---------------|----------------|
| **value_delivery** | User received the value they came for | Success screen shown, but cart silently emptied |
| **task_completion** | Final state matches success criteria (judge by pixels, not URL) | URL changed to /success but no confirmation visible |
| **operating_cost** | Zero unintentional steps (excess = actual steps − core steps − intentional friction) | "Are you sure?" on a reversible archive action |
| **feedback_quality** | Every step communicated; every mistake recoverable | Form failed silently — no error message, no indication of what broke |

**Operating cost accounting:** Count user-meaningful actions (clicks, submits, navigations, modal dismissals). Subtract intentional friction (irreversibility confirmations, security guards). Subtract core required steps. Any remainder > 0 = fail.

**Taxonomy rule — FLOW vs. TRUST for modal/popup issues:**
A modal that *interrupts* the flow is a **FLOW** finding (operating_cost fails). A modal whose *content* contradicts the product brand or contains a different product name is a **separate TRUST** finding. These are two distinct issues — file them separately.
Example: VirtualGF shows a "Download BiBi Chat!" modal on a site called VirtualGF. File TWO findings:
- FLOW-001: Modal interrupts web chat path before first value (Cooper friction)
- TRUST-001: Modal uses a different product name — users see "VirtualGF" everywhere then get "BiBi Chat" popup, which reads as a scam

**"What if" failure scenario testing — run the top 3 rows minimum; run all 9 if time permits:**

| Test | How to trigger | Pass condition |
|------|---------------|----------------|
| Invalid email in signup | Type `notanemail` and submit | Inline error on the field, not a page reload |
| Wrong password | Type any wrong password | Inline error, not "account locked" on first try |
| Empty required field submit | Leave required field blank and submit | Specific field highlighted + error message, not just a generic toast |
| Back button mid-form | Fill 2 fields, hit back, come forward | Field values preserved — not cleared |
| Network error mid-submit | Submit form while DevTools → Network → Offline | User sees "check your connection" + retry button, not a blank page |
| Session expired mid-flow | Wait for token to expire (or delete cookie) then perform an action | Clean redirect to login with "Your session expired, please sign in" — not a broken page or raw 401 |
| Upload large/wrong file type | Upload a 500MB file or wrong extension | Immediate client-side validation error before upload starts |
| Search with no results | Search for `xzxzxzxzxz` | Helpful empty state with search tips or alternate action — not just "0 results" |
| Rate limit trigger | Submit a form rapidly 5+ times | User-readable explanation + retry time, not a raw 429 |

For each test, record: **Expected** (correct behavior) and **Actual** (what happened). Any gap = a finding.

Note: slow network simulation (DevTools → Network throttle) tests how the UI behaves under realistic mobile conditions. The top 3 rows (invalid email, wrong password, empty required field) cover the highest-frequency failure paths — always run these. Run the remaining 6 if the audit has time budget remaining.

**Mobile app additional "what if" tests** — run these for every mobile app audit:
- **App backgrounded mid-task** — user switches away and returns. Does the app restore the exact screen and state, or reset to home?
- **Permission denied** — user denies camera/location/notification permission. Does the app explain why it's needed and offer a path to grant it later, or silently fail?
- **Push notification tapped** — does the app open to the relevant screen (e.g. tapping a comment notification opens that comment), or always home?
- **Session expired while in background** — user's token expires while the app is backgrounded. On return, does the app redirect cleanly to login with state preserved, or show a broken screen?
- **No network on launch** — app launched with no internet. Does it show a meaningful offline state or crash/show raw error?
- **Deep link clicked** — user taps a link that should open a specific screen. Does it route correctly, or open home?

**"3 Days Later" check** — does the product show "continue where you left off", recent items, or draft-saved signals for a returning user? If the user left mid-task, can they pick up without starting over? Absence is a P2 retention issue for any CRUD or multi-step flow.

**Mobile "3 Days Later" additions:**
- Does the app restore scroll position in lists/feeds between sessions?
- Is the user returned to their last active tab, or always the first tab?
- Are unsent messages, draft posts, or incomplete forms recovered after the app closes?

#### EXCISE — Friction Accounting (Cooper's Catalog)

Flag any unintentional friction pattern. These are the most common:

| Pattern | Example | Correct fix |
|---------|---------|-------------|
| Confirmation on reversible action | "Are you sure you want to archive?" | One-click + undo toast |
| Modal interrupting active task | Survey popup mid-checkout | Never interrupt active flows |
| Required field that should be optional | Phone number on newsletter signup | Make optional or remove |
| Multi-step where one step suffices | 4-screen wizard for email + password | Single form |
| Re-asking for known info | "What's your email?" when user is logged in | Pre-fill from session |
| Forced account creation | "Sign up to read more" on public content | Allow guest access |
| Decorative confirmation | "✓ Saved" toast for auto-saved single-char edit | Subtle inline state change only |
| Blocking spinner on background work | "Saving…" disables entire UI | Let user continue; background save |
| Context-switch for trivial edit | "Edit" opens a new page for a short text field | Inline editing |
| Cluttered settings | 50 toggles when 5 matter to 90% of users | Default sensibly; progressive disclosure |
| Full-screen cookie consent | GDPR modal blocking content before interaction | Bottom banner; defer to first interaction |
| Two-click delete on reversible content | Confirm → delete on an archivable item | One-click + undo toast |

**Intentional friction is acceptable with justification:** type DELETE to confirm on truly irreversible actions, re-enter password before billing changes, two-step confirm on permanent data destruction.

#### GOODWILL — Trust Reservoir (Krug)

The trust reservoir is finite. Drains and builders both have compound effect — list specific instances observed.

**Drains (depletes user trust):**
- Hiding information users want (pricing, support contact, shipping cost until step 4)
- Punishing users for "wrong" input format (phone with dashes rejected, but no hint given)
- Asking for personal information before providing value
- Faux sincerity / corporate-speak that says nothing ("We're passionate about your journey")
- Sizzle blocking the path (marketing imagery in the way of task completion)
- Amateurish errors (broken images, placeholder text, spelling mistakes in UI)
- **False claims listed as builders** — do NOT list a marketing claim ("100% anonymous", "Cancel anytime", "Free forever") as a goodwill builder if the actual product contradicts it. A false promise is always a drain, not a builder — it creates a worse disappointment than if the claim were never made.

**Builders (increases user trust):**
- Main user tasks are obvious and frictionless on first visit
- Upfront about cost, limitations, and what happens next
- Saves user steps — pre-fills, remembers preferences, does the obvious thing automatically
- FAQs are real and candid, not marketing-speak answers to marketing-speak questions
- Apologizes and offers recovery when things go wrong
- Effort and craft are visible — small details signal that someone cared

#### DELIGHT — Desirability Check

Most AI-generated UIs achieve only the behavioral layer (it works). Flag if visceral or reflective layers are absent.

| Layer (Norman) | Question | Pass condition |
|---------------|----------|---------------|
| **Visceral** | Does the first impression feel intentional and crafted? | Design doesn't look like a template; distinct visual identity |
| **Behavioral** | Does it work and achieve the user's goal? | Task completion + feedback quality pass |
| **Reflective** | Does it create a sense of "this product gets me"? | Microcopy has voice; at least 2 named delight signals present |

**Delight signals — name 2 specific ones to pass. If you have to talk yourself into one, fail:**
- Custom brand illustration (not undraw.co/storyset.com stock art)
- Microcopy with voice — a 404 that's funny, a placeholder that's actually helpful, a tooltip with an aside
- Deliberate easing curves — cubic-bezier motion with intent, not default `ease-in-out`
- Considered empty state — personality and an action, not just "No items found."
- Human date formatting — "yesterday at 3pm", "ships Tuesday" instead of ISO timestamps
- Celebratory first-action moment — subtle on first meaningful task completion
- Custom focus styles matching brand (not just default browser blue ring)
- Loading state with personality — tied to brand, not a generic spinner
- Easter egg / unexpected detail — a pun, inside reference, or hidden touch

#### PSYCH — Behavioral Psychology Audit

Most UX checklists catch broken flows. This section catches flows that work technically but fail psychologically — where users bail not because something is broken, but because they're afraid, confused about the cost, or running out of motivation.

**Cognitive load per screen:**
- Does any screen force the user to make more than 3 unrelated decisions before they can proceed? High decision density → abandonment. Progressive disclosure is pass.
- Is the next action always obvious without reading? If the user has to pause and scan, cognitive load is too high.

**Social proof quality and placement:**
- Social proof present AND specific? ("12,847 creators, avg 4.7★ on 2,300 reviews" converts; "creators love us" is invisible.)
- Is it placed at the moment of hesitation — near CTAs, near price, near the commitment step — or marooned on a testimonials page the user never reaches?
- **For ecommerce, marketplace, and consumer apps: if social proof (ratings, reviews, purchase counts, trust badges) is completely absent from the homepage and product cards, file this as a P2 TRUST/CONTENT finding — not just a note in PSYCH.** Social proof absence on a shopping homepage is a real conversion problem, not a minor style note.

**Anxiety signals at commitment points:**
For each high-commitment step (sign-up, payment, content upload, sharing), ask: what fear or doubt arises here? Flag if the UI fails to preemptively answer it inline.
- Sign-up: "Will I get spam?" / "Can I delete this?" → reassurance copy needed next to the submit button
- Payment: "Is this safe?" / "Will I be auto-charged?" → security badge + clear billing terms at point of payment
- Content upload/share: "Who can see this?" / "Can I undo?" → inline privacy hint before submit
Missing inline reassurance at a commitment step = PSYCH finding. **MANDATORY: write at least one PSYCH-001 finding for every full audit.** If you finish the checklist and have no PSYCH finding, you missed something — every product has at least one commitment moment without enough reassurance. Go back and find it.

**Progress and completion bias:**
- Multi-step flows show a progress indicator so the user feels partially invested in completion?
- Early onboarding steps low-friction (email only) to build momentum before asking for more?
- First meaningful success (aha moment) celebrated with a specific, personal confirmation — not a generic "Done."?

**Reciprocity (give before you ask):**
- Does the product give meaningful value before asking for account creation or payment? If not, flag it — asking for commitment before demonstrating value is the single most common conversion failure.
- Is the ask proportional to the value shown? (Credit card before seeing results = reciprocity failure.)

**Default choice architecture:**
- Are defaults set to the recommended/most-popular option, or does the user have to opt in to sensible behavior?
- Are form fields pre-filled with context-appropriate defaults where possible?

**Peak-end rule (final impression):**
- What is the very last moment of the primary flow? Is the success state specific, personal, and clearly final?
- "Done." or no success state = fail. A specific confirmation with the user's name/result + a next action = pass.

#### NOTIFY — Notification & Async UX

Async events (background jobs, emails sent, imports completed, file exports ready) are where most SaaS products fail silently.

**Scope: NOTIFY applies to async/background operations only.** Standard navigation — including external link redirects, "Apply" buttons that open partner sites, and page-to-page transitions — is NOT a NOTIFY issue. Do not flag expected navigation behavior as NOTIFY. Only flag:
- Background work the user cannot observe (file export, email send, import job)
- Silent tracking or analytics calls whose failure changes user outcome
- Delayed consequences the user has no signal for ("we'll email you when it's ready" with no confirmation the email was queued)

- **Proactive vs reactive:** Does the system notify users when async work completes, or must users know to check? Proactive notification (in-app, email, push) is pass; "check back later" is fail.
- **Background task feedback:** Long-running operations (>10s) show progress, estimated time, or allow cancellation — never a frozen screen.
- **Async button behavior:** Action buttons show a loading state and disable themselves on click to prevent duplicate submissions.
- **Event-driven state:** If another user's action changes shared data (a colleague edits a doc, a payment status changes), does the current user's view update or serve stale data?
- **Notification permission timing:** Push/email permission requested AFTER user has seen value — never on first page load.
- **External link navigation:** An "Apply" or "Visit" button that opens an external site is expected behavior. Do not score it as a NOTIFY failure unless the redirect itself can silently fail and leave the user stranded with no fallback URL shown.

#### VOICE — Tone Consistency

Check all text-bearing surfaces for whether the same "voice" speaks across all of them:
- Marketing site copy (what the brand promises)
- App UI copy (navigation, buttons, settings labels)
- Empty states and onboarding
- Error messages (the moment when the brand is most human or most robotic)
- System emails (confirmation, notification, re-engagement)

Failure: error messages sound like engineering; marketing sounds like copywriting; they're different products written by different people with no shared voice guide. Flag mismatches with specific examples.

---

### Lane B: Code / Repository (When Source is Available)

When frontend or full-stack code is provided, additionally check:

**HTML Semantics (structure and correctness)**
- Form `<label>` elements are associated via `for` or wrapping (no placeholder-as-label)
- `<button>` used for actions; `<a href>` used for navigation — not swapped
- Heading structure follows sequential nesting (no h2 → h4 skips)

**Component State Coverage**
Every interactive component must handle all 8 visible states:
- Default, Hover (`@media (hover: hover)`), Focus (`:focus-visible`), Active/Pressed, Disabled (`opacity: 0.5` + `cursor: not-allowed`), Loading, Error, Success

**Performance Code Checks**
- No `loading="lazy"` on LCP/hero images
- `fetchpriority="high"` on above-fold critical images
- `font-variant-numeric: tabular-nums` on all number columns
- No `width: 100vw` (causes horizontal scroll with scrollbar); use `width: 100%` with container padding
- Images serve modern formats (WebP/AVIF)

**Anti-Slop Code Checks**
- No `transition-all` (specify properties)
- No `z-index: 9999` (use named 6-level scale: 10=sticky, 20=dropdown, 30=overlay, 40=modal, 50=toast, 60=tooltip)
- No `height: 100vh` centred hero
- No `background-clip: text` gradient headline
- No `#000000` or `#ffffff` — tint neutrals toward anchor hue
- No bounce/spring easing on UI controls
- No auto-rotating carousel without pause control (distracting and inaccessible to users with cognitive differences)
- Audio/video uses `autoplay muted loop playsinline`

---

### Lane B (Mobile): Mobile App Code (React Native / Expo / Flutter / Swift / Kotlin)

Apply this section INSTEAD OF the web Lane B when the code is a mobile app. These checks work across all mobile frameworks — map concepts to the framework's equivalent (e.g. `TouchableOpacity` = button, `FlatList` = virtualised list, `UIButton` = button).

#### USER FLOW MAPPING — do this first before any code checks

Read the screen files and navigation config to reconstruct the app's complete user journey map:

1. **Identify all screens** — list every screen file (`.tsx`, `.swift`, `.kt`, `.dart`)
2. **Map the navigation graph** — read the router/navigator config:
   - React Native: `App.tsx`, `navigation/`, React Navigation `Stack.Navigator`, `Tab.Navigator`
   - Flutter: `GoRouter`, `MaterialApp routes`, `Navigator.push`
   - Swift: `UINavigationController`, `TabBarController`, SwiftUI `NavigationStack`
   - Kotlin: Android Jetpack Navigation graph XML, `NavController`
3. **Trace the 5 critical mobile journeys from the code:**

| Journey | Entry point to find in code | Success condition |
|---------|---------------------------|-------------------|
| Cold-start / first launch | `SplashScreen`, `onboarding/`, `AppDelegate`, `MainApplication` | User reaches the first interactive screen in ≤3 taps |
| Onboarding | `Onboarding*`, `Welcome*`, `Intro*` screens | User completes setup and reaches home — every step has back + skip option |
| Core task | Primary feature screen — the reason users download the app | User achieves the task's success state with ≤5 taps from home |
| Return visit | State restoration, `AsyncStorage`/`SharedPreferences` reads at app launch | App re-opens to correct context, not always to the home screen |
| Account / settings | Profile, settings, sign-out, delete account flows | All account actions are self-serve and reversible where applicable |

4. **For each journey, flag:**
   - **Missing back navigation** — any screen that can be reached but has no back/close affordance in code
   - **Dead ends** — screens with no onward navigation in the router config (missing route, commented-out link)
   - **Broken return** — app always relaunches to the root/home instead of restoring the user's last position
   - **Missing empty states** — list/feed screens with no code path for zero items
   - **Missing error states** — async screens (`useEffect`/`viewDidLoad` with network calls) with no error branch rendered
   - **Missing loading states** — async screens that render data directly without a loading skeleton or spinner

Output the journey map as a table at the top of findings before any individual issues.

#### TOUCH & INTERACTION

- **Touch target size** — every tappable element must be ≥ 44×44pt/dp. Check:
  - React Native: `style={{ width, height }}` on `TouchableOpacity`, `Pressable`, `Button` — flag anything < 44
  - Flutter: `SizedBox` wrapping `GestureDetector` or `InkWell` — flag < 44
  - Swift: `frame` or Auto Layout constraints on `UIButton`, `UIControl` — flag < 44×44
  - Kotlin: `layout_width`/`layout_height` on `Button`, `ImageButton`, `View` with click listener — flag < 44dp
- **Tap spacing** — adjacent tap targets need ≥ 8px gap. Flag icon rows and tab bars where icons are ≤ 8px apart
- **Thumb zone** — primary CTA must be in the lower 60% of the screen. Flag primary actions placed above the midpoint on tall screens
- **Haptic feedback** — destructive actions, toggles, and confirmations should trigger haptics. Flag absence of `UIFeedbackGenerator` (Swift), `HapticFeedback` (Flutter), `Vibrator`/`VibrationEffect` (Android), `Haptics` (Expo)
- **Active/pressed state** — every tappable element must show immediate visual feedback. Flag `TouchableOpacity` with no `activeOpacity`, `Pressable` with no `pressed` style change, `UIButton` with no `highlighted` state, Android `View` with no ripple/selector

#### NAVIGATION PATTERNS

- **Platform convention** — iOS apps use tab bar at bottom + stack navigation. Android apps use bottom nav or nav drawer. Flag any app that uses a hamburger menu as the primary nav on iOS, or a tab bar that doesn't follow Material 3 on Android
- **Back navigation** — every pushed/presented screen must have a back/close control in code. Flag screens where `navigation.goBack()` / `dismiss()` / `popViewController` is absent
- **Deep link handling** — check for `Linking` (React Native), `Intent` filters (Android), Universal Links (iOS). Flag if no deep link config exists — users tapping push notifications land on home instead of the relevant screen
- **Tab bar state** — tab bar items should be specific ("My Orders" not "Home"). Flag generic labels in the navigator config
- **Modal vs push** — modals should be used for temporary tasks (confirm, pick, create), not for primary navigation. Flag if modal screens are used as the primary flow progression
- **Gesture conflicts** — React Native: flag `ScrollView` or `FlatList` inside a swipe gesture handler without `simultaneousHandlers`. iOS: flag custom swipe gestures that conflict with the system back gesture (`interactivePopGestureRecognizer`)

#### KEYBOARD & FORMS

- **KeyboardAvoidingView** — any screen with a text input must use `KeyboardAvoidingView` (React Native) or `ScrollView` with `keyboardShouldPersistTaps`. Flag screens where a `TextInput` is NOT inside one. Swift equivalent: `NotificationCenter` observer for `UIResponder.keyboardWillShowNotification` adjusting bottom constraint
- **Keyboard type** — flag `TextInput`/`UITextField`/`EditText` fields where `keyboardType`/`textContentType`/`inputType` doesn't match the expected input:
  - Email → `keyboardType="email-address"` / `textContentType="emailAddress"` / `inputType="textEmailAddress"`
  - Phone → `keyboardType="phone-pad"` / `textContentType="telephoneNumber"` / `inputType="phone"`
  - Password → `secureTextEntry` / `isSecureTextEntry` / `inputType="textPassword"` + toggle to reveal
  - Numeric → `keyboardType="numeric"` / `inputType="number"`
- **Autocorrect/autocapitalize** — disable for email, username, and code fields. Flag missing `autoCorrect={false}` / `autocorrectionType="no"` / `inputType` without `textNoSuggestions`
- **Return key action** — the keyboard's return/go/done key should match the field's purpose. Flag `TextInput` without `returnKeyType` (React Native) or `UITextInputTraits.returnKeyType` (iOS)
- **Field validation** — flag forms where validation only fires on submit. Should fire on blur for each field

#### PERFORMANCE CODE PATTERNS

- **FlatList vs ScrollView for long lists** — `ScrollView` renders all children at once. Flag any `ScrollView` containing a `.map()` that renders > 10 items. Use `FlatList` or `SectionList` instead
- **Memo / useCallback on list items** — `FlatList` `renderItem` that creates a new function every render causes every item to re-render. Flag `renderItem={() => <Item />}` without `useCallback`
- **Image optimisation** — flag `<Image>` without explicit `width`/`height` (causes layout shift), without `resizeMode`, or loading from a non-CDN URL at full resolution
- **Animated API** — flag `Animated.Value` updates inside `setState` (defeats native driver). Flag `useNativeDriver: false` on opacity or transform animations — use `true` for 60fps
- **Unnecessary re-renders** — flag `useEffect` with no dependency array (runs every render), or context providers wrapping large trees where value changes frequently
- **Bundle size** — flag `import * as` from large libraries when only one function is used. Flag `moment.js` — use `date-fns` or `dayjs`. Flag `lodash` full import — use individual imports

#### STATE & ASYNC PATTERNS

- **Loading states** — every component that fetches data must render a skeleton or spinner while `isLoading`. Flag async components with no loading branch
- **Error states** — every async component must render an error message + retry action when the request fails. Flag components with no `isError` / `catch` branch visible to the user
- **Empty states** — every list/feed must render a helpful empty state when data is an empty array. Flag lists that render nothing with zero items
- **Optimistic updates** — quick actions (like, bookmark, toggle) should update the UI immediately and revert on failure. Flag actions that disable the UI and wait for the server before updating
- **AsyncStorage race conditions** — flag `AsyncStorage.getItem` without `await` inside `useEffect`, which can cause reads to complete after the component unmounts
- **Session expiry handling** — flag apps where a 401 from any API call silently fails or shows a raw error. There must be a global interceptor (Axios interceptor, `onQueryStarted` in RTK Query, URLSession delegate) that redirects to the login screen

#### PLATFORM-SPECIFIC PATTERNS

- **SafeAreaView** — every root screen must use `SafeAreaView` (React Native) or `safeAreaInsets` (Flutter) or `safeAreaLayoutGuide` (iOS) to avoid content under notch/status bar/home indicator. Flag screens missing this
- **Platform.OS checks** — flag platform-specific UI differences that should be using `Platform.OS === 'ios' ? ... : ...` but use a single hard-coded style for both platforms (e.g. fixed padding for the status bar instead of `StatusBar.currentHeight`)
- **Permission flows** — location, camera, microphone, notifications must request permission only when the user initiates the relevant feature — never on app launch. Flag `requestPermissions` calls in `componentDidMount` / `useEffect` on the root screen
- **Push notification tap** — flag apps that handle `messaging().onNotificationOpenedApp` / `UserNotifications.UNUserNotificationCenterDelegate` — verify the handler navigates to the relevant screen, not always to home
- **Offline / no network** — flag screens that make network calls with no offline handling. There must be a `NetInfo`/`NWPathMonitor`/`ConnectivityManager` check and a user-visible "no connection" state
- **Dark mode** — flag hard-coded colour hex values (`backgroundColor: '#FFFFFF'`) that don't respond to `useColorScheme()` / `@Environment(\.colorScheme)` / `UIDynamicProviderColor`

#### ANTI-PATTERNS (MOBILE)

- No `console.log` calls left in production code (bundle them out via Babel plugin or flag as tech debt)
- No inline styles on list item components (re-creates style object every render — use `StyleSheet.create`)
- No `setTimeout` used as a substitute for a proper loading state or animation callback
- No fixed pixel dimensions for text (use scalable units or `PixelRatio`)
- No gesture handlers on non-interactive elements without accessible labels
- No `TouchableWithoutFeedback` wrapping non-interactive content just to dismiss the keyboard — use `ScrollView` with `keyboardShouldPersistTaps="handled"` instead

---

### Lane C: Backend Code (When Server-Side Source is Available)

When backend code is provided (Node/Express, Django, Rails, Go, etc.), check UX-relevant patterns only:

**Error Response UX**
- 4xx/5xx responses return a structured `{ message: "..." }` (or equivalent) field the frontend can display — not raw stack traces or generic "Internal Server Error"
- Validation errors return field-level detail: `{ field: "email", message: "..." }` so the client can highlight the specific field — not a single top-level error string
- Error messages are written in plain language (user-facing), not internal codes or exception class names

**Auth & Session Expiry**
- Token expiry during active use triggers a clean redirect to sign-in (not a broken page or raw 401 JSON response surfaced in the UI)
- Redirect preserves the user's current URL so they land back on the right page after re-authenticating
- Session expiry response is distinguishable from other auth errors (`401 + reason: "session_expired"` vs `401 + reason: "invalid_credentials"`) so the frontend can show the correct message

**Rate Limiting**
- 429 responses include `Retry-After` header (seconds or HTTP date)
- 429 response body includes a human-readable explanation and retry time — not just a status code
- Rate limits are documented in API responses, not discovered by users hitting silent failures

**Validation Alignment**
- Server-side validation rules match client-side rules exactly — divergence means users can pass client validation, submit, and see a confusing server-side rejection
- Required fields, format rules (email regex, password requirements), and length limits are identical on both sides
- If server adds extra validation the client doesn't surface (e.g., username uniqueness), the client must display the server's error inline at the field, not at the top of the form

**Long-Running Operations**
- Endpoints that routinely take >10s are backed by an async job pattern: `POST /action` → `202 Accepted + { jobId }`, then `GET /jobs/{id}` for the UI to poll or a websocket/SSE stream
- Synchronous endpoints that can block for >10s under load are flagged — the UI will appear frozen with no feedback

**Label all findings:** `[Backend]` so they're distinguishable from Lane A/B findings in the report.

---

## Step 3 — Detect AI-Slop Fingerprints

Before scoring, run a pre-emit self-critique on 6 axes (score each 1–5):
- **Philosophy** — is there a clear why behind every major decision?
- **Hierarchy** — can you tell primary/secondary/tertiary in 2 seconds?
- **Execution** — are all details specified (tokens, variants, states)?
- **Specificity** — does this look like this product, or could it be any SaaS?
- **Restraint** — is everything earning its place?
- **Variety** — is the structural fingerprint different from common AI output?

Any axis scoring < 3 = flag as AI-slop risk.

**Critical slop tells (flag any present):**
- Purple/indigo-to-pink gradient hero
- The AI nav: wordmark + 4–5 centred inline links + CTA right + sticky white + hairline border-bottom
- The AI footer: 4-column Product/Company/Resources/Legal layout
- 3-column feature grid (every LLM defaults to this)
- Full-viewport centred hero (`height: 100vh`, everything centred)
- Card-in-card (bordered container containing cards — pick one containment layer)
- Gradient headline (`background-clip: text` with gradient fill)
- Aurora-blob or floating-orb background decorations
- Invented metrics ("10× faster", "saves 5 hours/week" with no source)
- Generic emoji as feature icons (✨🚀⚡🔥🎯)
- Inter as the only typeface (one-font page = template page)
- `transition-all` on interactive elements
- Universal `hover:scale-105` on all cards
- Celebratory toast for trivial save operations
- Confirmation dialog for a reversible delete
- Auto-rotating carousel without pause control
- `loading="lazy"` on the hero/LCP image
- Re-drawn UI chrome (fake browser bar or phone frame in HTML/CSS)
- Lottie community animation (someone else's work)
- AI-generated photography: people/places imagery with six fingers, melted text, or uncanny facial smoothness
- No signature design element: every screen could belong to any other SaaS (fails the "which product is this?" test)

---

## Step 3.5 — UX Advisory: Flow & Experience Suggestions

After the issue checklist and anti-slop check, run a forward-looking advisory pass. This is separate from findings — it is not about what is broken, it is about what could be meaningfully better.

**Purpose:** Give the product team specific, actionable ideas for improving user experience — better flows, simpler journeys, smarter patterns — even when nothing is technically broken.

**Rule:** Every suggestion must be specific to this product. Generic advice ("improve onboarding") is not a suggestion. A suggestion names a specific flow, screen, or pattern and describes the improved version concretely.

### Advisory Categories

**FLOW SIMPLIFICATION — Can this journey be shorter?**
For each critical journey, ask: what is the minimum number of steps to reach the user's goal? If the current flow takes more steps than that, identify the gap and describe the simplified version.
- Map: current steps → minimum possible steps → what to remove or combine
- Example: "Sign-up currently requires 4 screens. Email + password is all that's needed — company and profile can be auto-detected or collected post-onboarding. Collapse to 1 screen."

**CONVERSION MOMENTS — Where will users hesitate or leave?**
Identify the 2–3 moments in the primary journey where a user's confidence will be tested before they commit:
- What question will they ask themselves at this moment? ("Is this safe to buy?" / "Will I be locked in?")
- What signal is the product giving them right now?
- What signal should it give instead?
- Example: "On the paid-agent detail page, users ask 'what happens if this doesn't work?' The page shows no refund or trial signal. Adding a one-line 'Refund policy' link directly below the Buy CTA answers this at the exact moment of doubt."

**FEATURE DISCOVERABILITY — What is hidden that should be obvious?**
Identify features, options, or information that exist but are not surfaced where users need them:
- A filter that exists but is buried 2 scrolls below the fold
- A free tier or trial that only appears on the pricing page
- A search shortcut that expert users would want but new users never find
Example: "The `?sort=price_asc` URL param works but there is no price sort in the visible filter UI — only 'Most Popular.' Price-conscious buyers will leave before finding it."

**INFORMATION HIERARCHY — Is the most important thing most prominent?**
Check whether each key page answers the user's primary question first:
- What is the user's primary question on this page?
- What does the page lead with?
- Are those the same thing?
Example: "On the agent detail page the user's primary question is 'What exactly does this agent do and what does it output?' The page leads with hero animation. The 'Before vs After' section — which answers the question — is 4 scrolls down."

**EMPTY & ZERO STATES — Do they guide, not just inform?**
Check every empty or zero state in the audited flows:
- Does it tell the user what to do next?
- Does it communicate why the state is empty?
- Does it offer an action, not just a label?
Example: "Empty search results say 'No agents found.' Better: 'No agents match your filters — try removing the Free Only filter or browse all 38 agents.'"

**PATTERN UPGRADE — What do best-in-class products in this category do that this product doesn't?**

Load `skill_view("ux-audit", "knowledge/13-pattern-library-real-apps.md")` internally. Match the product under audit to the closest category in that file and use the patterns to sharpen your recommendations — this is for YOUR reasoning, not for copying into the report.

**The pattern library informs the recommendation — it does not become the recommendation.**

A senior UX consultant knows patterns from dozens of products. They use that knowledge to give precise, specific advice. They do NOT tell the client "go copy Airbnb." They say: "Show the total trip cost on the listing card — users currently have to do mental math, which is a conversion killer." The Airbnb knowledge informed that, but it's not mentioned.

**In the report, write recommendations specific to THIS product's problem:**

❌ Wrong: "Duolingo locks social features behind 9 lessons — you should do the same."
✅ Right: "Lock the leaderboard behind the user's first 3 completed sessions. Users who invest 3 sessions have enough context to care about ranking — showing it earlier adds noise and sets no goal to work toward."

❌ Wrong: "Coinbase shows total balance first — apply this same progressive reveal."
✅ Right: "Show the total portfolio value at the top, then break it into asset categories below. Right now users see 12 asset rows before they see a total — they're doing math before they understand their position."

**The ONLY place a reference app may appear in the report** is a brief "Reference:" line at the END of a UX-OPP entry — optional, for credibility. Never as the headline or main argument of any recommendation.

Use the CROSS-CUTTING PRINCIPLES INDEX at the bottom of the knowledge file for quick internal lookup.

**EMOTIONAL JOURNEY MAPPING — What does the user feel at each step?**
For the primary critical journey, plot the emotional arc from entry to success. Don't describe steps — describe feelings.
- Create a simple arc: [Landing] → [step 2] → ... → [success moment]
- Mark each step: confident (+), neutral (0), uncertain (–), anxious (– –)
- Identify the lowest-confidence valley before the payoff. The valley depth × duration is what kills conversion.
- Ask: can the valley be shortened (remove steps), or can a micro-delight be injected into it?
- Example: "User arrives curious (+), reads feature list and feels unsure about complexity (–), starts upload and worries about output quality (– –), sees the result and feels surprised and pleased (+3). The valley spans 3 steps. Shortening or reassuring at step 2 would raise conversion."
- Include this as a PSYCH-001 entry in the report if the valley is long or deep.

**PSYCHOLOGICAL BARRIERS — What stops users from committing?**
For each conversion moment (sign-up, first upload, payment, first share), name the specific fear/doubt that arises, what the UI currently provides as reassurance, and what it should provide.
Output as a compact table in the report:
| Commitment moment | User's fear/doubt | Current signal | Required signal |
|-------------------|-------------------|----------------|----------------|
| [step name] | [the question in the user's head] | [what the UI currently gives them] | [what it should give] |
A row with "none" in the Current signal column is a PSYCH finding. Use the table, not prose.

**STRATEGIC UX ALIGNMENT — Does the UX reinforce the brand promise?**
This is the one high-altitude question that sits above all findings. Answer it in 3–5 sentences:
1. **Brand promise vs. UX reality:** What does the brand promise (speed, simplicity, quality, power)? Does the UX deliver that at every touchpoint, or is there a gap?
2. **Differentiation through UX:** Name one thing this product's UX does that a direct competitor's does not. If you cannot name one, the product is undifferentiated at the experience layer — flag it.
3. **Activation moment (aha moment):** At what exact step does the user first feel "this is worth it"? Every step before that moment is pure cost — name them, count them.
4. **Retention mechanic:** After the first session, what brings the user back? Is it designed in (trigger, progress saved, social loop, email re-engagement) or left to chance?
5. **Identity hook:** Does using this product make the user feel something specific about themselves ("I'm a creator" / "I'm on top of this")? If not, it's a pure utility — harder to retain. Name the hook or flag its absence.
Include this as a STRAT-001 entry in the report.

**NEW FEATURE IDEAS — What new capability would meaningfully improve the user's experience?**
Based on what you observed about the users' goals and the product's current gaps, suggest 2–3 specific new features or interactions the product does not yet have but would directly serve the user's JTBD. These are not fixes — they are additive ideas.

Rules for a valid feature idea:
- It must be grounded in an observed user need or gap in the current flow (not a generic "add dark mode")
- It must be described concretely enough that a PM could write a ticket from it
- It must fit the product's current stage and technical surface (no "build a mobile app" if the product is a web SaaS)
- Rate effort: Low (days) / Medium (weeks) / High (months)

Example: "AgentPlace has no 'try before you buy' affordance. A free single-run trial for paid agents — where the user inputs one sample and sees the output before purchase — would address the primary trust barrier on the detail page. Effort: Medium."

### Advisory Output Format

Add a dedicated section to the report after the findings:

```
## UX Recommendations

### UX-OPP-001 — [Title: the improvement, not the problem]

**Current experience:**
[Describe what happens today — be specific about the flow, screen, or moment]

**Suggested experience:**
[Describe the improved version — be specific enough that a designer can wireframe it from this description]

**Why it's better:**
- User benefit: [what the user gains]
- Business benefit: [conversion / retention / trust impact]

**Effort:** Low / Medium / High
[Low = copy change or 1-component edit, ~hours; Medium = new component or flow change, ~days; High = architectural or multi-page change, ~weeks]

**Expected impact:** [Specific outcome: "Reduces signup drop-off" / "Increases first-session completion" / "Cuts support tickets about billing" — not "improves UX"]

**Inspired by / reference:**
[Name a product or pattern that does this well, or describe the UX principle it applies — one credibility sentence at the end only]
```

Produce 3–6 UX-OPP recommendations per audit. Fewer is better — only include suggestions that are genuinely specific and actionable for this product. Generic suggestions are worse than none.

**Prioritize UX-OPP recommendations by impact:** The first recommendation should be the one with the highest conversion/retention/trust impact, not the easiest to implement. If the user has provided funnel data, cite it: "Analytics show 41% drop-off at this step — this is the highest-ROI fix in the audit."

Also produce a **Psychological Barriers** table and a **Strategic UX Position** block:

```
## Psychological Barriers

| Commitment moment | User's fear/doubt | Current signal | Required signal |
|-------------------|-------------------|----------------|----------------|
| [step] | [the question in the user's head] | [what the UI gives now] | [what it should give] |
```
Include one row per high-commitment step. A "none" in Current signal = PSYCH finding, reference it here.

```
## Strategic UX Position

**Brand promise vs. UX reality:** [One sentence — does the UX deliver what the brand promises?]
**Differentiation:** [The one UX thing this product does that competitors don't — or "None identified."]
**Activation moment:** [The exact step where the user first feels "this is worth it." Count steps before it.]
**Retention mechanic:** [What brings the user back, or "Not designed in — relies on habit/memory."]
**Identity hook:** [How using this product makes the user feel about themselves, or "None — pure utility."]
```

Also produce a **New Feature Ideas** subsection within UX Recommendations:

```
## New Feature Ideas

### IDEA-001 — [Feature name]

**What it is:**
[One paragraph — what the feature does, how the user interacts with it]

**Why now:**
[What user gap or observed friction makes this the right next thing]

**How it fits:**
[Where it lives in the current UI and how it connects to existing flows]

**Effort:** Low (days) / Medium (weeks) / High (months)
```

Produce 2–4 feature ideas per audit. These are creative, forward-looking, and grounded in what you observed — not a wishlist. If you cannot connect a feature idea to a specific observed user need, do not include it.

---

## Step 4 — Score Every Issue

Use this 5-factor rubric. Score each factor 0–4. Max total = 20.

| Factor | 0 | 2 | 4 |
|--------|---|---|---|
| User impact | Cosmetic | Slows task | Task failure / exclusion |
| Business criticality | Peripheral | Important flow | Revenue / sign-in / legal |
| Reach | Edge case | Many users | Most sessions / sitewide |
| Recoverability | Easy self-recovery | Hard to recover | Data loss / dead end |
| Compliance / trust risk | None | Significant | Legal / security exposure |

**Priority bands:**
- **P0** (17–20 or override) → immediate hotfix
- **P1** (13–16) → current sprint
- **P2** (8–12) → planned backlog
- **P3** (1–7) → opportunistic

**P0 override rule:** Force P0 regardless of score when an issue **completely prevents** sign-in, payment/billing, or legal consent on a critical journey.

**"Blocks" means the user cannot complete the step at all and cannot self-recover.** Examples:
- ✅ P0: Signup submit returns 500 with no error message and no retry — account cannot be created
- ✅ P0: Payment form crashes the page on submit — purchase impossible
- ✅ P0: Cookie consent modal has no dismiss/accept — user is locked out of the page
- ❌ NOT P0 (P1): App-download modal appears before web chat — user can dismiss it and continue
- ❌ NOT P0 (P1): Signup has no age/consent checkbox — user can still create account, it's a compliance gap
- ❌ NOT P0 (P1): Login page has no "show password" toggle — user can still log in

Note: accessibility auditing (keyboard-only navigation, screen readers, ARIA, contrast compliance) is out of scope for this skill. Do not flag these as findings.

---

## Issue Taxonomy Reference

| Code | Priority tendency | What it covers |
|------|------------------|----------------|
| IA | High | Navigation, labels, wayfinding, hierarchy, search |
| CONTENT | High | Language clarity, CTA text, empty states, copy tone |
| FORM | Very High | Labels, validation, field types, error recovery |
| AUTH | Very High | Login, registration, session, password, social sign-in |
| A11Y | — | **Out of scope** — accessibility auditing (screen readers, keyboard-only, ARIA, WCAG) is not part of this audit |
| UX-OPP | Medium–High | UX opportunities — flow simplification, conversion moments, discoverability, hierarchy, pattern upgrades. Not bugs — proactive improvements. |
| IDEA | Medium–High | New feature ideas grounded in observed user needs. Additive, not fixes. |
| VISUAL | High | Hierarchy, typography, colour, 8-state components, animation |
| MOBILE | High | Touch targets, thumb reach, orientation, keyboard types |
| PERF | Very High | LCP ≤ 2.5s, INP ≤ 200ms, CLS ≤ 0.1, TTFB ≤ 800ms |
| SEO | Medium–High | Indexing, metadata, structured data |
| TRUST | Very High when present | Security headers, SSL, permissions, privacy, OWASP |
| PWA | Medium–High | Offline, installability, update messaging |
| FLOW | High | Journey evaluation — 4-axis scores, TTFV, "what if" failures, "3 Days Later" |
| EXCISE | High | Friction accounting — Cooper's 15 unintentional friction patterns |
| GOODWILL | High | Trust reservoir — drains and builders (Krug) |
| DELIGHT | Medium | Desirability — Norman's 3 layers, delight signals, brand voice |
| PSYCH | High | Behavioral psychology — cognitive load, social proof quality, anxiety signals at commitment points, reciprocity, completion bias, peak-end rule |
| NOTIFY | High | Notification and async UX — proactive vs reactive, background task feedback |
| VOICE | Medium | Tone consistency across marketing, app, errors, emails |
| AI-SLOP | High | AI-generated UI fingerprints — 50+ patterns |

---

## Core Web Vitals Thresholds

| Metric | Good | Needs improvement | Poor |
|--------|------|-------------------|------|
| LCP (Largest Contentful Paint) | ≤ 2.5s | 2.5–4s | > 4s |
| INP (Interaction to Next Paint) | ≤ 200ms | 200–500ms | > 500ms |
| CLS (Cumulative Layout Shift) | ≤ 0.1 | 0.1–0.25 | > 0.25 |
| TTFB (Time to First Byte) | ≤ 800ms | 800ms–1.8s | > 1.8s |

---

## Audit Scope Floors (Minimum Journeys to Cover)

| Product type | Minimum journey count |
|-------------|----------------------|
| Marketing / landing page | 2–3 |
| CRUD tool | 4 |
| Social / community | 6–8 |
| SaaS application | 6–10 |
| Complex enterprise | 10–20+ |

Always include: at least one empty state, one error state, one auth flow, and the mobile viewport of the primary journey.

---

## Limitations (State These When Relevant)

- No automated tool alone determines full conformance — always pair tool output with manual walkthroughs of every critical journey
- A URL audit cannot reveal code-level preventions (lint rules, component constraints)
- A code audit cannot establish whether the rendered interface communicates clearly or preserves focus
- Field performance (CrUX data) is only available for origins with sufficient real-user traffic
- Security findings from ZAP baseline are indicators — they do not replace a full penetration test
