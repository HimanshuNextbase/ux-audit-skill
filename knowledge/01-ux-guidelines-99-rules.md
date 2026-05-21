# 99 UX Guidelines (from ui-ux-pro-max-skill)

---

## Navigation (6 rules)

| # | Issue | Platform | Do | Don't | Severity |
|---|-------|----------|----|-------|----------|
| 1 | Smooth Scroll | Web | `scroll-behavior: smooth` on html | Jump directly without transition | High |
| 2 | Sticky Navigation | Web | Add `padding-top` = nav height | Let nav overlap first section | Medium |
| 3 | Active State | All | Highlight active nav item with color/underline | No visual feedback on current location | Medium |
| 4 | Back Button | Mobile | Preserve navigation history properly | Break browser/app back button behavior | High |
| 5 | Deep Linking | All | Update URL on state/view changes | Static URLs for dynamic content | Medium |
| 6 | Breadcrumbs | Web | Use for sites with 3+ levels of depth | Use for flat single-level sites | Low |

---

## Animation (8 rules)

| # | Issue | Platform | Do | Don't | Severity |
|---|-------|----------|----|-------|----------|
| 7 | Excessive Motion | All | Animate 1–2 key elements per view max | Animate everything that moves | High |
| 8 | Duration Timing | All | Use 150–300ms for micro-interactions | Animations longer than 500ms for UI | Medium |
| 9 | Reduced Motion | All | Check `prefers-reduced-motion` media query | Ignore accessibility motion settings | High |
| 10 | Loading States | All | Use skeleton screens or spinners | Leave UI frozen with no feedback | High |
| 11 | Hover vs Tap | All | Use click/tap for primary interactions | Rely only on hover for important actions | High |
| 12 | Continuous Animation | All | Use for loading indicators only | Use for decorative elements | Medium |
| 13 | Transform Performance | Web | Use `transform` and `opacity` for animations | Animate width/height/top/left | Medium |
| 14 | Easing Functions | All | `ease-out` for entering, `ease-in` for exiting | Linear for UI transitions | Low |

---

## Layout (8 rules)

| # | Issue | Platform | Do | Don't | Severity |
|---|-------|----------|----|-------|----------|
| 15 | Z-Index Management | Web | Define z-index scale system (10, 20, 30, 50) | Use arbitrary large z-index values | High |
| 16 | Overflow Hidden | Web | Test all content fits within containers | Blindly apply overflow-hidden | Medium |
| 17 | Fixed Positioning | Web | Account for safe areas and other fixed elements | Stack multiple fixed elements carelessly | Medium |
| 18 | Stacking Context | Web | Understand what creates new stacking context | Expect z-index to work across contexts | Medium |
| 19 | Content Jumping | Web | Reserve space for async content | Let images/content push layout around | High |
| 20 | Viewport Units | Web | Use `dvh` or account for mobile browser chrome | Use `100vh` for full-screen mobile layouts | Medium |
| 21 | Container Width | Web | Limit max-width for text content (65–75ch) | Let text span full viewport width | Medium |

---

## Touch (6 rules)

| # | Issue | Platform | Do | Don't | Severity |
|---|-------|----------|----|-------|----------|
| 22 | Touch Target Size | Mobile | Minimum 44×44px touch targets | Tiny clickable areas | High |
| 23 | Touch Spacing | Mobile | Minimum 8px gap between touch targets | Tightly packed clickable elements | Medium |
| 24 | Gesture Conflicts | Mobile | Avoid horizontal swipe on main content | Override system gestures | Medium |
| 25 | Tap Delay | Mobile | Use `touch-action: manipulation` | Default mobile tap handling | Medium |
| 26 | Pull to Refresh | Mobile | Disable where not needed | Enable by default everywhere | Low |
| 27 | Haptic Feedback | Mobile | Use for confirmations and important actions | Overuse vibration feedback | Low |

---

## Interaction (8 rules)

