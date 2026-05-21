# Comprehensive UX Audit Framework

Source: "Building a Comprehensive UX Audit Capability" — internal research document
Note: Duplicates from notes 01–11 filtered out — only unique content saved here.

---

## The Two-Lane Audit Model

A complete audit requires two lanes running in parallel — not just URL scanning:

| Lane | Input | Best for | What it can assess |
|------|-------|----------|--------------------|
| **URL-first** | Live or staged URL | Rendered experience | Accessibility, performance, SEO, mobile behavior, basic security, visual UX |
| **Code-first** | Frontend / full-stack repo | Prevention (shift-left) | Static a11y linting, component constraints, CI gates, route-level performance budgets |

> URL tells you what users experience now. Code tells you what teams can prevent next. The strongest audits use both.

### Input Mode Capability Matrix

| Input mode | Well-suited for | Cannot fully assess |
|-----------|-----------------|---------------------|
| Public or staged URL | Rendered UX, a11y, perf, SEO, basic security | Hidden authenticated flows, code-level preventions |
| URL + credentials | Signed-in flows, permissions, error handling, empty states | Deeper code hygiene unless repo access also provided |
| Frontend repo | Static a11y linting, component tests, CI gating, route budgets | Real field performance, SEO index state |
| Full-stack repo + preview env | Frontend UX + backend latency, auth states, error contracts, CI enforcement | Production field metrics without RUM/CrUX |
| Storybook / component catalog | Component semantics, contrast, accessible names, reusable regressions | End-to-end flow quality and cross-page content strategy |

---

## Canonical Standards Map

Every audit layer maps to its authoritative source:

| Audit layer | Primary standard | What it contributes |
|-------------|-----------------|---------------------|
| General usability | Nielsen's 10 heuristics | Core interaction rules: visibility, user control, consistency, error prevention, recognition, flexibility, error recovery |
| Formative usability testing | NN/g usability testing guidance | ~5 users for formative work on critical journeys |
| E-commerce / domain-specific | Baymard research | Empirical guidance for checkout, navigation, product pages, mobile commerce |
| Accessibility standard | WCAG 2.2 | Normative success criteria and pass/fail checklist |
| Accessibility patterns | WAI-ARIA APG + WAI tutorials | Keyboard behavior, component patterns, forms, page structure |
| Accessibility methodology | WCAG-EM + W3C report tools | Scope definition, sampling, reporting structure |
| Mobile ergonomics | Material Design 3 + Apple HIG | Touch targets, navigation, platform patterns |
| Performance | Lighthouse + Core Web Vitals + PageSpeed + CrUX | Lab diagnostics, field data, CWV thresholds |
| PWA quality | web.dev PWA checklist | Installability, offline behavior, app-like experience |
| SEO | Google Search Essentials + Search Console + Rich Results Test | Crawlability, indexing, structured data validation |
| Security | OWASP ASVS + WSTG + ZAP + MDN HTTP Observatory | Security controls, baseline scanners, header hygiene |

---

## 8-Stage Audit Pipeline

Based on WCAG-EM generalized to the full UX stack:

| Stage | Objective | Key actions | Primary tools |
|-------|-----------|-------------|---------------|
| **1. Intake** | Define audit boundaries | Business goals, personas, critical paths, environments, credentials, devices | WCAG-EM scope concepts |
| **2. Inventory** | Build representative sample | Crawl routes/templates, pick top flows, include empty/error/auth states | Playwright/Puppeteer crawl |
| **3. Automated pass** | Gather broad evidence fast | Run Lighthouse, axe/Pa11y, SEO and security baselines | Lighthouse, axe-core, Pa11y, Search Console, ZAP, Observatory |
| **4. Manual pass** | Assess what tools miss | Heuristics, reading level/tone, keyboard, screen reader, zoom/reflow, mobile ergonomics | NN/g, W3C tutorials, APG, HIG, Material |
| **5. User benchmark** | Validate critical task friction | 5-user qualitative benchmark on 3–5 high-value tasks | NN/g usability testing guidance |
| **6. Synthesis** | Turn findings into action | De-duplicate, score severity, map to owners and standards | Taxonomy + severity rubric (below) |
| **7. Delivery** | Make the audit usable | Executive readout, issue backlog, quick wins, roadmap, CI recommendations | W3C report template |
| **8. Retest** | Confirm closure | Re-run same flows and checks against fixed versions | Lighthouse CI, Playwright CI, Pa11y CI |

