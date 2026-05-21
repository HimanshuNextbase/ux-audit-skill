# UX Audit Research Index

Building a UX audit AI skill for automated UX testing of any site or app.

---

## Notes (Processed & Organized)

| File | Contents |
|------|----------|
| `notes/01-ux-guidelines-99-rules.md` | All 99 UX rules by category (Navigation, Animation, Layout, Touch, Interaction, Accessibility, Performance, Forms, Responsive, Typography, Feedback) with Do/Don't and severity |
| `notes/02-priority-quick-reference.md` | 10 rule categories ranked by priority (CRITICAL → LOW) with full sub-rules per category |
| `notes/03-ui-styles-67.md` | All 67 UI styles (General, Landing Page, Dashboard) with Best For, NOT For, and style selection framework |
| `notes/04-industry-reasoning-rules.md` | 161 industry reasoning rules grouped by sector (SaaS, Finance, Healthcare, E-commerce, Services, Creative, Social, Education, Government, Emerging Tech) |
| `notes/05-pre-delivery-checklist.md` | Pre-delivery checklists (Web + App), common UI anti-patterns, icon/layout/interaction issues |
| `notes/06-design-system-workflow.md` | Full design system generation workflow, example output (Beauty Spa), when to use the skill, query strategy tips |
| `notes/07-krug-ux-audit-methodology.md` | Steve Krug's behavioral UX audit: Trunk Test, 3 Laws, Billboard Design, Home Page 5 Questions, Goodwill Drains/Builders, Satisficing, Audit report template |
| `notes/08-design-fundamentals-and-accessibility-deep.md` | Z/F reading patterns, Hick's Law, whitespace numbers, color scale 50–900, typography letter-spacing, CSS Grid vs Flexbox, WCAG POUR + levels, aria-live values, ARIA states/relationships, focus trapping, tabIndex rules, alt text rules, testing tools (axe/Lighthouse/WAVE), common gotchas, 5 Laws of Beautiful UI |
| `notes/09-uxaudit-framework-and-checks.md` | Full testing stack pyramid, UX layers (usability/desirability/retention), 4 lenses (understand/decide/act/recover), 17 AI-slop checks, Cooper's excise catalog, 4-axis journey evaluation, delight signals, Norman's 3 emotional layers, JTBD framework, journey scenario floors by product type, cold/returning/power-user modes, category friction red flags |
| `notes/10-hallmark-anti-slop-design.md` | Pre-emit self-critique (6 axes: Philosophy/Hierarchy/Execution/Specificity/Restraint/Variety), 21 named macrostructures, SaaS page sequence, 50+ anti-patterns by severity (Critical/Major/Microinteraction/Minor), 8-state interactive element requirement, hit-target expansion via ::before, tooltip timing split (hover 800ms vs focus 0ms), focus ring instant-appearance rule, icon library defaults by project type |
| `notes/11-headway-ux-audit-checklist.md` | Pre-audit setup (define goals + personas + KPIs + watch sessions first), 5-category heuristic checklist (Content/Design+Typography/Navigation/Accessibility/Mobile), 5-section report format (Executive Summary/Key Findings/Interview Quotes/Major Callouts/Roadmap), loader with remaining-time hint rule, progress indicator requirements, auth/login complete checklist, mobile-specific checks, 3 new audit tools (Contrast/Stark/Coblis), micro-audit cadence |

---

## Key Takeaways So Far

1. **Priority order for any UX audit:** Accessibility → Touch/Interaction → Performance → Style → Layout → Typography → Animation → Forms → Navigation → Charts

2. **Top HIGH-severity rules to always check:**
   - Color contrast 4.5:1 minimum
   - Touch targets 44×44px minimum
   - Focus states visible (no `outline: none` without replacement)
   - No emoji as icons
   - `prefers-reduced-motion` respected
   - Loading feedback for async operations
   - Error messages near the problem (not just at form top)
   - Confirmation dialogs before destructive actions

3. **Industry-specific anti-patterns:**
   - Finance/Legal/Healthcare: NEVER use AI purple/pink gradients
   - Wellness/Spa: NO dark mode, NO bright neon, NO harsh animations
   - Gaming: NO minimalist design, NO static assets
   - Government: NO ornate design, NO low contrast, NO motion effects

4. **Design system generation process:** Product type → parallel 5-domain search → reasoning engine → complete system (pattern + style + colors + typography + effects + anti-patterns)

5. **Krug's 3 behavioral facts about users (from note 07):**
   - Users scan, they don't read — design for scanning not reading
   - Users satisfice — they pick the first reasonable option, not the best one
   - Users muddle through — they skip instructions; if muddling works, the design works

6. **Krug's Trunk Test:** Drop on any random page — can you instantly answer: What site? What page? Major sections? Options here? Where am I? How to search? Each answer should take under 2 seconds.

7. **Goodwill model:** Sites have a trust reservoir. Drains: hiding pricing, punishing wrong input format, unnecessary data collection. Builders: obvious tasks, upfront costs, saves steps, real FAQs.

8. **Hallmark pre-emit critique:** Before running any slop gate checks, score 6 axes (Philosophy, Hierarchy, Execution, Specificity, Restraint, Variety) — any score < 3 triggers a revision pass first.

9. **21 macrostructures:** Every page has a named shape (Bento Grid, Stat-Led, Workbench, Marquee Hero, Manifesto, Letter, Catalogue, etc.). Never use the same shape twice in one output set.

10. **Critical AI-tells beyond note 09:** The AI nav (wordmark+centred links+CTA right+sticky white), The AI footer (4-column links), pure #000/#fff colors, 3-column feature grid, card-in-card, gradient headline text, full-viewport centred hero, aurora-blob backgrounds, invented metrics.

11. **Microinteraction rules:** Tooltip hover delay 800–1000ms / focus delay 0ms. Focus rings never animate in. Toasts must be fixed-position. Spinners: delay-show 150ms, minimum visible 300ms. Confirmation dialogs only for irreversible actions — use optimistic delete + undo for reversible.

12. **Pre-audit setup (Headway):** Define audit goals before touching any screen. Unpack personas, review KPIs, watch recorded user sessions first. Choose one focus area — don't try to audit everything at once.

13. **Loader rule:** If anything takes >3 seconds, show a loader with a hint containing the remaining time — not just a spinner.

14. **Progress indicator rule:** Multi-step workflows need a progress indicator that shows both where the user is AND how much is left.

15. **Auth checklist:** Password requirements shown BEFORE entry; eye toggle to reveal; browser password gen supported; field name visible in filled state; password match shown in real time; T&C "I agree" next to register button.

16. **Major Callout format:** Each audit issue needs 3 things: screenshot + explainer of why it's a problem + plan to address it.

17. **5-section audit report:** Executive Summary → Key Findings (3–5) → Interview Quotes → Major Callouts → Roadmap (sprint backlog or larger conversation).
