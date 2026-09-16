# S9 · P5R Style (Persona 5 Royal)

Keywords: pure red/black/white, asymmetry, jagged edges, graffiti, comic dialogue, kinetic energy.
Axioms: clash is tension; maximal flamboyance, maximal irreverence; the UI is a performance.
Decision order: content → color-block & jagged composition → asymmetric tension → kinetic motion (performance layer). The material layer does not exist.

## Color system
- Pure red #E60012 primary.
- Pure black #000000.
- Pure white #FFFFFF.
- A little yellow #FFCC00 as seasoning.
- Ratio: red 50%, black 30%, white 15%, yellow 5%.
- Dark mode: same logic, black/white inverted.
- Prohibited: low saturation, soft colors.

## Typography
- Latin: DIN Condensed Bold / Bebas Neue.
- CJK: heavy Gothic (Source Han Sans Bold).
- Handwritten: brush style (used sparingly).
- Sizes: headlines 40/56/72pt, body 16/18pt.
- Weight: 900 or Bold.
- Tilted, rotated, offset.
- Prohibited: light weights, serif, elegant faces.

## Shape & layout
- Angled symmetry, jagged edges, torn effects.
- Comic dialogue balloons, command trees wrapping around characters.
- Built from color blocks + text.
- Radius: 0–8 or square.
- Asymmetric, dynamic, high-tension layouts.

## Material
- No frosted glass.
- Flat blocks, vector graphics, graffiti, halftone dots.
- Prohibited: glass, soft materials.

## Shadow
- Hard shadow, no blur, offset 4–8px, pure black.
- Prohibited: soft shadows.

## Components
- Buttons: jagged edge + pure red + hard shadow + hover shift.
- Cards: angled + flat color + graffiti.
- Inputs: thick border + solid fill.
- Navigation: asymmetric + high contrast.
- Modals: comic dialogue balloon + flat color.

## Motion
- Dense screen-transition choreography, popping text, fast harsh displacement, jitter allowed. 80–300ms.
- Prohibited: soft transitions, slow animation.

## Effects
- Graffiti, jagged tearing, halftone dots, color-block flips, popping text, dynamic indicator stripes.

## Implementation

### Web / CSS (best fit)
- Jagged edges: `clip-path: polygon(...)` or SVG paths for tears; cut corners `polygon(8px 0, 100% 0, 100% calc(100% - 8px), calc(100% - 8px) 100%, 0 100%, 0 8px)`.
- Tilt: `transform: rotate(-2deg) skewX(-3deg);` (container-level; rotate text back for readability).
- Popping text: enter at `scale(1.3) → 1` + rotate spring-back, 80–150ms with `steps()` or a strong spring.
- Halftone: `background-image: radial-gradient(#000 1px, transparent 1px); background-size: 4px 4px; opacity: 0.08;`
- Type: Bebas Neue (Google Fonts, free) instead of DIN Condensed (licensed); Chinese in Source Han Sans Bold.
- Performance: animate only transform/opacity; use clip-path, not images, for jagged edges.

### SwiftUI
- Angled blocks: custom Shape (Path); rotation `.rotationEffect(.degrees(-2))`; skew needs a custom GeometryEffect.
- Popping text: `.scaleEffect` + `.spring(response: 0.25, dampingFraction: 0.5)`.
- Torn edges: SVG converted to assets or masks.

### Compose mapping
| Concept | Equivalent | Notes |
|---|---|---|
| Jagged/cut corners | Custom Shape (Path polygon) | — |
| Tilt/offset | Modifier.graphicsLayer { rotationZ = -2f; transformOrigin } | Skew via Matrix |
| Hard shadow | drawBehind offset solid-black layer (same as S4) | Don't use elevation |
| Popping text | animateFloatAsState spring(dampingRatio = 0.4f) | 80–150ms |
| Color-block flip | Crossfade / AnimatedContent + tween(100) | — |
| Halftone dots | Canvas dot pattern or texture asset | — |

## Accessibility
- **Red background with white text #E60012/#FFF ≈ 4.0:1 — passes 3:1 only for large type (≥24pt Bold); small body text must switch to black background with white text (≈ 18:1)**. Hard constraint, not a suggestion.
- Yellow #FFCC00 is for blocks and strokes only, never text color (≈ 1.6:1 on white).
- Dense kinetic motion is the worst case for photosensitivity and Reduce Motion: flicker <3Hz; provide a "skip the performance" fallback — transition choreography jumps straight to content (game UIs especially; cf. P5R's own fast-forward setting).
- Even in asymmetric layouts, Tab/focus order must follow logical order.

## Prohibitions
Soft rounded corners, low saturation, restraint, breathing whitespace, elegant fonts.

## Self-check list
- [ ] Pure red/black/white/yellow only, zero low saturation?
- [ ] All shadows hard, no blur?
- [ ] Small body text kept off red backgrounds?
- [ ] Performance motion skippable, flicker <3Hz?
- [ ] Focus/Tab order logical (asymmetric ≠ unordered)?
- [ ] No crossover (breathing whitespace / rounded cards / glass = S1/S7/S3 residue)?

## Suitable for
Game UI, streetwear, music products, creative event pages, Gen-Z products.