**Critical design principle:** Use the same sampled pages and tasks consistently across automation, manual review, and retest. This makes comparisons reproducible and prevents scope drift.

---

## Issue Taxonomy (9 Codes)

| Code | Priority tendency | Typical issues | Primary standards |
|------|------------------|----------------|-------------------|
| **IA** | High | Hidden navigation, weak labels, disorienting hierarchy, poor wayfinding, unclear search/nav split | Nielsen heuristics; Baymard navigation; Apple HIG |
| **CONTENT** | High | Jargon, ambiguous CTA text, unreadable copy, weak empty states, unclear policies | Nielsen match-to-real-world and minimalist design |
| **FORM** | Very High | Poor labels, missing instructions, wrong input types, invalid field lengths, broken recovery | W3C Forms tutorials; Baymard form usability; NN/g error messages |
| **A11Y** | Very High | Missing names/roles/states, poor contrast, focus loss, keyboard traps, reflow failures, bad alt text | WCAG 2.2, APG, Easy Checks |
| **MOBILE** | High | Small touch targets, thumb-unfriendly controls, cramped bottom nav, gesture ambiguity | Material Design 3, Apple HIG, WCAG mobile criteria |
| **PERF** | Very High | Slow loading, delayed interaction, unstable layouts, slow server response | Core Web Vitals, PageSpeed, document latency |
| **SEO** | Medium–High | Indexing blocks, duplicate metadata, broken structured data, no rich-result eligibility | Search Essentials, Search Console, Rich Results Test |
| **TRUST** | Very High (when present) | Mixed-content warnings, missing security headers, risky forms/auth flows, opaque privacy | OWASP ASVS/WSTG, ZAP, MDN Observatory |
| **PWA** | Medium–High | Poor offline handling, weak install UX, stale-cache confusion, no update messaging | Lighthouse PWA, web.dev PWA checklist |

---

## Severity Scoring Rubric (0–20)

Score each issue across 5 factors (0–4 each) to get a comparable priority across all issue types:

| Factor | 0 | 1–2 | 3 | 4 |
|--------|---|-----|---|---|
| **User impact** | Cosmetic | Annoyance | Slows task | Outright task failure or exclusion |
| **Business criticality** | Peripheral page | Minor flow | Important flow | Revenue, sign-in, activation, legal |
| **Reach** | Edge case | Small segment | Many users | Most sessions / sitewide template |
| **Recoverability** | Easy self-recovery | Workaround exists | Difficult to recover | Dead end / data loss / restart required |
| **Compliance / trust risk** | None | Minor | Significant | Legal exposure, security, privacy break |

### Priority Bands

| Priority | Score | Meaning | Typical SLA |
|----------|-------|---------|-------------|
| **P0** | 17–20 or override | Blocker: key flow impossible, severe exclusion, security/privacy break, data loss | Immediate / hotfix |
| **P1** | 13–16 | Serious friction in primary journey; many users affected; weak recovery | Current sprint / next release |
| **P2** | 8–12 | Noticeable friction or quality loss; recoverable | Planned backlog |
| **P3** | 1–7 | Minor or localized issue; polish, consistency, or optimization | Opportunistic |

**Override rule:** Force any issue to P0 regardless of numeric score when it blocks: checkout, sign-in, payment, legal consent, or keyboard-only completion on a critical journey.

---

## Reproducible Test Procedure Defaults

Use these defaults for every audit unless the product requires stricter settings. Consistency makes results comparable over time.

