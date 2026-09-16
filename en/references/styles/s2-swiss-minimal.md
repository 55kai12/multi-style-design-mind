# S2 · Swiss Minimal (International Typographic Style)

Keywords: grid, whitespace, order, neutrality, weight contrast, zero decoration, rationality.
Axioms: the grid is order; whitespace is breath; type is graphic; decoration is noise; alignment is beauty; rationality is universality.
Decision order: information architecture → grid setup → typographic hierarchy (weight contrast) → alignment calibration → presentation. The decoration layer does not exist — that's a feature, not a gap.

## Color system
- Black #000000, white #FFFFFF, grays #F5F5F5 / #E5E5E5 / #999999 / #666666 / #333333.
- Exactly one accent: red #E30613, blue #0055FF, or yellow #FFD500.
- No gradients, no transparency, no colored glass.
- Color ratio: black 10%, white 70%, gray 15%, accent 5%.
- Dark mode: inverted, same logic.

## Typography
- Families: Helvetica Now / Inter / SF Pro / Univers.
- Headlines: large and heavy, 48/64/80pt, weight Bold/Black, tracking -1 to -2.
- Body: 16/18pt, Regular, line-height 1.5–1.6.
- Strong weight contrast: headline Black vs body Regular.
- Strictly left-aligned; no centering (except occasional poster layouts).
- Baseline grid: 4pt or 8pt.
- Prohibited: gimmicky fonts, calligraphy, decorative type.

## Shape & layout
- Grid: 12 or 6 columns, gutter 24–32, margins 32–64.
- Spacing: 8/16/24/32/48/64/96/128.
- Radius: 0–4 or square.
- Separators: 1px hairlines #E5E5E5.
- Alignment: strictly left; elements snap to the grid.
- Whitespace: generous, strong breathing room.

## Material & shadow
- No frosted glass, no gradients, no noise.
- Flat blocks and hairline separators.
- Shadows: none, or a single ultra-faint layer y 1 blur 2 opacity 0.05.
- Prohibited: glass, glow, skeuomorphism, textures.

## Components
- Buttons: rectangular or small radius, solid fill, no shadow.
- Cards: no radius or 4pt, hairline border or flat block.
- Inputs: bottom 1px line, no radius.
- Navigation: top, left-aligned, strong type-size contrast.
- Lists: hairline separators, no radius.

## Motion
- Fast, linear or tiny spring. Fade + 8–16px shift. 120–240ms. No overshoot.
- Prohibited: exaggerated springs, particles, parallax, floating.

## Effects
- None. At most a mask reveal or simple fade.

## Implementation

### SwiftUI
- Type: system SF Pro (Helvetica lineage), `.font(.system(size: 64, weight: .black))` + `.kerning(-2)`; body `.system(size: 16, weight: .regular)`.
- Hairline: `Rectangle().fill(Color(hex: "#E5E5E5")).frame(height: 1)`.
- Layout: `LazyVGrid(columns: 12)` or a custom Layout; everything `.leading`.
- Motion: `.animation(.linear(duration: 0.18), value: ...)`, fade + offset 8–16px; no springs.

### Compose mapping
| Concept | Equivalent | Notes |
|---|---|---|
| 12-column grid | Custom Layout (manual Row/Column allocation) | No native 12-col grid; implement it |
| Weight contrast | FontWeight.Black(900) vs FontWeight.Normal(400) | Contrast is the hierarchy |
| Tracking | TextStyle letterSpacing = (-1).sp | Negative on headlines |
| Hairline separator | HorizontalDivider(thickness = 1.dp, color = #E5E5E5) | — |
| Square corners | RoundedCornerShape(0.dp) / RectangleShape | — |
| Motion | tween(180, LinearEasing), fade + slide 8–16dp | No springs |

### Web / CSS
- Grid: `grid-template-columns: repeat(12, 1fr); gap: 24–32px;` margins 32–64px.
- Type: Inter (Google Fonts, free), headlines `font-weight: 900; letter-spacing: -2px`.
- Inputs: `border: none; border-bottom: 1px solid #E5E5E5; border-radius: 0;`
- Motion: `transition: opacity .18s linear, transform .18s linear;`

## Accessibility
- Black/white/gray is naturally high contrast: #333 on #FFF ≈ 12:1, body text passes easily.
- Accent red #E30613 as text on white ≈ 5:1, usable; yellow #FFD500 only as a block background with black text (≈ 14:1), never as text color.
- Reduce Motion: it's already a linear fade; degrade to instant switch.
- Responsive: collapse grid columns on narrow screens / large type (12→4→2); left alignment never changes.

## Prohibitions
Frosted glass, glow, gradients, rounded cards, skeuomorphism, particles, exaggerated springs, decorative elements.

## Self-check list
- [ ] Strictly aligned to the grid?
- [ ] Strictly left-aligned (except poster layouts)?
- [ ] Exactly one accent color, ≤5% coverage?
- [ ] Zero decoration (no shadows, no glass, no gradients)?
- [ ] Headline/body weight contrast strong enough?
- [ ] No crossover (rounded cards / frosted glass / springy motion = S1/S3 residue)?

## Suitable for
Editors, portfolios, data-heavy dashboards, brand sites, architecture & design agencies.
