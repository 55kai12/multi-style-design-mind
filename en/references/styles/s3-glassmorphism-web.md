# S3 · Glassmorphism Web

Keywords: colorful gradients, glass cards, large radii, glow borders, translucency, ambience.
Axioms: the background is ambience; glass is hierarchy; light is guidance; translucency is modern.
Decision order: background ambience → glass hierarchy → light guidance → motion.

## Color system
- Background gradients: purple-blue #667EEA→#764BA2, pink-orange #FF6B6B→#FFA07A, teal-green #43E97B→#38F9D7.
- Glass fill: rgba(255,255,255,0.08–0.18).
- Border: 1px rgba(255,255,255,0.18–0.35).
- Text: white #FFFFFF primary, rgba(255,255,255,0.7) secondary.
- Accent: bright cyan #00E5FF or hot pink #FF2D95.
- Inner glow: inset 0 1px 0 rgba(255,255,255,0.3).
- Dark mode: deeper gradients + lower opacity.

## Typography
- Families: Inter / SF Pro / Manrope / Poppins.
- Headlines: 32/40/48pt, weight 600–700.
- Body: 16/18pt, weight 400–500, line-height 1.6.
- Tracking: 0 to 0.5.
- Prohibited: serif faces, gimmicky fonts.

## Shape & layout
- Radius: cards 20–32, buttons capsule, inputs 12–16.
- Spacing: 16/24/32/48/64.
- Grid: 12 columns, gutter 24.
- Generous whitespace, card gaps 24–32.

## Material
- backdrop-blur 16–40px.
- Background rgba(255,255,255,0.08–0.18).
- Border 1px rgba(255,255,255,0.18–0.35).
- Inner + outer glow optional.
- Prohibited: more than 2 stacked glass layers, full-screen blur that kills performance.

## Shadow
- Large and soft: y 20 blur 60 opacity 0.2.
- Colored shadow optional: 0 20 60 rgba(102,126,234,0.3).

## Components
- Buttons: capsule + glass + glowing border + hover lift.
- Cards: large radius + glass + inner glow.
- Inputs: glass + radius + focus glow.
- Navigation: top glass bar + blur.
- Modals: glass + large radius + background blur.

## Motion
- Floating, subtle parallax, hover lift, gradient flow. 200–500ms, ease-out.
- Hover: translateY(-4px) + shadow boost.
- Prohibited: harsh movement, flicker.

## Effects
- Light blobs, noise overlay, mouse-follow highlight, gradient displacement.
- Animated gradient backgrounds allowed.

## Implementation

### Web / CSS (this style's home turf)
- Glass: `backdrop-filter: blur(24px) saturate(160%); background: rgba(255,255,255,0.12); border: 1px solid rgba(255,255,255,0.25);`
- Inner glow: `box-shadow: inset 0 1px 0 rgba(255,255,255,0.3);` colored shadow: `0 20px 60px rgba(102,126,234,0.3)`.
- Background: `linear-gradient(135deg, #667EEA, #764BA2)` + light blobs (`position:absolute; border-radius:50%; filter: blur(80px); opacity:0.4`).
- Hover: `transform: translateY(-4px); box-shadow: 0 24px 68px rgba(102,126,234,0.4);`
- Performance budget: ≤3 backdrop-filter elements per screen, no nested glass; on low-end devices degrade to translucent solid cards.

### SwiftUI
- `.background(.ultraThinMaterial, in: RoundedRectangle(cornerRadius: 24, style: .continuous))`, with the colorful gradient at the very bottom for ambience.
- Note: iOS materials are inherently restrained — put ambience in the background gradient and blobs, don't tint the glass.

### Compose mapping
| Concept | Equivalent | Notes |
|---|---|---|
| backdrop-blur | `Modifier.graphicsLayer { renderEffect = RenderEffect.createBlurEffect(24f, 24f, TileMode.CLAMP).asComposeRenderEffect() }` | API 31+; fall back to translucent solid cards below |
| Glass fill | Translucent white surface (0.08–0.18 alpha) | — |
| Glowing border | Modifier.border(1.dp, Brush.linearGradient(white→transparent)) | — |
| Hover lift | animateFloatAsState + graphicsLayer translationY | — |

## Accessibility
- **The biggest risk is low-contrast white text**: primary text on glass must be measured at ≥4.5:1; if it fails, add a rgba(0,0,0,0.2) scrim behind the glass or raise fill opacity.
- Reduce Transparency: degrade glass cards to solid rgba(30,30,60,0.95), keeping radius and shadow.
- Reduce Motion: stop all floating / gradient-flow / mouse-follow animation; keep the static gradient.
- Dynamic type: glass card heights adapt to enlarged text; never clip with fixed heights.

## Prohibitions
Low-contrast white text, more than 2 stacked glass layers, full-screen blur that kills performance, pure black backgrounds.

## Self-check list
- [ ] Glass ≤2 layers, no glass-on-glass?
- [ ] White-text contrast measured ≥4.5:1 (scrim if needed)?
- [ ] backdrop-filter within performance budget (≤3 per screen)?
- [ ] Opaque fallback exists (Reduce Transparency)?
- [ ] No crossover (S1-style 1px highlights / semantic color system = residue)?

## Suitable for
SaaS landing pages, dashboards, Web3, product sites, AI tools.
