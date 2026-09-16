# S8 · Classic Chinese (Dignified)

Keywords: cultural restraint, vermilion/gold/ink/moon-white, azure/moon-white/ochre/ink-gray, symmetry, ink-wash, ceremony.
Axioms: splendor within stillness; color names are culture; restraint is sophistication; whitespace is artistic conception.
Decision order: cultural register (courtly vs Song literati — pick one, never mix) → symmetric layout → whitespace conception → material textures (ink-wash / rice paper / gold thread) → motion (ink bloom / scroll unfurl).

## Color system
### Courtly route
- Vermilion #C3272B primary.
- Gold #C9A961 accent.
- Ink #1C1C1C depth.
- Moon-white #F5F0E6 whitespace.
- Zisha (purple clay) #6B4A3A support.
### Song literati route
- Azure #7BA8A0 primary.
- Moon-white #F0EDE5 whitespace.
- Light-ochre (xiang) #D4B483 accent.
- Ink-gray #3A3A3A depth.
- Indigo-blue (dai) #4A5C6A support.
- Ratio: primary 40%, whitespace 40%, accent 15%, depth 5%.
- Prohibited: large-area abuse of saturated red-gold.

## Typography
- Headlines: Song/Ming serif (Source Han Serif / Founder Song-typeface) or calligraphy (used sparingly).
- Body: clean sans (Source Han Sans) or serif.
- Sizes: headlines 32/40/48pt, body 16/18pt.
- Tracking: headlines 2–4, body 0.5–1.
- Occasional vertical text as accent.
- Prohibited: large-area calligraphy fonts, hard-to-read faces.

## Shape & layout
- Symmetric layout, nine-square grid.
- Radius: 0–8 or square.
- Gold-thread borders, hairline ornaments.
- Spacing: 16/24/32/48/64.
- Generous whitespace, sense of conception.

## Material
- Ink-wash texture, rice-paper grain, gold-thread stroke, zisha base.
- Weak frosted glass acceptable in modern-Chinese interpretations.
- Prohibited: heavy glass, neon.

## Shadow
- Near-none or ink-bleed feel.
- Prohibited: heavy shadows, hard shadows.

## Components
- Buttons: gold-thread stroke or vermilion fill + small radius.
- Cards: rice-paper base + gold-thread border.
- Inputs: hairline + moon-white base.
- Navigation: symmetric + serif headline.
- Modals: scroll (unfurling) or rounded + gold-thread border.

## Motion
- Ink blooming, scroll unfurling, rain curtain, gradual reveal. Slow and dignified. 400–800ms.
- Prohibited: fast, harsh, exaggerated.

## Effects
- Ink bleed, gold leaf, rice-paper texture, rain curtain, cloud and mist.

## Implementation

### Web / CSS
- Type: Source Han Serif (Noto Serif SC) + Source Han Sans (Noto Sans SC) (Google Fonts, free); headlines `letter-spacing: 2–4px`.
- Gold thread: `border: 1px solid #C9A961` + pseudo-element outer hairline 4px away (double stroke).
- Rice-paper texture: SVG feTurbulence or low-opacity noise PNG, `opacity ≤ 0.06`.
- Motion: scroll unfurl `clip-path: inset(0 50%) → inset(0)` 600ms ease; ink bloom radial-gradient mask expansion 800ms.
- Gold leaf: linear-gradient(90deg, #C9A961, #E0D5A8, #C9A961) for hairlines or background-clipped text.

### SwiftUI
- Gold-thread stroke: `.overlay(RoundedRectangle(cornerRadius: 4).stroke(LinearGradient(colors: [#C9A961, #E0D5A8, #C9A961], ...), lineWidth: 1))`.
- Texture: rice-paper asset image overlaid `.opacity(0.06)`, `.allowsHitTesting(false)`.
- Motion: `.animation(.easeInOut(duration: 0.6))`; ink bloom via mask + radialGradient.

### Compose mapping
| Concept | Equivalent | Notes |
|---|---|---|
| Serif headlines | Bundle the Noto Serif SC font file (OFL license, commercial OK) | Don't rely on system fonts |
| Gold-thread stroke | Modifier.border(1.dp, Brush.linearGradient(gold 3-stop), shape) | — |
| Rice-paper texture | Texture asset + Image alpha 0.06 | — |
| Symmetric layout | Row/Column + Arrangement.Center + symmetric fixed padding | — |
| Vertical text accents | No native vertical text: hand-rolled per-character Column, or restrict to logo/inscriptions | Report the cost honestly; never vertical body text |
| Motion | tween(600–800, FastOutSlowInEasing), AnimatedVisibility | — |

## Accessibility
- Ink #1C1C1C on moon-white #F5F0E6 ≈ 14:1, passes; serif body starts at 16pt (small serif gets muddy).
- **Gold #C9A961 on moon-white ≈ 2.4:1 — gold is for decorative lines/borders only, never for body or headline text color**.
- Calligraphy only for logos/inscriptions (with accessible alternatives); body text must be serif or sans.
- Slow motion must still be skippable: Reduce Motion → direct reveal; scroll/ink effects must never block access to content.
- Decorative ink/textures marked `aria-hidden` / excluded from the semantic tree.

## Prohibitions
Large-area abuse of saturated red-gold, cheap dragon-phoenix motifs, symbol pile-ups, gimmicky motion.

## Self-check list
- [ ] Courtly/Song route picked — one, not mixed?
- [ ] Red-gold ratio within constraints (primary 40% / whitespace 40% / accent 15% / depth 5%)?
- [ ] Gold decorative-only, never text color?
- [ ] Cheap dragon-phoenix motifs and symbol pile-ups avoided?
- [ ] Motion dignified and skippable?
- [ ] No crossover (glassmorphism / neon / hard shadows = S3/S5/S4 residue)?

## Suitable for
Cultural brands, tea/wine/incense, premium gifts, museum exhibitions, Chinese lifestyle.
