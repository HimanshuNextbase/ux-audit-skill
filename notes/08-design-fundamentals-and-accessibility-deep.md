# Design Fundamentals & Accessibility Deep Dive

---

## Reading Patterns (New — not in prior notes)

Users don't read pages linearly. Two dominant scan patterns:

| Pattern | Path | When It Applies |
|---------|------|-----------------|
| **Z-pattern** | Logo (top-left) → CTA (top-right) → Content (middle-left) → Final CTA (bottom-right) | Landing pages, hero sections, pages with clear CTAs |
| **F-pattern** | Scan headline → scan first line of each section downward | Content-heavy pages, articles, search results |

**Design implication:** Place the most important elements along the Z or F path. Content outside those paths gets skimped.

---

## Hick's Law

> More choices = slower decisions.

**Application:** Use whitespace to reduce visual noise and limit the number of choices presented at once. Every extra option on screen has a cost. Decision paralysis is a real UX failure mode.

---

## Whitespace as Premium Signal

Whitespace is not wasted space — it signals quality and reduces cognitive load.

| Feel | Whitespace Level |
|------|-----------------|
| Premium (Apple, Stripe) | Generous — lots of breathing room |
| Cheap / overwhelming | Crowded — no breathing room |

**Specific numbers:**
- Space elements in multiples of **8px** (8, 16, 24, 32, 48, 64)
- Between sections: **48–64px minimum**
- Inside cards: **24–32px**

---

## Color Scale Architecture (50–900)

Build a full tonal scale for every brand color for consistency across states:

```
50:  Lightest — page backgrounds, hover fills
100: Very light — subtle backgrounds
200–300: Light — disabled states, borders
400: Mid-light — placeholder text
500: Base brand color — main usage
600: Darker — hover states on primary
700: Dark — pressed/active states
800–900: Darkest — text on light backgrounds
```

**Palette structure every project needs:**
1. **Primary** — brand color, CTAs, links, active states
2. **Neutrals** — gray 50–900 for text, backgrounds, borders
3. **Success** — green (confirmations, checkmarks)
4. **Error** — red (warnings, destructive actions)
5. **Warning** — yellow/orange (alerts)

**2026 color trends:**
- Soft gradients as backgrounds (subtle ambient shifts — not 2015 loud gradients)
- Cinematic color fields (inspired by lighting/fog effects)
- High saturation for CTAs (makes them unmissable)

**Tools:** Huevy.app, Coolors.co, Adobe Color

---

## Typography: Letter Spacing Rule

Already have line-height and line-length rules. This is new:

