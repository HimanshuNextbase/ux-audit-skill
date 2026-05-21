# uxaudit — UX Regression Testing Framework

> Every check cites a published source (WCAG 2.2, NN/g, Nielsen, Krug, Baymard, ISO 9241). No vibes.

---

## The Testing Stack — Where UX Regression Fits

Most teams stop at E2E. The full quality stack:

| Layer | Question | Tool |
|-------|----------|------|
| Unit | Does the function behave as specified? | Jest / Vitest / pytest |
| Property-based | Do invariants hold across varied inputs? | fast-check / Hypothesis |
| Integration | Do the parts work when combined? | Jest / pytest |
| E2E | Does the user flow execute correctly? | Playwright / Cypress |
| Visual / A11y | Major UI breakages or accessibility failures? | Percy / axe / Lighthouse |
| **⬆ Everything above can make CI green ⬆** | | |
| **⬇ Everything below decides if it's actually usable ⬇** | | |
| **UX regression (uxaudit)** | Can a human understand the product, choose the next action, complete the core job, and recover when things go wrong? | uxaudit |
| Manual QA | Is anything subjectively off? | Humans |

**Key distinction:** E2E tells you the flow *runs*. UX regression tells you the flow *makes sense while running*.

An app can be CI-green while still being:
- **Unusable** — broken primary journey, missing empty states, unreadable contrast
- **AI-slop-shaped** — purple gradients, "your AI copilot" taglines, shadcn defaults everywhere
- **Inaccessible** — WCAG AA violations
- **Incoherent** — design system applied inconsistently, journey dead ends

---

## UX Measurement Layers — What Can Actually Be Measured

```
┌─────────────────────────────────────┐
│ Retention                           │  ✗ NOT measurable in a session
│ Will users come back tomorrow?      │     Needs real user logs over time
├─────────────────────────────────────┤
│ Desirability                        │  △ Partially measurable
│ Does it feel intentionally crafted? │     Heuristics + LLM judgment
├─────────────────────────────────────┤
│ Usability                           │  ◎ Fully measurable in a session
│ Can a user complete their goal?     │     Nielsen heuristics, journey evaluation
└─────────────────────────────────────┘
```

**Critical implication:** Don't try to predict retention from a single audit session. It's the wrong tool for the job. A passing audit score means "this product passes the bar for someone to actually try it. Whether they want to keep using it is a question for real users."

### What UX audits CANNOT evaluate (be honest)

| Limitation | Why | What to use instead |
|------------|-----|---------------------|
| Long-term retention | One session can't see this | Real product analytics, cohort retention curves |
| Emotional resonance over time | Subjective, longitudinal | User interviews, NPS, qualitative research |
| Word-of-mouth quality | Cultural / social signal | Net Promoter Score, social listening |
| Cultural fit | Requires market context | Localized user testing |
| Habit formation | Requires weeks of observation | Behavior cohort analysis |
| "True intuition" — it just feels right | Tacit, not cognitive | Senior designer review |

---

## The 4 UX Evaluation Lenses

Everything auditable in a session maps to one of four questions:

| Lens | Question | What to look for |
|------|----------|-----------------|
| **understand** | Can users see what's there? | Value prop clarity, visual hierarchy, labeling |
| **decide** | Can users decide what to do? | Choice architecture, vague labels, decision cost |
| **act** | Can users actually act on it? | Task completion, flow continuity, entry points |
| **recover** | Can users recover when something goes wrong? | Error messages, back behavior, undo, dead ends |

These are fixed questions. The concrete rubric changes per product.

---

## The 5 Check Categories

### 1. AI-Slop (`ai-slop/`) — Fingerprints of AI-Generated UI

NN/g's 2024–25 AI Prototyping research found that all AI tools (Bolt, v0, Lovable, Claude, Figma Make) converge on the same generic look. These are the tells:

| Check | What It Detects | Why It Matters |
|-------|----------------|----------------|
| **purple-gradient** | `linear-gradient` using Tailwind `from-purple-*`, `from-indigo-*`, `to-pink-*`, or Stripe-era `#667eea → #764ba2` | LLM default — most likely token, not a brand decision |
| **default-tailwind-palette** | Unmodified Tailwind default colors throughout the app | Means no custom design language was applied |
| **generic-card-shadow** | `box-shadow: 0 4px 12px rgba(0,0,0,0.15)` everywhere | The default shadow every LLM writes |
| **generic-font-stack** | Inter (or system UI only) with no custom typographic identity | LLM default font — not a brand choice |
| **shadcn-signature** | Exact default shadcn/ui component styling with no customization | Means the template wasn't adapted to the product |
| **rote-dark-toggle** | A dark mode toggle added without a real dark theme designed | "Added dark mode" without tuning the dark palette |
| **coming-soon-text** | "Coming soon", "Coming soon…", "🚀 Launching soon" in visible UI | Unfinished stubs shipped to production |
| **lorem-ipsum-data** | Lorem ipsum or "Lorem ipsum dolor sit amet" in visible text | Placeholder content shipped |
| **placeholder-names** | "John Doe", "Jane Smith", "user@example.com" in visible UI | Hardcoded fake data instead of real or empty states |
| **emoji-as-icon** | Emoji used as structural UI icons (nav, settings, controls) | Emoji can't be color-controlled, scale inconsistently, render differently across platforms |
| **cta-trailing-emoji** | CTAs ending with emoji: "Get Started 🚀", "Sign Up ✨" | Emoji as decoration on action labels — visual noise |
| **sparkle-ai-combo** | "✨ Your AI…", "✨ AI-powered…", sparkle + "AI" within 3 words | Overused pattern that signals generic AI product |
| **default-tagline** | Taglines like "The all-in-one platform for…", "Streamline your workflow", "The future of X" | No differentiation — the LLM's most likely tagline token |
| **hero-button-cliche** | Primary hero CTAs: "Get Started", "Get Started for Free", "Start for Free" only | No specificity about what the user is starting |
| **marketing-buzzwords** | "Seamless", "intuitive", "robust", "revolutionary", "cutting-edge", "next-gen" | Vague claims that say nothing to the user |
| **stock-illustration-hotlinks** | `<img>` src pointing to undraw.co, storyset.com, or freepik.com | Stock illustrations hotlinked instead of custom assets |
| **emoji-feel** | Emoji used as overall UI feel/tone (emoji bullets, emoji section headers) | Reduces visual professionalism |

---

### 2. Accessibility (`accessibility/`)

Already covered in detail in notes 01, 02, 08 — unique additions here:

- **font-hierarchy** check: verifies font size establishes clear visual hierarchy (Krug Ch 3 "Billboard Design 101"), not just minimum sizes
- axe-core covers bulk of WCAG 2.2 automatically — targeted L1 checks add things it misses or under-weights

---

### 3. Usability (`usability/`) — Nielsen Heuristics + Journey Continuity

#### Vague Button Labels
Bad labels that pass no information to the user:

| Fail | Better |
|------|--------|
| Submit | Save changes / Send invoice / Create account |
| OK | Confirm / Got it / Done |
| Click here | Download PDF / View details |
| Send (alone) | Send message / Send invoice |
| Done (alone) | Finish setup / Complete order |
| Go | Search / Find |