| Element | Default | Why |
|---------|---------|-----|
| Environments | Staging preview + production URL | Need both fix-ready and real-world views |
| Browsers | Chromium baseline; add Safari/WebKit and Firefox for final pass on critical flows | Playwright supports all three in one API |
| Viewports | Desktop 1440×900; Mobile 390×844 | Matches common desktop/mobile review conditions |
| Browser state | Incognito / clean profile; no extensions except audit tools | Extensions and stored data influence Lighthouse results |
| Lighthouse runs | 3 minimum; use median result | Multiple runs reduce variance |
| Qualitative sample | 5 users on primary workflow | NN/g's long-running guidance for formative studies |
| Accessibility reference | WCAG 2.2 Quickref filtered to level and technologies used | Working checklist form of WCAG |
| SEO reference | Search Console + Search Essentials + Rich Results Test | Official search visibility references |
| Security reference | OWASP ASVS/WSTG + ZAP/Observatory | Official verification and baseline scanner sources |

---

## Full Audit Checklist Matrix (16 Test Types)

| Test | Procedure | Primary tools | Output |
|------|-----------|---------------|--------|
| Representative sampling | Identify templates, top tasks, auth states, error states, empty states | WCAG-EM process; Playwright crawl | Page/flow inventory |
| Heuristic review | Review each key flow against Nielsen's 10 heuristics | Human evaluator(s) | Heuristic scorecard |
| Task-based usability check | Ask 5 participants to complete 3–5 key tasks; log success, time, friction | Moderated or unmoderated test | Task metrics + observations |
| Keyboard-only walkthrough | Tab through entire flow; verify all actions complete and focus is always visible | Browser, Accessibility Insights, manual | Pass/fail per flow |
| Screen-reader semantics | Inspect landmark structure, labels, names, role/state announcements | NVDA/VoiceOver + axe + APG patterns | SR notes + defects |
| Reflow and zoom | Check 320 CSS px equivalent / 400% zoom without functional loss | Browser zoom + manual review | Pass/fail with screenshots |
| Forms and validation | Verify labels, instructions, field sizing, errors, recovery, preserved effort | axe, Pa11y, manual, Baymard references | Issue log with remediation |
| Images and alt text | Validate functional and informative image alternatives | axe + manual content review | Alt-text defects |
| Heading and landmark structure | Verify heading nesting and labeled regions | Browser accessibility tree; manual | IA/content structure issues |
| Mobile ergonomics | Real-device or emulated review for navigation, thumb reach, target size | Material, Apple HIG, device lab | Mobile issue list |
| Performance lab | Run Lighthouse and inspect opportunities/diagnostics | Lighthouse | HTML/JSON reports |
| Performance field | Compare PageSpeed Insights and CrUX data for origin/page | PageSpeed Insights; CrUX | Field/lab gap analysis |
| SEO baseline | Validate indexing, robots, performance report, structured data | Search Console; Rich Results Test | SEO defect list |
| Security baseline | Run passive baseline and header checks | ZAP baseline; HTTP Observatory | Risk summary |
| PWA readiness | Validate installability, offline behavior, update behavior | Lighthouse + manual offline test | PWA score and defects |
| Component accessibility | Run static linting and Storybook addon checks | jsx-a11y; Storybook addon-a11y | Shift-left issues |

---

## Tool Stack

### Core Open-Source Stack

