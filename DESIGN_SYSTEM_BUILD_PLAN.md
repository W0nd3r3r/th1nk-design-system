# Th1nk Design System — Build Plan
**For Claude Code to execute**
Last updated: 2026-06-12

---

## Before starting any task in this plan

Read these files in full before touching anything else:

1. `D:\OneDrive\Work\th1nk\Think Online\th1nk-design-system\tokens.css`
2. `D:\OneDrive\Work\th1nk\Think Online\th1nk-design-system\web-components.css`
3. `D:\OneDrive\Work\th1nk\Think Online\th1nk-design-system\DESIGN_SYSTEM_BUILD_NOTES.md`

---

## Two repositories — know which is which

| Repo | URL | What lives here |
|---|---|---|
| `th1nk-design-system` | https://github.com/W0nd3r3r/th1nk-design-system | `tokens.css`, `web-components.css`, `deck-components.css`, `html-components.html` |
| `th1nk` | https://github.com/W0nd3r3r/th1nk | All Th1nk Online web pages (`online/` folder) |

---

## Three design system folder locations

| Folder | Purpose |
|--------|---------|
| `D:\OneDrive\Work\th1nk\Think Online\th1nk-design-system\` | **Master copy** — all files. Source of truth. |
| `D:\OneDrive\Work\th1nk\Think Online\Th1nk Online\th1nk-design-system\` | **Server copy** — web files only. What live pages reference. |
| `D:\OneDrive\Work\th1nk\Decks\Th1nk co-work\th1nk-design-system\` | **Deck/PPTX tools only** |

---

## Critical background — the nav naming problem

Every existing old web page uses unprefixed `nav-*` class names with inline styles.
`web-components.css` uses `th1nk-nav-*` prefixed class names. These are incompatible.

- **Existing old pages:** never add a `<link>` to `web-components.css`
- **New/rebuilt pages:** always use `th1nk-nav-*` and link both CSS files

---

## NEXT TASK — Deploy online-rebuild to live and push to GitHub

**Steve has reviewed the rebuilt pages in `online-rebuild/` and approved them.**

Execute these steps in order. Stop and report if anything fails.

### Step 1 — Sync design system server copy from master

Copy these four files from master to server copy, overwriting existing:

```
FROM: D:\OneDrive\Work\th1nk\Think Online\th1nk-design-system\tokens.css
TO:   D:\OneDrive\Work\th1nk\Think Online\Th1nk Online\th1nk-design-system\tokens.css

FROM: D:\OneDrive\Work\th1nk\Think Online\th1nk-design-system\web-components.css
TO:   D:\OneDrive\Work\th1nk\Think Online\Th1nk Online\th1nk-design-system\web-components.css

FROM: D:\OneDrive\Work\th1nk\Think Online\th1nk-design-system\deck-components.css
TO:   D:\OneDrive\Work\th1nk\Think Online\Th1nk Online\th1nk-design-system\deck-components.css

FROM: D:\OneDrive\Work\th1nk\Think Online\th1nk-design-system\html-components.html
TO:   D:\OneDrive\Work\th1nk\Think Online\Th1nk Online\th1nk-design-system\html-components.html
```

Do NOT copy Python files, node_modules, markdown files, or any PPTX tools.

### Step 2 — Copy rebuilt pages to live online/ folder

Copy all 13 HTML files from `online-rebuild/` to `online/`, overwriting the old pages:

```
FROM: D:\OneDrive\Work\th1nk\Think Online\Th1nk Online\online-rebuild\*.html
TO:   D:\OneDrive\Work\th1nk\Think Online\Th1nk Online\online\
```

Files to copy (13 total):
- `index.html`
- `high-performance-teams.html`
- `how-it-works.html`
- `five-stages.html`
- `pricing.html`
- `innovation.html`
- `product-lifecycle.html`
- `business-track.html`
- `mastery-track.html`
- `fractionals-offer.html`
- `th1nk-online.html`
- `th1nk-workshop.html`
- `th1nk-talk-hidden-wiring.html`

Do NOT touch any subfolders (`wiring/`, `hpt-quiz/`, `High Performance Team deck/`, `images/`).

### Step 3 — Verify CSS paths in copied files

After copying, verify every file in `online/` now references `../th1nk-design-system/` (one level up). Run:

```bash
grep -r "th1nk-design-system" online/*.html
```

All references must be `../th1nk-design-system/` — not `../../` or any other path. Fix any that are wrong before proceeding.

### Step 4 — Push pages to W0nd3r3r/th1nk

```bash
cd "D:\OneDrive\Work\th1nk\Think Online\Th1nk Online"
git add online/*.html
git commit -m "Rebuild online/ pages to use shared design system (th1nk-nav-*, tokens.css, web-components.css)"
git push origin main
```

### Step 5 — Push design system files to W0nd3r3r/th1nk-design-system

```bash
cd "D:\OneDrive\Work\th1nk\Think Online\th1nk-design-system"
git add tokens.css web-components.css deck-components.css html-components.html
git commit -m "Update design system: bump font sizes, add 26 new web components, fix token variables"
git push origin main
```

### Step 6 — Report

Report:
- Files copied to `online/`
- Git commit hashes for both repos
- Any errors or files that couldn't be processed

---

## Hard rule

Do NOT push until Steve explicitly confirms the pages are approved. The steps above assume approval has been given.

---

## Future tasks (not yet scheduled)

- Review dense grid components for cramped text: `th1nk-char-grid` (4-col), `th1nk-maturity-track` (4-col), `th1nk-stages-flow` (5-col), `th1nk-phase-grid` (4-col) — may need column reduction like `th1nk-journey-grid`
- Push design system to `W0nd3r3r/th1nk-design-system` repo separately from pages
- Sync `Decks/Th1nk co-work/th1nk-design-system/tokens.css` if brand colour changes are made

