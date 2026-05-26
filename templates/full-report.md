# UX Audit Report: [Product / Site Name]

**URL / Repo:** [target]
**Audit type:** Full / Performance / Quick scan
**Input mode:** URL / URL + credentials / Frontend repo / Full-stack + preview / Screenshots
**Auditor:** [name or "AI agent"]
**Date:** [date]
**Pages / flows reviewed:** [list]
**Viewports tested:** Desktop 1440×900 · Mobile 390×844
**Browsers:** Chromium · [Safari/WebKit if final pass] · [Firefox if final pass]

---

## Executive Summary

[2–3 sentences overall assessment. Lead with what works. Identify the most critical risk area. State the overall grade: A / B / C / D / F with one-line justification.]

**Overall grade:** [A–F]
**Blocking issues (P0):** [count]
**Serious issues (P1):** [count]
**Moderate issues (P2):** [count]
**Polish items (P3):** [count]

---

## Journey Scores

Score each audited journey on 4 axes. A single fail on any axis fails the journey.

| Journey | Mode | value_delivery | task_completion | operating_cost | feedback_quality | TTFV | Chain |
|---------|------|---------------|-----------------|---------------|-----------------|------|-------|
| [e.g. Sign-up → first task] | cold-start | ✅/⚠️/❌ | ✅/⚠️/❌ | ✅/⚠️/❌ | ✅/⚠️/❌ | [# clicks] | [chain name or —] |

**TTFV** = clicks from landing to first meaningful value. Target: ≤ 5 (cold-start), ≤ 2 (returning).

---

## What Is Working

[3–5 things done well. Specific — name the element, page, or pattern. Being concrete here builds credibility for the critical findings that follow.]

- ✅ [Positive 1]
- ✅ [Positive 2]
- ✅ [Positive 3]

---

## Findings by Category

### IA — Information Architecture

| ID | Issue | Priority | Score |
|----|-------|----------|-------|
| IA-001 | [title] | P[0–3] | [0–20] |

**IA-001: [Title]**
- **What:** [Specific description of the issue on the specific page/element]
- **Why it matters:** [User impact + business impact]
- **Standard violated:** [Nielsen heuristic / Core Web Vitals / OWASP ASVS / Cooper / Krug / Norman / etc.]
- **Fix:** [One sentence — what to change and why. Written for product/design.]
- **Implementation:** [Developer-ready detail. One of:]
  - Code issue → before/after code block
  - Copy issue → before/after copy rewrite
  - Structural issue → plain description of the structural change
  - Design constraint → the specific rule + implementation hint
- **Screenshot:** `~/audits/screenshots/[slug]-[ID].png` (P0/P1 with URL) or `N/A` (P2/P3 or code-only)
- **Evidence:** [Screenshot ref / page URL / element selector / file:line]

---

### CONTENT — Copy & Language

<!-- Repeat issue block pattern for each category -->

---

### FORM — Forms & Input

---

### AUTH — Login & Registration

---

### VISUAL — Design & Interaction

---

### MOBILE — Mobile Experience

---

### PERF — Performance

**Core Web Vitals (lab)**

| Metric | Value | Status |
|--------|-------|--------|
| LCP | [value] | ✅ ≤ 2.5s / ⚠️ / ❌ |
| INP | [value] | ✅ ≤ 200ms / ⚠️ / ❌ |
| CLS | [value] | ✅ ≤ 0.1 / ⚠️ / ❌ |
| TTFB | [value] | ✅ ≤ 800ms / ⚠️ / ❌ |

---

### FLOW — Journey Evaluation

| Journey | value_delivery | task_completion | operating_cost | feedback_quality | TTFV |
|---------|---------------|-----------------|---------------|-----------------|------|
| [Journey name] | ✅/⚠️/❌ | ✅/⚠️/❌ | ✅/⚠️/❌ | ✅/⚠️/❌ | [# clicks] |

**"What if" failures tested:** [list]
**"3 Days Later" check:** ✅/❌ — [finding]

---

### EXCISE — Friction Accounting

[List Cooper friction patterns observed. If none: "No unintentional friction patterns detected."]

---

### NOTIFY — Async UX

**Proactive notification:** ✅/❌ — [finding]
**Background task feedback:** ✅/❌ — [finding]
**Async button behavior:** ✅/❌ — [finding]

---

### SEO

---

### TRUST — Security Baseline

---

### AI-SLOP — Template/AI-Generated UI

[List any detected patterns. If none: "No AI-slop fingerprints detected."]

---

### DELIGHT — Desirability

**Norman's layer achieved:** Visceral ✅/❌ · Behavioral ✅/❌ · Reflective ✅/❌

**Delight signals present (need 2 to pass):**
1. [Signal name + specific instance, or "none found"]
2. [Signal name + specific instance, or "none found"]

**Verdict:** ✅ Pass / ❌ Fail — [one sentence]

---

### GOODWILL — Trust Reservoir

**Drains identified:**
- [Specific instance on specific page]

**Builders identified:**
- [Specific instance on specific page]

**Net assessment:** [positive / neutral / negative — one sentence]

---

### VOICE — Tone Consistency

**Surfaces checked:** Marketing · App UI · Empty states · Error messages · System emails
**Consistent:** ✅/⚠️/❌
**Mismatches found:** [specific examples, or "none"]

---

## UX Recommendations

Proactive improvements — these are not bugs. They are specific, actionable suggestions to make the experience meaningfully better for users.

### UX-OPP-001 — [Title: the improvement, not the problem]

**Current experience:**
[What happens today — specific flow, screen, or moment]

**Suggested experience:**
[The improved version — specific enough to wireframe from this description]

**Why it's better:**
- User benefit: [what the user gains]
- Business benefit: [conversion / retention / trust impact]

**Effort:** Low / Medium / High

**Reference:**
[Product or pattern that does this well, or the UX principle applied]

---

## New Feature Ideas

Specific additive ideas grounded in observed user needs — not a wishlist.

### IDEA-001 — [Feature name]

**What it is:**
[What the feature does and how the user interacts with it]

**Why now:**
[The specific user gap or friction observed that makes this the right next thing]

**How it fits:**
[Where in the current UI it lives and how it connects to existing flows]

**Effort:** Low (days) / Medium (weeks) / High (months)

---

## Quick Wins (Fixable in < 1 Hour)

| # | Fix | Category | Impact |
|---|-----|----------|--------|
| 1 | [description] | [code] | [why it matters] |

---

## Roadmap

### Immediate (P0 — fix before next release)
1. [Issue ID + title + owner]

### Current Sprint (P1)
1. [Issue ID + title + owner]

### Planned Backlog (P2)
1. [Issue ID + title + owner]

### Opportunistic Polish (P3)
1. [Issue ID + title + owner]

---

## Remediation Plan

| Initiative | Problem | Target outcome | Priority | Owner | Fix type | Acceptance criteria | Verify |
|-----------|---------|---------------|----------|-------|----------|--------------------|----|
| [sprint/project] | [what users can't do] | [what success looks like] | P[0–3] | [team] | [frontend/design/content/etc.] | [observable pass conditions] | [tool rerun / manual / usability retest] |

---

## Retest Criteria

[List which issues will be verified by automated tool rerun vs manual check vs usability retest. Specify the exact Playwright scenario or Lighthouse assertion to use.]

---

## Tools Used

| Tool | Purpose | Result |
|------|---------|--------|
| Lighthouse | Performance, SEO, PWA | Score: [score] |
| ZAP baseline | Security headers | [findings] |
| HTTP Observatory | Header hygiene | Grade: [grade] |
| Browser DevTools | Network, performance, component state | [findings] |

---

## Audit Limitations

This audit can determine: whether the product clears the usability floor, completes its primary tasks, and shows evidence of design craft. It cannot determine:

| Cannot assess | Why | Use instead |
|--------------|-----|-------------|
| Long-term retention | One session cannot see this | Real product analytics, cohort retention curves |
| Emotional resonance over time | Subjective, longitudinal | User interviews, NPS |
| Habit formation | Requires weeks of observation | Behavioral cohort analysis |
| Cultural / market fit | Requires market context | Localized user testing |
| "True intuition" — it just feels right | Tacit, not cognitive | Senior designer review + usability testing |

A passing audit means: *"This clearly avoids the floor for someone to actually try it."* Whether they keep using it requires real users and time.