| Tool | Best use | Key strength | Limitation |
|------|----------|-------------|------------|
| **Lighthouse** | Performance, a11y, SEO, PWA, best-practices | CLI, DevTools, Node, auth-capable | Not a substitute for manual UX judgment |
| **Lighthouse CI (LHCI)** | Regression gates on PRs | Repeated runs, diffs, assertions, budgets | Needs stable CI environment and calibration |
| **PageSpeed Insights** | Lab + field performance | Combines Lighthouse lab + real CrUX field data | Best for perf/SEO, not whole UX |
| **CrUX** | Real-user CWV benchmarking | Real-world Chrome-user field data | Not available for every page/origin |
| **axe-core** | Accessibility engine in tests and extensions | JSON results, iframe support, local | Only catches automatically detectable issues |
| **Pa11y / Pa11y CI** | CI-oriented URL accessibility sweeps | CLI-first, CI-friendly | Broader a11y still needs manual review |
| **Playwright** | Authenticated E2E flows, cross-browser regression | Chromium/Firefox/WebKit, auth state reuse, CI docs | Needs engineering setup and stable fixtures |
| **Puppeteer** | Browser automation, screenshots, PDFs, accessibility tree snapshots | Fast Chrome/Firefox automation; PDF + a11y snapshot API | Narrower cross-browser than Playwright |
| **Accessibility Insights for Web** | Guided fast/manual accessibility review | FastPass, guided assessments, visual helpers | Part of a full audit only |
| **WAVE** | Human-aided accessibility review | Finds WCAG errors, facilitates manual evaluation | Explicitly insufficient to determine a11y by itself |
| **Storybook addon-a11y** | Component-library accessibility | Runs axe-core in stories | Component-level only |
| **eslint-plugin-jsx-a11y** | React static a11y linting | Shift-left checks in JSX | Static only; doesn't test rendered DOM |
| **OWASP ZAP** | Security baseline and automated scans | Docker automation, baseline/full/API scans | Findings need risk review and safe scan design |
| **MDN HTTP Observatory** | Security headers/config hygiene | Actionable header and config feedback | Narrower than full app security verification |
| **Search Console + Rich Results Test** | Search performance and structured data | Query/page visibility, indexing signals | Requires property access for full value |

### Commercial Accelerators (When Budget Allows)

| Tool | Best use |
|------|----------|
| **axe DevTools** | Team-scale a11y automation, enterprise reporting, commercial browser extension |
| **BrowserStack Accessibility** | Real-device accessibility testing across many browsers/devices |
| **Siteimprove** | Large-site a11y/SEO/content governance at scale |
| **Hotjar** | Heatmaps, recordings, surveys — understanding where users actually get stuck |
| **Contentsquare** | Enterprise experience analytics and voice-of-customer insights |

---

## Minimum Viable Metrics Set

Track these 13 metrics for a defensible, repeatable audit baseline:

| Metric | Target / interpretation |
|--------|------------------------|
| **Task success rate** | Higher = better; track per critical task |
| **Time on task** | Compare before/after; benchmark against flow |
| **Critical error rate** | Lower = better; track per flow |
| **SUS or UMUX-Lite** | Benchmark longitudinally — not as sole truth |
| **LCP (Largest Contentful Paint)** | ≤ 2.5s |
| **INP (Interaction to Next Paint)** | ≤ 200ms |
| **CLS (Cumulative Layout Shift)** | ≤ 0.1 |
| **TTFB (Time to First Byte)** | ≤ 800ms |
| **Accessibility violations by impact** | Trend down; always pair with manual results |
| **Keyboard completion rate** | 100% on every critical flow |
| **Structured data validity** | No critical errors on target resource types |
| **Search CTR / impressions / position** | Baseline and trend by key pages |
| **Security header score / ZAP findings** | No high-severity header/config gaps |

---

## Automation Snippets

### Lighthouse CLI + LHCI Config

```bash
# One-off local audit
npm install -g lighthouse @lhci/cli

lighthouse https://example.com \
  --only-categories=performance,accessibility,best-practices,seo,pwa \
  --output=html --output=json \
  --output-path=./reports/home \
  --chrome-flags="--headless=new"
```

```json
{
  "ci": {
    "collect": {
      "url": ["http://localhost:3000/", "http://localhost:3000/checkout", "http://localhost:3000/dashboard"],
      "numberOfRuns": 3
    },
    "assert": {
      "assertions": {
        "categories:performance": ["warn", { "minScore": 0.9 }],
        "categories:accessibility": ["error", { "minScore": 1 }],
        "categories:seo": ["warn", { "minScore": 0.95 }],
        "largest-contentful-paint": ["warn", { "maxNumericValue": 2500 }],
        "interaction-to-next-paint": ["warn", { "maxNumericValue": 200 }],
        "cumulative-layout-shift": ["warn", { "maxNumericValue": 0.1 }]
      }
    }
  }
}
```

### Playwright + axe-core

