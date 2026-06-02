# Real-App UX Pattern Library

Source: UXSnaps.com — bite-sized breakdowns from billion-dollar apps.
Use this during the PATTERN UPGRADE advisory step. When you identify a gap, name the specific app and pattern, not just the principle.

---

## HOW TO USE THIS FILE

This file is **internal agent knowledge** — it informs the quality of your recommendations. It is NOT a reference list to copy into the report.

During **Step 3.5 — PATTERN UPGRADE**:
1. Match the product under audit to the closest category below
2. For each gap found, find the named pattern that addresses it
3. Use the pattern to write a recommendation specific to THIS product's exact problem — do not mention the source app unless it appears briefly in a "Reference:" line at the end

**The goal:** go from vague ("consider progressive disclosure") to precise ("show the total first, then the breakdown — users currently see 12 line items before they see a summary, which forces mental arithmetic before they understand their position").

The pattern tells you WHAT to suggest. Your job is to explain WHY it applies to this specific product and HOW to implement it here.

**When a reference app DOES belong in the recommendation:**
If the pattern is genuinely surprising or non-obvious, you may add one sentence at the END of the recommendation as credibility: "This pattern is proven — Coinbase, Airbnb, and Duolingo all use it in their core flows." Don't make it the headline, but do use it as a closing credibility signal when the recommendation is bold or asks for significant design change. The client needs to know the fix isn't speculation.

---

## CATEGORY: DASHBOARDS (Mobile & Desktop)

### ElevenLabs — Minimal Yet Powerful Dashboard (Desktop)

| Pattern | What the app does | Principle | When to apply |
|---------|------------------|-----------|---------------|
| **Visual hierarchy through spacing** | Separates greetings, features, voice library, actions with spacing + card containers — users scan each zone without confusion | Visual Hierarchy — spatial separation lets users process grouped info without reading everything | Any dashboard with 3+ distinct content zones |
| **Action-oriented cards with labels + icons** | "Create or clone a voice" section shows clear buttons with both labels and icons — reduces decision fatigue at the action point | Hick's Law — fewer, clearer choices reduce cognitive effort | Onboarding screens and dashboards where users need direction to their first action |
| **Familiar sidebar navigation** | Left sidebar vertical menu matches common SaaS layouts — no learning curve | Jakob's Law — users bring expectations from other apps | Desktop SaaS applications with significant dwell time |
| **Personalized time-aware greeting** | "Good morning, Sam" — uses name + time of day for emotional connection | Emotional Design / Personalization — contextual greetings increase retention | Dashboard home screens for tools where retention matters |
| **Subtle interactive support button** | "Ask El" button uses brand gradient — noticeable but not distracting | Microinteractions / Feedback — visual affordance signals interactivity before the user acts | Persistent help/support elements that must be visible but not dominant |

### MyFitnessPal — Fitness Dashboard (Mobile)

| Pattern | What the app does | Principle | When to apply |
|---------|------------------|-----------|---------------|
| **Circular progress ring for primary metric** | Calorie ring shows goal – food + exercise = remaining with color-coded progress — instantly scannable | Visual Encoding — circular fills map to "filling up" a quota, matching mental model | Any metric with a daily/periodic goal and a "remaining" state |
| **KPIs with icon + bold number pairing** | Calories, food, exercise stats use bold typography + colorful icons — two retrieval paths (verbal + visual) | Dual Coding — text + icon creates two memory paths | KPI sections in any dashboard |
| **Editable dashboard** | "Edit" button lets users reorder what data is visible | User Control / Personalization — satisfies diverse needs without complex config | Data-heavy dashboards with 5+ metric types |
| **Barcode scanner in primary nav** | Search + barcode scanner in bottom nav tab — core daily action is one tap away | Fitts's Law — high-frequency actions in thumb-accessible nav reduces effort | Apps where a core action is repeated daily |
| **Dual-purpose progress cards** | Step/exercise cards show summary AND act as navigation entry points for deeper actions | Progressive Disclosure / Dual-Purpose UI — cards serve as both summary and trigger | Activity or metric cards on dashboards |

### TimeSpent — Activity Dashboard (Mobile)

