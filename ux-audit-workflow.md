# UX Audit Workflow — Complete Implementation Guide

**Date:** 2026-05-21  
**Author:** Assistant (OpenClaw)  
**Purpose:** Reference doc for building a UX audit skill/tool that automates finding UX issues in web/mobile apps.

---

## 1. Overview

A UX audit is an automated or semi-automated review process that evaluates a digital product's user experience against established best practices, platform conventions, and design system rules. 

This document describes a **3-layer UX audit system** that covers:
- **Layer 1:** Spec-level audit (before any UI is generated)
- **Layer 2:** Visual audit (after screenshots exist)
- **Layer 3:** Cross-screen consistency audit (holistic review)

---

## 2. Architecture

```
┌──────────────────────────────────────────────────┐
│                   INPUT                          │
│  Product spec, screenshots, or live app URL      │
└──────────────────┬───────────────────────────────┘
                   │
                   ▼
┌──────────────────────────────────────────────────┐
│        LAYER 1: SPEC-LEVEL AUDIT                 │
│                                                  │
│  Pass 1 → Information Architecture Audit         │
│  Pass 2 → Mobile Pattern Compliance Audit        │
│                                                  │
│  Output: findings, warnings, missing screens,    │
│          navigation model, IA score, mobile score │
└──────────────────┬───────────────────────────────┘
                   │
                   ▼
┌──────────────────────────────────────────────────┐
│        LAYER 2: VISUAL SCREEN CRITIQUE           │
│                                                  │
│  For each screen screenshot:                     │
│  → Score 8 criteria (1-10 each)                  │
│  → Detect design rule violations                 │
│  → Generate specific, actionable fixes           │
│  → Compare against reference app screenshots     │
│                                                  │
│  Output: per-screen scores, violations, fixes    │
└──────────────────┬───────────────────────────────┘
                   │
                   ▼
┌──────────────────────────────────────────────────┐
│        LAYER 3: CROSS-SCREEN CONSISTENCY         │
│                                                  │
│  → Navigation consistency across all screens     │
│  → Color/typography/spacing uniformity           │
│  → Icon style consistency                        │
│  → State handling patterns                       │
│  → Empty/error/loading state coverage            │
│                                                  │
│  Output: consistency report, global violations   │
└──────────────────┬───────────────────────────────┘
                   │
                   ▼
┌──────────────────────────────────────────────────┐
│              FINAL REPORT                        │
│                                                  │
│  Combined score, prioritized issues,             │
│  fix instructions, before/after comparison       │
└──────────────────────────────────────────────────┘
```

---

## 3. Layer 1 — Spec-Level UX Audit

This runs BEFORE any UI is generated. It audits the product spec/requirements to catch structural UX problems early.

### Pass 1: Information Architecture Audit

**What it checks:**

| # | Check | What it means |
|---|-------|---------------|
| 1 | Screen flow completeness | Are there missing screens for key user journeys? |
| 2 | Navigation hierarchy | Is the nav model clear and consistent? |
| 3 | Content hierarchy | Does each screen serve a clear purpose without duplication? |
| 4 | Cognitive load | Are there screens trying to do too much? |
| 5 | Entry/exit points | Are there clear entry points and graceful exits? |
| 6 | Intent clarity | For each screen: who is the user, what must they accomplish, how should it feel? |
| 7 | Signature check | Does each screen have ONE deliberate design choice that makes it distinct? |
| 8 | Navigation as product | Is navigation designed intentionally, or is it just scaffolding? |

**Input:**
```json
{
  "productName": "PDF Tools",
  "productCategory": "utility",
  "screens": [
    { "name": "Home", "description": "Tool grid with categories" },
    { "name": "Settings", "description": "App preferences and account" },
    { "name": "Files", "description": "File browser for processed files" }
  ],
  "uiDirection": "Dark theme with orange accents, privacy-focused"
}
```