```js
import { test, expect } from "@playwright/test";
import AxeBuilder from "@axe-core/playwright";

test("checkout flow is accessible", async ({ page }) => {
  await page.goto(process.env.APP_URL ?? "http://localhost:3000/checkout");
  const results = await new AxeBuilder({ page }).include("main").analyze();
  expect(results.violations).toEqual([]);
});

test("main navigation remains semantically stable", async ({ page }) => {
  await page.goto(process.env.APP_URL ?? "http://localhost:3000/");
  await expect(page.locator("body")).toMatchAriaSnapshot(`
    - banner
    - navigation
    - main
    - contentinfo
  `);
});
```

### Pa11y CI Config

```json
{
  "defaults": {
    "standard": "WCAG2AA",
    "timeout": 30000,
    "chromeLaunchConfig": { "args": ["--no-sandbox"] }
  },
  "urls": [
    "http://localhost:3000/",
    "http://localhost:3000/pricing",
    "http://localhost:3000/signup",
    "http://localhost:3000/checkout"
  ]
}
```

### Puppeteer — Audit Artifacts

```js
import puppeteer from "puppeteer";
const browser = await puppeteer.launch();
const page = await browser.newPage();
await page.goto("http://localhost:3000/", { waitUntil: "networkidle2" });

await page.screenshot({ path: "./reports/home-full.png", fullPage: true });
const accessibilityTree = await page.accessibility.snapshot();
console.log(JSON.stringify(accessibilityTree, null, 2));
await page.pdf({ path: "./reports/home.pdf", format: "A4", printBackground: true });
await browser.close();
```

### GitHub Actions CI Workflow

```yaml
name: ux-audit
on:
  pull_request:
  push:
    branches: [main]

jobs:
  audit:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with: { node-version: 22 }
      - run: npm ci
      - run: npm run build
      - run: npm run start & npx wait-on http://localhost:3000
      - run: npx lhci autorun
      - run: npx playwright test
      - run: npx pa11y-ci
      - name: ZAP baseline
        run: |
          docker run --network=host -t owasp/zap2docker-stable \
            zap-baseline.py -t http://localhost:3000 -r zap-report.html
```

**Auth pages note:** Use Playwright auth-state reuse for pages behind login. Keep the stored auth state file out of source control.

---

## Issue Entry Template (Structured Format)

Each reported issue should include all of these fields:

```json
{
  "id": "FORM-004",
  "title": "Checkout email field loses input after validation error",
  "category": "FORM",
  "priority": "P1",
  "severityScore": 15,
  "affectedFlows": ["Guest checkout"],
  "affectedPages": ["/checkout"],
  "evidence": {
    "viewport": "390x844",
    "browser": "Chromium 124",
    "steps": ["Open checkout", "Enter shipping details", "Submit with invalid postal code", "Observe email field cleared"],
    "artifacts": ["checkout-error.png", "playwright-trace.zip"]
  },
  "whyItMatters": "Creates extra effort, increases abandonment risk, violates error recovery principle.",
  "standards": ["Nielsen heuristic: Help users recognize, diagnose, and recover from errors", "WCAG 3.3.1 / 3.3.3"],
  "recommendation": "Preserve valid inputs, focus first invalid field, show inline actionable message.",
  "owner": "Checkout FE",
  "acceptanceCriteria": [
    "Valid fields remain populated after submit",
    "Focus moves to first invalid field",
    "Error is programmatically associated with the field"
  ],
  "retest": "Playwright scenario + manual keyboard check"
}
```

---

## Remediation Plan Template

| Field | Description |
|-------|-------------|
| Initiative | Human-readable project or sprint grouping |
| Problem statement | What users cannot do, or do inefficiently |
| Target outcome | What successful experience should look like |
| Priority and owner | P0–P3 plus accountable team |
| Fix type | Content / design / frontend / backend / SEO / security / analytics |
| Dependencies | API, design system, CMS, legal, infrastructure |
| Acceptance criteria | Observable pass conditions |
| Verification method | Tool rerun, manual check, or usability retest |
| Rollout risk | Low / medium / high |
| Post-fix KPI | Task success rate, CWV delta, violation reduction, CTR change |

---

## 4 Report Deliverable Types

