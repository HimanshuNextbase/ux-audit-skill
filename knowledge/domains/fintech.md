# Domain Module — Fintech / Financial Services

Load this when: the product handles money, banking, investments, payments, crypto, insurance, or lending.

---

## Top 7 Failure Patterns (check these first)

### 1. KYC / verification UX is a drop-off machine
Identity verification is the #1 drop-off point in fintech onboarding. Every unnecessary step here costs real users.
- Document upload has no guidance on photo quality (blurry/dark photo → rejection with no help) → P1 FORM
- Selfie capture doesn't explain liveness check (users don't know to blink/move) → P1 CONTENT
- Verification failure message is generic ("Verification failed. Try again.") with no reason → P0 CONTENT
- No status page after submission — user doesn't know if review is 5 mins or 5 days → P1 NOTIFY
- Verification re-submission flow is harder than initial submission → P1 FLOW
- No fallback for users without a supported document type → P2 FLOW

### 2. Fee and cost transparency failures
Fintech dark patterns cause regulatory risk, not just UX problems.
- Fees not shown until final confirmation screen → P0 TRUST — potential regulatory issue
- Exchange rate shown without spread disclosure → P0 TRUST
- Subscription/recurring charge not clearly stated at sign-up → P0 TRUST
- "Free" claims that exclude mandatory fees → P0 TRUST
- Dynamic fees that change between the preview and the confirmation → P0 TRUST

### 3. Transaction and operation feedback gaps
- Sending money shows no confirmation of recipient (just account number — no name verification) → P1 TRUST
- Transaction in progress shows no estimated completion time → P1 NOTIFY
- Failed transaction gives generic error, not specific reason (insufficient funds vs. recipient blocked vs. daily limit) → P0 CONTENT
- No transaction reference number shown (user can't reference it with support) → P1 NOTIFY
- Receipt not downloadable or shareable → P2 UX-OPP

### 4. Security UX that hurts usability
Security is mandatory but bad security UX causes abandonment.
- 2FA flow has no "remember this device" option → P2 FLOW
- Session timeout too aggressive (e.g., logs out after 5 minutes of inactivity) → P1 FLOW
- Session timeout warning appears with no countdown → P2 NOTIFY
- Password requirements not shown until after submission fails → P1 FORM
- Biometric auth available but not offered as primary (user must use PIN) → P2 UX-OPP
- Clipboard warning for copied account numbers (some apps block paste — this breaks UX, not helps it) → P1 FLOW

### 5. Sensitive data display handling
- Full account/card numbers shown by default without mask → P1 TRUST
- No reveal/hide toggle for masked sensitive data → P2 UX-OPP
- CVV shown permanently on a virtual card → P1 TRUST
- No blur/mask on financial summary when sharing screen → P2 UX-OPP (many users do screen shares)

### 6. Trust signals at high-stakes moments
Users moving large amounts of money need more trust signals, not fewer.
- No regulatory body badge / banking license information visible → P1 TRUST
- No "your money is insured up to X" signal on balance/deposit screen → P1 TRUST
- Support contact method not visible before committing a large transaction → P1 TRUST
- No fraud protection or dispute resolution process explained → P2 TRUST

### 7. Notification and alert UX
- Transaction alerts arrive after a delay (users find out about fraud late) → P1 NOTIFY
- Notification preferences hidden or hard to find → P2 IA
- Low balance warning threshold not configurable → P3 UX-OPP
- Push notifications for every small transaction (notification fatigue → users disable all) → P2 NOTIFY

---

## PSYCH Focus Points

| Commitment moment | The user's real fear | What to check |
|-------------------|---------------------|---------------|
| First money transfer | "What if I send to the wrong person?" | Recipient confirmation (name shown, not just account number) |
| Connecting bank account | "Will they drain my account?" | Permissions explained (read-only vs. write), institution badge |
| Submitting KYC documents | "Where does my ID go?" | Data retention policy, who sees it, when it's deleted |
| Seeing a suspicious transaction | "Was I hacked?" | Alert copy (calm, specific, actionable) vs. panic-inducing |
| Entering a large amount | "Is this reversible?" | Cancellation window, confirmation step with explicit amount shown |

**Anxiety amplification check:** Fintech products often trigger anxiety by default (your money is at risk). Check whether the product reduces or amplifies anxiety at each step. Every error message that says "failed" instead of "let's try again" is amplifying anxiety unnecessarily.

**Loss aversion in feature adoption:** Investment/savings features should lead with gain framing ("Start earning 7.5% APY") not loss framing ("You're leaving money on the table").

---

## Regulatory / Compliance UX (check these — failing them is a business risk)

These aren't pure UX issues but UX is the delivery mechanism:
- Cookie consent before any tracking (GDPR / DPDP Act 2023 for India) → P0 TRUST if missing
- Terms and Privacy Policy linked at sign-up (not just footer) → P1 TRUST
- Data deletion request flow accessible to users → P1 TRUST (GDPR right to erasure)
- Marketing communication opt-in is opt-in, not opt-out (pre-ticked checkbox) → P1 TRUST
- For lending: APR shown prominently before user commits → P0 TRUST

---

## What Good Looks Like

- KYC: step-by-step with progress, photo quality tips, 2-minute expected wait communicated upfront.
- Transaction flow: 3 screens max — enter amount → confirm with full details (amount, fees, recipient name) → success with reference number + downloadable receipt.
- Error messages: always specific ("Daily limit of ₹50,000 reached — resets at midnight") never generic ("Transaction failed").
- Sensitive data: masked by default, tap-to-reveal with biometric confirm.
- Security: session timeout with 2-minute warning, biometric as primary auth, "remember this device for 30 days".

---

## Domain-Specific "What If" Tests

| Test | How | Pass condition |
|------|-----|----------------|
| Enter a wrong IFSC/routing code | Submit transfer with invalid code | Immediate validation error before submission, not after |
| Transfer to an unregistered number | Send money to a phone not on the platform | Clear message: "This number is not registered. Notify them to join?" |
| Cancel a pending transfer | Initiate transfer, then cancel | Clear cancellation confirmation + time window for when it's too late |
| Request a statement for a large date range | Download 12 months of statements | No timeout, progress shown, file delivered to email if large |
| Exceed daily limit | Try to transfer above daily limit | Limit shown before user starts entering amount, not after |

---

## Priority Codes to Check First

`TRUST` (fees, compliance) → `CONTENT` (error messages, KYC guidance) → `NOTIFY` (transaction feedback) → `FLOW` (KYC, transfer) → `FORM` (document upload, amount entry)