Rule (from Nielsen #2 + Krug Law #1): fewer than 3 buttons with these generic labels = acceptable. 3+ = fail.

#### Cooper's Excise — Complete Pattern Catalog

**Excise** = work the user must do that does not directly serve their goal (Alan Cooper, *About Face*, Ch 11).

| Pattern | Example | Fix |
|---------|---------|-----|
| **Confirmation on reversible action** | "Are you sure you want to mark as read?" | Just do it; offer Undo toast |
| **Modal mid-task interruption** | "Rate the app!" while user is checking out | Never interrupt active task flows |
| **Required field that should be optional** | "Phone number *" on newsletter signup | Mark optional or remove |
| **Multi-step where one step works** | 4-screen wizard for email + password | Single form |
| **Decorative acknowledgment** | "✓ Saved" toast for autosaved single-char edit | Subtle inline state only |
| **Re-asking for known info** | "What's your email?" after user is logged in | Pre-fill from session |
| **Forced account creation** | "Sign up to read more" on a public article | Allow guest access |
| **Paywall on basics** | Charging to export your own data | Table stakes should be free |
| **Unnecessary breadcrumb cost** | Wizard with no clean Cancel path | Always provide exit |
| **Required TOS acknowledgment** | "I have read 30-page TOS" checkbox no one reads | Remove or simplify |
| **Cluttered settings** | 50 toggles when 5 matter | Default sensibly; hide the rest |
| **Full-screen cookie consent before content** | GDPR modal blocking an article | Bottom banner; defer until interaction |
| **Context-switch for trivial task** | "Edit" opens a new page for a 10-char field | Inline editing |
| **Blocking spinner on background work** | "Saving…" disables entire UI | Let user continue; background save |
| **Two-click delete** | Confirm-then-delete for reversible deletions | One click + Undo toast (Linear pattern) |

**Cooper's intentional friction** (these are OK with justification):
- "Type DELETE to confirm" on truly irreversible actions
- Re-enter password before payment / sensitive data changes
- Two-step confirm on destructive operations
- Trust-building moments at start of high-stakes journey (e.g., financial review screen)

#### System Status Visibility
Based on Nielsen Heuristic #1 and the 3 time limits (Nielsen 1993):

| Response time | What users perceive | Required feedback |
|--------------|--------------------|--------------------|
| < 0.1s | Instantaneous | None needed |
| 0.1–1.0s | Noticeable but flow unbroken | No indicator needed |
| 1–10s | User attention wanders | Show progress indicator |
| > 10s | User switches tasks | Progress bar + estimated time |

---

### 4. Core Experience (`core-experience/`)

#### 4-Axis Journey Evaluation Framework

Every user journey is scored on 4 independent axes:

| Axis | Question | Pass Condition |
|------|----------|----------------|
| **value_delivery** | Did the user actually receive the value they came for? | All first_value signals visible on final state |
| **task_completion** | Did the visible final state match success criteria? | Success state rendered — judge by pixels, not URL |
| **operating_cost** | Was the process efficient or padded with excise? | `unintentional_excess == 0` |
| **feedback_quality** | Did each step communicate? Could the user recover? | Every step showed its outcome; mistakes recoverable |

**These axes are not interchangeable:**
- A flow that reaches the success page but silently empties the cart = `task_completion: pass` + `value_delivery: fail`
- A flow that delivers value in 11 steps when 4 would suffice = `value_delivery: pass` + `operating_cost: fail`

**Operating cost accounting:**
- `actual_steps` — user-meaningful actions (clicks, submits, navigations, modal dismissals)
- `intentional_steps` — steps that match declared "intentional friction" (security guards, irreversibility confirms)
- `unintentional_excess` = actual - intentional - core flow steps. Any value > 0 = fail.

#### Friction Signals Mapped to Axes

| Signal | Axis |
|--------|------|
| No visible feedback after action | feedback_quality |
| State lost on back — form empty after returning | feedback_quality (recoverability) |
| Hidden error — something failed, no message shown | feedback_quality (Norman's Gulf) |
| Dead end — no clear way forward | task_completion (if blocking) |
| Surprising destination — clicked one thing, ended up elsewhere | feedback_quality |
| Unnecessary confirmation on reversible action | operating_cost |
| Newsletter/survey/cookie interstitial blocking flow | operating_cost |
| Re-asking for known info | operating_cost |
| Required step needs info user doesn't have | task_completion (blocked) |
| Primary entry point hidden | task_completion (blocked) |
| Reached end but can't tell what was bought/created | value_delivery |

> **Norman's Gulf:** When something fails silently — no error, no message — the user has no way to understand what happened or what to do next.

---

### 5. Desirability (`desirability/`) — Visual Craft, Microcopy, First Impression

#### Don Norman's 3 Layers of Emotional Response
*(Emotional Design, 2004)*

| Layer | What it is | Most AI UIs achieve |
|-------|------------|---------------------|
| **Visceral** | Immediate aesthetic response | Often fails (AI-slop look) |
| **Behavioral** | It works; goal achieved | Usually achieved |
| **Reflective** | Makes me feel something; I identify with it | Rarely achieved |

Most LLM-generated UIs achieve only the **behavioral** layer. That's why they feel hollow even when they technically work.

#### Delight Signals Catalog

Pass if you can name **2 specific** delight signals. If you have to talk yourself into one, fail.

| Signal | What to look for | What does NOT count |
|--------|-----------------|---------------------|
| **Considered illustration** | Custom brand illustration | undraw.co, storyset.com stock art |
| **Real photography** | Actual EXIF-quality photos of real things | Unsplash stock (same 5 people) |
| **Deliberate easing curves** | Motion with intent — cubic-bezier that fits the context | Default `ease-in-out` |
| **Considered hover states** | Color, weight, scale, or elevation tuned by someone | Default browser highlight |
| **Microcopy with voice** | 404 that's funny, tooltip with an aside, placeholder that helps | Generic "Enter your email" |
| **Easter egg / unexpected detail** | Pun, hidden joke, inside reference, custom hover cursor | — |
| **Considered empty state** | Opportunity for personality (Trello's calypso, Mailchimp's high-five) | "No items found." |
| **Numbers that come alive** | Counters animate up, charts draw in, transitions show change | Static numbers |
| **Loading state with personality** | Custom loading animation tied to the brand | Generic spinner |
| **Celebratory first-action** | Subtle celebration on first meaningful action | No reaction to milestone |
| **Distinctive focus rings** | Custom focus styles matching the brand | Default browser blue outline |
| **Considered dividers/borders** | Thin hand-drawn lines, asymmetric rules, textured borders | Default `border-gray-200` |
| **Dark mode that's warm** | Tuned dark palette (warm dark, considered grays) | Inverted light mode |
| **Human date/time formatting** | "yesterday at 3pm", "ships Tuesday" | "2026-04-06T15:00:00Z" |
| **Inline jokes / cultural references** | Brand voice that breaks formality at the right moment | Flat corporate tone throughout |

---

## Experience Model — Project-Shaped Evaluation

The most important distinction: uxaudit's catalog catches the **universal floor**. The experience model catches **what this specific product needs to do for its specific users**.

### Jobs-To-Be-Done Framework (Christensen)

Users "hire" apps to do a specific job in a specific context. The classic example: users hired fast-food milkshakes as solo commute-time companions — a job no taste test could surface because the situational context was invisible.

**Implication:** The same feature can serve or fail depending on what job the user is trying to complete, and that job is often NOT what surface language suggests. Evaluate against the job, not the interface.

### Experience Model Fields

For each product, define:

| Field | Purpose |
|-------|---------|
| `first_value` | What does the user come to get? The anchor for evaluating FTUE. |
| `must_understand` | What must be clear on first visit? (feeds the `understand` lens) |
| `key_decisions` | What decisions define the journey? (feeds `decide`) |
| `decisions_to_default` | Where should the UI reduce choice instead of ask? |
| `progress_signals` | What shows the user they're moving forward? (feeds `act` and `recover`) |
| `recovery_points` | Where does undo/back/confirmation matter? |
| `simplicity_rules` | Domain-specific "do less" expectations |
| `evidence_basis` | What was this job derived from? (e2e test, route, README, inference) |

### Scenario Contract & Regression

Once a scenario is ratified ("locked"), future audit runs regress against the same contract:
- **Locked:** same journeys evaluated the same way every iteration → enables "did it get better?"
- **Refresh:** discard lock and re-synthesize (use after major IA/product changes)
- **Hybrid (default):** keep lock but let Scout add new candidates

---

## Journey Scenario Count Floors by Product Type

| Product type | Minimum journeys | Coverage |
|--------------|-----------------|---------|
| Marketing landing page | 2–3 | Read value prop + take primary CTA |
| CRUD app (todo, notes) | 4 | Onboard, create, edit, delete with undo |
| Two-sided marketplace | 6 | Buyer browse, buyer purchase, seller list, seller fulfill, buyer review, dispute |
| Social / content platform | 6–8 | Discover, consume, save, share, post/upload, settings |
| SaaS team tool | 6–10 | Onboard, invite, main work loop, collaborate, export, admin |
| Complex platform (Spotify, Notion) | 10–20+ | Multiple chained loops + admin |

**Diminishing returns past 7–10 journeys.** Beyond that, chain existing journeys rather than adding new ones.

---

## Journey Context Modes

| Mode | When to use | What changes |
|------|-------------|-------------|
| **cold-start** | First-time user, no cookies, no account | Fresh context; onboarding must work; empty data state |
| **returning** | Logged-in user with populated data | Skip onboarding; test the actual work loop |
| **power-user** | Returning with realistic-volume data | Test scale, density, search/filter, keyboard shortcuts |

**First-time-user-only checks:**
- Onboarding completion rate
- Empty state guidance
- Time-to-first-value (clicks until something meaningful happens)
- Account creation friction
- Permission request timing (should come AFTER user sees value, not before)

---

## Journey Chains — The Connecting Flows

Real product experiences are chains, not isolated tasks:

```
discover → play → save-to-playlist → share-playlist
               ↓
           adjust-quality → download-offline
```

Each link is scored independently AND the chain as a whole gets a verdict. A break at any link fails the chain.

---

## Category-Specific Friction Red Flags

### Music / Audio Streaming
- Audio doesn't start within 1 second of pressing play
- "Add to playlist" requires more than 3 clicks
- Persistent player disappears or resets when navigating
- Recommendations feel stale after 2 sessions

### Video Streaming
- Player controls hide while user is reaching for them
- Buffering with no progress indication
- "Up next" panel pushes content the user just watched
- Subscribe button harder to find than the like button

### E-Commerce
- Required account creation before checkout
- Hidden shipping cost until step 4
- No price-per-unit on bulk items
- Cart loses items on session timeout

### Productivity / SaaS
- "Are you sure?" on every delete (excise)
- Required setup steps before any value is delivered
- Bulk select is keyboard-only or hidden
- Search doesn't index newly created items quickly

### Communication / Messaging
- Unread state doesn't survive page reload
- @-mentions buried with no notification badge
- Cannot scroll to past messages without losing position
- Notification permission requested before any value is shown

### Booking / Scheduling
- Date picker doesn't work on mobile
- Total price hidden until the last step
- Confirmation email arrives without a calendar invite
- Cancellation policy hidden until after booking

### Content Publishing
- Newsletter modal pops up before reading
- Cookie banner blocks the article body
- Paywall at sentence 1
- Share buttons hijack the URL with tracking junk

### Banking / Fintech
- Balance hidden until biometric auth (already authenticated — pure excise)
- Transaction descriptions are gibberish ("MCD#3145 NORTH AVE")
- "Send money" requires 5+ steps
- Lost-card flow buried 4 levels deep in settings
- Disputes require a phone call

---

## Source Citation Discipline

The rule for any check involving a judgment call: **cite a publicly-verifiable published source**.

**Acceptable sources:**
- Nielsen Norman Group (NN/g) articles
- WCAG 2.2 (W3C)
- ISO 9241-11 / ISO 9241-110
- Canonical UX books: Krug, Norman, Cooper, Christensen
- Peer-reviewed empirical studies (e.g., Lindgaard et al. 2006 — 50ms first impressions)
- axe-core (Deque) — each rule tagged to specific WCAG SC

**NOT acceptable sources:**
- Proprietary / internal guidance (can't be independently verified)
- Tweets and social posts
- Single-author blog posts without peer review
- Popular frameworks without empirical grounding
- Design-system opinions restating the same Nielsen/ISO principle (cite the original)

> Self-evident anti-patterns don't need citations. Lorem ipsum in production, "Coming soon" badges — these are stub tells, not judgment calls.

---

## UX Audit Lifecycle Workflow

| Phase | Action | Goal |
|-------|--------|------|
| **1. Initial build** | Run full audit on first deployable build | Get the catalog floor score; fix anything in "Action required" until pass ≥ 80% on UX band |
| **2. Ratify scenario contract** | Review Scout's journey hypothesis; fix inferences; add chains; tag cold-start/returning | Lock the contract as the regression baseline |
| **3. Per-feature iteration** | Run feature-scope audit on each new feature; check excise + consistency | Fix before merging |
| **4. Periodic health check** | Weekly/monthly whole-app audit | Open History mode; investigate any band that regressed |
| **5. Pre-launch** | All journeys including chains; cold-start mode; confirm UX band + core-experience pass | Clear the craft excuse before launch |

---

## Honest Claims — What the Audit Can and Can't Say

The audit can get you to: *"This clearly avoids the AI-slop floor, completes its main tasks, has a clear value prop, and shows evidence of craft."* That covers ~70% of what makes an app feel good.

The remaining 30% — sustained delight, emotional resonance, habit formation — **needs real users and time.** The audit's job is to eliminate the obvious failures so that remaining 30% has a chance to matter.
