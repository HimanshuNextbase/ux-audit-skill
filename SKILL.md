---
name: ux-audit
description: "Systematic UX audit for SaaS web apps and mobile apps — WCAG 2.2, Nielsen heuristics, anti-slop detection, 5-factor severity scoring. Accepts a live URL, source code, or screenshots. Outputs prioritised findings with P0–P3 bands, fix recommendations, and standards citations."
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

Performs systematic, evidence-backed UX audits on SaaS web apps and mobile apps. Accepts a live URL, source code, screenshots, or any combination. Produces prioritised findings with severity scores, standards citations, and actionable fix recommendations.

---

## When to Use

Trigger this skill when the user asks to:
- Audit a website, SaaS app, mobile app, or PWA for UX/usability issues
- Check accessibility compliance (WCAG 2.2, ARIA, keyboard, screen reader)
- Review a product before launch, after shipping new features, or when conversion drops
- Run a quick scan for obvious issues (top 10 problems in <10 min)
- Generate a UX report, executive scorecard, or issue backlog for engineering

---

## Procedure

### Step 0 — Understand First (always required)

Before touching any checklist, ask or infer:
1. **What is the product?** — URL / repo / screenshots provided?
2. **Product type** — SaaS web app / marketing site / mobile app / PWA / internal tool?
3. **Critical user journeys** — sign-up, onboard, core task, billing, settings, error recovery?
4. **Audit scope** — full audit / accessibility-only / quick scan / specific flow?
5. **Known problem areas** — user complaints, drop-off points, stakeholder concerns?

Confirm understanding before auditing. Load the full intake procedure:
`skill_view("ux-audit", "prompts/system.md")` — Step 0 section for the complete confirmation format.

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

Follow the two-lane model from `prompts/system.md`:
- **Lane A** (URL / screenshot) — rendered experience: IA, content, visual design, a11y, forms, performance
- **Lane B** (code / repo) — static analysis: semantic HTML, ARIA, focus management, linting, CWV

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

## Standards Cited

WCAG 2.2 (A/AA/AAA) · Nielsen 10 Heuristics · Google Core Web Vitals · OWASP ASVS · Material Design 3 · Apple HIG · W3C WAI-ARIA APG · WCAG-EM

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
- ✅ At least one empty state, one error state, one auth flow, and the mobile viewport covered
- ✅ Quick wins table with time estimates
- ✅ Roadmap organized by priority band
- ✅ Anti-slop check completed
- ✅ Every finding cites at least one published standard
