# Th1nk Design System — Build Notes
*Last updated: 2026-06-12 (post-deploy fix)*

---

## What This Document Is

A summary of all design system decisions and changes, maintained across sessions. Hand this to Claude (Cowork or Claude Code) at the start of any future session to pick up where we left off.

---

## The Problem We're Solving

Claude Code guesses at CSS values, padding, coordinates, and proportions when building HTML pages or PowerPoint decks. The solution is a shared design system that gives Claude Code a source of truth to read rather than guess from.

---

## Two Repositories

| Repo | URL | What lives here |
|------|-----|-----------------|
| `th1nk-design-system` | https://github.com/W0nd3r3r/th1nk-design-system | `tokens.css`, `web-components.css`, `deck-components.css`, `html-components.html` |
| `th1nk` | https://github.com/W0nd3r3r/th1nk | All Th1nk Online web pages (`online/` folder) |

---

## Three Design System Folder Locations

| Folder | Purpose |
|--------|---------|
| `D:\OneDrive\Work\th1nk\Think Online\th1nk-design-system\` | **Master copy** — all files including Python/PPTX tools. Source of truth. |
| `D:\OneDrive\Work\th1nk\Think Online\Th1nk Online\th1nk-design-system\` | **Server copy** — web files only (no Python, no node_modules). This is what gets uploaded and what live pages reference. |
| `D:\OneDrive\Work\th1nk\Decks\Th1nk co-work\th1nk-design-system\` | **Deck/PPTX tools only** — `th1nk_design_constants.py`, `th1nk_slide_components.py`, `deck-components.css`. No `web-components.css`. |

**Rule:** When updating CSS files, update the master copy first, then sync to the server copy. Never copy from server copy back to master.

---

## The Nav Naming Problem (Critical)

Old pages use unprefixed `nav-*` class names with inline styles. New pages use `th1nk-nav-*` class names with `web-components.css`. **These are incompatible** — linking `web-components.css` to an old page collapses the nav.

- **Existing old pages:** never add a `<link>` to `web-components.css`
- **New/rebuilt pages:** always use `th1nk-nav-*` and link both CSS files

---

## Page Rebuild — June 2026

### What was done
All 13 live pages in `online/` were rebuilt from scratch using the new design system into a staging folder `online-rebuild/`. Pages were NOT copied to `online/` yet — awaiting review and approval.

**Pages rebuilt:**
`index.html`, `high-performance-teams.html`, `how-it-works.html`, `five-stages.html`, `pricing.html`, `innovation.html`, `product-lifecycle.html`, `business-track.html`, `mastery-track.html`, `fractionals-offer.html`, `th1nk-online.html`, `th1nk-workshop.html`, `th1nk-talk-hidden-wiring.html`

### CSS path correction
Rebuilt pages use `../th1nk-design-system/` (one level up) — correct for both local browsing from `online-rebuild/` and the live server. Do NOT use `../../`.

### New components added to web-components.css
Claude Code added 26 new components during the rebuild (components 13–39), covering gaps that existed in the original 12-component library:

- `th1nk-container` — page layout wrapper (max-width, centred, padded)
- `th1nk-section`, `th1nk-bg-*` — section scaffolding and background variants
- `th1nk-hpt-hero` — HPT teaser hero with stat meta
- `th1nk-journey-flow.five` — 5-phase journey grid variant
- `th1nk-journey-grid` — 6-step linear grid (now 3×2)
- `th1nk-stats-grid` / `th1nk-stat-card` — big-number stat cards
- `th1nk-cohort-grid` / `th1nk-cohort-card` — cohort track cards
- `th1nk-track-grid` / `th1nk-track-card` — business/personal track cards
- `th1nk-diff-grid` / `th1nk-diff-item` — differentiator grid
- `th1nk-persona-grid` / `th1nk-persona-card` — persona cards
- `th1nk-concept-grid` / `th1nk-concept-card` — concept cards
- `th1nk-module-list` — numbered module/step list
- `th1nk-char-grid` / `th1nk-char-card` — 8 characteristics grid
- `th1nk-cadence-grid` / `th1nk-cadence-card` — team cadence cards
- `th1nk-phase-grid` / `th1nk-phase-card` — 4-phase product lifecycle grid
- `th1nk-prog-phases` — two-column programme phase cards with image
- `th1nk-stages-flow` + full five-stages set — 5-stage overview + per-stage sections
- `th1nk-maturity-track` — Crawl/Walk/Run/Fly dark band
- `th1nk-event-meta` — hero stat/pricing callout
- `th1nk-stat-callout` — two stats + quote block
- `th1nk-promo-block` — cross-sell/bridge two-column blocks
- `th1nk-speaker-card` — speaker bio card
- `th1nk-takeaway-list` — two-column takeaway checklist
- `th1nk-faq-wrap` — FAQ accordion blocks
- `th1nk-phase1-card` — single Phase 1 pricing card
- `th1nk-comparison-band` — Delivery vs Innovation comparison grid
- `th1nk-calendar-btn` — Add to Calendar button

---

## Font Size Changes — June 2026

### tokens.css
Old values → new values (body text was too small):

| Token | Old | New |
|-------|-----|-----|
| `--text-medium` | `clamp(1rem, ..., 1.05rem)` | `clamp(1.0625rem, ..., 1.1875rem)` |
| `--text-large` | `clamp(1.125rem, ..., 1.375rem)` | `clamp(1.125rem, ..., 1.5rem)` |
| `--text-xlarge` | `clamp(1.5rem, ..., 1.88rem)` | `clamp(1.5rem, ..., 2.25rem)` |

### web-components.css
44 hardcoded font-size values bumped across all components. Key changes:
- Card body copy: `0.9375rem` → `1rem`
- Small card text: `0.875rem` → `0.9375rem`
- Lead text / section leads: `1.0625rem` → `1.125rem`
- Section header h2: `clamp(1.875rem, 3.2vw, 2.5rem)` → `clamp(2rem, 3.5vw, 2.75rem)`

### Layout change: th1nk-journey-grid
Changed from 6 columns to 3 columns × 2 rows. Text bumped to `1.0625rem` / `1rem`. Reason: 6-column layout forced text too small to read comfortably.

---

## Missing Token Variables (resolved)
`web-components.css` references `--muted`, `--ink`, `--charcoal`, `--border`, `--white`, `--dark-alt`, `--panel`, `--warm` which were not in `tokens.css`. These have been added to `tokens.css` under the semantic aliases section.

---

## Deploy — June 2026

### What was done
Steve approved the rebuilt pages. All steps were executed in a single session.

**Step 1 — Design system server copy synced**
Copied `tokens.css`, `web-components.css`, `deck-components.css`, `html-components.html` from master (`th1nk-design-system/`) to server copy (`Th1nk Online/th1nk-design-system/`).

**Step 2 — Pages deployed to `online/`**
All 13 HTML files copied from `online-rebuild/` to `online/`, overwriting old pages.

**Step 3 — CSS paths verified**
All 13 files confirmed using `../th1nk-design-system/` — correct for both local and live server. No fixes needed.

**Step 4 — W0nd3r3r/th1nk: pages pushed**
Commit `b410a19` — "Rebuild online/ pages to use shared design system"
13 files changed, 2570 insertions, 10130 deletions.

**Step 5 — W0nd3r3r/th1nk-design-system: design system pushed**
Commit `1c33ebc` — "Update design system: bump font sizes, add 26 new web components, fix token variables"
`tokens.css`, `web-components.css`, `README.md` updated; `DESIGN_SYSTEM_BUILD_NOTES.md` and `DESIGN_SYSTEM_BUILD_PLAN.md` added as new tracked files.

---

## Post-Deploy Bug — June 2026

### Symptom
Four pages broke after deploy: `th1nk-online.html`, `how-it-works.html`, `mastery-track.html`, `business-track.html`.

### Root cause
The `W0nd3r3r/th1nk` repo holds its own copy of the design system CSS (`th1nk-design-system/tokens.css`, `web-components.css`). These were updated locally in the Step 1 sync but were NOT staged or pushed in Step 4 — only the `online/*.html` files were committed. The live server was left serving the old CSS, which was missing the new component classes used by the four broken pages (`th1nk-track-grid`, `th1nk-track-card`, `th1nk-prog-phases`, and others added during the rebuild).

The other nine pages happened to use only component classes that existed in the old CSS, so they rendered correctly.

### Fix
Committed and pushed `tokens.css` + `web-components.css` to `W0nd3r3r/th1nk`.
Commit `b42ef84` — "Fix broken pages: push updated design system CSS to live repo" — 635 lines added.

### Rule to add
**When deploying rebuilt pages to `W0nd3r3r/th1nk`, always also stage and push the `th1nk-design-system/` CSS files in the same repo.** The two repos (`th1nk` and `th1nk-design-system`) are separate git repos but both contain a copy of the CSS. Pushing to `th1nk-design-system` alone is not enough.

---

## What Still Needs Doing

1. **Review dense grid components** — `th1nk-char-grid` (4-col), `th1nk-maturity-track` (4-col), `th1nk-stages-flow` (5-col), `th1nk-phase-grid` (4-col) may still have cramped text at smaller viewports

---

## Key Principle

**Tokens → Components → Instructions → Output**

- Tokens: raw values (colours, sizes, spacing) in `tokens.css`
- Components: named patterns in `web-components.css`
- Instructions: CLAUDE.md tells Claude Code to use components, never invent
- Output: pages assembled from the system, not guessed