| Deliverable | Best use | Core sections | Typical audience |
|------------|----------|---------------|-----------------|
| **Executive scorecard** | Leadership snapshot | Business risk, top issues, positives, quick wins, roadmap | Execs, PMs, product leaders |
| **Full audit report** | Main deliverable | Scope, methods, pages/flows tested, issues, evidence, standards mapping, positives, remediation | Product, design, engineering, QA |
| **Remediation backlog** | Implementation bridge | Ticket-ready issues, owners, acceptance criteria, ETA, retest method | Engineering and design teams |
| **Re-test memo** | Closure artifact | Fixed issues, evidence of pass, residual risks, next iteration | PM, QA, compliance, stakeholders |

---

## Sample Audit: Before/After Patterns

### E-commerce Checkout

| Before | Problem | After | Priority |
|--------|---------|-------|----------|
| Two-column checkout on mobile | Increases parsing effort and error risk | Single-column responsive layout for core inputs | P1 |
| Card number rejects spaces | Conflicts with user expectation | Accept and auto-format spaces; store normalized | P1 |
| Error message: "Invalid input" only | Poor diagnosis and recovery | Field-specific inline error with correction hint | P1 |
| Valid fields cleared on submit error | Wastes user effort, raises abandonment | Preserve valid inputs; focus first invalid field | P0 |

### SaaS Dashboard

| Before | Problem | After | Priority |
|--------|---------|-------|----------|
| Icon-only sidebar items | Weak recognition, slower learnability | Add labels or persistent tooltips + active state clarity | P1 |
| Keyboard focus disappears in modal | Blocks keyboard/AT users | APG-compliant modal focus management; restore focus on close | P0 |
| Chart area shifts during loading | CLS + scanning disruption | Reserve chart dimensions; use skeleton loading | P1 |
| Low-contrast status chips | Hard to distinguish for low-vision users | Raise contrast + add secondary non-color signifier | P1 |
| Empty states say "No data" only | Missed guidance opportunity | Add explanation, setup action, and docs link | P2 |

### Mobile PWA

| Before | Problem | After | Priority |
|--------|---------|-------|----------|
| Small tappable controls | Error-prone for thumb use and motor a11y | Increase target size and spacing to platform minimums | P1 |
| Ambiguous bottom-nav labels | Slows recognition, increases mis-taps | Clear task-oriented labels + active-state indicators | P1 |
| Offline mode silently serves stale data | Users can't trust data freshness | Add sync state, last-updated timestamp, retry/update messaging | P1 |
| Booking form breaks at high zoom | Excludes zoom users | Fix reflow, wrapping, and field order for narrow viewports | P0 |

---

## Audit Service Tiers

| Package | Scope | Effort | Key deliverables |
|---------|-------|--------|-----------------|
| **Rapid diagnostic** | 1–3 core flows, no user testing | 8–16 hrs | Executive scorecard, top 15–25 issues, quick wins |
| **Standard audit** | 5–10 flows, a11y + perf + SEO + security baseline | 24–40 hrs | Full report, issue backlog, readout, retest plan |
| **Deep audit** | Authenticated app, multiple roles, component checks, CI recommendations, optional benchmark tasks | 60–120 hrs | Full report + backlog + CI snippets + owner plan |
| **Continuous audit** | Recurring per release or sprint | Ongoing retainer | Regression dashboard, spot checks, trend review, sign-off memo |

**Pricing principle:** Price from scope clarity + business criticality + implementation support — not page count. A checkout or sign-in flow is worth more than a ten-page brochure sweep because the risk and remediation value are higher.

---

## Key Limitations (By Design)

- **No automated tool alone determines full accessibility conformance.** W3C, WAVE, and Playwright all explicitly state this. Always pair automated scans with manual review and inclusive user testing.
- **URL cannot expose code-level preventions.** A live URL can't show lint rules, component constraints, or CI policies.
- **Repo cannot establish rendered UX quality.** A backend repo can reveal latency and auth issues but can't confirm the interface communicates clearly or preserves focus.
- **Strongest practice is hybrid:** URL + repo + representative user flows where possible.
