# Domain Module — SaaS / B2B Application

Load this when: the product is a web app, dashboard, or B2B tool with sign-up, onboarding, and a core work loop.

---

## Top 7 Failure Patterns (check these first)

### 1. Activation gap — user never reaches the "aha moment"
Activation is the single most important metric in SaaS UX. Most products never measure it.
- No empty state guidance on first login (blank dashboard with no "start here") → P0 FLOW
- Core feature requires >5 clicks from sign-up to first use → P1 FLOW
- Setup requires data import or API key before anything renders — no demo data option → P1 FLOW
- Onboarding checklist exists but is dismissible — >50% of users dismiss without completing → P2 UX-OPP

**Identify the activation moment in Step 0.2:** what is the exact action after which users are statistically likely to return? (e.g., "created first project", "invited first team member", "connected first integration"). If the product team hasn't defined it, flag as a finding.

### 2. Empty states are walls, not guides
- Empty states show only "No data yet" with no action → P1 CONTENT
- Empty state action CTA is vague ("Get started") not specific ("Create your first report") → P1 CONTENT
- No sample data or template to give users a mental model of what filled looks like → P2 UX-OPP
- Empty states differ in quality between features (main feature has good empty state, secondary features don't) → P3 CONTENT

### 3. Billing and upgrade UX is hostile
- Plan limits hit without warning (user hits limit, gets blocked with no advance notice) → P0 NOTIFY
- Upgrade modal appears mid-task with no "remind me later" — forces a billing decision at wrong moment → P1 FLOW
- Plan comparison page buries the difference between tiers — requires reading fine print → P1 CONTENT
- Downgrade flow is deliberately hidden (cancellation requires email or phone) → P1 TRUST — dark pattern
- Annual vs monthly pricing default not shown upfront (monthly shown, annual hidden behind toggle) → P2 TRUST

### 4. Settings and configuration discoverability
- Account settings, API keys, and integrations buried 3+ clicks from the main UI → P2 IA
- Notifications settings missing or in wrong location (email pref inside profile not notifications) → P2 IA
- No keyboard shortcut to open settings or search → P3 UX-OPP
- Destructive actions (delete account, remove data) are too easy — no confirmation step → P1 TRUST

### 5. Team and collaboration friction
- Invite flow requires too many steps (more than: enter email → send invite) → P1 FLOW
- Role/permission explanations are missing or use internal jargon ("Owner", "Member", "Viewer" without tooltip) → P2 CONTENT
- No way to see what a team member's view looks like before assigning a role → P2 UX-OPP
- Shared workspace with no activity feed / audit log → P2 NOTIFY

### 6. Error messages are useless
The biggest quality gap in SaaS UX is error messaging — it's always written by developers.
- API errors surfaced as raw messages (`500 Internal Server Error`, `ECONNREFUSED`) → P1 CONTENT
- Validation errors appear after submit (not inline as user types) → P1 FORM
- No retry mechanism after a failed operation (user must start over) → P1 NOTIFY
- Rate limit error (`429`) shown without time-to-retry → P1 CONTENT

### 7. Performance in data-heavy views
- Table/list with 100+ rows loads all at once (no pagination or virtual scroll) → P1 PERF
- Search/filter results update only on submit, not as-you-type → P2 FLOW
- Long-running operations (exports, imports, batch jobs) show no progress → P1 NOTIFY
- No optimistic UI — every action waits for server confirmation before showing feedback → P2 FLOW

---

## PSYCH Focus Points

| Commitment moment | The user's fear | What to check |
|-------------------|----------------|---------------|
| Entering credit card for trial | "Will I be charged if I forget to cancel?" | "Cancel anytime" visibility, trial end reminder promised |
| Inviting team members | "What will they be able to see/do?" | Role explanation before invite is sent |
| Hitting a plan limit | "Is this product worth upgrading for?" | Upgrade prompt shows what they'd gain, not just the limit hit |
| Deleting data | "Is this reversible?" | Soft-delete / undo window, "this cannot be undone" explicit |

**Loss aversion at upgrade:** Does the upgrade prompt frame what the user loses by NOT upgrading (feature gating) or what they gain? Gain framing ("Unlock unlimited reports") converts better than loss framing ("You've used 10/10 reports").

**Completion bias:** Does the onboarding have a checklist? If yes, does it start pre-filled with 1-2 items already checked? (Pre-completion increases completion rate 40%+.)

---

## What Good Looks Like

- Time-to-first-value: user creates/sees something meaningful within 2 minutes of sign-up, no credit card required.
- Empty states: each one has an illustration, a specific CTA ("Create your first X"), and a secondary link ("See an example").
- Upgrade prompts: appear only when the user hits a genuine limit, not randomly. Shows exactly what they'd unlock.
- Error messages: every error has a human-readable explanation + a specific next action ("Try again" is not enough — "Check your API key in Settings → Integrations").
- Settings: accessible in 1 click from anywhere in the app via a persistent nav item or keyboard shortcut.

---

## Domain-Specific "What If" Tests

| Test | How | Pass condition |
|------|-----|----------------|
| Hit plan limit | Create items until the limit is reached | Warning shown at 80%, blocked with clear upgrade path at 100% |
| Revoke team member access | Remove a member mid-session | Their session is invalidated immediately |
| Start a long operation then navigate away | Trigger export, then click elsewhere | Operation continues in background, user notified on completion |
| Import malformed data | Upload a CSV with wrong columns | Specific error on which column/row failed, not "import failed" |
| Use the product without onboarding | Skip/dismiss onboarding | Core feature still reachable, not permanently hidden behind incomplete onboarding |

---

## Priority Codes to Check First

`FLOW` (activation) → `CONTENT` (empty states, errors) → `NOTIFY` (async ops, limits) → `TRUST` (billing) → `IA` (settings discoverability)