**Output:**
```json
{
  "findings": [
    "Home screen has no empty state for first-time users",
    "Settings conflates app preferences and account management — split into tabs"
  ],
  "warnings": [
    "No onboarding screen — new users may not understand on-device processing benefit",
    "No search functionality despite potentially large file library"
  ],
  "missingScreens": ["Onboarding", "Search Results", "Processing Progress"],
  "navigationModel": "bottom-tab with 3 primary destinations (Tools, Files, Settings)",
  "iaScore": 7
}
```

### Pass 2: Mobile Pattern Compliance Audit

**What it checks:**

| # | Category | Checks |
|---|----------|--------|
| 1 | Touch targets | All interactive elements ≥ 44×44pt |
| 2 | Safe areas | iOS status bar (47px top) and home indicator (34px bottom) |
| 3 | Gesture conflicts | Swipe gestures not conflicting with system gestures |
| 4 | Thumb reachability | Primary actions in bottom 2/3 of screen (thumb zone) |
| 5 | Loading states | Loading, empty, and error states for all async data |
| 6 | Keyboard handling | Layout accommodates keyboard for form screens |
| 7 | Platform conventions | Follows iOS/Android conventions as appropriate |

**Output:**
```json
{
  "findings": [
    "Settings form has no keyboard-aware scroll container",
    "Primary 'Merge' CTA is at top of screen — out of thumb zone"
  ],
  "warnings": [
    "File list items may be below 44px touch target height",
    "No pull-to-refresh on file list"
  ],
  "patterns": [
    "Use bottom sheet for quick file actions instead of modal",
    "Add pull-to-refresh on file list",
    "Floating action button for primary scan/import action"
  ],
  "mobileScore": 7
}
```

---

## 4. Layer 2 — Visual Screen Critique

This runs AFTER screenshots are generated. Uses a vision AI model to analyze each screen image against scoring criteria.

### 4.1 Scoring Criteria (8 dimensions, 1-10 each)

#### 1. `layout_spacing`
- Spacing values consistent (use a spacing scale: 4/8/12/16/24/32px)
- Clear visual grouping using whitespace, not boxes/borders
- Touch targets ≥ 44×44px
- CTAs isolated with calm surrounding space
- **Score 1-3:** Random spacing, cramped layout
- **Score 7-10:** Disciplined spacing system

#### 2. `typography`
- At least 4 distinct text levels (display, body, label, caption)
- Hierarchy carried by weight + size first, color last
- Body line-height ≥ 1.5
- Text left-aligned for dense content
- No equal-weight text blocks competing for attention
- **Score 1-3:** Uniform weight, unclear hierarchy
- **Score 7-10:** Clear editorial hierarchy

