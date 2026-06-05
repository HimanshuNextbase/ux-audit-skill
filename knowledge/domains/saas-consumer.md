# Domain Module — Consumer SaaS / B2C App

Load this when: the product is a consumer-facing app or web tool used by individuals (not teams/businesses) — e.g. creative tools, productivity apps, learning platforms, entertainment, AI tools, health/fitness apps, personal finance dashboards.

Difference from B2B SaaS: users choose this voluntarily and can quit with zero switching cost. The UX must earn continued use every single session. There is no IT department locking users in.

---

## Top 8 Failure Patterns (check these first)

### 1. Freemium wall placed at the wrong moment
The freemium model lives or dies by WHERE the paywall appears. Too early = no value delivered. Too late = users got what they needed for free and never upgrade.
- Free tier ends before the user understands the product's full value → P1 FLOW
- Upgrade prompt appears mid-task (user is in the middle of doing something, forced to stop) → P1 FLOW
- Upgrade page lists features, not outcomes ("Unlimited exports" not "Save and share unlimited designs") → P1 CONTENT
- No trial of premium features before committing — user upgrades blind → P1 TRUST
- Cancellation requires email or phone call (no self-serve cancel in app) → P0 TRUST — dark pattern
- Annual plan shown as default without monthly comparison → P2 TRUST

### 2. Habit loop not designed in
Consumer apps that don't build habits get deleted in 2 weeks. Check whether the product has any retention mechanic beyond "the user remembers to come back."
- No trigger mechanism: no push notification, email digest, or streak system → P2 UX-OPP
- No reward for returning: user opens app and sees the same state they left → P2 PSYCH
- No progress signal: user has no sense of "I'm getting better at this" → P2 PSYCH
- No personalisation after 3+ sessions: app still feels generic for a returning user → P2 UX-OPP
- Streak or progress resets for any reason with no recovery mechanic → P1 FLOW

### 3. Onboarding skips personalisation
Consumer apps must feel personal immediately. Generic onboarding creates zero attachment.
- Onboarding doesn't ask about the user's goal or use case → P2 FLOW
- No name or avatar on first login (app feels anonymous even when logged in) → P3 UX-OPP
- Same onboarding for all users regardless of experience level → P2 FLOW
- No "quick win" — the user doesn't produce or see something meaningful in the first 60 seconds → P1 FLOW
- Onboarding is 8+ steps before reaching the actual product → P1 FLOW

### 4. Social proof and community absent
Consumer products grow through word of mouth. Products without social signals look abandoned.
- No user count, review count, or notable user mention → P2 TRUST
- Reviews shown but not verifiable (no platform source like App Store or G2) → P2 TRUST
- No sharing mechanism for outputs (can the user share what they made?) → P2 UX-OPP
- Creator/user showcase absent — user can't see what's possible → P2 UX-OPP
- No referral or invite-a-friend mechanic → P3 UX-OPP

### 5. Mobile experience is second-class
Consumer tools are used on mobile 60-70% of the time. Many web-first consumer tools treat mobile as an afterthought.
- Core feature disabled on mobile ("Available on desktop only" for a creative tool) → P1 MOBILE
- Navigation inaccessible at 390px (menus overlap, sidebars break) → P1 MOBILE
- Output/creation limited on mobile vs desktop without explanation → P2 CONTENT
- No native app despite heavy mobile usage in the category → P3 UX-OPP

### 6. Notification design creates fatigue, not engagement
- App sends notifications for every minor event (notification spam → users disable all) → P1 NOTIFY
- No notification preference screen where user can tune frequency → P1 NOTIFY
- Notifications don't deep-link to the relevant screen (tapping opens home, not the item) → P1 NOTIFY
- Re-engagement emails feel generic ("We miss you!") not personalised ("Your draft is waiting") → P2 NOTIFY
- Push notifications arrive at wrong time (midnight, or 3am due to timezone issue) → P1 NOTIFY

