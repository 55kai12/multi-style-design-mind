# S11 · European Elegance

Keywords: neutral colors, cream/light-gray/dark-brown, gold accents, symmetry, elegance, simplified classic.
Axioms: noise reduction is sophistication; restraint is luxury; symmetry is dignity; detail is quality.
Decision order: dignified register → symmetric composition → detail linework → materials (matte/fabric/metal) → motion (ceremony).

## Color system
- Cream #F5F0E8 primary.
- Light gray #E5E0D8 support.
- Dark brown #3A2E24 depth.
- Gold #C9A961 accent ≤5%.
- Ratio: cream 50%, light gray 25%, dark brown 20%, gold 5%.
- Classic triad: cream + gold + dark brown (7:2:1).
- Dark mode: dark-brown base + cream text + gold accents.
- Prohibited: saturated clashes, neon.

## Typography
- Headlines: serif (Cormorant / Playfair Display / Didot).
- Body: sans (Inter / SF Pro) or serif.
- Sizes: headlines 32/40/56pt, body 16/18pt.
- Fine weights: headlines Light/Regular, body Regular.
- Tracking: headlines 1–3, body 0.5.
- Prohibited: heavy black type, gimmicky fonts.

## Shape & layout
- Symmetric layout.
- Refined frames, moderate radii.
- Simplified classical elements (ornate moldings reduced to hairlines).
- Spacing: 16/24/32/48/64/96.
- Generous whitespace, sense of dignity.

## Material
- Matte stone textures, fine fabric weave, metallic edging.
- Weak frosted glass acceptable in modern-European takes.
- Avoid strong reflections.
- Prohibited: neon, heavy glass.

## Shadow
- Soft: y 8 blur 24 opacity 0.08.
- Prohibited: hard shadows, heavy projections.

## Components
- Buttons: gold stroke or dark-brown fill + small radius.
- Cards: cream base + gold hairline border.
- Inputs: hairline + cream base.
- Navigation: symmetric + serif headline.
- Modals: rounded + gold border.

## Motion
- Graceful and slow: fades, subtle scaling, parallax. 300–600ms.
- Ceremonial but not excessive.
- Prohibited: harsh, fast, exaggerated.

## Effects
- Golden shimmer, fabric texture, stone texture, crossfades.

## Implementation

### Web / CSS
- Type: Playfair Display + Cormorant + Inter (Google Fonts, free; Didot is licensed — don't embed).
- Gold hairline: `border: 1px solid #C9A961;` double line via pseudo-element 3px out; metallic shimmer `linear-gradient(90deg, #C9A961, #E5D9A8, #C9A961)` as divider backgrounds.
- Fabric/stone textures: low-opacity texture images, `opacity ≤ 0.05`, `mix-blend-mode: multiply`.
- Motion: `opacity + scale(0.98 → 1)` 400–600ms ease-out; parallax ≤8px.
- Symmetry: grid or flex centered composition; pseudo-elements complete left-right symmetric ornament lines.

### SwiftUI
- Serif: `.fontDesign(.serif)` (system serif approximation) or bundle Cormorant.
- Gold gradient stroke: `.overlay(RoundedRectangle(cornerRadius: 8).stroke(LinearGradient(colors: [#C9A961, #E5D9A8, #C9A961], startPoint: .topLeading, endPoint: .bottomTrailing), lineWidth: 1))`.
- Texture: asset image `.opacity(0.05)` + `.allowsHitTesting(false)`.

### Compose mapping
| Concept | Equivalent | Notes |
|---|---|---|
| Serif headlines | FontFamily.Serif or bundle Cormorant/Playfair (OFL license, commercial OK) | — |
| Gold gradient stroke | Modifier.border(1.dp, Brush.linearGradient(gold 3-stop), shape) | — |
| Double frame | Box with two border layers (inner 1dp gold + outer 1dp gold, 3dp padding apart) | — |
| Fabric texture | Texture asset + Image(alpha = 0.05f) | — |
| Motion | tween(400–600, FastOutSlowInEasing), scale 0.98→1 | — |

## Accessibility
- Dark brown #3A2E24 on cream #F5F0E8 ≈ 11:1, passes.
- **Gold #C9A961 on cream ≈ 2.3:1 — gold is for decorative frames and hairlines only, never as text color**; golden shimmer text effects are banned for the same reason.
- Serif headline Light weights get muddy on low-DPI screens; use Light only at ≥32pt; body always Regular.
- Slow ceremonial motion must be skippable: Reduce Motion → direct reveal; parallax ≤8px to prevent dizziness.

## Prohibitions
Saturated clashes, neon, brutalism, excessive ornament.

## Self-check list
- [ ] Gold ≤5% and never as text color?
- [ ] Symmetric composition (ornament lines completed on both sides)?
- [ ] Classical elements reduced to hairlines (no molding pile-ups)?
- [ ] Motion skippable, parallax ≤8px?
- [ ] No crossover (saturation/neon/hard shadows = S4/S9 residue)?

## Suitable for
Luxury goods, premium hotels, jewelry & watches, lifestyle brands, corporate sites.