| # | Issue | Platform | Do | Don't | Severity |
|---|-------|----------|----|-------|----------|
| 28 | Focus States | All | Visible focus rings on interactive elements | Remove focus outline without replacement | High |
| 29 | Hover States | Web | Change cursor + add subtle visual change | No hover feedback on clickable elements | Medium |
| 30 | Active States | All | Add pressed/active state visual change | No feedback during interaction | Medium |
| 31 | Disabled States | All | Reduce opacity + change cursor | Confuse disabled with normal state | Medium |
| 32 | Loading Buttons | All | Disable button + show loading state | Allow multiple clicks during processing | High |
| 33 | Error Feedback | All | Show clear error messages near problem | Silent failures with no feedback | High |
| 34 | Success Feedback | All | Show success message or visual change | No confirmation of completed action | Medium |
| 35 | Confirmation Dialogs | All | Confirm before delete/irreversible actions | Delete without confirmation | High |

---

## Accessibility (10 rules)

| # | Issue | Platform | Do | Don't | Severity |
|---|-------|----------|----|-------|----------|
| 36 | Color Contrast | All | Min 4.5:1 ratio for normal text | Low contrast text | High |
| 37 | Color Only | All | Use icons/text in addition to color | Red/green only for error/success | High |
| 38 | Alt Text | All | Descriptive alt text for meaningful images | Empty or missing alt attributes | High |
| 39 | Heading Hierarchy | Web | Sequential heading levels h1–h6 | Skip heading levels or misuse for styling | Medium |
| 40 | ARIA Labels | All | Add aria-label for icon-only buttons | Icon buttons without labels | High |
| 41 | Keyboard Navigation | Web | Tab order matches visual order | Keyboard traps or illogical tab order | High |
| 42 | Screen Reader | All | Use semantic HTML and ARIA properly | Div soup with no semantics | Medium |
| 43 | Form Labels | All | Use `<label>` with `for` attribute | Placeholder-only inputs | High |
| 44 | Error Messages | All | Use `aria-live` or `role=alert` for errors | Visual-only error indication | High |
| 45 | Skip Links | Web | Provide "skip to main content" link | No skip link on nav-heavy pages | Medium |

---

## Performance (8 rules)

| # | Issue | Platform | Do | Don't | Severity |
|---|-------|----------|----|-------|----------|
| 46 | Image Optimization | All | Use appropriate size and format (WebP) | Unoptimized full-size images | High |
| 47 | Lazy Loading | All | Lazy load below-fold images and content | Load everything upfront | Medium |
| 48 | Code Splitting | Web | Split code by route/feature | Single large bundle | Medium |
| 49 | Caching | Web | Set appropriate cache headers | No caching strategy | Medium |
| 50 | Font Loading | Web | Use `font-display: swap` or optional | Invisible text during font load | Medium |
| 51 | Third Party Scripts | Web | Load non-critical scripts async/defer | Synchronous third-party scripts | Medium |
| 52 | Bundle Size | Web | Monitor and minimize bundle size | Ignore bundle size growth | Medium |
| 53 | Render Blocking | Web | Inline critical CSS, defer non-critical | Large blocking CSS files | Medium |

---

## Forms (10 rules)

| # | Issue | Platform | Do | Don't | Severity |
|---|-------|----------|----|-------|----------|
| 54 | Input Labels | All | Always show label above or beside input | Placeholder as only label | High |
| 55 | Error Placement | All | Show error below related input | Single error message at top of form | Medium |
| 56 | Inline Validation | All | Validate on blur for most fields | Validate only on submit | Medium |
| 57 | Input Types | All | Use email, tel, number, url, etc. | `type="text"` for everything | Medium |
| 58 | Autofill Support | Web | Use `autocomplete` attribute properly | Block or ignore autofill | Medium |
| 59 | Required Indicators | All | Use asterisk or "(required)" text | No indication of required fields | Medium |
| 60 | Password Visibility | All | Toggle to show/hide password | No visibility toggle | Medium |
| 61 | Submit Feedback | All | Show loading then success/error state | No feedback after submit | High |
| 62 | Input Affordance | All | Use distinct input styling | Inputs that look like plain text | Medium |
| 63 | Mobile Keyboards | Mobile | Use `inputmode` attribute | Default keyboard for all inputs | Medium |

---

## Responsive (8 rules)

