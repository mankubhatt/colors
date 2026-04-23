# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Running the project

No build step. Open `index.html` directly in a browser:

```bash
open index.html
```

## Architecture

Everything lives in a single file: `index.html`. It is structured in three blocks:

1. **`<style>`** — all CSS inline. Sections are separated by `/* ─── Name ─── */` comments.
2. **`<body>`** — static HTML shell with empty container divs (`id="familyGrid"`, `id="compareGrid"`, etc.). All visible content is injected by JavaScript at runtime.
3. **`<script>`** — all JavaScript inline. Sections are separated by `// ── Name ──` banners.

### JavaScript layout (line numbers approximate)

| Section | What it does |
|---|---|
| `// ── Data` | Pure data arrays: `families`, `confusablePairs`, `gradients`, `cbTypes`, `ishiharaPlates`, `intensityColors`, `bezoldData` |
| `// ── Helpers` | `hexToRgb(hex)`, `textColor(hex)` — used across all sections |
| `// ── Build Families/Comparison/Gradients/Quiz` | One builder per tab; each reads a data array and appends DOM nodes into its container div |
| `// ── Color Blindness` | Builds type-selector buttons; `applyCbFilter(typeObj)` sets a CSS `filter: url(#cb-<id>)` on the simulated panel using inline SVG `<feColorMatrix>` filters defined in the HTML |
| `// ── Ishihara-style plates` | `generateIshihara(canvas, plate)` — draws packed random dots on a `<canvas>`, classifying each dot as signal/background via an offscreen pixel-mask of the digit text |
| `// ── Intensity Effects` | `updateIntensity(val)` — called on slider input; directly manipulates `hsl()` values on pre-built DOM elements to simulate Purkinje, Hunt, Bezold-Brücke, and Stevens effects |
| `// ── Tooltip / Tabs` | Global hover tooltip; tab switching via `data-tab` attribute on nav buttons |

### Key patterns

- **Data → DOM**: each tab section has a data array and a builder that runs once at page load. To add a new color or pair, edit the data array only.
- **Intensity effects**: elements are pre-built into `#purkinjeColors`, `#huntGrid`, `#bezoldRows`, `#stevensGrid` with predictable `id` attributes (`pk-Red`, `hunt-Blue`, `bz-Orange`, `st-0-3`, etc.) so `updateIntensity` can `getElementById` and update `style.background` directly.
- **Color blindness filters**: SVG `<filter>` elements with `id="cb-<type>"` are defined once in the HTML. `applyCbFilter` just sets `style.filter = url(#cb-<type>)` on the swatch container — no pixel manipulation needed.
- **Ishihara plates**: the digit is rendered into an offscreen canvas at high weight/size with a 5×5 offset grid to thicken strokes, then `getImageData` is used as a pixel mask. Signal dots and background dots share the same lightness range (44–60%) so only hue distinguishes them, matching authentic Ishihara design.

### Adding a new tab

1. Add a `<button data-tab="id">` in `<nav>`.
2. Add a `<section class="section" id="id">` in `<main>`.
3. Add a data array and builder function in the script block.
4. If the tab needs re-initialization on each visit (like Quiz), add it to the `if (btn.dataset.tab === '...')` check in the Tabs section.
