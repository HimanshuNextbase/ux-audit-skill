# Headway UX Audit Checklist & Report Framework

Source: Headway (headway.io) — UX Audit: Create a Roadmap for Product Improvement (PDF)
Note: Duplicates from notes 01–10 filtered out — only unique content saved here.

---

## Pre-Audit Setup (Before Any Checklist)

Define the goal of the audit first. Pick from the question types below — don't try to answer all of them in one pass:

- Checking for accessibility issues
- Design consistency across the board
- Where do users get stuck
- Does our UX copy make sense
- Are users converting as expected

**Before you open a single screen:**
1. Unpack the personas affected and how they relate to the audit goals
2. Review any business goals or KPIs that might be affected
3. Watch recorded experience sessions or conduct interviews to get real observations before forming opinions

---

## Audit Checklist — 5 Categories

### 1. Content

Goal: familiar language, clear structure, scalable.

- [ ] Familiar words and phrases used instead of technical or system terms
- [ ] All questions directed to users are concise and friendly
- [ ] All abbreviations and acronyms are explained/deciphered
- [ ] CTAs and buttons are written with their context in mind
- [ ] All messaging (including error messages) uses the brand's Tone & Voice style
- [ ] Information on the page follows the F or Z pattern and is easily scannable
- [ ] Content is written in common language and easily understood

---

### 2. Design & Typography

#### Forms & Text Fields

- [ ] Form intent is clearly communicated
- [ ] Forms are grouped by intent and context (not just by field type)
- [ ] Tap targets and padding between form elements are large enough for easy mobile selection
- [ ] Only the required number of fields are present — minimize whenever possible
- [ ] Text fields are sized to match the expected length of the input
- [ ] Placeholder clearly indicates what should go into the field
- [ ] Complex fields (date, time) reduce number of clicks as much as possible
- [ ] Long dropdown fields are avoided

#### Input & Buttons

- [ ] Button sizes are visually similar (consistent sizing system)
- [ ] Button hierarchy is clear (primary vs secondary vs tertiary)
- [ ] Grouped buttons clearly indicate which one is currently selected
- [ ] Radio buttons are used for single-select choices only
- [ ] Checkboxes are used for multi-select choices only
- [ ] Text links are visually different from body copy

#### Typography

- [ ] Font size/weight differs for various content types (heading vs body vs caption)
- [ ] Fonts used in text content are at least 14px
- [ ] Font styles on each page are limited to 3 or fewer
- [ ] Different font styles/families distinguish screen content from controls and navigation
- [ ] Uppercase used only for labels, headers, or acronyms
- [ ] No more than two different font families used
- [ ] Line length is around 45–75 characters for paragraphs and headings
- [ ] Capital letters are not overused
- [ ] Type hierarchy is standardized on every page/screen
- [ ] Type is readable at its smallest size

#### Visual Design

- [ ] Visual hierarchy leads users to the required action or most important information
- [ ] Related information is grouped together clearly
- [ ] Alert messages (snack bars, toasts, banners) are consistent and follow defined rules
- [ ] Primary actions differ visually from secondary actions
- [ ] Confirmation on form submission is visually distinct
- [ ] Hierarchy, content, or functionality is conveyed through more than just color
- [ ] Content controls stand out from background elements
- [ ] No more than 3 primary colors on any page
- [ ] Interactive elements follow standard web conventions — don't deviate without reason
- [ ] Data is demonstrated by proximity and alignment (grouping like items together)
- [ ] On any page, the user can see the relevant information without scrolling
- [ ] Information is arranged according to the F or Z pattern

#### Iconography, Images & Illustration

- [ ] No text embedded in any illustration or image
- [ ] Icons reflect the element they represent
- [ ] Images are highest quality and optimized for the target platform
- [ ] Icon set is consistent and does not mix styles
- [ ] Illustrations look like they belong to this product and convey brand ideas

#### System

- [ ] All clickable elements have a hover state indicating they are clickable
- [ ] If anything takes longer than 3 seconds, the page provides a loader **with a hint showing the remaining time** (not just a spinner)

---

### 3. Navigation & Structure

Goal: users can navigate easily and find what they need without friction.

- [ ] When users complete an action, the system doesn't require additional steps like "submit" or "apply" (auto-save / implicit confirmation)
- [ ] Navigation is in familiar locations based on the product's platform conventions
- [ ] The current page is clearly communicated and visible
- [ ] Company's physical address is displayed
- [ ] Support number or email is easily accessible and/or in the footer
- [ ] About page is easily accessible
- [ ] Menu and page terms are user-friendly and follow conventional names
- [ ] Navigation is consistent across every page/screen
- [ ] There is room for future navigation elements (design for growth)
- [ ] Users can navigate back and forth on any page/screen
- [ ] Search bar is present and visible on every page if search is a large product component
- [ ] Footer clearly indicates secondary links, social networks, and includes a complete site map
- [ ] **Progress indicator is clearly visible for multi-step workflows** — shows where the user is AND how much is left to go
- [ ] Product navigation is similar to navigation of comparable products in the same category
- [ ] Main navigation items are always visible and not hidden behind a menu button (except on mobile)
- [ ] All information a user needs at a particular point is visually available and **pre-populated**
- [ ] Logo in the header is displayed on every page and leads to the main page

---

