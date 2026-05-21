# UX Audit Report: [Product / Site Name]

**URL / Repo:** [target]
**Audit type:** Full / Accessibility-only / Performance / Quick scan
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
- **Standard violated:** [WCAG criterion / Nielsen heuristic / Baymard finding / etc.]
- **Fix:** [Specific, actionable recommendation]
- **Evidence:** [Screenshot ref / page URL / element selector]

---

### CONTENT — Copy & Language

<!-- Repeat issue block pattern for each category -->

---

### FORM — Forms & Input

---

### A11Y — Accessibility

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

### SEO

---

### TRUST — Security Baseline

---

### AI-SLOP — Template/AI-Generated UI

[List any detected patterns. If none: "No AI-slop fingerprints detected."]

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

[List which issues will be verified by automated tool rerun vs manual check vs usability retest. Specify the exact Playwright scenario, Lighthouse assertion, or pa11y config to use.]

---

## Tools Used

| Tool | Purpose | Result |
|------|---------|--------|
| Lighthouse | Performance, a11y, SEO, PWA | Score: [score] |
| axe / axe DevTools | Accessibility violations | [count] violations |
| WAVE | Accessibility overlay | [findings] |
| Pa11y | CI accessibility sweep | [findings] |
| ZAP baseline | Security headers | [findings] |
| HTTP Observatory | Header hygiene | Grade: [grade] |
| Manual keyboard | Keyboard-only walkthrough | [pass/fail notes] |
| Screen reader | NVDA / VoiceOver | [pass/fail notes] |
