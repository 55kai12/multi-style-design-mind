# S7 · Ins Minimal

Keywords: content-first, black & white & gray, whitespace, rounded, nearly invisible, lifestyle.
Axioms: content is the interface; whitespace is breath; decoration is noise; the photo is the protagonist.
Decision order: content (photos/copy) → whitespace zoning → typographic hierarchy → presentation. No effects layer.

## Color system
- Black/white/gray: #FFFFFF / #FAFAFA / #F5F5F5 / #E0E0E0 / #999999 / #666666 / #000000.
- At most one ultra-low-saturation lifting tone: #F5E6D3 (cream), #E8F0E8 (pale green), #F0E8F0 (pale purple).
- No gradients, no colored glass.
- Dark mode: #000000 / #1A1A1A / #2A2A2A.

## Typography
- Families: Montserrat Light / Helvetica Neue / Futura PT / SF Pro.
- Headlines: 28/36/48pt, Light or Bold, tracking -0.5.
- Body: 15/16pt, Regular, line-height 1.6.
- Minimal, clean, lots of whitespace.
- Prohibited: gimmicky fonts, multi-typeface mixing.

## Shape & layout
- Radius: large 16–24, soft curves.
- Spacing: 16/24/32/48/64.
- Grid: single or double column, gutter 16–24.
- Whitespace maximal; content breathes.
- Images edge-to-edge or large-radius.

## Material
- Minimal; no frosted glass.
- Hierarchy from flat blocks and whitespace.
- Prohibited: glass, gradients, noise.

## Shadow
- Near-none. y 4 blur 12 opacity 0.04.
- Prohibited: heavy shadows.

## Components
- Buttons: capsule or small radius, solid or outlined.
- Cards: large radius + no shadow or near-none.
- Inputs: rounded + hairline.
- Navigation: minimal + large title.
- Modals: rounded + solid color.

## Motion
- Restrained, fast, fade + micro-shift, no overshoot. 150–300ms.
- Prohibited: exaggerated motion, particles, parallax.

## Effects
- None. Fades at most.

## Implementation (very low cost on all three platforms)

### SwiftUI
- Native controls suffice: `List` / `ScrollView` + `LazyVGrid`.
- Colors: `Color(white: 0.98)` gray family; define the single lifting tone once and reference it globally.
- Type: `.system(size: 36, weight: .light)` headlines + `.kerning(-0.5)`.
- Motion: `.animation(.easeOut(duration: 0.2), value: ...)`, opacity + offset 8px.

### Compose mapping
| Concept | Equivalent | Notes |
|---|---|---|
| Large-radius cards | RoundedCornerShape(20.dp) + solid surface | No shadow |
| Light-weight headlines | FontWeight.Light(300) | Pair Chinese with Source Han Sans Light |
| Two-column grid | LazyVerticalGrid(GridCells.Fixed(2), horizontalArrangement 16.dp) | Gutter 16–24 |
| Motion | tween(200, FastOutSlowInEasing) fade + slide 8dp | No overshoot |

### Web / CSS
- Single/double-column grid; images with fixed `aspect-ratio` to prevent layout shift; `object-fit: cover`.
- Type: Montserrat (Google Fonts, free) or the system font stack.
- Lazy-load images with explicit dimensions; gray placeholder blocks (#F5F5F5) while loading.

## Accessibility
- Black/white/gray contrast passes naturally: #666 on #FFF ≈ 5.7:1 and up.
- Lifting-tone backgrounds (#F5E6D3) with black text ≈ 13:1, safe; **never light text on light backgrounds**.
- All images get descriptions (alt / accessibilityLabel) — the photo is the protagonist; the protagonist must be readable aloud.
- Reduce Motion: fade → instant display.

## Prohibitions
Heavy color blocks, complex textures, multi-color accents, exaggerated motion, cramped layouts.

## Self-check list
- [ ] At most one lifting tone?
- [ ] Whitespace generous (err on the side of more)?
- [ ] Zero shadows, zero textures (glass/gradient = S3 residue)?
- [ ] Photos the absolute protagonist, with accessible descriptions?
- [ ] No crossover (heavy shadows / colors = residue)?

## Suitable for
Social, reading, e-commerce display, lifestyle apps, photography products.
