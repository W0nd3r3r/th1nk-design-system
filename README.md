# Th1nk Design System

Single source of truth for all Th1nk CI — colours, typography, spacing, and visual style — used across th1nk.co.za HTML pages, tools, and questionnaires.

---

## How to use this

When building any Th1nk HTML page or tool, reference `tokens.css` for all design decisions. Import it in the `<head>` of your HTML file:

```html
<link rel="stylesheet" href="/path/to/tokens.css">
```

Or if building a self-contained single-file tool, copy the `:root { }` block from `tokens.css` directly into a `<style>` tag in your file.

---

## Quick reference

### Colours

| Name | Hex | Use |
|---|---|---|
| Blue | `#59c0d9` | Primary accent, buttons, selected states, Fly stage |
| Green | `#57c26d` | Positive actions, Run stage |
| Orange | `#f29138` | Walk stage, warnings |
| Red | `#de6868` | Crawl stage, alerts |
| Purple | `#ae70de` | Secondary accent |
| Black | `#111111` | Body text, headings |
| White | `#ffffff` | Page background |
| Grey | `#9eacb0` | Subdued text, borders |
| Light BG | `#f4f4f4` | Card backgrounds |
| Link | `#1f86c7` | Inline links |

### Typography

- **Primary font:** Parkinsans (Google Fonts)
- **Mono font:** Fira Code
- Load from: `https://fonts.googleapis.com/css2?family=Parkinsans:wght@300;400;600;700;800&display=swap`

| Element | Size token | Weight |
|---|---|---|
| h1 | `--text-xxlarge` | 800 |
| h2 | `--text-xlarge` | 700 |
| h3 | `--text-large` | 600 |
| Body | `--text-medium` | 400 |
| Small / label | `--text-small` | 400 or 700 |

### HPT Stage colours

| Stage | Hex |
|---|---|
| CRAWL | `#de6868` |
| WALK | `#f29138` |
| RUN | `#57c26d` |
| FLY | `#59c0d9` |

---

## Files in this repo

| File | Purpose |
|---|---|
| `tokens.css` | All design tokens as CSS custom properties — the authoritative source |
| `README.md` | This file — quick reference for humans and AI agents |
| `Th1nk Design System.html` | Saved snapshot of the design system UI (reference only — not machine-readable) |

---

## Visual style guidelines

- **Cards:** White background, `border-radius: 8px`, shadow `0px 2px 5px 2px rgba(0,0,0,0.05)`
- **Buttons:** Default black with white text; primary actions use `--color-blue`
- **Progress bars:** Use `--color-blue`
- **Selected / active states:** Blue background (`--color-blue`) with white text
- **Page background:** Always white (`#ffffff`)
- **No decorative clutter** — clean, minimal, consistent with the Th1nk site aesthetic
- **Spacing:** Use the `--space-*` tokens; default page padding is `clamp(30px, 5vw, 50px)` each side

---

## Th1nk site structure (for reference)

```
th1nk.co.za/
├── (WordPress home)
├── people/
├── process/
├── tech/
└── hpt-quiz/          ← HPT questionnaire lives here
    ├── index.html
    ├── submit.php
    └── .htaccess
```

---

*Tokens extracted from the live th1nk.co.za WordPress theme — May 2026.*