### 7. Output / creation quality ceiling
For tools that produce something (designs, documents, AI outputs, plans):
- No way to export in a standard format (PDF, PNG, CSV) on free tier → P1 UX-OPP (evaluate vs business model)
- Watermark on free tier outputs is so prominent it makes the output unusable → P2 TRUST — evaluate fairness
- Quality of generated output isn't shown clearly (user doesn't know what "good" looks like) → P2 CONTENT
- No history of past outputs (user can't find yesterday's work) → P1 FLOW
- Output can't be edited after creation (no iterative workflow) → P1 FLOW

### 8. Account and data portability
Consumer users are increasingly aware of data ownership.
- No data export option (can't download everything you created) → P1 TRUST
- Account deletion is hard to find (buried in settings, requires email) → P1 TRUST
- What happens to data after deletion is not stated → P1 TRUST
- No "pause" or deactivation option (binary: active or delete) → P2 UX-OPP

---

## PSYCH Focus Points

| Commitment moment | User's question | What to check |
|-------------------|----------------|---------------|
| First use (within 60 seconds) | "Is this going to be worth my time?" | Quick win — user produces or sees something in under 60 seconds |
| Hitting the freemium limit | "Is this product worth paying for?" | The wall should appear AFTER the user has experienced value, not before |
| Upgrade pricing page | "Is X/month worth it for me personally?" | Outcome-focused copy, specific examples, trial option |
| Sharing output publicly | "Will I look good if I share this?" | Output quality, branding options, one-click share |
| Returning after 3 days away | "Where was I? What should I do next?" | Resumable state, personalised prompt, streak mechanics |

**Variable reward check:** Does the product use variable reward mechanics (AI generation, random discovery, social likes)? These are powerful but create compulsive use. Check whether they respect the user's attention (e.g., Duolingo's streak vs. social media's infinite scroll).

**Identity hook:** Consumer products that survive long-term make users feel like the product is part of their identity ("I'm a Notion user", "I use Canva"). Is there any identity signal in this product? If not, retention is entirely dependent on habit — much harder.

**Loss aversion in retention:** "Your 7-day streak is at risk!" is powerful when the streak is real and earned. It's manipulative when the streak metric is artificial or when the email arrives regardless of actual usage. Distinguish between genuine and manufactured loss aversion.

---

## What Good Looks Like

- **Onboarding:** User creates or sees their first personalised output within 60 seconds. 3-4 screens max.
- **Freemium wall:** Appears only after the user has had a genuine "aha" moment. Upgrade prompt explains exactly what becomes possible, not just what's unlocked.
- **Habit loop:** Daily/weekly trigger (notification or email), in-app reward signal, progress tracking that feels meaningful.
- **Mobile:** Full parity with web on core task. Native app for regular-use categories.
- **Notifications:** Max 2-3 per week default. User can tune frequency in preferences. All deep-link to relevant content.
- **Data portability:** One-click export of all user data. Clear account deletion with 30-day recovery window.

---

## Domain-Specific "What If" Tests

| Test | How | Pass condition |
|------|-----|----------------|
| Reach the freemium limit mid-task | Use the product until the limit is hit | Upgrade prompt appears after task completion, not mid-task |
| Skip onboarding entirely | Find and use the skip button | Core feature still accessible, not gated behind incomplete onboarding |
| Share output with someone without an account | Generate output, click share | Recipient can view without signing up |
| Return after 7 days without logging in | Log back in after a week | App shows where you left off, not a generic home |
| Try to cancel subscription | Go to billing settings and cancel | Self-serve cancel available, no phone/email required, no dark patterns |
| Delete account | Find delete account option | Reachable within 3 taps. Clear statement on what's deleted and recovery window |

---

## Priority Codes to Check First

`FLOW` (freemium wall timing, onboarding quick win) → `PSYCH` (habit loop, identity hook) → `NOTIFY` (notification quality) → `MOBILE` (feature parity) → `TRUST` (data portability, dark patterns) → `CONTENT` (empty states, error messages)
