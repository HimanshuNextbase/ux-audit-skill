# Lane A-Mobile — Rendered Mobile Experience Procedure

This file is loaded by the Lane A-Mobile subagent. It contains the full procedure for
auditing the mobile (390px) rendered experience: URL acquisition, Pass 1B mobile sweep,
screenshots, CWV measurement, and output format.

The subagent also loads audit-checks.md for the checklist categories and scoring rubric.

---

You are Lane A-Mobile. Audit the rendered MOBILE experience of this product.

Load this skill file:
  skill_view("ux-audit", "prompts/audit-checks.md")   # checklist, anti-slop, advisory, scoring, output format

**SCOPE OVERRIDE — Mobile only:**
- Your entire audit runs at 390×844 (iPhone 14) viewport. Do NOT use 1440px.
- Run Pass 1B only (mobile discovery). Do NOT run Pass 1 (desktop).
- In Pass 2, all screenshots are at 390px only.
- Run CWV at 390px only.
- Audit the PRIMARY JOURNEY only — not every page.

**Step 0: URL Acquisition — do this first, before any auditing**

Same rules as Lane A-Desktop: detect whether you have a URL (Case 1), runnable code (Case 2), URL in codebase (Case 3), or backend only (Case 4). Run the app locally if no URL given.

**GEO-BLOCK / UNREACHABLE SITE — same detection as Lane A-Desktop:**
1. Try browser_navigate. If ERR_TIMED_OUT, run TCP probe.
2. If TCP blocked → stop, message user for screenshots.
3. Do NOT file "site unreachable" as a UX finding.

**PASS 1B — Mobile discovery:**

Start at 390×844 immediately. Run the settled-check after every navigate:
```js
(async () => {
  await new Promise(resolve => {
    if (document.readyState === 'complete') { resolve(); return; }
    window.addEventListener('load', resolve, { once: true });
  });
  const anims = document.getAnimations();
  if (anims.length > 0) { await Promise.all(anims.map(a => a.finished.catch(() => {}))); }
  await new Promise(r => setTimeout(r, 800));
  console.log(JSON.stringify({ settled: true, readyState: document.readyState }));
})();
```

Check for mobile-specific issues on the primary journey:
- **Horizontal scroll** — any element wider than 390px
- **Navigation collapse** — desktop nav → hamburger? Does hamburger work?
- **Touch targets** — buttons/links visually smaller than ~44px height
- **Text overflow** — headings or long words that overflow containers
- **Stacked layout breaks** — side-by-side elements that overlap at 390px
- **Font sizes** — text readable at 1440px but too small at 390px
- **Forms** — inputs extending beyond screen width
- **Fixed elements** — sticky headers eating too much vertical space
- **Image scaling** — images breaking containers or becoming unreadable
- **Modal/sheet sizing** — modals that don't fit or can't scroll

Detect horizontal overflow:
```js
(async () => {
  await new Promise(r => setTimeout(r, 500));
  console.log(JSON.stringify({
    viewport: 'set to 390px',
    innerWidth: window.innerWidth,
    hasScrollX: document.body.scrollWidth > window.innerWidth,
    overflowingElements: [...document.querySelectorAll('*')]
      .filter(el => el.getBoundingClientRect().right > window.innerWidth)
      .slice(0,5).map(el => el.tagName + (el.className ? '.'+el.className.split(' ')[0] : ''))
  }));
})();
```

Tag all findings `[Mobile only]`.

**CWV — mobile only:**
After first navigate (before any interaction), run the LCP/TTFB observer from system.md. Record in CWV table as Mobile 390px row.

**Score all findings:** assign P0/P1/P2/P3.

**CHECKPOINT — write before starting screenshots:**
```bash
python3 -c "
findings = '''[paste your draft mobile findings here]'''
open('/tmp/mobile-findings-draft.txt', 'w').write(findings)
print('Mobile checkpoint saved')
"
```

**PASS 2 — Evidence (P0/P1 mobile findings only, at 390px):**
Use the same 3-step screenshot workflow from system.md (annotate → browser_screenshot → PIL crop).
All screenshots at 390px. Save to `/home/brew/audits/screenshots/[slug]-[CODE-NNN]-mobile.png`.
Include full absolute paths in Screenshot fields.

**Output format — return a structured finding list only (tagged [Mobile]):**

  #### [CODE-NNN] — Title [Mobile]
  **Priority: P[0-3] | Viewport: Mobile 390px**

  ![CODE-NNN](/home/brew/audits/screenshots/[slug]-[CODE-NNN]-mobile.png)

  **What:** [1–2 sentences]
  **Fix:** [one sentence]

  - **Evidence:** [CSS selector or DOM observation]
  - **Impact:** [who is affected on mobile]
  - **Repro steps:**
      1. Open on 390px mobile viewport
      2. Navigate to [URL/screen]
      3. Observe [broken behaviour]
  - **Expected:** [what should happen]
  - **Actual:** [what actually happens]
  - **Implementation:** [developer-ready fix]
  - Files affected: [specific file:line if from code, else "UI only"]
  - Standard: [Material Design 3 touch target / WCAG 2.5.5 / etc.]

Also return:
- CWV table — Mobile 390px row only
- Journey scores for mobile primary journey
""",
