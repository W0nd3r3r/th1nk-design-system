# Th1nk Design System
*Last updated: June 2026*

Single source of truth for all Th1nk CI — colours, typography, spacing, and component patterns — used across th1nk.co.za HTML pages, tools, and questionnaires.

---

## Files in this repo

| File | Purpose |
|------|---------|
| `tokens.css` | All design tokens as CSS custom properties — colours, type scale, spacing, shadows |
| `web-components.css` | 39 reusable web page components — nav, hero, cards, grids, pricing, footer etc. |
| `deck-components.css` | Slide deck components for HTML presentations |
| `html-components.html` | Copy-paste HTML blocks for wiring/Enneagram pages [C00]–[C10] |
| `DESIGN_SYSTEM_BUILD_NOTES.md` | Full history of decisions and changes across sessions |
| `DESIGN_SYSTEM_BUILD_PLAN.md` | Claude Code prompt for deploying pages and pushing to GitHub |
| `CLAUDE_CODE_BUILD_GUIDE.md` | Standing instructions for Claude Code when building pages |

---

## How to use

Import both files in the `<head>` of any new Th1nk Online page:

```html
<link rel="stylesheet" href="../th1nk-design-system/tokens.css">
<link rel="stylesheet" href="../th1nk-design-system/web-components.css">
```

Path assumes the page lives in `online/` (one level up from `th1nk-design-system/`).

**Never link `web-components.css` to old pages that use `nav-*` unprefixed class names — it will collapse the nav.**

---

## Colour tokens

| Alias | Hex | Use |
|-------|-----|-----|
| `--navy` | `#1a2535` | Primary dark — headings, nav, dark sections |
| `--teal` | `#59c0d9` | Primary accent — buttons, highlights |
| `--amber` | `#f29138` | Secondary accent — eyebrows, CTAs |
| `--green` | `#57c26d` | Positive / success |
| `--gold` | `#b9a478` | Decorative / mastery |
| `--ink` | `#111111` | Body text |
| `--muted` | `#6B7280` | Subdued text, captions |
| `--charcoal` | `#3A3A3A` | Card body copy |
| `--border` | `#E5E7EB` | Card and divider borders |
| `--panel` | `#F5F7FA` | Light section background |
| `--warm` | `#FFF8F0` | Warm section background |

---

## Type scale (June 2026 — bumped for readability)

| Token | Size range | Used for |
|-------|-----------|---------|
| `--text-small` | `0.875rem` | Labels, captions, badges |
| `--text-medium` | `1.0625rem – 1.1875rem` | Body copy |
| `--text-large` | `1.125rem – 1.5rem` | H3, lead text |
| `--text-xlarge` | `1.5rem – 2.25rem` | H2 section headings |
| `--text-xxlarge` | `1.5rem – 2.5rem` | H1 page headings |

Fonts: `--font-display` = Montserrat (headings/labels), `--font-body` = Inter (body copy)

---

## Component index (web-components.css)

1. Navigation — `th1nk-nav`, `th1nk-subnav`
2. Hero — `th1nk-hero` (add `.dark-grad` for no-photo variant)
3. Eyebrow label — `th1nk-eyebrow` (`.on-dark`, `.teal`, `.green`, `.gold`)
4. Section header — `th1nk-section-header`, `th1nk-section-lead`
5. Buttons — `th1nk-btn` (`.primary`, `.ghost`, `.outline`, `.green`, `.teal`)
6. CTA box — `th1nk-cta-box`
7. Pillar cards — `th1nk-pillar-grid` / `th1nk-pillar-card` (`.people`, `.process`, `.tech`)
8. Outcome items — `th1nk-outcome-grid` / `th1nk-outcome-item`
9. Journey flow — `th1nk-journey-flow` / `th1nk-journey-phase` (add `.five` for 5-phase grid)
10. Event panel — `th1nk-event-panel`
11. Pricing cards — `th1nk-pricing-grid` / `th1nk-pricing-card` (add `.featured`)
12. Footer — `th1nk-footer`
13. Page layout — `th1nk-container`, `th1nk-section`, `th1nk-bg-panel/warm/white/dark`
14. HPT teaser hero — `th1nk-hpt-hero`, `th1nk-bg-hpt`
15. Five-phase journey — `th1nk-journey-flow.five`
16. Six-step journey grid — `th1nk-journey-grid` (3×2 layout)
17. Pillar card with image — `th1nk-pillar-card-img`
18. Stat cards — `th1nk-stats-grid` / `th1nk-stat-card`
19. Cohort cards — `th1nk-cohort-grid` / `th1nk-cohort-card` (`.gold`)
20. Track cards — `th1nk-track-grid` / `th1nk-track-card` (`.business`, `.personal`)
21. Differentiator grid — `th1nk-diff-grid` / `th1nk-diff-item` (`.on-dark`)
22. Persona cards — `th1nk-persona-grid` / `th1nk-persona-card`
23. Concept cards — `th1nk-concept-grid` / `th1nk-concept-card`
24. Module list — `th1nk-module-list` / `th1nk-module-item`
25. Characteristics grid — `th1nk-char-grid` / `th1nk-char-card`
26. Cadence cards — `th1nk-cadence-grid` / `th1nk-cadence-card`
27. Phase grid — `th1nk-phase-grid` / `th1nk-phase-card`
28. Programme phases — `th1nk-prog-phases` / `th1nk-prog-phase-card`
29. Five-stages set — `th1nk-stages-flow`, `th1nk-stage-section`, `th1nk-criteria-grid`, `th1nk-side-card`, `th1nk-marker-list`
30. Maturity track — `th1nk-maturity-track` / `th1nk-maturity-stage`
31. Event meta — `th1nk-event-meta` (`.th1nk-event-meta-priced`)
32. Stat callout — `th1nk-stat-callout`, `th1nk-stat-grid`
33. Promo block — `th1nk-promo-block` (`.navy`, `.teal`, `.reverse`, `.bridge`)
34. Speaker card — `th1nk-speaker-card`
35. Takeaway list — `th1nk-takeaway-list`
36. FAQ — `th1nk-faq-wrap` / `th1nk-faq-item`
37. Phase-1 pricing card — `th1nk-phase1-card`
38. Comparison band — `th1nk-comparison-band`, `th1nk-comparison`
39. Calendar button — `th1nk-calendar-btn`

---

## Stage colours (HPT)

| Stage | Token | Hex |
|-------|-------|-----|
| CRAWL | `--color-crawl` | `#de6868` |
| WALK | `--color-walk` | `#f29138` |
| RUN | `--color-run` | `#57c26d` |
| FLY | `--color-fly` | `#59c0d9` |

---

*Tokens extracted from the live th1nk.co.za WordPress theme. Component library built June 2026.*