| # | Issue | Platform | Do | Don't | Severity |
|---|-------|----------|----|-------|----------|
| 64 | Mobile First | Web | Start with mobile styles, add breakpoints | Desktop-first causing mobile issues | Medium |
| 65 | Breakpoint Testing | Web | Test at 320, 375, 414, 768, 1024, 1440 | Only test on your device | Medium |
| 66 | Touch Friendly | Web | Increase touch targets on mobile | Same tiny buttons on mobile | High |
| 67 | Readable Font Size | All | Minimum 16px body text on mobile | Tiny text on mobile | High |
| 68 | Viewport Meta | Web | `width=device-width initial-scale=1` | Missing or incorrect viewport | High |
| 69 | Horizontal Scroll | Web | Ensure content fits viewport width | Content wider than viewport | High |
| 70 | Image Scaling | Web | Use `max-width: 100%` on images | Fixed width images overflow | Medium |
| 71 | Table Handling | Web | Use horizontal scroll or card layout | Wide tables breaking layout | Medium |

---

## Typography (5 rules)

| # | Issue | Platform | Do | Don't | Severity |
|---|-------|----------|----|-------|----------|
| 72 | Line Height | All | Use 1.5–1.75 for body text | Cramped or excessive line height | Medium |
| 73 | Line Length | Web | Limit to 65–75 characters per line | Full-width text on large screens | Medium |
| 74 | Font Size Scale | All | Consistent modular scale | Random font sizes | Medium |
| 75 | Font Loading | Web | Reserve space with fallback font | Layout shift when fonts load | Medium |
| 76 | Contrast Readability | All | Use darker text on light backgrounds | Gray text on gray background | High |
| 77 | Heading Clarity | All | Clear size/weight difference from body | Headings similar to body text | Medium |

---

## Feedback (6 rules)

| # | Issue | Platform | Do | Don't | Severity |
|---|-------|----------|----|-------|----------|
| 78 | Loading Indicators | All | Show spinner/skeleton for ops > 300ms | No feedback during loading | High |
| 79 | Empty States | All | Show helpful message and action | Blank empty screens | Medium |
| 80 | Error Recovery | All | Provide clear next steps | Error without recovery path | Medium |
| 81 | Progress Indicators | All | Step indicators or progress bar | No indication of progress | Medium |
| 82 | Toast Notifications | All | Auto-dismiss after 3–5 seconds | Toasts that never disappear | Medium |
| 83 | Confirmation Messages | All | Brief success message | Silent success | Medium |

---

## Content (3 rules)

| # | Issue | Platform | Do | Don't | Severity |
|---|-------|----------|----|-------|----------|
| 84 | Truncation | All | Truncate with ellipsis and expand option | Overflow or broken layout | Medium |
| 85 | Date Formatting | All | Use relative or locale-aware dates | Ambiguous date formats | Low |
| 86 | Number Formatting | All | Use thousand separators or abbreviations | Long unformatted numbers | Low |

---

## Specialized Rules

| # | Category | Issue | Platform | Do | Don't | Severity |
|---|----------|-------|----------|----|-------|----------|
| 88 | Onboarding | User Freedom | All | Provide Skip + Back buttons | Force linear unskippable tour | Medium |
| 89 | Search | Autocomplete | Web | Show predictions as user types | Require full type and enter | Medium |
| 90 | Search | No Results | Web | Show "No results" with suggestions | Blank screen | Medium |
| 91 | Data Entry | Bulk Actions | Web | Allow multi-select and bulk edit | Single row actions only | Low |
| 92 | AI Interaction | Disclaimer | All | Clearly label AI-generated content | Present AI as human | High |
| 93 | AI Interaction | Streaming | All | Stream text response token by token | Show loading spinner for 10s+ | Medium |
| 94 | Spatial UI | Gaze Hover | VisionOS | Scale/highlight element on look | Static element until pinch | High |
| 95 | Spatial UI | Depth Layering | VisionOS | Use glass material and z-offset | Flat opaque panels | Medium |
| 96 | Sustainability | Auto-Play Video | Web | Click-to-play or pause when off-screen | Auto-play high-res video loops | Medium |
| 97 | Sustainability | Asset Weight | Web | Compress and lazy load 3D models | Load 50MB textures | Medium |
| 98 | AI Interaction | Feedback Loop | All | Thumbs up/down or Regenerate | Static output only | Low |
| 99 | Accessibility | Motion Sensitivity | All | Respect `prefers-reduced-motion` | Force scroll effects | High |
