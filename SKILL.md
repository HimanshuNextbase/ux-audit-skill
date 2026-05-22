---
name: ux-audit
description: "Systematic UX audit for SaaS web apps and mobile apps — WCAG 2.2, Nielsen heuristics, anti-slop detection, 5-factor severity scoring. Accepts a live URL, frontend code, backend code, screenshots, design specs, or any combination. Outputs prioritised findings with P0–P3 bands, fix recommendations, and standards citations."
version: 1.1.0
author: HimanshuNextbase
license: MIT
metadata:
  hermes:
    tags: [UX, Accessibility, WCAG, Audit, A11y, Mobile, Performance, SaaS, Design, Usability]
    category: creative
    related_skills: [claude-design, popular-web-designs, architecture-diagram]
---

# UX Audit

Performs systematic, evidence-backed UX audits on SaaS web apps and mobile apps. Accepts a live URL, frontend code, backend code, screenshots, design specs, or any combination — including a single specific page or flow. Produces prioritised findings with severity scores, standards citations, and actionable fix recommendations.

---

## When to Use

Trigger this skill when the user asks to:
- Audit a website, SaaS app, mobile app, or PWA for UX/usability issues
- Check accessibility compliance (WCAG 2.2, ARIA, keyboard, screen reader)
- Review a product before launch, after shipping new features, or when conversion drops
- Run a quick scan for obvious issues (top 10 problems in <10 min)
- Generate a UX report, executive scorecard, or issue backlog for engineering

---

## Input Types — What You Can Accept

| Input | What's auditable | Limitations | Request additionally |
|-------|-----------------|-------------|---------------------|
| **Live URL** | IA, content, visual, a11y (visual), forms, mobile, performance, SEO, trust | Cannot inspect code-level ARIA or lint issues | Auth credentials if behind login |
| **URL + auth credentials** | All of the above plus auth flows, gated pages | Same code-level limits | Confirm login flow to try |
| **Screenshots / images** | Layout, hierarchy, copy, CTAs, form labels, visual states shown, typography, colour, anti-slop | Cannot assess: keyboard nav, ARIA states, focus rings, actual contrast ratios, performance, hover/focus/active states not captured in screenshot | State labels per image (which page, which state, viewport); request error + empty + mobile screenshots if not provided |
| **Frontend code (HTML/CSS/JS/React/Vue/etc.)** | Semantic HTML, ARIA correctness, focus management, 8-state coverage, performance code patterns, anti-slop code tells | Cannot assess visual rendering or copy without seeing the page | None required |
| **Backend code** | Error response UX, auth expiry behavior, rate-limit messaging, server/client validation alignment, long-running request handling | Cannot assess rendered UI | None required |
| **Spec / requirements doc** | Missing screens, cognitive load per screen, entry/exit points, single purpose per screen | No rendered UI to check | None required |
| **Combination** | Union of all applicable lanes | Each input type's limits still apply | Confirm which inputs are authoritative when they conflict |

**Single-page mode:** If the user asks to audit one specific page or flow (e.g., "audit the login page", "check the billing settings"), skip full journey mapping from Step 0.2 — apply only checklist items relevant to that page, still complete Step 0 context questions.

---

## Procedure

### Step 0 — Load the Audit System (do this first, always)

Load the full procedure before asking any questions:
```
skill_view("ux-audit", "prompts/system.md")
```

Then follow **Step 0 in that file**. It covers:
- Product understanding (what it is, industry, users, stage)
- JTBD framing + journey context mode (cold-start / returning / power-user)
- User flow mapping with journey chains and TTFV
- Input type protocol (URL / screenshots / frontend code / backend code / spec)
- A structured confirmation the user reviews before the audit begins

**If the user already provided context** (URL, description, scope), infer what you can from it — do not ask for information already given. Confirm your understanding in the 0.4 format and proceed.

### Step 1 — Choose Audit Mode

**Full audit** (recommended for any serious review):
- Load the full system prompt: `skill_view("ux-audit", "prompts/system.md")`
- Load the relevant checklist:
  - Website / web app → `skill_view("ux-audit", "checklists/site.md")`
  - Mobile app / PWA → `skill_view("ux-audit", "checklists/app.md")`
- Load one, not both.

**Quick scan** (top 10 issues, < 10 min):
- Load: `skill_view("ux-audit", "prompts/quick-scan.md")`
- No checklist needed — the quick scan prompt is self-contained.

### Step 2 — Run the Audit

Follow the three-lane model from `prompts/system.md`:
- **Lane A** (URL / screenshot) — rendered experience: IA, content, visual, a11y, forms, performance, journey evaluation, excise, goodwill, delight, notify, voice
- **Lane B** (frontend code) — static analysis: semantic HTML, ARIA, focus management, 8-state components, CWV code patterns
- **Lane C** (backend code) — UX-relevant server patterns: error format, auth expiry, rate limiting, validation alignment, long-running ops

Score every finding with the 5-factor rubric (0–4 each, max 20) → P0–P3 band.

**P0 override:** Force P0 if an issue blocks sign-in, payment/billing, legal consent, or keyboard-only navigation on a critical journey — regardless of score.

### Step 3 — Deliver the Report

