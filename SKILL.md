# UX Audit Skill

**Version:** 1.0.0
**Type:** AI Skill / Agent Tool
**Domain:** UX Quality Assurance

---

## What This Skill Does

Performs systematic, evidence-backed UX audits on any website, web app, or mobile app. Accepts a live URL, frontend/backend source code, screenshots, or any combination. Produces prioritised findings with severity scores, standards citations, and actionable fix recommendations.

## Capabilities

- **Heuristic review** — Nielsen's 10 heuristics applied to every key flow
- **Accessibility audit** — WCAG 2.2 AA/AAA, keyboard-only walkthrough, screen-reader semantics, ARIA correctness, reflow/zoom checks
- **Visual & interaction audit** — hierarchy, whitespace, colour, typography, motion, all 8 interactive states, focus management
- **Navigation & IA audit** — wayfinding, page naming, breadcrumbs, progress indicators, empty states
- **Forms & auth audit** — labels, validation timing, error recovery, field sizing, full login-flow checklist
- **Mobile audit** — touch targets, thumb reach, orientation, keyboard types, one-hand reachability
- **Performance audit** — Core Web Vitals (LCP / INP / CLS / TTFB), loading patterns, CLS prevention
- **SEO audit** — indexing, metadata, structured data, Core Web Vitals as ranking signals
- **Security baseline** — HTTPS, headers, permissions model, OWASP ASVS alignment
- **AI-slop detection** — 50+ fingerprints of AI-generated / template-default UI
- **Severity scoring** — 5-factor rubric producing P0–P3 priority bands with override rules
- **Report generation** — executive scorecard, full report, structured issue backlog, remediation plan

## Input Types

| Input | Use when |
|-------|----------|
| Live URL | Rendered UX, accessibility, performance, SEO, security baseline |
| URL + credentials | Signed-in flows, dashboards, error states, transaction paths |
| Frontend repo | Static a11y linting, component state coverage, shift-left checks |
| Full-stack repo + preview | Backend latency, auth contracts, CI enforcement, error handling |
| Screenshots / video | Visual-only review when live access is unavailable |
| Any combination | Strongest audits use URL + repo together |

## Output Types

- `templates/full-report.md` — complete audit for product, design, and engineering teams
- `templates/executive-scorecard.md` — leadership snapshot with business risk framing
- `templates/issue-entry.json` — ticket-ready structured issue for engineering backlog
- Remediation plan with sprint-backlog mapping

## When to Use

- Before a major release or product launch
- After shipping a batch of new features (consistency check)
- When conversion, activation, or task completion rates drop
- Accessibility compliance review (ADA, WCAG, Section 508)
- Onboarding a new product into a design system
- As a recurring micro-audit cadence in each sprint

## When NOT to Use

- Pure brand/aesthetic review (logo design, illustration art direction)
- Code architecture review unrelated to user-facing behaviour
- Full penetration testing (this covers security UX baseline only — not pentest)

## Entry Point

Load `prompts/system.md` as the system message to activate the full skill.
For lightweight URL scans use `prompts/quick-scan.md`.

## Knowledge Base

`knowledge/` contains 12 reference files covering:
- 99 UX rules with severity ratings
- 161 industry-specific patterns
- 67 UI style guides
- Steve Krug behavioral methodology
- Hallmark anti-slop detection patterns (50+ tells)
- Comprehensive audit framework with tool stack and CI automation
- Accessibility deep dive (WCAG, ARIA, testing tools)
- Headway heuristic checklists

## Integration

See `README.md` for agent-specific integration instructions (Claude, Codex, OpenClaw, Hermes).
