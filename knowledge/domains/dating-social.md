# Domain Module — Dating / Social / Community Apps

Load this when: the product is a dating app, social network, creator platform, or community product where users interact with strangers or build a social identity.

---

## Top 7 Failure Patterns (check these first)

### 1. Time-to-first-value is too long
The single biggest drop-off point in dating/social apps. Users should see their first match or content within 2 minutes of install, not after a 15-step profile setup.
- Profile setup requires 10+ fields before seeing any content → P1 FLOW
- No preview of what the app looks like before sign-up (no "explore first") → P1 FLOW
- Onboarding doesn't explain what the user's first action should be → P1 CONTENT
- Core feature (swipe, browse, post) is gated behind completing "100% of profile" → P1 FLOW

**TTFV definition for dating apps:** The moment the user sees real potential matches or real community content relevant to them. Not the homepage, not the onboarding screens.

### 2. Trust and safety signals missing
Users — especially women — are evaluating whether the platform is safe before they evaluate whether it's useful.
- No verification badge system for real users → P1 TRUST
- No block/report mechanism visible on the profile card (requires 3+ taps to find) → P0 TRUST
- No in-app safety guidelines or community standards accessible from profiles → P1 TRUST
- No "share my location/date plans" or emergency contact feature for meeting strangers → P2 UX-OPP
- Photos not moderated (explicit content visible without warning or reported content still visible) → P0 TRUST

### 3. Match and messaging UX
- Notification that a match occurred doesn't include enough context (just "You have a new match!" not who) → P2 NOTIFY
- Message request vs. match distinction not clear → P2 CONTENT
- No read receipts opt-out → P3 UX-OPP
- Chat input covered by keyboard on mobile (classic keyboard-push-up bug) → P1 MOBILE
- No way to send GIFs, voice notes, or reactions (parity with iMessage is user expectation) → P3 UX-OPP
- Ghost block (blocking someone without notification) vs explicit rejection — no option → P2 UX-OPP

### 4. Premium paywall placement and fairness
- Core features (seeing who liked you, sending a "super like") locked behind paywall with no free preview → P1 TRUST — evaluate whether this is appropriate for the business model
- Paywall appears without any context (no trial, no value demonstration) → P1 PSYCH
- Premium features advertised in marketing but not available in the free tier without disclosure → P0 TRUST
- Free users shown fake engagement signals to pressure upgrade (e.g., "3 people liked you — upgrade to see who") when the engagement may be fake → P0 TRUST — dark pattern, regulatory risk

### 5. Profile and content quality UX
- No photo quality guidance (size, face visibility, no group photos rule) → P2 CONTENT
- No prompt or icebreaker feature to help users write a bio → P2 UX-OPP
- Profile completeness indicator not tied to match rate signal → P3 UX-OPP
- Photos appear in wrong order (not the order the user set) on mobile → P2 VISUAL

### 6. Empty state for new accounts
New accounts have no matches, no connections, no content — this is the highest-churn moment.
- New user shown an empty feed with no guidance → P1 CONTENT
- No "here's what you need to do to get your first match" moment → P1 UX-OPP
- Wait time for matches after profile completion not communicated → P2 NOTIFY

### 7. Privacy and data control
Dating app users are sharing highly personal information — privacy controls must be visible and trustworthy.
- Location shared without clear explanation of precision (exact location vs. city-level) → P1 TRUST
- No "invisible mode" or "hide my profile" option → P2 UX-OPP
- Profile photos indexable by search engines (Google can find profile photo) → P1 TRUST
- Account deletion removes profile but not messages from matched users' inboxes (no "delete for everyone" option) → P2 TRUST
- Face photos used in AI features without explicit disclosure → P0 TRUST (DPDP Act 2023 / GDPR biometric)

---

## PSYCH Focus Points

| Commitment moment | The user's fear / question | What to check |
|-------------------|---------------------------|---------------|
| Uploading profile photo | "Will this be used by AI or shared?" | Photo usage policy visible at upload |
| First match | "Do they actually like me or is this fake?" | Verification badge, mutual signal clarity |
| Sending the first message | "Will I look desperate? Will they reply?" | Conversation starter prompts, "icebreaker" suggestions |
| Subscribing to premium | "Is this worth it? Will I actually get more matches?" | Outcome-based upgrade promise, not just "unlock features" |
| Sharing personal details in chat | "Is this person real and safe?" | Verification signals visible in chat, report button accessible |

**Variable reward check:** Does the app use slot-machine mechanics (swipe reveals a match randomly, like Tinder)? If yes, this is intentional and powerful — but check whether it's creating compulsive use signals that the product then exploits for premium revenue. Variable reward + artificial scarcity = dark pattern risk.

**Social proof quality:** "10 million users" is weak social proof. "Join 10 million users who found their match in under 3 months" is specific and outcome-oriented. Check all social proof claims for specificity.

---

## What Good Looks Like

- Onboarding: 3-4 screens max before seeing real content. Profile completed over time, not upfront.
- Safety: Block/Report reachable in 1 tap from any profile. Verification system visible. Community standards linked.
- Premium: Free tier provides genuine value. Premium removes friction, not core functionality.
- Empty state for new users: Specific guidance ("Add 3 more photos to get 5x more matches — our data shows this works").
- Privacy: Location at city-level by default, exact location opt-in. Profile hidden from search engines.

---

## Domain-Specific "What If" Tests

| Test | How | Pass condition |
|------|-----|----------------|
| Report a profile | Open a profile, find report option | Reachable in 2 taps max. Confirms report was received. |
| Delete account mid-subscription | Start account deletion while subscribed | Clear statement of what happens to remaining subscription days |
| Upload a photo that violates guidelines | Upload a screenshot/text image | Moderation response (auto or manual) communicated |
| Use the app without notifications enabled | Deny push notification permission | App still functional; in-app notification fallback exists |
| Unmatch after conversation | Unmatch someone with messages | Messages disappear from both sides, unmatching is not notified to the other person |

---

## Priority Codes to Check First

`TRUST` (safety, privacy, dark patterns) → `FLOW` (TTFV, onboarding) → `CONTENT` (empty states, messaging) → `PSYCH` (variable reward, paywall) → `NOTIFY` (match alerts)
