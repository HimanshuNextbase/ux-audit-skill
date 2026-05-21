# Source: ui-ux-pro-max-skill README

Repo: https://github.com/nextlevelbuilder/ui-ux-pro-max-skill
License: MIT
Description: An AI skill that provides design intelligence for building professional UI/UX across multiple platforms and frameworks.

## What's Included

- 67 UI Styles
- 161 Color Palettes (industry-specific, 1:1 with 161 product types)
- 57 Font Pairings (Google Fonts)
- 25 Chart Types
- 15 Tech Stacks
- 99 UX Guidelines
- 161 Reasoning Rules (industry-specific design system generation)

## Key Files

| File | Description |
|------|-------------|
| `src/ui-ux-pro-max/data/ux-guidelines.csv` | 99 UX rules (do/don't/code examples) |
| `src/ui-ux-pro-max/data/ui-reasoning.csv` | 161 industry reasoning rules |
| `src/ui-ux-pro-max/data/styles.csv` | 67 UI styles with full metadata |
| `src/ui-ux-pro-max/data/typography.csv` | 57 font pairings |
| `src/ui-ux-pro-max/data/colors.csv` | 161 color palettes |
| `src/ui-ux-pro-max/data/landing.csv` | 24 landing page patterns |
| `src/ui-ux-pro-max/data/charts.csv` | 25 chart types |
| `src/ui-ux-pro-max/scripts/search.py` | Main search + design system engine |
| `src/ui-ux-pro-max/scripts/design_system.py` | Design system generation logic |
| `src/ui-ux-pro-max/templates/base/skill-content.md` | Full skill workflow template |
| `src/ui-ux-pro-max/templates/base/quick-reference.md` | Priority rule quick reference |
| `.claude/skills/ui-ux-pro-max/SKILL.md` | Claude Code skill definition |

## Stack Support

React, Next.js, shadcn/ui, Vue, Nuxt.js, Nuxt UI, Angular, Laravel, Svelte, Astro, SwiftUI, Jetpack Compose, React Native, Flutter, HTML+Tailwind

## Installation

```bash
npm install -g uipro-cli
uipro init --ai claude
```

Or global:
```bash
uipro init --ai claude --global  # installs to ~/.claude/skills/
```