| Pattern | What the app does | Principle | When to apply |
|---------|------------------|-----------|---------------|
| **Horizontal strip calendar** | Compact date strip saves space, highlights today with full-sun icon + contrast | Visual Hierarchy / Affordance — contrast + iconography direct attention to today | Mobile apps needing date navigation without a full calendar modal |
| **Contextual feature promotion card** | "Get notified, stay inspired" introduces notifications in the screen where notifications are most relevant — feels helpful not interruptive | Contextual Design / Autonomy — feature promotions embedded in context feel helpful | Promoting notifications, widgets, or companion features |
| **Floating bottom navigation** | Floating nav creates visual separation from content — activities and stats take visual focus | Minimalism / Figure-Ground — floating nav creates hierarchy between content and navigation | Mobile apps with content-heavy screens where breathing room matters |
| **Calm whitespace + restrained palette** | Ample whitespace, 2–3 color palette, consistent icon style — calm, intentional rhythm | Minimalism / Attentional Direction — palette restraint focuses the eye | Wellness, productivity, or focus apps |
| **Consistent action-oriented activity cards** | Each card is touch-friendly, consistent, with icon + label guiding toward interaction | Fitts's Law / Consistency — uniform card design sets expectations | Any grid or list of actionable items on mobile |

### Coinbase — Home Dashboard (Desktop)

| Pattern | What the app does | Principle | When to apply |
|---------|------------------|-----------|---------------|
| **Primary KPI + trend chart at the top** | Total balance in large type + small line chart — user immediately sees value + trajectory | Visual Hierarchy / Glanceability — most critical metric has highest visual weight | Financial, analytics, or any dashboard where the primary KPI and trajectory are the user's first question |
| **Progressive breakdown below main metric** | Total → crypto vs. cash split below, with contextual APY messages | Progressive Disclosure — secondary info in logical sequence after the summary | Any dashboard with a primary summary metric |
| **Task-ordered action panel** | Right-side actions ordered: buy → select payment → fund → manage — natural task sequence | Visual Storytelling / Task Flow — actions in natural order create implicit workflow | Multi-step transactional dashboards with a primary workflow sequence |
| **Non-interruptive "For You" cards** | Personalized cards in a predictable carousel — features + promotions that feel helpful, not intrusive | Consistent / Non-Interruptive Personalization — personalized content in predictable container | Financial or feature-rich apps that need to surface content without competing with primary tasks |
| **Data table with favorites + mini charts** | Asset price table with strong hierarchy, spacing, sortability, mini charts, and favoriting | Data Table UX / Microinteractions — hierarchy + spacing makes scanning effortless | Any data table with 10+ rows where users need to locate items quickly |

### Alma — Health Dashboard (Mobile)

| Pattern | What the app does | Principle | When to apply |
|---------|------------------|-----------|---------------|
| **Hero card = metric + insight + action** | Score ring + bold number + one-line food insight answers: "What should I do today?" — actionable, not just informational | Actionable Data Design — metric paired with insight and implied next step | Health, wellness, or performance apps where the goal is behavior change |
| **Contextual widget prompt** | Widget install prompt framed as "quicker access to your progress" — user's benefit, easy to dismiss | Non-Interruptive Growth — growth feature framed as user benefit, not a promotion | Any time you need to promote a feature requiring user action |
| **Circular fills for nutritional KPIs** | Calories, protein, carbs, fat as filled circles with soft color coding — no raw numbers required | Visual Encoding / Metaphor — circular fills map to "how much of goal is filled" | Dashboards tracking progress toward multiple daily goals |
| **Subtle gamification in the header** | Small vegetable icon streak count in the header — habit reinforcement without a full widget | Subtle Gamification — lightweight indicator reinforces habit while staying non-distracting | Habit-forming apps where engagement loops matter |
| **FAB for primary high-frequency action** | "Add food" sits as a large central FAB within thumb reach | Fitts's Law / Task Hierarchy — most frequent action is most physically accessible | Mobile apps with a high-frequency primary action |

### Duolingo — Learning Dashboard (Mobile)

| Pattern | What the app does | Principle | When to apply |
|---------|------------------|-----------|---------------|
| **Visual learning path** | Playful path shows exactly where to start and what's next — removes sequence ambiguity | Linear Path Design — visual path removes ambiguity, reduces cognitive load | Sequential learning or skill-building products |
| **FOMO gate on social feature** | "Unlock Leaderboards at 9 lessons" — social feature gated behind an achievable milestone | Gamification / Loss Aversion — concrete milestone creates goal to work toward | Learning or habit apps with social features |
| **Daily XP quest system** | Daily mini-quests give small wins — builds habit without pressure | Variable Reward Schedule — daily quests create recurring pull to open the app | Habit-forming apps; implement daily quests with low completion thresholds |
| **Minimal freemium upsell card** | "Try Super for free" = one benefit + one visual + one CTA — no walls of text | Value Clarity / Minimalism — premium upsell communicates one thing clearly | In-product premium upsell on any freemium platform |
| **Playful visual language reduces anxiety** | Mascot, rounded shapes, bright colors — turns learning into play | Emotional Design / Anxiety Reduction — playful visuals signal that mistakes are safe | Educational or self-improvement apps |

