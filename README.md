# UX Audit Skill

A comprehensive AI skill for automated UX auditing of any website, web app, or mobile app. Accepts a live URL, source code (frontend or full-stack), screenshots, or any combination. Produces prioritised, evidence-backed findings mapped to WCAG 2.2, Nielsen heuristics, Core Web Vitals, OWASP, Material Design, and Apple HIG.

---

## Repository Structure

```
ux-audit-skill/
├── README.md                        ← This file — integration guide
├── SKILL.md                         ← Human-readable skill manifest
├── skill.json                       ← Machine-readable manifest
│
├── prompts/
│   ├── system.md                    ← Full audit system prompt (load this)
│   └── quick-scan.md                ← Lightweight quick-scan variant
│
├── checklists/                      ← Platform-specific checklists (load one, not both)
│   ├── site.md                      ← Website / web app checklist
│   └── app.md                       ← Mobile app checklist
│
├── knowledge/                       ← Reference knowledge base (12 files)
│   ├── index.md                     ← Index of all knowledge files
│   ├── 01-ux-guidelines-99-rules.md
│   ├── 02-priority-quick-reference.md
│   ├── 03-ui-styles-67.md
│   ├── 04-industry-reasoning-rules.md
│   ├── 05-pre-delivery-checklist.md
│   ├── 06-design-system-workflow.md
│   ├── 07-krug-ux-audit-methodology.md
│   ├── 08-design-fundamentals-and-accessibility-deep.md
│   ├── 09-uxaudit-framework-and-checks.md
│   ├── 10-hallmark-anti-slop-design.md
│   ├── 11-headway-ux-audit-checklist.md
│   └── 12-comprehensive-audit-framework.md
│
├── templates/
│   ├── full-report.md               ← Full audit report template
│   ├── executive-scorecard.md       ← Leadership snapshot template
│   └── issue-entry.json             ← Structured issue ticket format
│
└── examples/
    ├── saas-dashboard.md            ← Sample SaaS dashboard audit
    └── mobile-pwa.md                ← Sample mobile PWA audit
```

---

## Quick Start

### What to send the agent

**For a URL audit:**
```
Audit this site: https://example.com
Focus on: [accessibility / full / quick scan / specific section]
Critical flows: [sign-in, onboarding, billing, core task, etc.]
```

**For a code audit:**
```
Audit this frontend repo for UX and accessibility issues.
[paste repo URL or share files]
```

**For a combined audit:**
```
Audit https://example.com using prompts/system.md.
I also have the frontend repo at [URL] — use both.
```

---

## Agent Integration

### Claude (Anthropic)

Load the system prompt directly as a system message:

```
System: [contents of prompts/system.md]
User: Audit https://example.com — focus on accessibility and mobile.
```

Or reference the file when using Claude Code / Claude API:

```python
with open("prompts/system.md") as f:
    system_prompt = f.read()

response = client.messages.create(
    model="claude-opus-4-7",
    max_tokens=8096,
    system=system_prompt,
    messages=[{"role": "user", "content": "Audit https://example.com"}]
)
```

For deep dives, pass relevant `knowledge/` files as additional context.

---

### OpenAI / Codex

```python
with open("prompts/system.md") as f:
    system_prompt = f.read()

response = client.chat.completions.create(
    model="gpt-4o",
    messages=[
        {"role": "system", "content": system_prompt},
        {"role": "user", "content": "Audit https://example.com"}
    ]
)
```

---

### OpenClaw

Register the skill using `skill.json`:

```json
{
  "skill": "ux-audit-skill",
  "manifest": "skill.json",
  "system_prompt": "prompts/system.md",
  "knowledge": "knowledge/",
  "templates": "templates/"
}
```

Invoke:
```
/skill ux-audit audit https://example.com --scope=full
/skill ux-audit quick-scan https://example.com
```

---

### Hermes Agent

Load the skill manifest and system prompt:

```yaml
skill:
  name: ux-audit
  version: 1.0.0
  manifest: skill.json
  instructions: prompts/system.md
  knowledge_dir: knowledge/
  template_dir: templates/
  example_dir: examples/
```

Invoke with:
```
agent.load_skill("ux-audit")
agent.run("Audit https://example.com — full report, focus on accessibility")
```

---

## Audit Modes

| Mode | Prompt file | Checklist | Use when |
|------|------------|-----------|----------|
| **Full site audit** | `prompts/system.md` | `checklists/site.md` | Complete web audit with severity scores, remediation plan, CI recommendations |
| **Full app audit** | `prompts/system.md` | `checklists/app.md` | Complete mobile app audit |
| **Quick scan** | `prompts/quick-scan.md` | — | Rapid triage — top 10 issues in < 10 min |

**Context tip:** Load `prompts/system.md` + one checklist file only. Load `knowledge/` files selectively when deeper reference is needed on a specific topic.

---

## Output Templates

| Template | Use for |
|----------|---------|
| `templates/full-report.md` | Full audit deliverable for product, design, and engineering teams |
| `templates/executive-scorecard.md` | Leadership snapshot with business risk framing |
| `templates/issue-entry.json` | Ticket-ready structured issue for engineering backlog (GitHub Issues, Jira, Linear) |

---

## Knowledge Base

The `knowledge/` directory contains 12 curated reference files:

| File | Contents |
|------|----------|
| `01` | 99 UX rules with Do/Don't and severity ratings |
| `02` | Priority quick reference — 10 categories ranked CRITICAL → LOW |
| `03` | 67 UI styles — Best For, NOT For, style selection framework |
| `04` | 161 industry-specific patterns (SaaS, Finance, Healthcare, Government, etc.) |
| `05` | Pre-delivery checklists (Web + App) and common anti-patterns |
| `06` | Design system generation workflow |
| `07` | Steve Krug behavioral UX methodology (Trunk Test, 3 Laws, Goodwill model) |
| `08` | Design fundamentals and accessibility deep dive (WCAG, ARIA, testing tools) |
| `09` | UX regression testing framework (AI-slop checks, Cooper's Excise, JTBD) |
| `10` | Hallmark anti-slop design (50+ patterns, 21 macrostructures, 8-state requirement) |
| `11` | Headway heuristic checklists (5-category, auth/login, mobile) |
| `12` | Comprehensive audit framework (two-lane model, severity rubric, tool stack, CI automation) |

---

## Standards Referenced

- WCAG 2.2 (Level A, AA, AAA)
- Nielsen's 10 Usability Heuristics
- Google Core Web Vitals (LCP / INP / CLS / TTFB)
- OWASP ASVS + WSTG
- Material Design 3
- Apple Human Interface Guidelines
- W3C WAI-ARIA Authoring Practices Guide
- WCAG-EM evaluation methodology
- Steve Krug — Don't Make Me Think
