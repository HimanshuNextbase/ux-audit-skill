# Domain Module — Marketplace / Platform

Load this when: the product connects two sides (buyers + sellers, creators + fans, freelancers + clients, hosts + guests). Both sides have distinct flows and needs.

---

## Two-Sided Audit Rule

Always identify which side you're auditing. Most marketplaces fail the seller/creator/supply side far more than the buyer side — because the buyer experience gets more attention. Audit both explicitly.

- **Demand side** (buyer, client, guest, fan): discovery, trust, transaction, fulfillment
- **Supply side** (seller, creator, freelancer, host): listing creation, pricing, payout, reputation

If only one side was provided for audit, note the gap: "Demand-side experience audited. Supply-side (seller onboarding, listing creation, payout flow) not covered — recommend separate audit."

---

## Top 7 Failure Patterns (check these first)

### 1. Discovery and search failure (demand side)
The product only has value if users can find what they're looking for.
- Search returns irrelevant results for common queries → P1 FLOW
- No filter options on results with 20+ items → P1 IA
- Filters and sort not preserved when navigating back → P2 FLOW
- Search empty state has no suggestions or alternative actions → P1 CONTENT
- Personalised recommendations not explained ("Why am I seeing this?") → P3 CONTENT
- Category structure doesn't match how users think (internal taxonomy, not user mental model) → P1 IA

### 2. Trust signals for strangers transacting
The fundamental problem of marketplaces: buyers and sellers don't know each other.
- Seller/creator profile lacks: verification badge, transaction count, response rate, join date → P1 TRUST
- Reviews are unverified (anyone can review, even without a transaction) → P1 TRUST
- Review distribution not shown (overall 4.8 stars, but 1-star reviews hidden) → P1 TRUST
- No dispute resolution process explained before transaction → P1 TRUST
- No buyer protection / money-back guarantee visible at checkout → P1 TRUST

### 3. Listing quality gate is too low (supply side)
Bad listings hurt the whole marketplace. Most marketplaces have no quality floor.
- Listing creation has no photo guidance, minimum fields, or quality score → P2 UX-OPP
- A listing can go live with 1 photo and no description → P2 TRUST
- Price is the only required field — no structured attributes (size, condition, category) → P2 IA
- No preview of how the listing looks to buyers before publishing → P2 UX-OPP
- Duplicate listings allowed with no deduplication → P3 IA

### 4. Seller onboarding and payout UX (supply side)
The hardest drop-off point to fix because it's the highest friction on the supply side.
- KYC/identity verification for payouts is complex with no progress indicator → P1 FLOW
- Tax information required before any earning is possible (even $0 earned) → P1 FLOW
- Payout timeline not clearly communicated (when will I get paid? D+7? Monthly?) → P1 NOTIFY
- No payout history or statement download → P2 UX-OPP
- Failed payout gives generic error with no resolution path → P0 NOTIFY

### 5. Communication UX between sides
- No structured messaging system — users default to sharing phone numbers or emails to communicate → P1 TRUST (takes transactions off-platform)
- Message request from unknown buyer has no context (no listing attached, no intent) → P2 CONTENT
- No read receipt or "seller typically replies in X hours" signal → P2 NOTIFY
- After transaction completes, communication channel disappears (no post-purchase support path) → P2 FLOW

### 6. Review and reputation system UX
- Review prompt appears at wrong time (immediately after payment, before delivery/service) → P1 NOTIFY
- Review is optional and hard to find post-transaction → P2 NOTIFY
- Seller can see who wrote a review before responding — creates intimidation dynamic → P2 TRUST
- Review response UX: seller response not visible to future buyers → P2 TRUST
- No way for a seller to flag a fraudulent or unfair review → P3 UX-OPP

### 7. Mobile listing creation is unusable
Most supply-side activity happens on mobile, but listing creation UX is always built for desktop.
- Photo upload on mobile opens gallery but offers no crop/rotate tools → P1 MOBILE
- Long text fields (description) don't auto-expand on mobile → P1 FORM
- Save draft not available — if user leaves the create flow, work is lost → P1 NOTIFY
- Category/attribute selection uses desktop dropdowns not mobile pickers → P1 MOBILE

---

## PSYCH Focus Points

| Commitment moment | Fear / hesitation | What to check |
|-------------------|------------------|---------------|
| First purchase from new seller | "Is this seller real? Will I get what I ordered?" | Verification badge, review count, response time signal |
| Publishing first listing | "Will anyone see this? Am I pricing it right?" | Visibility guidance, pricing suggestions, first-listing tips |
| Requesting a custom order | "Will the creator understand what I want?" | Structured brief template, revision policy visible before payment |
| Leaving a review | "Will the seller retaliate with a bad review?" | Review anonymity policy, mutual review reveal timing |
| Completing payout setup | "Will I actually get paid? Is this secure?" | Clear payout guarantee, bank-grade security signal |

**Network effect anxiety:** On small or new marketplaces, supply-side users fear "I'll list here but no one will find me." Demand-side users fear "Prices are good but sellers seem unresponsive." Check how the platform communicates its network density without faking it.

---

## What Good Looks Like

- Discovery: faceted filters, relevance sort by default, personalisation opt-in, empty state with trending or staff picks.
- Trust: verified badge system, transaction-verified reviews only, buyer protection banner at checkout.
- Listings: minimum 3 photos required, structured attributes, preview before publish, listing completeness score.
- Payout: clear timeline on payout page ("Funds available for withdrawal: [date]"), statement download, tax doc generation.
- Communication: structured messaging with transaction context attached, seller response time shown on profile.

---

## Domain-Specific "What If" Tests

| Test | How | Pass condition |
|------|-----|----------------|
| Search for a misspelled term | Search for `[main category] typo` | Fuzzy match or "did you mean?" |
| Start creating a listing, leave halfway | Begin listing creation, close tab | Draft saved automatically, resumed on return |
| Message a seller from search results | Click message without viewing full listing | Message includes listing context, not blank |
| Attempt to withdraw below minimum payout | Set payout amount below threshold | Clear minimum amount shown before attempt |
| Request a refund | Initiate dispute on a completed transaction | Dispute form reachable within 3 taps, resolution timeline communicated |

---

## Priority Codes to Check First

`TRUST` (reviews, verification, buyer protection) → `FLOW` (discovery, listing creation, payout) → `NOTIFY` (payout timeline, review prompt timing) → `MOBILE` (listing creation at 390px) → `CONTENT` (empty states, search zero-results)
