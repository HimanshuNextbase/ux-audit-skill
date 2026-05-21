# Steve Krug UX Audit Methodology

> This is a behavioral UX framework — how real users think and fail — complementing the technical/code rules in other notes.

---

## The Core: How Users Actually Behave (3 Immutable Facts)

These override every assumption about user behavior:

1. **We don't read, we scan.** Users skip most text, hunting for things that match their task. Pages that assume careful reading fail.
2. **We don't make optimal choices, we satisfice.** Users pick the first reasonable-looking option — not the best one. Design so the first reasonable option IS the right one.
3. **We don't figure out how things work, we muddle through.** Users rarely read instructions or build mental models. If they can muddle through successfully, it works. Wrong mental models cause real damage.

---

## Krug's Three Laws

### Law 1: "Don't make me think!"
Scan the page for **question marks** — anything that makes users pause:

| Problem | Examples |
|---------|----------|
| Unclear names | Cute/clever/marketing-speak labels instead of obvious ones |
| Ambiguous clickability | Links/buttons that don't look clickable; non-links that look clickable |
| Confusing choices | Options that require thought to distinguish (e.g., "RFPs" vs "Fixed-Price") |
| Mental chatter | Form fields/labels/flows that make users ask "What do they mean by…?" |

**Standard:** Page should be **self-evident** (no thought required) or at minimum **self-explanatory** (tiny amount of thought). If neither → fails.

> *"If you can't make something self-evident, you at least need to make it self-explanatory."*

### Law 2: "It doesn't matter how many times I click, as long as each click is a mindless, unambiguous choice."
Check all navigation paths:

