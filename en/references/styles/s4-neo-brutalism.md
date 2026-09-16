# S4 · Neo-Brutalism

Keywords: thick black borders, hard shadows, saturated colors, sticker feel, deliberate roughness, attitude.
Axioms: clash is tension; bluntness is attitude; rules are made to be broken; imperfection is real.
Decision order: content → saturated color-block zoning → thick borders defining edges → hard shadows creating depth → motion.

## Color system
- Saturated clashes: yellow #FFE600, black #000000, pink #FF2D95, cyan #00E5FF, green #00FF88, orange #FF6B00.
- Solid colors, no gradients.
- Ratio: black 40%, white 20%, primary 30%, secondary 10%.
- Dark mode: keep saturation, switch background to dark gray #1A1A1A.

## Typography
- Families: ultra-bold sans (Archivo Black / Space Grotesk / Inter Black) or mono (JetBrains Mono / Space Mono).
- Sizes: headlines 40/56/72pt, body 16/18pt.
- Weight: 900 or Bold.
- All-caps allowed, tracking 1–2.
- Prohibited: light weights, serif, elegant faces.

## Shape & layout
- Radius: 0–8.
- Borders: 2–4px solid black.
- Spacing: 8/16/24/32/48.
- Layout may be deliberately offset, overlapped, tilted 1–3°.
- The grid may be broken.

## Material
- No frosted glass.
- Halftone dots, stickers, pixel textures, hand-drawn doodles allowed.
- Backgrounds solid or coarse grid.

## Shadow
- Hard shadow, zero blur, offset 4–8px, pure black.
- Prohibited: soft shadows, gradients.

## Components
- Buttons: thick black border + hard shadow + hover shift.
- Cards: thick black border + hard shadow + sticker feel.
- Inputs: thick black border + solid fill.
- Navigation: thick black border + saturated.
- Modals: thick black border + hard shadow.

## Motion
- Harsh, fast, displacement-based. 80–200ms, linear or strong spring.
- Offsets, jitters, color-block flips allowed.
- Prohibited: soft transitions, slow animation.

## Effects
- Stroke offset, hover shift, color-block flip, halftone dots.

## Implementation

### Web / CSS (most natural here)
- Border: `border: 3px solid #000; border-radius: 0–8px;`
- Hard shadow: `box-shadow: 6px 6px 0 #000;` (**no blur**)
- Hover shift (press feel): `transform: translate(2px, 2px); box-shadow: 2px 2px 0 #000;`
- Type: Archivo Black / Space Grotesk (Google Fonts, free).
- Halftone: `background-image: radial-gradient(#000 1px, transparent 1px); background-size: 6px 6px; opacity: 0.1;`
- Motion: `transition: transform 0.12s linear;`

### SwiftUI
- Thick border: `.overlay(RoundedRectangle(cornerRadius: 4).stroke(Color.black, lineWidth: 3))`.
- Hard shadow: system `.shadow` has blur — use `.background(Color.black.offset(x: 6, y: 6))` layering instead.
- Motion: `.animation(.linear(duration: 0.12))` or strong spring `.spring(response: 0.2, dampingFraction: 0.5)`.

### Compose mapping
| Concept | Equivalent | Notes |
|---|---|---|
| Thick border | Modifier.border(3.dp, Color.Black, RoundedCornerShape(4.dp)) | — |
| Hard shadow | drawBehind: offset 6.dp solid-black rounded rect; or offset Box layer | Don't use elevation/shadow (has blur) |
| Color-block flip | AnimatedContent + tween(120, LinearEasing) | — |
| Tilt/offset | Modifier.graphicsLayer { rotationZ = -2f } | ≤3° |
| Halftone dots | Texture asset or Canvas dot pattern | — |

## Accessibility
- Saturation clashes still need spot checks: yellow #FFE600 with black text ≈ 14:1, safe; **yellow background with white text, and white background with yellow text, are banned**.
- Fast harsh motion still requires a Reduce Motion fallback: displacement animations degrade to instant state switches.
- Tilt ≤3° and must not cover tap areas; touch targets stay ≥44pt despite the sticker aesthetic.
- All-caps text keeps letter-spacing 1–2 for readability; never all-caps long paragraphs.

## Prohibitions
Soft shadows, delicate gradients, refined frosted glass, low saturation, elegant fonts.

## Self-check list
- [ ] All shadows blur-free, pure black, offset 4–8px?
- [ ] Borders 2–4px solid black?
- [ ] Zero gradients, zero glass (soft shadow / blur = S1/S3 residue)?
- [ ] Tilts ≤3° and not covering touch targets?
- [ ] Reduce Motion fallback present?
- [ ] Text contrast measured per color combination?

## Suitable for
Creative agencies, event pages, streetwear, indie products, Gen-Z brands.