- **Headings:** `-0.02em` letter spacing (tighter = more impactful)
- **Body text:** Normal / default letter spacing (don't override)

Full scale reference (8px baseline):
```
text-xs:   12px / 16px line-height
text-sm:   14px / 20px
text-base: 16px / 24px  ← body default
text-lg:   18px / 28px
text-xl:   20px / 28px
text-2xl:  24px / 32px
text-3xl:  30px / 36px  ← section headers
text-4xl:  36px / 40px
text-5xl:  48px / 1     ← hero titles
```

**Font pairing rule:** 2 fonts maximum — sans-serif for UI (Inter, Geist, SF Pro), optional serif for premium headings (Playfair, Merriweather).

**Safe system stack (zero load time):**
```css
font-family: -apple-system, BlinkMacSystemFont, "Segoe UI",
             Roboto, "Helvetica Neue", Arial, sans-serif;
```

---

## CSS Grid vs Flexbox — When to Use Each

| Tool | Dimension | Use For |
|------|-----------|---------|
| **CSS Grid** | 2D (rows + columns) | Page structure: header, sidebar, main, footer |
| **Flexbox** | 1D (row or column) | Component internals: card rows, button groups |

**Auto-fit grid — no media queries needed for simple grids:**
```css
.grid {
  display: grid;
  gap: 1.5rem;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
}
```
Automatically wraps items when they don't fit — works at any viewport width.

---

## Micro-Interaction: Error Shake

Already have hover/press scale in prior notes. This is the missing error state:

- **Error shake:** Subtle 2px left-right shake animation (not jarring — 2px is enough)
- **Success big win:** Confetti animation (for milestone moments like first post scheduled, account created)

---

## WCAG 2.2 Framework (POUR)

The 4 core accessibility principles everything is measured against:

| Principle | Meaning | Failure Example |
|-----------|---------|-----------------|
| **Perceivable** | Information must be presentable to users in ways they can perceive | Image with no alt text — invisible to screen readers |
| **Operable** | Interface components must be operable | Dropdown with no keyboard support |
| **Understandable** | Information and UI must be understandable | Error message that says "Invalid" with no explanation |
| **Robust** | Content must work with current and future assistive technologies | Custom widget with no ARIA roles |

**Conformance levels:**
- **Level A** — Minimum (basics covered)
- **Level AA** — Target for most sites (what WCAG compliance usually means)
- **Level AAA** — Highest (specialized/government/healthcare)

> Accessibility is a **legal requirement** (ADA in the US, Section 508 for federal). 1 in 4 adults in the US has a disability. Accessibility is not optional.

---

## ARIA Deep Dive (States + Relationships)

Already have basic aria-label in prior notes. These are new:

### Dynamic State Attributes
```jsx
aria-expanded={isOpen}      // dropdown/accordion open state
aria-selected={isActive}    // selected tab/option
aria-checked={isChecked}    // checkbox/radio/toggle state
aria-disabled="true"        // disabled (but still focusable)
```

### Relationship Attributes
```jsx
// aria-labelledby: reference a visible heading as the label
<h2 id="dialog-title">Delete Account</h2>
<div role="dialog" aria-labelledby="dialog-title">...</div>

// aria-describedby: add supplementary description
<input id="password" aria-describedby="pw-hint" />
<p id="pw-hint">Must be at least 8 characters</p>

// aria-controls: element controls another element
<button aria-controls="menu-panel" aria-expanded={isOpen}>Open Menu</button>
<div id="menu-panel">Menu content</div>
```

### aria-live Regions (Announcing Dynamic Changes)
```jsx
// Status updates — announce when screen reader is idle
<div role="status" aria-live="polite" aria-atomic="true">
  {statusMessage}
</div>

// Errors — interrupt immediately
<div role="alert" aria-live="assertive">
  {errorMessage}
</div>
```

| Value | Behavior |
|-------|----------|
| `polite` | Wait until screen reader is idle before announcing |
| `assertive` | Interrupt current speech and announce immediately |
| `off` | Don't announce changes |

---

## Focus Management in Modals

When a modal opens, **focus must move inside it** — and be **trapped there** until closed:

```jsx
const closeButtonRef = useRef(null)

useEffect(() => {
  if (isOpen && closeButtonRef.current) {
    closeButtonRef.current.focus()  // move focus in on open
  }
}, [isOpen])
```

**Rules:**
- On open → move focus to first focusable element (or close button)
- While open → Tab/Shift+Tab cycles only within the modal
- On close → return focus to the element that triggered the modal
- Escape key must close the modal

---

## tabIndex Rules

| Value | When to Use |
|-------|-------------|
| `tabIndex={0}` | Add a non-interactive element to the natural tab order (e.g., a custom widget) |
| `tabIndex={-1}` | Remove from tab order but keep programmatically focusable (for JS-managed focus) |
| `tabIndex={1+}` | **Avoid** — overrides natural order, creates confusing tab sequences |

**Rule:** Don't use positive tabIndex values. Fix the DOM order instead.

---

## Buttons vs Links — Semantic Distinction

| Element | Use For | Wrong Use |
|---------|---------|-----------|
| `<button>` | Actions (submit, delete, toggle, open modal) | Navigation |
| `<a href="...">` | Navigation (going to a URL or anchor) | Triggering actions |

```jsx
// ✅ Correct
<button onClick={handleSubmit}>Submit Form</button>
<a href="/about">About Us</a>

// ❌ Wrong — link doing an action
<a href="#" onClick={handleSubmit}>Submit Form</a>

// ❌ Wrong — button doing navigation
<button onClick={() => navigate('/about')}>About Us</button>
```

Screen readers announce `<button>` as "button" and `<a>` as "link" — wrong usage breaks the mental model.

---

## Alt Text Specific Rules

Already have "add alt text" in prior notes. These are the specific writing rules:

- Describe **content/function**, not appearance
- Keep under **125 characters**
- **Don't start with** "image of" or "picture of" (screen readers already say "image")
- Use **empty alt** (`alt=""`) for decorative/spacer images — screen readers skip them
- For complex images (charts, graphs): provide a text summary in the alt or a linked description

```jsx
// ✅ Good
<img src="chart.png" alt="Bar chart showing 50% sales increase from 2024 to 2025" />

// ❌ Bad
<img src="chart.png" alt="image" />
<img src="chart.png" />  // missing entirely

// ✅ Decorative — skip it
<img src="divider-line.png" alt="" />
```

---

## Accessibility Testing Tools

| Tool | Type | What It Finds |
|------|------|---------------|
| **axe DevTools** (Chrome extension) | Automated | WCAG violations; most accurate automated tool |
| **Lighthouse** (Chrome DevTools → Lighthouse tab) | Automated | Score + recommendations; built into browser |
| **WAVE** (wave.webaim.org) | Automated | Visual overlay showing errors and warnings |
| **NVDA** (Windows, free) | Manual / Screen reader | Hear how your UI sounds to blind users |
| **VoiceOver** (Mac, Cmd+F5) | Manual / Screen reader | Same, native to macOS |
| **Chrome → Rendering → Emulate vision deficiencies** | Manual | Simulate color blindness (deuteranopia, etc.) |
| **Zoom to 200%** (Cmd/Ctrl + +) | Manual | Verify no horizontal scroll, no text overflow |

**Quality targets:**
- Lighthouse accessibility score: **> 95**
- axe DevTools: **0 violations**

---

## Common Accessibility Gotchas

Things that look fine visually but break accessibility — test these specifically:

- Custom dropdowns (Select replacements) often lack keyboard support
- Modal focus trapping frequently broken — Tab escapes the modal
- Icon-only buttons missing aria-labels
- Form validation errors not announced to screen readers
- Loading states not communicated (spinner with no aria-label or aria-live)
- Color used as the only indicator (error red without icon or text)
- Placeholder text too light — fails 4.5:1 contrast (placeholder ≠ label)
- Disabled buttons: exempt from contrast rules but should still be visually distinct

---

## Placeholder Text Contrast Warning

Placeholder text is often styled too light and fails contrast requirements.

- Placeholder text is **not** a label substitute
- It should meet **3:1 contrast** minimum (it's hint text, not body text)
- Common failure: `#999999` on white = 2.9:1 (fails)
- Fix: darken placeholder color to at least `#767676` on white (4.5:1)

---

## One h1 Per Page Rule

Each page should have **exactly one `<h1>`** — the page title. All other headings use h2–h6 in logical order. Multiple h1s confuse screen reader navigation.

---

## Pre-Build Design Checklist (Before Writing Code)

Different from the post-delivery checklist in note 05 — this is for planning before any code starts:

- [ ] Color palette defined (primary + 4 neutrals minimum + semantic colors)
- [ ] Typography scale chosen (6–8 sizes)
- [ ] Component library picked (e.g., Shadcn/ui + Tailwind)
- [ ] Mobile breakpoints planned (576px, 768px, 992px)
- [ ] Accessibility contrast ratios checked (4.5:1 text, 3:1 UI)
- [ ] Micro-interaction list defined (hover, click, error, success states)
- [ ] Grid layout sketched (mobile → desktop progression)

---

## 5 Laws of Beautiful UI

A memorable summary of what makes UI work:

1. **Contrast creates hierarchy** — big vs small, dark vs light
2. **Whitespace creates calm** — never fear empty space
3. **Consistency builds trust** — same patterns repeated throughout
4. **Feedback confirms action** — animations and success messages
5. **Accessibility includes everyone** — contrast, keyboard, screen readers

---

## Inspiration Sources — Real Products to Study

Products worth studying for UI/UX quality:

| Product | Why Study It |
|---------|-------------|
| **Linear** (linear.app) | Best keyboard-first UI, subtle animations done right |
| **Stripe Dashboard** | Clean data visualization, perfect spacing |
| **Vercel** | Minimalist, fast, modern gradient usage |
| **Notion** | Intuitive drag-and-drop, clear hierarchy |

**Design systems to reference:**
- Material Design 3 (Google)
- Human Interface Guidelines (Apple HIG)
- Radix Themes
- Tailwind UI

---

## Component Folder Structure Convention

```
/components
  /ui          ← Component library primitives (button, card, dialog)
  /layout      ← Navbar, footer, sidebar
  /features    ← Feature-specific components (upload, calendar, preview)
  /shared      ← Reusable custom components used across features
```