---

## CATEGORY: CHAT / MESSAGING

### WhatsApp — Multi-Modal Communication (Mobile)

| Pattern | What the app does | Principle | When to apply |
|---------|------------------|-----------|---------------|
| **Contextual icon grouping** | Call/video icons at top near contact info; camera/voice at bottom near input — icons live near the content they relate to | Spatial Contextual Design / Affordance — proximity maps action to context | Any interface with multiple action types (communication, media, navigation) |
| **Icon-only message status** | Single tick / double tick / blue tick — shows sent/delivered/read without text labels | Feedback / Learnability — compact icon system communicates state once learned | Asynchronous communication where delivery confirmation matters |
| **Subtle emoji/star reactions** | Reactions add personality without overwhelming — small enough not to distract | Microinteractions / Delight — small emotional touches humanize communication | Messaging, collaboration, or social apps where emotional expression is contextual |
| **Progressive information density by content type** | Links get preview cards, calls get duration/status, text stays clean — visual weight matches information weight | Progressive Disclosure — reveal more detail only when content type warrants it | Any feed with heterogeneous content types |
| **Strict visual hierarchy in dense content** | Messages, timestamps, reactions, call logs all coexist — everything has correct visual weight | Visual Hierarchy — deliberate typographic scale guides eye through complexity | High-density screens with many element types |

---

## CATEGORY: LANDING PAGES / MARKETING

### n8n — High-Impact Technical Landing Page (Desktop)

| Pattern | What the app does | Principle | When to apply |
|---------|------------------|-----------|---------------|
| **Bold hero metaphor over product screenshot** | Lightning bolt with warm glow on dark background — communicates power + speed before copy is read | Visual Contrast / First Impressions — high-contrast imagery sets brand character instantly | Developer tools, automation platforms; use a bold visual metaphor rather than a product screenshot |
| **Headline: who + what + why in one sentence** | Hero answers: who this is for + what it does + why it matters — all in the headline | Inverted Pyramid Writing — lead with essential message, support text expands for engaged readers | Any product landing page — hero headline should answer all three questions |
| **Primary + secondary CTA pair** | "Get started for free" (high contrast) + "Talk to sales" (lower prominence) — two segments, no choice paralysis | CTA Hierarchy / Hick's Law — primary-secondary pair serves two audiences without splitting attention | SaaS landing pages with both PLG and enterprise GTM motions |
| **Role-based use-case tabs** | IT Ops / Sec Ops / Dev Ops / etc. tabs — each persona self-selects into relevant value | Persona-Based Navigation — role tabs let product feel relevant to multiple audiences simultaneously | Platform products with 3+ distinct user personas |
| **Audience-matched social proof** | GitHub stars as credibility signal — matches what technical buyers trust | Social Proof / Audience-Matched Credibility — use the proof your specific audience trusts | Developer and open-source products — use GitHub stars, not generic star ratings |

### TravelPerk — Trust-First Landing Page (Mobile)

| Pattern | What the app does | Principle | When to apply |
|---------|------------------|-----------|---------------|
| **Authentic in-hand photography** | Real hand holding phone — grounds the design in reality, activates mental simulation of using it | Real-World Match / Mental Simulation — authentic photography makes product relatable before a word is read | Consumer mobile app landing pages |
| **Partial UI reveal around device** | Floating cards and status badges around the phone — teases the interface without overwhelming | Storytelling / Curiosity Gap — partial reveal sparks curiosity about full experience | Mobile app landing pages where UI polish is a differentiator; show 2–3 floating elements |
| **6–8 word punchy headline** | "Travel for work made simpler and smarter" — strong verb, minimal words, instant recall | UX Writing / Cognitive Ease — short rhythmic headlines reduce processing and increase recall | Any landing page; hero headline should be 6–8 words max |
| **Highest-contrast color for CTA** | Bold neon CTA is the highest-contrast element on screen — eye finds it even while scanning | CTA Design / Visual Flow — high-chroma CTA creates a visual anchor for rapid scanning | Hero sections on any landing page |
| **Logo strip + rating below hero** | Partner logos + star rating immediately below headline — credibility before the user scrolls | Social Proof / Trust Hierarchy — third-party validation placed in first viewport answers "can I trust this?" | Any B2B landing page or consumer app page |

---