### 4. Accessibility & Compliance

#### General

- [ ] Product is compatible with most web browsers
- [ ] Main text contrast is not less than WCAG AA (4.5:1)
- [ ] Active objects are visually clickable; inactive ones don't change the mouse pointer or respond when clicked
- [ ] SSL certificate is present on the website
- [ ] Hints help the user *perform* an action — they don't merely *explain* it
- [ ] Empty states clearly define what action must be done (not just "nothing here")
- [ ] **Product does some work for users:** offers ready currency signs, country mobile codes, divides numbers into threes (9,999,999)
- [ ] When a button is not active, the product tells the user *why* it's not
- [ ] Users can skip or start onboarding from the beginning

#### Errors & Alerts

- [ ] After an error, users can easily restart the process **or** go to the error point **without losing their progress**
- [ ] Error pages 404 and 503 tell the user what to do next (not just "page not found")
- [ ] Alert messages stand out visually from the rest of the page/screen design

#### Permissions

- [ ] Option to refuse cookies
- [ ] Location detection is always done with explicit user permission
- [ ] When accessing users' contacts, product asks for permission
- [ ] If the product costs a fee, prices are clearly shown and no hidden fees exist

#### Forms & Auth (Accessibility Angle)

- [ ] Real-time validation for complex fields (password, username) — user doesn't find out they did something wrong only after submit
- [ ] Text fields are not case-sensitive when applicable
- [ ] Text fields contain default values when applicable
- [ ] Names/labels of fields and the text inside are visually different
- [ ] Button remains inactive in forms with 2+ fields until all required fields are filled
- [ ] Forms leverage browser auto-fill
- [ ] The text field's name/label is always visible in the filled state (not replaced by value)
- [ ] Input of incorrect data type is blocked at the field (e.g., numbers blocked in name field)
- [ ] Users can sign in with social networks
- [ ] Login page has a "create account" option
- [ ] Login/sign-in heading is visible
- [ ] Forgot password is present on the login screen
- [ ] Entered password can be revealed using an eye button
- [ ] Browser password generation is supported
- [ ] Product logo is on the login page
- [ ] "Remember me" checkbox is present on login screens
- [ ] **Password requirements are communicated BEFORE entering a password** (not revealed after a failed attempt)
- [ ] "I agree" to terms and conditions is located next to the registration button
- [ ] Password confirmation field shows whether passwords match in real time
- [ ] Clickable element sizes and distances between them prevent accidental clicks
- [ ] Users can tab through forms and the tab order makes sense

#### Data & Account

- [ ] Users can easily edit information about themselves

#### Help & Support

- [ ] Users can resume work where they left off after receiving help — help page opens in a new tab
- [ ] Users can easily find where to delete their account or cancel a subscription
- [ ] FAQ page is divided into categories and is searchable

---

### 5. Mobile Responsiveness

- [ ] Main body text is 16px or larger
- [ ] Site is responsive to both horizontal and vertical orientation
- [ ] Buttons are large enough to be selected
- [ ] Clickable elements have enough padding around them
- [ ] The corresponding keyboard type opens based on the data input field (numeric, email, etc.)
- [ ] Active and important elements can be reached with one hand
- [ ] Access to phone functions is requested only in context and when needed
- [ ] Product image occupies 60–90% of the screen (e-commerce)
- [ ] Photos in galleries are swipeable
- [ ] Text on images is easy to read
- [ ] **Autocorrect does not activate while the user is entering data in form fields**
- [ ] The design matches the product screenshots in the app stores

---

## Audit Tools (New — Not in Prior Notes)

| Tool | What It Does |
|------|-------------|
| **Contrast** (usecontrast.com) | Figma plugin + native desktop app — checks contrast on live sites without needing screenshots |
| **Stark** | All-in-one accessibility: color contrast + vision simulation + focus order checking |
| **Coblis** (color-blindness.com/coblis) | Upload an image, simulate different color blindness types — for validating palette decisions |

*(Lighthouse and WAVE already documented in note 08)*

---

## Audit Report Structure (5 Sections)

### 1. Executive Summary
High-level summary of the overall experience + what was found + high-level plan to address it. Keep it brief enough for stakeholders who won't read the rest.

### 2. Key Findings
3–5 findings from the audit. Each must connect back to the executive summary and stay at a high enough level for non-design stakeholders.

### 3. Interview Quotes
Pull 2–4 quotes from user sessions or observation recordings to capture real sentiment. If producing a video report: cut footage into a montage. This grounds recommendations in the user's actual voice, not just the auditor's opinion.

### 4. Major Callouts
Specific issues that need to be called out directly. Each callout must include:
- A **screenshot** of the issue
- An **explainer** of why it's a problem
- A **plan** for how it will be addressed

Example callout: "Color contrast isn't meeting target rating across the product" or "8 different button styles exist with no clear hierarchy."

### 5. Roadmap
Map every finding to next steps. Items fall into one of:
- **Sprint backlog** — addressable in the current or next sprint
- **Larger conversation** — requires stakeholder alignment before action

The roadmap is what transforms an audit from a report into a plan of attack.

---

## Cadence Recommendation

- **Micro audits** added to every sprint cadence — catch issues as they ship
- **Full audits** performed periodically or before major releases
- Regular audits increase satisfaction and loyalty from both team members and customers