- Are choices **mindless** (obvious what you'll get) or do they require thought?
- Is the **scent of information** strong? (Do links clearly signal their destination?)
- When choices are hard, is there **just-in-time guidance** — brief, timely, unavoidable?

### Law 3: "Get rid of half the words on each page, then get rid of half of what's left."
Evaluate text for:

| Problem | Description |
|---------|-------------|
| Happy talk | Intro/welcome text that says nothing ("Welcome to our amazing…") |
| Instruction bloat | Long instruction blocks instead of self-explanatory design |
| Needless words | Paragraphs that could be cut in half without losing meaning |
| Wall of words | Long unbroken paragraphs instead of short ones |
| Missing bullet lists | Series of items written as paragraphs that should be bulleted |

---

## The Trunk Test (Drop Test)

Imagine being dropped blindfolded on a random page. Answer these **instantly** (no reading, no exploring):

| Question | What to Look For | Score |
|----------|-----------------|-------|
| What site is this? | Site ID/logo — top-left, distinctive, recognizable at any size | ✅ / ⚠️ / ❌ |
| What page am I on? | Page name — prominent, in the right place, matches what you clicked | ✅ / ⚠️ / ❌ |
| What are the major sections? | Primary navigation — visible, consistent, well-labeled | ✅ / ⚠️ / ❌ |
| What are my options at this level? | Local/secondary navigation — clear subsections | ✅ / ⚠️ / ❌ |
| Where am I in the scheme of things? | "You are here" indicators — highlighted nav items, breadcrumbs | ✅ / ⚠️ / ❌ |
| How can I search? | Search box — visible, standard pattern (box + button + "Search") | ✅ / ⚠️ / ❌ |

---

## Billboard Design Test

Users scan pages like billboards going by at 60 mph. Evaluate each principle:

| Principle | What to Check |
|-----------|--------------|
| **Conventions** | Follows standard web conventions for layout, navigation, element appearance? |
| **Visual hierarchy** | Important things more prominent? Related things grouped? Nesting clear? |
| **Clearly defined areas** | Can you play "$25,000 Pyramid" — point at any area and say what it is? |
| **Obvious clickability** | Can you instantly tell what's clickable and what's not? |
| **Noise level** | Shouting (everything competing)? Disorganization (no grid)? Clutter (too much stuff)? |
| **Scannable text** | Plenty of headings? Short paragraphs? Bullet lists? Key terms bolded? |
| **Heading hierarchy** | Clear visual distinction between heading levels? Each heading closer to its section than to the previous one? |

---

## Home Page Audit (The Big Bang)

First impressions are disproportionately critical. Must answer **at a glance**:

### The Five Questions
1. **What is this?** — Is the site's purpose immediately clear?
2. **What can I do here?** — Are available actions/content obvious?
3. **What do they have here?** — Is the offering visible?
4. **Why should I be here and not somewhere else?** — Is differentiation clear?
5. **Where do I start?** — Obvious starting point for search, browse, sign in, or primary task?

### Key Home Page Elements

| Element | Standard |
|---------|----------|
| **Tagline** | 6–8 words, informative, conveys differentiation — NOT a vague motto |
| **Welcome blurb** | Terse, prominent site description (not marketing fluff) |
| **"Learn more" option** | Video or explainer for complex propositions |
| **Entry points** | Clear "where to start" for search, browse, and key tasks |
| **Promo balance** | Are promos overwhelming the core purpose? (Tragedy of the commons) |

---

## Navigation Design Audit

### Persistent Navigation Checklist
- [ ] Present on every page (except forms)?
- [ ] Contains all four required elements: **Site ID, Sections, Utilities, Search**?
- [ ] Consistent location and appearance throughout?

### Page Names
- [ ] Every page has one?
- [ ] Prominent and in the right place (framing the content area)?
- [ ] **Matches what the user clicked** to get there?

### "You Are Here" Indicators
- [ ] Current location highlighted in navigation?
- [ ] Stands out enough? (Multiple visual distinctions — not too subtle)

### Breadcrumbs
- [ ] At the top of the page?
- [ ] Uses ">" between levels?
- [ ] **Last item is bold and not a link?**

### Tabs
- [ ] Active tab visually connects with the content below?
- [ ] Different color/shade from inactive tabs?

---

## Mobile & Responsive Audit

| Check | What to Evaluate |
|-------|-----------------|
| Prioritization | Most-needed features close at hand? Everything else still reachable? |
| Affordances visible | Tap targets obvious? No hidden gestures? No reliance on hover? |
| Flat design tradeoffs | Has visual flattening removed useful affordances? |
| Performance | Signs of bloat that would hurt mobile load times? |
| Zooming allowed | Can users zoom if they need to? |
| Deep links | Do shared links go to the right page, not home? |
| Full site option | Is there a way to access the desktop version? |

---

## Goodwill — Trust Drains vs. Builders

### Goodwill Drains (depletes user trust)
- [ ] Hiding information users want (pricing, support phone, shipping costs)
- [ ] Punishing users for "wrong" input formatting (phone numbers, credit cards)
- [ ] Asking for unnecessary personal information
- [ ] Faux sincerity / corporate "shucking and jiving"
- [ ] Sizzle blocking the path (marketing photos in the way of actual content)
- [ ] Amateurish appearance

### Goodwill Builders (increases user trust)
- [ ] Main user tasks are obvious and easy to accomplish
- [ ] Upfront about costs, limitations, and shipping
- [ ] Saves user steps wherever possible
- [ ] Effort clearly put into quality
- [ ] FAQs are real, current, and candid — not marketing
- [ ] Graceful error recovery
- [ ] Apologizes when inconveniencing users

> *"The reservoir of goodwill is not bottomless."*

---

## Accessibility Quick Checks (Krug's Low-Hanging Fruit)

| Check | What to Look For |
|-------|-----------------|
| Text contrast | Sufficient contrast between text and background? No small low-contrast type? |
| Form labels | Labels outside fields (not floating inside)? |
| Text resizing | Does the page respond to browser text size changes? |
| Headings | Using semantic heading hierarchy (h1 → h2 → h3)? |
| **Link distinction** | **Visited vs unvisited links visually different?** *(unique to Krug)* |
| Keyboard navigation | Can all content be accessed via keyboard? |

---

## Audit Report Output Format

```markdown
# Krug UX Audit: [Site Name]
**URL:** [url]
**Date:** [date]
**Pages reviewed:** [list]

## Executive Summary
[2–3 sentence overall assessment]
[Overall grade: A/B/C/D/F with brief justification]

## Trunk Test Results
[Table with ✅/⚠️/❌ for each of the 6 questions]

## Krug's Laws Assessment
### Law 1: Don't Make Me Think
[Findings with specific page elements as examples]

### Law 2: Mindless Choices
[Findings with specific examples]

### Law 3: Omit Needless Words
[Findings with specific examples]

## Billboard Design
[Findings organized by the 7 principles]

## Navigation
[Findings: persistent nav, page names, "you are here", breadcrumbs, tabs]

## Home Page
[Five Questions assessment + element review]

## Mobile/Responsive
[If applicable]

## Courtesy & Goodwill
[Specific drains and builders identified]

## Accessibility
[Quick check results]

## Top 5 Issues (Prioritized)
1. [Most critical — fix first]
2. ...
3. ...
4. ...
5. ...

## Quick Wins
[Things fixable in under an hour]

## Recommendations
[Specific, actionable changes ordered by impact]
```

---

## Audit Principles (How to Write a Good Audit)

- **Be specific.** Every finding must reference a concrete element — not abstract theory.
- **Prioritize ruthlessly.** Fix the most serious problems first. Don't drown the report in minor issues.
- **No jargon without explanation.** Keep the audit readable to non-UX people.
- **Suggest, don't just criticize.** Every problem needs a practical fix suggestion.
- **Grade on real impact.** A beautiful site with confusing navigation is worse than an ugly site that's easy to use.

---

## Key Krug Quotes (Anchor Points for Any Audit)

| Quote | Use When |
|-------|----------|
| *"Don't make me think!"* | Anchor for any confusion finding |
| *"Clarity trumps consistency."* | When a convention should be broken for clarity |
| *"We don't read pages. We scan them."* | Text-heavy or wall-of-words issues |
| *"We don't make optimal choices. We satisfice."* | Navigation / choice architecture issues |
| *"We don't figure out how things work. We muddle through."* | Mental model / instruction issues |
| *"The reservoir of goodwill is not bottomless."* | Trust / friction issues |
| *"FOCUS RUTHLESSLY ON FIXING THE MOST SERIOUS PROBLEMS FIRST."* | Prioritization of findings |
| *"People won't use your Web site if they can't find their way around it."* | Navigation failures |
| *"If your audience is going to act like you're designing billboards, then design great billboards."* | Scanning/visual hierarchy |

---

## What Makes This Unique vs. Technical UX Rules

The Krug methodology is **behavioral** — it focuses on how users actually use sites, not code standards:

| Krug Approach | Technical Rules (notes 01–06) |
|--------------|-------------------------------|
| Trunk test — drop test to assess orientation | Breadcrumb implementation rules |
| "Satisficing" — users pick first good-enough option | Navigation item count limits |
| "Scent of information" — link clarity | Deep linking / URL structure |
| Happy talk / wall of words detection | Typography line length rules |
| Goodwill drain/builder model | Trust signals checklist |
| Billboard scan test | Visual hierarchy tokens |
| "$25K Pyramid" area clarity test | Z-index / layout structure |
| Tagline: 6–8 words, differentiating | Copy/content guidelines (none prior) |

These two approaches are **complementary** — technical rules ensure the code is correct; Krug ensures the experience works for real humans.