Choose the output template that matches the audience:
- `skill_view("ux-audit", "templates/full-report.md")` — product, design, and engineering teams
- `skill_view("ux-audit", "templates/executive-scorecard.md")` — leadership / business stakeholders
- `skill_view("ux-audit", "templates/issue-entry.json")` — per-issue structured ticket (GitHub Issues, Jira, Linear)

---

## Reference Files

Load these on demand — only when needed for the specific audit:

| File | When to load |
|------|-------------|
| `prompts/system.md` | Full 8-step audit pipeline — always load for a full audit |
| `prompts/quick-scan.md` | Quick scan mode (5 checks, top 10 issues) |
| `checklists/site.md` | Website / web app audit — self-contained with scoring |
| `checklists/app.md` | Mobile app / PWA audit — self-contained with scoring |
| `templates/full-report.md` | Full audit report template |
| `templates/executive-scorecard.md` | Leadership snapshot template |
| `templates/issue-entry.json` | Structured issue ticket format |
| `examples/saas-dashboard.md` | Sample SaaS dashboard audit (A11Y, PERF, IA findings) |
| `examples/mobile-pwa.md` | Sample mobile PWA audit (touch targets, offline, reflow) |
| `knowledge/index.md` | Index of 12 knowledge files — load individual files as needed |

---

## Scoring Quick Reference

| Factor | 0 | 2 | 4 |
|--------|---|---|---|
| User impact | Cosmetic | Slows task | Task failure / exclusion |
| Business criticality | Peripheral | Important flow | Revenue / sign-in / legal |
| Reach | Edge case | Many users | Most sessions / sitewide |
| Recoverability | Easy | Hard to recover | Dead end / data loss |
| Compliance risk | None | Significant | Legal / security exposure |

**Bands:** P0 = 17–20 (or override) · P1 = 13–16 · P2 = 8–12 · P3 = 1–7

---

## Issue Taxonomy

| Code | What it covers |
|------|---------------|
| IA | Navigation, labels, wayfinding, hierarchy, search |
| CONTENT | Language clarity, CTA text, empty states, copy tone |
| FORM | Labels, validation, field types, error recovery |
| AUTH | Login, registration, session, password |
| A11Y | Contrast, keyboard, screen reader, ARIA, reflow, focus |
| VISUAL | Hierarchy, typography, colour, 8-state components, animation |
| MOBILE | Touch targets, thumb reach, orientation, keyboard types |
| PERF | LCP ≤ 2.5s, INP ≤ 200ms, CLS ≤ 0.1, TTFB ≤ 800ms |
| SEO | Indexing, metadata, structured data |
| TRUST | Security headers, SSL, permissions, privacy |
| PWA | Offline, installability, update messaging |
| FLOW | Journey evaluation — 4-axis scores, TTFV, "what if" failure scenarios, "3 days later" |
| EXCISE | Friction accounting — Cooper's 15 unintentional friction patterns |
| GOODWILL | Trust reservoir — drains and builders (Krug) |
| DELIGHT | Desirability — Norman's 3 layers, delight signals, brand voice |
| NOTIFY | Notification and async UX — proactive vs reactive, background task feedback |
| VOICE | Tone consistency across marketing, app, errors, emails |
| AI-SLOP | AI-generated UI fingerprints — 50+ patterns |

---

## Standards Cited

WCAG 2.2 (A/AA/AAA) · Nielsen 10 Heuristics · Google Core Web Vitals · OWASP ASVS · Material Design 3 · Apple HIG · W3C WAI-ARIA APG · WCAG-EM · Steve Krug (Don't Make Me Think) · Alan Cooper (About Face) · Don Norman (Emotional Design) · Christensen JTBD Framework

---

## Pitfalls

- Never start auditing before Step 0 — product type and user journeys determine which issues matter
- Load only one checklist (site.md OR app.md), never both
- Load knowledge files selectively — only when deeper reference is needed on a specific topic
- Every finding must have: taxonomy code, priority band, score breakdown, affected flows, fix recommendation, standards citation
- Anti-slop detection is mandatory — check for AI-generated UI fingerprints (The AI nav, gradient headline, 3-column feature grid, etc.)
- Self-critique before delivery: score on Philosophy / Hierarchy / Execution / Specificity / Restraint / Variety (1–5 each)

---

## Verification

A complete audit delivers:
- ✅ All findings scored with 5-factor rubric and assigned P0–P3
- ✅ Journey context mode declared (cold-start / returning / power-user) for each mapped journey
- ✅ 4-axis journey scores (value_delivery / task_completion / operating_cost / feedback_quality) for each journey
- ✅ TTFV (time-to-first-value click count) measured for the primary cold-start journey
- ✅ At least 3 "what if" failure scenarios tested per critical journey
- ✅ "3 Days Later" check completed for any CRUD or multi-step flow
- ✅ Excise audit — Cooper's friction patterns checked
- ✅ Goodwill accounting — drains and builders listed
- ✅ Desirability check — 2 named delight signals or explicit fail
- ✅ Voice consistency check across all text-bearing surfaces
- ✅ Notify/async check — proactive vs reactive assessment
- ✅ Anti-slop check completed
- ✅ At least one empty state, one error state, one auth flow, and the mobile viewport covered
- ✅ Quick wins table with time estimates
- ✅ Roadmap organized by priority band
- ✅ Audit limitations section in every full report
- ✅ Every finding cites at least one published standard
