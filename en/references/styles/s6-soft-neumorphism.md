# S6 · Soft Neumorphism

Keywords: monochrome, raised/sunken, low contrast, soft dual shadows, physical feel.
Axioms: light comes from the top-left; material is solid; pressing is deformation; softness is comfort.
Decision order: single base color → light-source setup (top-left, globally unique) → raised/sunken dual shadows → press deformation.

## Color system
- Single base: #E0E5EC / #E8EDF2 / #DFE6EE.
- Elements vary within the same hue: light #FFFFFF, dark #A3B1C6.
- Text: #4A5568 primary, #718096 secondary.
- Accent: soft blue #5B8DEF or soft green #48BB78.
- Dark mode: base #2D3748, dark #1A202C, light #4A5568.
- Prohibited: high contrast, pure black, neon.

## Typography
- Families: Nunito / SF Pro Rounded / Quicksand.
- Sizes: headlines 24/32/40pt, body 16/18pt.
- Weight: 600–700 headlines, 400 body.
- Rounded, friendly.

## Shape & layout
- Radius: 12–24.
- Spacing: 16/24/32/48.
- Elements share the background color.
- Loose layout, generous whitespace.

## Material
- No frosted glass.
- Dual shadows: light -6/-6 blur 12 rgba(255,255,255,0.8), dark 6/6 blur 12 rgba(163,177,198,0.6).
- Inner shadows for sunken surfaces.

## Shadow
- Soft, same-hue; pure black hard shadows banned.
- Raised: dual outer shadows.
- Sunken: dual inner shadows.

## Components
- Buttons: raised + sunken on press.
- Cards: raised + radius.
- Inputs: sunken + inner shadow.
- Navigation: raised bar.
- Modals: raised + soft shadow.

## Motion
- Press-in, spring-back, soft transitions. 150–300ms.
- Prohibited: harsh displacement, flicker.

## Effects
- Inner shadow, subtle highlight.

## Implementation

### Web / CSS
- Raised: `box-shadow: -6px -6px 12px rgba(255,255,255,0.8), 6px 6px 12px rgba(163,177,198,0.6);`
- Sunken: same values with `inset`. Press via `:active` switching outer→inner shadow, `transition: box-shadow 0.2s ease;`
- Type: Nunito / Quicksand (Google Fonts, free).
- Shadow colors must derive from the base color (base #E0E5EC → dark shadow from #A3B1C6 family); recompute the whole shadow set whenever the base changes.

### SwiftUI
- Dual shadow stack: `.shadow(color: .white.opacity(0.8), radius: 6, x: -6, y: -6)` + `.shadow(color: Color(red: 0.64, green: 0.69, blue: 0.78).opacity(0.6), radius: 6, x: 6, y: 6)` (modifier order affects compositing).
- Press-in: `@State` toggling raised/sunken parameters, `.animation(.easeOut(duration: 0.2))`.

### Compose mapping
| Concept | Equivalent | Notes |
|---|---|---|
| Dual outer shadow | drawBehind: two offset+blur rounded rects (light -6dp / dark +6dp) | Compose has no dual box-shadow — this is the costliest style to build in Compose |
| Sunken inner shadow | Same method, reversed + clip | Or degrade to a color change |
| Press deformation | interactionSource + animateFloatAsState toggling shadow direction | tween(200, FastOutSlowInEasing) |
| Rounded type | Bundle Nunito or FontFamily.SansSerif | — |

Be honest: Neumorphism is significantly more expensive than other styles in Compose. If the budget is tight, simplify to "raised = light stroke + faint shadow".

## Accessibility (highest-risk style; the risk must be flagged proactively)
- Same-hue low contrast is the style's essence and its hard flaw: primary text #4A5568 on #E0E5EC ≈ 7:1, passes; secondary #718096 ≈ 4.2:1, barely passes — nothing fainter.
- Any state expressed only by shadows (pressed/selected/disabled) is invisible to low-vision users — always add color/icon/text redundancy.
- **A "high-contrast mode" fallback is mandatory**: strokes + solid fills replace shadow semantics.
- Reduce Motion: press-in degrades to a color change.

## Prohibitions
High contrast, pure black strokes, neon, glass, hard shadows.

## Self-check list
- [ ] Light source consistently top-left (all element shadows agree)?
- [ ] Same-hue only (pure black strokes / neon = S4/S5 residue)?
- [ ] Contrast risk flagged and high-contrast fallback provided?
- [ ] States expressed by more than shadows?
- [ ] Shadow colors recomputed when the base color changes?

## Suitable for
Smart home, health, meditation product concepts, soft-style apps.
