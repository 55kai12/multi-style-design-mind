# S10 · Minimalist

Keywords: fewest elements, clearest information, whitespace, basic shapes, order, affordance.
Axioms: content is king; whitespace is breath; restraint is sophistication; less is more.
Decision order: information architecture → single focal point → hierarchy (size contrast + whitespace) → micro-motion. The effects layer is zero.

## Color system
- Simple palette; single primary color ≤30% coverage.
- Black/white/gray for hierarchy: #FFFFFF / #FAFAFA / #F0F0F0 / #D0D0D0 / #999999 / #333333 / #000000.
- Primary color examples: blue #0055FF, red #E30613, green #00A86B.
- No gradients, no multiple primaries.
- Exactly one visual focal point per screen.
- Dark mode: inverted.

## Typography
- Families: sans / hei-ti (Inter / SF Pro / Helvetica Neue / Source Han Sans).
- Sizes: headlines 24/32/40pt, body 16/18pt.
- Weight: headlines 600–700, body 400.
- Left-aligned, stable reading path.
- Line-height 1.5–1.6.
- Prohibited: gimmicky fonts, multi-typeface mixing.

## Shape & layout
- Basic shapes, large and whole.
- Radius: 8–16.
- Spacing: 8/16/24/32/48/64.
- Minimal elements; similar but not repeated.
- Generous whitespace, bright backgrounds.
- Grid: 12 columns, gutter 24.

## Material
- No frosted glass, no gradients.
- Bright background + ample whitespace.
- Hierarchy from whitespace, size contrast, and sparing shadows.
- Prohibited: glass, textures, ornament.

## Shadow
- Subtle: y 2 blur 8 opacity 0.06.
- Prohibited: heavy shadows.

## Components
- Buttons: rounded + solid or outlined.
- Cards: rounded + white + subtle shadow.
- Inputs: rounded + hairline.
- Navigation: minimal + left-aligned.
- Modals: rounded + white.

## Motion
- Minimal transitions, subtle shifts. 150–300ms.
- Keep effects strictly rationed.
- Prohibited: exaggerated motion, particles.

## Effects
- None. Fades at most.

## Implementation (cheapest of all styles)

### SwiftUI
- Native controls work as-is: `List` / `Form` / `Button`.
- One primary color: define a single AccentColor in the Asset Catalog, referenced globally — no scattered hardcoding.
- Card: `RoundedRectangle(cornerRadius: 12).fill(.white).shadow(color: .black.opacity(0.06), radius: 8, y: 2)`.
- Motion: `.animation(.easeOut(duration: 0.2), value: ...)`, opacity + micro-shift.

### Compose mapping
| Concept | Equivalent | Notes |
|---|---|---|
| Single primary | MaterialTheme(colorScheme = lightColorScheme(primary = ...)) defined once | — |
| Card | Card / Surface(shape = RoundedCornerShape(12.dp), tonalElevation = 0) + hand-drawn subtle shadow | tonalElevation tints the surface; disable it for the white flat look |
| Motion | tween(200, FastOutSlowInEasing) fade | — |
| 12-col grid | Custom Layout or simplified Column | Single column suffices for most cases |

### Web / CSS
- Plain CSS, no framework needed: cards `box-shadow: 0 2px 8px rgba(0,0,0,0.06); border-radius: 12px;`
- Type: Inter / Source Han Sans (Google Fonts, free).
- Whitespace via `--space` CSS variables on an 8pt scale.

## Accessibility
- Black/white/gray passes naturally: #333 on #FFF ≈ 12:1.
- Primary-color button text: blue #0055FF with white ≈ 4.6:1, passes; green #00A86B with white ≈ 3.0:1 only for large-type buttons, banned for body-size text; red #E30613 with white ≈ 5:1, usable.
- A single focal point is a cognitive-accessibility bonus: one task per screen.
- Reduce Motion: fade is enough.

## Prohibitions
Ornamental elements, multi-color accents, complex textures, exaggerated motion, cramped layouts.

## Self-check list
- [ ] Exactly one visual focal point per screen?
- [ ] Primary color unique and ≤30% coverage?
- [ ] Zero ornament (textures/glass/multi-color = residue)?
- [ ] Whitespace ample?
- [ ] Hierarchy built from whitespace and size contrast (not stacked shadows)?

## Suitable for
Productivity tools, editors, premium sites, data panels, efficiency apps.