## CATEGORY: SEARCH / MARKETPLACE / DISCOVERY

### Airbnb — Exploration by Design (Mobile)

| Pattern | What the app does | Principle | When to apply |
|---------|------------------|-----------|---------------|
| **"Guest Favorite" badge reduces decision load** | Single badge on listing cards signals high-rated reliability — no need to read reviews to filter quality | Hick's Law — curating a top-tier label reduces choice complexity | Marketplace and search results where quality variance is high |
| **Prominent search bar as primary CTA** | Search bar at the top is the first interactive element — first in visual and motor path | Fitts's Law / Affordance — large, top-placed search minimizes time and motor effort | Any search-driven marketplace or content discovery app |
| **Total price instead of nightly rate** | Shows total cost for the stay, not per-night — eliminates mental arithmetic | Cognitive Load Reduction / Transparency — eliminating required math reduces friction in decision-making | Any booking platform where trip length varies |
| **"Prices include all fees" tag** | Small tag on listing cards preempts hidden-cost anxiety — biggest frustration in travel | Clarity / Cognitive Ease — removing anticipated uncertainty at point of scanning prevents drop-off | Any marketplace with variable pricing, fees, or taxes |
| **Curated destinations over blank search prompt** | Shows inspiring destinations before asking "where do you want to go?" — foot-in-the-door technique | Foot-in-the-Door / Invitation Over Pressure — exploration before intent reduces initial friction | Discovery apps where users may not have a specific destination in mind |

### Medium — Content-First Discovery (Mobile)

| Pattern | What the app does | Principle | When to apply |
|---------|------------------|-----------|---------------|
| **Algorithm vs. curated tabs (user chooses)** | For You / Following tabs — user controls whether they see algorithmic or curated feed | User Control / Locus of Control — explicit agency over algorithm reduces distrust | Content apps with both subscription-following and algorithm-driven discovery |
| **Premium content icon (yellow) — single color signal** | Yellow icon flags premium content across all surfaces — users understand value tier immediately | Visual Hierarchy / Gestalt — distinctive icon color creates pre-attentive pop | Freemium content products; one consistent icon or color signals premium throughout |
| **Monochrome base palette — color reserved for key signals** | Almost entirely black/white/gray — green badge and FAB stand out dramatically | Color Sparsity / Figure-Ground — color is most effective when surrounding content is neutral | Content-heavy apps, reading platforms, news apps |
| **"Not interested" dismiss on feed items** | Minus button trains the algorithm without preference settings — implicit feedback | Implicit Personalization — lightweight dismiss collects preference signal while keeping UI clean | Algorithmic feeds of any kind |
| **Content-first layout — interface recedes** | Minimal author info, clean typography, subtle metrics — design disappears so content is prominent | Content-First Design / Subordinate Chrome — interface elements recede to give content maximum prominence | Reading, content discovery, and editorial apps |

---

## CATEGORY: PROFILE / ACCOUNT

### Duolingo — Profile Design (Mobile)

| Pattern | What the app does | Principle | When to apply |
|---------|------------------|-----------|---------------|
| **Motivational empty state with illustration** | "Following" section shows friendly illustration + motivation to connect — blank state becomes opportunity | Empty State Design — blank states should teach, motivate, or guide | Any social section that starts empty |
| **Shareable achievement cards** | "Add Duolingo score to LinkedIn" — benefits user (validates achievement) + brand (social proof) | Social Proof / Viral Loop — user-initiated sharing generates authentic social proof at low cost | Apps where users develop measurable skills or hit milestones |
| **2–3 key metrics with brand-consistent icons** | Streaks, XP, league badges — key stats styled with brand iconography | Information Architecture / Brand Consistency — 2–3 key metrics with brand iconography keeps data simple and recognizable | Learning, fitness, or productivity profile pages; display 3–5 metrics max |
| **Grouped social actions** | "Add friends" block groups find + invite together — reduces search time | Gestalt Proximity — related actions grouped together reduce mental effort | Profile pages with social features; create discrete action groups |
| **Bright colors + simple layout = broad accessibility** | Large tap targets, welcoming avatar, approachable color — friendly across all ages | Inclusive Design / Aesthetic Accessibility — simple layout + vibrant color supports diverse users | Consumer apps with broad demographic reach |

---

## CATEGORY: TRANSPORTATION / BOOKING

### Tesla Robotaxi — Booking Dashboard (Mobile)

