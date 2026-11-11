# Brand & Logo Assets — `readme-generator`

Lean vector logo suite for the `readme-generator` skill, styled after the **M.O.B Signal** palette from `mob-design-system`.

## Mark Concept

**Turned Codex** — two facing codex pages separated by a crisp negative-space spine slit, with the top-right page corner turned upward in Signal Green (`#00cc5c`) to evoke turning a blank page into structured documentation.

## Color Tokens (M.O.B Signal)

| Role | Token / Variant | Hex | Usage |
| --- | --- | --- | --- |
| Primary Accent | `Signal Green` | `#00cc5c` | Turned corner accent (flat solid fill only) |
| Ink (Light Mode) | `Charcoal Base` | `#0a0a0a` | Codex wings and wordmark on light surfaces |
| Ink (Dark Mode) | `Light Foreground` | `#ededed` | Codex wings and wordmark on dark surfaces (`#0a0a0a` / `#0d1117`) |

## Asset Inventory

| File | Purpose | Surface | Dimensions |
| --- | --- | --- | --- |
| `readme-generator-horizontal-light.svg` | Horizontal lockup (`<picture>` light source & fallback) | Light | `1082 x 216` |
| `readme-generator-horizontal-dark.svg` | Horizontal lockup (`<picture>` dark source) | Dark | `1082 x 216` |
| `readme-generator-symbol-light.svg` | Standalone square mark | Light | `256 x 256` |
| `readme-generator-symbol-dark.svg` | Standalone square mark | Dark | `256 x 256` |
| `readme-generator-symbol.png` | Raster symbol fallback (avatars, non-SVG embeds) | Light / neutral | `512 x 512` |

## Usage Guidelines

- **Wordmark typography**: Outlined lowercase `readme-generator` (no live `<text>` dependencies in SVG files).
- **Clear space**: Maintain at least **1/4 mark width** (`64` SVG units) of unobstructed padding on all sides.
- **Minimum size**: Keep the standalone symbol at `>= 24px` and the horizontal lockup at `>= 160px` wide.
- **Do**: Keep transparent backgrounds intact when embedding via `<picture>` on GitHub Light/Dark themes.
- **Don't**: Add gradients, drop shadows, glow effects, or outlines to `#00cc5c`, stretch/skew lockups, recolor individual letters, or pair `-light.svg` on dark surfaces.
