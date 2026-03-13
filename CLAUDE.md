# CLAUDE.md — a-css-reset

## Project Overview

**a-css-reset** is a minimal, opinionated CSS reset file authored by Carl Johansson. Its purpose is to normalize browser default styles to a clean, predictable baseline before applying any project-specific styles.

The project consists of a single CSS file (`reset.css`) and a thin HTML wrapper (`index.html`) that redirects visitors directly to the CSS source.

---

## Repository Structure

```
a-css-reset/
├── reset.css       # The CSS reset — the main deliverable
├── index.html      # Redirects to reset.css for direct viewing
├── README.md       # Minimal project description
├── .gitattributes  # LF line-ending normalization for all text files
└── CLAUDE.md       # This file
```

---

## reset.css — Section Breakdown

The file is organized into clearly commented sections:

| Section | Selectors | Purpose |
|---|---|---|
| **Box Model** | `*, *::before, *::after` | `box-sizing: border-box` universally |
| **Body Margin** | `html, body` | `margin: 0; padding: 0; height: 100%` |
| **Media Handling** | `img, picture, video, iframe, canvas, audio` | Responsive sizing; `display: block` to remove inline gaps; `aspect-ratio: 16/9` for iframe/video |
| **Basics Reset** | `html, body, h1–h6, p, input, textarea, pre, code, img, dl, dt, dd, ol, ul, li` | Zero margin, padding, border; `font-size: inherit` |
| **Typography** | `h1–h6`, `p` | Font-size 100%, font-weight normal; `text-wrap: balance` (headings), `text-wrap: pretty` (paragraphs) |
| **Links** | `a, a:hover, a:visited` | `color: inherit; text-decoration: none` |
| **Lists** | `ul, ol` | `list-style: none; padding: 0` |
| **Blockquote** | `blockquote` | Left-border styling (noted in code as branding, not a reset) |
| **HR** | `hr` | Borderless with `background: #ccc` |
| **Details/Summary** | `details`, `summary` | Padding for disclosure widgets |
| **Form Font Inheritance** | `input, button, textarea, select, legend, ::placeholder` | `font: inherit` |
| **Checkboxes/Radios** | `input[type="checkbox"], input[type="radio"]` | Margin/padding zero, border-box |
| **Forms** | `form`, `fieldset`, `legend` | Margin/padding/border zero |
| **Appearance Reset** | `input[type=text/submit/reset/button/image]`, `textarea`, `select` | `-webkit-appearance: none; border-radius: 0` |
| **Focus Styles** | `input:focus, textarea:focus, button:focus, select:focus` | Custom 2px `#007bff` outline |
| **Cursor** | `label`, `input[type="submit/reset"]`, `button`, `select` | `cursor: pointer` |
| **Field Width** | `input[type=text/password]`, `select`, `textarea` | `width: 100%` |
| **Button Reset** | `button` | No background, border, padding; `appearance: none` |
| **Touch** | `button`, `input[type="submit/reset"]` | `touch-action: manipulation` |
| **Tap Highlight** | `input, button` | `-webkit-tap-highlight-color: transparent` |
| **Textarea** | `textarea` | `resize: vertical; display: block` |
| **Tables** | `table` | `border-collapse: collapse; border-spacing: 0` |

---

## Conventions and Style

- **Comments** use `/* SECTION NAME */` block-comment headings for each logical group.
- **Inline notes** are written directly in comments after property values to explain non-obvious choices (e.g., why `font-size: inherit` is preferred over `font-size: 100%`).
- `TODO` comments mark open questions or planned work (e.g., auto-height textarea).
- Code notes distinguish between **reset rules** (removing browser defaults) and **opinionated defaults** (e.g., the blockquote border styling is flagged as branding, not a reset).
- Line endings are normalized to **LF** via `.gitattributes`.

---

## Key Design Decisions

1. **`box-sizing: border-box` globally** — Applied via the universal selector including pseudo-elements.
2. **`font-size: inherit` not `100%`** — Inherits from parent, allowing relative font scaling to cascade correctly.
3. **`display: block` on media elements** — Eliminates the default `inline` bottom gap without needing `vertical-align` hacks.
4. **`aspect-ratio: 16/9` on iframe/video** — Enforces a default responsive video ratio.
5. **`text-wrap: balance` / `pretty`** — Modern CSS properties for improved heading and paragraph wrapping.
6. **Focus styles are kept** — `outline: none` on bare inputs is immediately followed by explicit `:focus` styles to preserve accessibility.
7. **`-webkit-appearance: none` on form inputs** — Overrides iOS Safari default styling for consistent cross-browser forms.

---

## Development Workflow

This is a single-file CSS project. There is no build system, package manager, or test runner.

### Making Changes

1. Edit `reset.css` directly.
2. Test by linking `reset.css` into an HTML prototype that exercises all element types (headings, forms, media, tables, etc.).
3. Annotate non-obvious rules with inline comments explaining the rationale.

### Branching

- Default branch: `main` (remote), `master` (local default)
- Feature/AI branches: `claude/<description>-<id>`

### Committing

Write clear, imperative commit messages describing what changed and why. Examples from history:
- `Removed CSS branding elements`
- `added meta tags`
- `Initial commit`

### What to Avoid

- Do not add build tooling, preprocessors (Sass/Less), or package.json unless the project scope explicitly expands.
- Do not remove the inline comment rationale — the comments are documentation.
- Do not conflate **reset rules** with **opinionated defaults**. If adding a style that is not a browser-default removal, mark it clearly (as the blockquote rule already is).
- Do not add vendor prefixes beyond `-webkit-` without checking current browser support first.

---

## Known Issues / TODOs (from source comments)

- `textarea` auto-height behavior is marked `TODO` in the source (`reset.css:282`).
- `option { cursor: pointer }` is commented out because it does not work in browsers (`reset.css:225`).
- The `blockquote` rule is noted as branding/styling, not a reset (`reset.css:128`) — consider moving it out if this reset is used as a strict baseline.
- The `::placeholder` selector in the font-inheritance block may not apply as intended due to selector grouping with non-pseudo elements (depends on browser handling).