#### 3. `color_contrast`
- All text passes WCAG AA (4.5:1 minimum contrast ratio)
- No banned colors in visible palette (define per design system)
- Warm tint on neutrals (no pure gray #808080)
- Single accent color — no multiple saturated colors competing
- **Score 1-3:** Contrast failures, multiple clashing accents
- **Score 8-10:** Excellent contrast, cohesive palette

#### 4. `touch_targets`
- Interactive elements ≥ 44×44px
- Primary actions in thumb zone (bottom 2/3 of screen)
- Hover/focus/disabled states visible
- Bottom-heavy layout for primary actions
- **Score 1-3:** Small tappable elements, top-screen primary actions
- **Score 7-10:** Thumb-friendly layout

#### 5. `mobile_patterns`
- Appropriate mobile patterns (bottom sheet vs modal, tab bar, swipe gestures)
- Navigation context always visible (where am I?)
- Feels like native mobile, not desktop web
- Tab bar: same background as content with subtle border, not contrasting color
- Canvas dominance on editor/viewer screens (≥ 55% viewport height)
- **Score 1-3:** Desktop-web patterns, no navigation context
- **Score 7-10:** Genuinely mobile-native

#### 6. `visual_polish`
- Looks hand-crafted, not AI-generated or template-like
- Shadows subtle (whisper, not shout)
- No AI gradients, glassmorphism, mesh backgrounds
- Has a "signature" — one deliberate design choice unique to this product
- Surface elevation steps are whisper-quiet
- **Score 1-3:** Generic AI-looking output
- **Score 8-10:** Distinctive, crafted design

#### 7. `design_system_compliance`
- Follows the defined design system rules (colors, fonts, spacing, components)
- No banned elements (varies per design system)
- Correct component usage (buttons, pills, icons)
- **Score 1-3:** Multiple design system violations
- **Score 8-10:** Fully compliant

#### 8. `craft_intentionality`
- Design feels like it emerged from THIS product's context
- Can you identify the intent (who, what, how it should feel)?
- Token names are semantic and evocative, not generic
- Typography IS the design, not just a container
- Navigation designed intentionally
- Would another AI produce substantially the same output? (If yes, score max 5)
- **Score 1-3:** Generic template output
- **Score 8-10:** Clearly intentional, context-specific

### 4.2 Pass/Fail Threshold

```
PASS = ALL criteria ≥ 7 AND design_system_compliance ≥ 8
```

If a screen fails, specific fix instructions are generated.

### 4.3 Fix Format

Fixes must be **specific and actionable**, not vague:

```
❌ BAD:  "Improve typography"
❌ BAD:  "Fix spacing issues"
✅ GOOD: "Change section title from 14px regular to 18px semibold"
✅ GOOD: "Increase file list row height from 36px to 48px for touch target compliance"
✅ GOOD: "Replace blue accent #3B82F6 with orange #E8761A to match design system"
✅ GOOD: "Move 'Merge' CTA button from header to floating bottom position"
```

### 4.4 Reference Comparison

The visual critique is **significantly more accurate** when reference screenshots from real apps are provided. The vision model uses them as quality benchmarks for:
- Spacing and padding standards
- Typography hierarchy
- Navigation patterns
- Visual polish level
- Mobile-native feel

**Sources for reference screenshots:**
- Mobbin (real app screen library, searchable by category)
- App Store / Play Store (actual published app screenshots)
- Direct app screenshots (captured via browser automation)

**NOT recommended:** Dribbble, Behance (return random unrelated design mockups, not real app screens)

---

## 5. Layer 3 — Cross-Screen Consistency Audit

This is the **holistic review** that catches issues only visible when looking at ALL screens together.

### 5.1 Navigation Consistency

| Check | Issue if violated |
|-------|-------------------|
| Same nav items across all screens | Different tabs on different pages = confusion |
| Same icons for same nav items | Home icon changes from 🏠 to 🏡 between screens |
| Consistent icon sizes | 24px on one screen, 20px on another |
| Active tab treatment | Active tab must have distinct color/highlight everywhere |
| Active tab text weight | Active = bold/colored, Inactive = lighter/muted |

**From your doc's issues:**
```
❌ Different navigation items across screens
❌ Different icons for same navigation menu
❌ Inconsistent icon sizes
❌ Active tab has no clear differentiation
❌ Navigation text lighter than icon weight
```

### 5.2 Settings Page Patterns

| Check | Issue if violated |
|-------|-------------------|
| Active/inactive tab styling | Active tab = different color + bold, Inactive = muted text |
| Consistent item styling | All setting items use same layout (icon + label + value/arrow) |
| Buttons look like buttons | "Clear cache" must look tappable (not plain text) |
| Field padding/margin | Every field has consistent internal padding |
| Icon padding from borders | Icons inside fields have breathing room from container edges |
| Section spacing | Proper spacing between setting groups |

**From your doc's issues:**
```
❌ Active settings tab has no distinct color
❌ Some items have outline box + arrow, others don't = inconsistent
❌ "Clear" button on cached files doesn't look clickable
❌ Fields lack consistent padding/margin
❌ Icons too close to field borders
❌ Top padding excessive
```

### 5.3 Sub-Page Navigation

| Check | Issue if violated |
|-------|-------------------|
| Back button on sub-pages | When navigating into Settings, replace tab bar with back button + title |
| Breadcrumb/context | User should always know where they are |
| Transition direction | Forward nav = slide left, back nav = slide right |

**From your doc's issues:**
```
❌ Settings sub-page still shows bottom nav instead of back button + heading
```

### 5.4 Dedicated vs Shared Pages

| Check | Issue if violated |
|-------|-------------------|
| Feature pages are self-contained | History should have its own page, not embedded in another |
| Active section indicator | Current active section shown at top (after search bar) |
| Action density | Prefer icon-only buttons when space is tight |

**From your doc's issues:**
```
❌ History page doesn't have its own dedicated page
❌ No active tab indicator at top
❌ Share/Rename/Delete/Open should be icon-only (saves space)
```

### 5.5 Empty States & Selection Flows

| Check | Issue if violated |
|-------|-------------------|
| No empty boxes | Empty containers without content = bad UX |
| Selection + proceed | Pages with selections need a visible "Proceed" button |
| Checkbox styling | Use rounded checkmarks that match design system |

---

## 6. Implementation — How to Build This

### 6.1 Tech Stack

```
Vision AI Model (Claude, GPT-4V, Gemini)   → Screen analysis
  +
Playwright / Puppeteer                      → Screenshot capture
  +
Node.js / Python backend                    → Pipeline orchestration
  +
Reference scraper (Mobbin, App Store)        → Quality benchmarks
```

### 6.2 Audit Flow (Code Pseudocode)

```javascript
async function runFullAudit(input) {
  // LAYER 1: Spec audit (if spec available)
  const iaAudit = await auditInformationArchitecture(input.spec);
  const mobileAudit = await auditMobilePatterns(input.spec, iaAudit);
  
  // LAYER 2: Visual critique (for each screen)
  const references = await scrapeReferences(input.spec.category);
  const screenResults = [];
  
  for (const screen of input.screenshots) {
    const critique = await critiqueScreen(screen.image, screen.metadata, references);
    screenResults.push(critique);
  }
  
  // LAYER 3: Cross-screen consistency
  const consistency = await auditConsistency(screenResults, input.screenshots);
  
  // Combine into final report
  return {
    specAudit: { ia: iaAudit, mobile: mobileAudit },
    screenCritiques: screenResults,
    consistencyReport: consistency,
    overallScore: calculateOverallScore(iaAudit, mobileAudit, screenResults, consistency),
    prioritizedFixes: prioritizeFixes(screenResults, consistency)
  };
}
```

### 6.3 Vision Model Prompt Pattern

The key to accurate visual audits is a **structured prompt with explicit scoring rubrics**:

```
1. Define the role: "You are a senior mobile product design reviewer"
2. Provide context: Screen name, description, key elements
3. Attach reference images: Real app screenshots as quality benchmarks
4. Define scoring criteria: Specific rubric for each dimension (1-10)
5. Define hard fails: Violations that cap scores
6. Define pass threshold: e.g., ALL criteria ≥ 7
7. Require structured output: JSON with scores, violations, and specific fixes
8. Require actionable fixes: "Change X from Y to Z" format
```

### 6.4 Critique-Fix Loop

For generative pipelines (where you're also generating the UI), add a feedback loop:

```
┌────────────────┐
│ Generate Screen │
└───────┬────────┘
        │
        ▼
┌────────────────┐     ┌──────────────────┐
│ Take Screenshot │────▶│ AI Visual Critique│
└───────┬────────┘     └────────┬─────────┘
        │                       │
        │              ┌────────▼─────────┐
        │              │ Pass? (all ≥ 7)  │
        │              └──┬───────────┬───┘
        │                 │ NO        │ YES
        │                 ▼           ▼
        │        ┌────────────┐   ┌──────┐
        │        │ Apply Fixes │   │ Done │
        │        └──────┬─────┘   └──────┘
        │               │
        └───────────────┘  (max 3 iterations)
```

---

## 7. Scoring Summary

### Per-Screen Score
```
Overall = average(layout_spacing, typography, color_contrast, 
                  touch_targets, mobile_patterns, visual_polish,
                  design_system_compliance, craft_intentionality)
```

### Cross-Screen Score
```
Consistency = average(nav_consistency, style_uniformity, 
                      icon_consistency, state_coverage, spacing_uniformity)
```

### Final App Score
```
Final = (spec_score × 0.2) + (avg_screen_score × 0.5) + (consistency_score × 0.3)
```

**Rating Scale:**
| Score | Rating | Meaning |
|-------|--------|---------|
| 9-10 | Excellent | Ship-ready, senior designer quality |
| 7-8 | Good | Minor polish needed |
| 5-6 | Fair | Significant UX improvements needed |
| 3-4 | Poor | Major structural issues |
| 1-2 | Critical | Fundamental redesign required |

---

## 8. Common UX Issues Checklist

A quick-reference checklist for the most frequent issues found in generated UIs:

### Navigation
- [ ] Same navigation items on ALL screens
- [ ] Same icons for same nav items everywhere
- [ ] Consistent icon sizes across all nav bars
- [ ] Active tab has distinct visual treatment (color, weight, indicator)
- [ ] Inactive tabs have muted/lighter text
- [ ] Sub-pages replace nav bar with back button + page title

### Spacing & Layout
- [ ] Consistent spacing scale (4/8/12/16/24/32px only)
- [ ] All touch targets ≥ 44×44px
- [ ] Primary actions in thumb zone (bottom 2/3)
- [ ] Proper field padding (icon → content, content → border)
- [ ] Section spacing between groups
- [ ] No excessive padding at top of pages

### Components
- [ ] Buttons look like buttons (not plain text)
- [ ] Active/inactive states are visually distinct
- [ ] Empty states have helpful content (not blank boxes)
- [ ] Selection flows have a clear "Proceed" / "Continue" CTA
- [ ] Text actions (Share, Delete, etc.) use icon-only when space is tight
- [ ] Checkmarks/selections match design system style

### Typography
- [ ] At least 4 text levels (title, subtitle, body, caption)
- [ ] Hierarchy via weight + size, not just color
- [ ] Body text line-height ≥ 1.5
- [ ] Consistent font family across all screens

### Visual Consistency
- [ ] Same color palette across all screens
- [ ] Same border radius, shadow, and elevation patterns
- [ ] Same card/container styling everywhere
- [ ] No screen looks like it belongs to a different app

---

## 9. Source Files

For reference, the working implementation lives in the UI Generator Pipeline:

| File | Purpose |
|------|---------|
| `src/pipeline/ux-auditor.js` | Spec-level 2-pass UX audit (IA + mobile patterns) |
| `src/pipeline/critic.js` | Visual screen critique with 8-criteria scoring |
| `src/pipeline/code-generator.js` | Applies critic fixes to regenerate screens |

---

## 10. How to Extend This

### Adding New Criteria
1. Add the criterion name to the `CRITERIA` array
2. Add scoring rubric to the critique prompt (with 1-3 / 7-10 examples)
3. Add it to the pass threshold logic
4. Update the fix application prompt to enforce new rules

### Adding Platform-Specific Rules
- **iOS:** Safe areas (47px top, 34px bottom), SF Symbols, large title navigation
- **Android:** Material 3 guidelines, 56dp app bar, bottom navigation ≤ 5 items
- **Web:** Responsive breakpoints, hover states, focus indicators, skip navigation

### Adding Design System Rules
Create a separate design system config that the audit loads:
```json
{
  "name": "MyDesignSystem",
  "bannedColors": ["#007bff", "#6c757d"],
  "allowedFonts": ["DM Sans", "Geist", "Sora"],
  "spacingScale": [4, 8, 12, 16, 24, 32, 48, 64],
  "borderRadius": { "small": 8, "medium": 12, "large": 16 },
  "minTouchTarget": 44,
  "maxPrimaryCTAs": 1
}
```

This makes the audit configurable for any design system, not just one.

---

*This document describes the UX audit workflow as implemented in the UI Generator Pipeline (May 2026). It can be adapted into a standalone skill, CLI tool, or API service.*