| Pattern | What the app does | Principle | When to apply |
|---------|------------------|-----------|---------------|
| **Live availability before any action** | "Ride can arrive in 12 min" shown directly below search bar — sets expectation before user commits | System Status Visibility (Nielsen #1) — proactively surface key operational info at the entry point | High-intent transactional screens (booking, checkout) where availability uncertainty is a barrier |
| **Search + category shortcuts side-by-side** | Search bar dominates, but Bars/Food/Shopping shortcuts sit below — serves both directed and exploratory users | Dual Navigation — accommodating directed and exploratory navigation simultaneously | Location-based apps and marketplaces where users arrive with varying intent clarity |
| **Minimal recent locations with distance** | Recent places: name + address + distance — no extra metadata, distance helps quick decision | Recognition Over Recall / Minimalism — recent history without overload | Navigation or booking apps where repeat use is expected |
| **Accessibility as first-class section** | Accessibility features visible at the primary level — not buried in settings | Inclusive Design / Transparent Communication — accessibility discoverable at decision point | Transportation, healthcare, and public-service apps |
| **Dead-end prevention with alternative options** | When service unavailable, direct buttons to partner services appear instead of just "not available" | Error Recovery — pair every limitation with a concrete next step | Any product with coverage gaps, out-of-stock states, or feature limitations |

---

## CATEGORY: AI / GENERATIVE TOOLS

### v0 — AI Website Builder (Desktop)

| Pattern | What the app does | Principle | When to apply |
|---------|------------------|-----------|---------------|
| **Prompt input as the hero element** | Large centered input field is the dominant element — start the core action instantly with no extra clicks | Affordance — design communicates function (type here to begin) | Any tool whose entire value is a single primary action (search, compose, generate) |
| **Quick-start action pills for paralyzed users** | 3–6 pill-shaped buttons with common task types below the prompt | Contextual Design — suggestions match most frequent user intents | Empty states or prompt interfaces where users may feel paralyzed by open-ended input |
| **Community creations as social proof** | "From the Community" section shows real projects built by users | Social Proof — seeing what others built validates the tool and lowers psychological barrier | Generative or creative tools where demonstrating output quality is the best marketing |
| **Intentional whitespace around the prompt** | Generous spacing draws the eye to the prompt and nothing else | Whitespace / Visual Breathing Room — negative space directs attention | Hero sections and any screen with one primary CTA |
| **Small "New" badge for feature announcements** | Small tag above the heading introduces updates without interrupting the primary experience | Minimalism — feature announcements additive, not distracting | Announcing minor updates on an active screen; use badge/tag, not a modal |

---

## CROSS-CUTTING PRINCIPLES INDEX

Quick lookup: which app demonstrates each principle best.

| Principle | Best example | Pattern name |
|-----------|-------------|-------------|
| **Hick's Law** (reduce choices) | Airbnb + ElevenLabs | "Guest Favorite" badge / Action-oriented cards |
| **Progressive Disclosure** | Coinbase | Total → breakdown → contextual info |
| **Visual Hierarchy** | MyFitnessPal + Coinbase | KPI pairing / Primary metric placement |
| **Social Proof** | n8n + Duolingo + v0 | GitHub stars / Achievement sharing / Community creations |
| **Gamification** | Duolingo + Alma | Daily XP quests / Streak header indicator |
| **Empty States** | Duolingo Profile | Motivational illustration + call-to-action |
| **CTA Design** | TravelPerk + n8n | Neon high-contrast CTA / Primary-secondary pair |
| **Microinteractions** | WhatsApp + ElevenLabs | Tick system / Gradient support button |
| **Contextual Promotion** | Alma + Duolingo | Widget prompt as user benefit / Minimal upsell card |
| **Content-First** | Medium | Design recedes; content is hero |
| **Personalization** | ElevenLabs + MyFitnessPal | Time-aware greeting / Editable dashboard |
| **Cognitive Load Reduction** | Airbnb | Total price / "Prices include all fees" tag |
| **Error Recovery** | Tesla Robotaxi | Partner alternatives when service unavailable |
| **Inclusive Design** | Duolingo + Tesla Robotaxi | Accessible layout / Accessibility as first-class feature |
| **Fitts's Law** | MyFitnessPal + Alma | Barcode in nav / FAB for primary action |
| **Foot-in-the-Door** | Airbnb | Curated destinations before the blank search |
| **Loss Aversion / FOMO** | Duolingo | Social feature locked behind 9 lessons |
| **Emotional Design** | Duolingo + ElevenLabs | Playful mascot + color / Personalized greeting |
| **Implicit Feedback** | Medium | "Not interested" dismiss trains algorithm |
| **Trust Hierarchy** | TravelPerk | Logo strip + star rating in first viewport |
