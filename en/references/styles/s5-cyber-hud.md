# S5 · Cyber HUD

Keywords: dark, neon, data, scanlines, HUD, density.
Axioms: information is the interface; light is status; density is professionalism; glitch is authenticity.
Decision order: information-density architecture → data hierarchy → light as status → motion (scan/pulse/glitch).

## Color system
- Dark backgrounds #05070A / #0B1020 / #0F1626.
- Neon cyan #00F0FF, magenta #FF00E5, neon green #00FF88, warning orange #FF6B00, danger red #FF2D55.
- Text: cyan-white #E0F7FF primary, rgba(224,247,255,0.6) secondary.
- Glow: 0 0 12–32px neon color.
- Dark mode: it's already dark.

## Typography
- Families: mono (JetBrains Mono / SF Mono / IBM Plex Mono) + sans (Inter / Rajdhani).
- Numbers: monospaced, tracking 1–2.
- Headlines: 24/32/40pt, weight 600–700, all-caps.
- Body: 14/16pt, weight 400.
- Prohibited: serif, rounded fonts.

## Shape & layout
- Radius: 0–4, mostly square.
- Cut corners, corner brackets, 1px strokes.
- Spacing: 4/8/12/16/24/32.
- High density, information-rich.
- Grid: fine grid background.

## Material
- Translucent dark panels + fine grid.
- Weak frosted glass allowed but must be dark.
- Prohibited: light glass, soft materials.

## Shadow
- Glow replaces shadows: 0 0 12–32px neon color.
- Prohibited: soft shadows.

## Components
- Buttons: 1px stroke + glow + hover boost.
- Cards: dark panel + fine grid + corner brackets.
- Inputs: mono + 1px stroke + focus glow.
- Navigation: top HUD bar + status indicators.
- Modals: dark panel + scanlines.

## Motion
- Scan, typewriter, data roll-up, pulse, glitch flicker. 150–600ms, mostly linear.
- Prohibited: soft springs, slow transitions.

## Effects
- Scanlines, noise, glitch displacement, radar, energy bars, data streams.

## Implementation

### Web / CSS (this style's home turf)
- Glow: `text-shadow: 0 0 12px #00F0FF; box-shadow: 0 0 24px rgba(0,240,255,0.5);`
- Scanlines: `background: repeating-linear-gradient(0deg, rgba(0,240,255,0.04) 0 1px, transparent 1px 3px);`
- Fine grid: bidirectional `repeating-linear-gradient`, rgba(0,240,255,0.06).
- Glitch: clip-path + transform frame animation 150–300ms, or SVG feTurbulence + feDisplacementMap.
- Corner brackets: pseudo-elements drawing L-shapes (2px neon border-top + border-left).
- Type: JetBrains Mono, Rajdhani (Google Fonts, free).
- Performance: limit glow layers; `will-change: transform` only on animating elements; scanlines as background, not DOM layers.

### SwiftUI
- Glow: `.shadow(color: Color(hex: "#00F0FF").opacity(0.6), radius: 8)` stacked twice (near-small, far-large).
- Scanline: TimelineView-driven LinearGradient mask; watch power, stop the clock when idle.
- Cut corners: custom Shape (Path octagon).

### Compose mapping
| Concept | Equivalent | Notes |
|---|---|---|
| Mono font | FontFamily.Monospace or bundle JetBrains Mono | Tabular figures for numbers |
| Glow | drawBehind double draw: blurred layer (blur 8–16) + solid layer | Compose has no text-shadow |
| 1px stroke | Modifier.border(1.dp, Color(0xFF00F0FF)) | — |
| Cut corners | Custom Shape (Path) | — |
| Scan/pulse | rememberInfiniteTransition + linear tween | Disable under Reduce Motion |

## Accessibility
- **Photosensitive safety is a hard constraint**: glitch flicker must stay < 3Hz (WCAG 2.3.1), and provide a "disable flicker/glitch" switch.
- Glow never substitutes for contrast: #E0F7FF on #05070A ≈ 16:1 passes; neon cyan #00F0FF as body text needs measuring (≈10:1, acceptable); magenta #FF00E5 is accent-only, never body text.
- Secondary rgba(224,247,255,0.6) on dark ≈ 6:1, fine for captions; anything fainter violates.
- Reduce Motion: scan / typewriter / data-roll / glitch all replaced with static status display or a single fade.

## Prohibitions
Soft rounded corners, warm colors, large whitespace, Apple-style restraint, elegant fonts.

## Self-check list
- [ ] Dark background, glow instead of shadow (no soft drop shadows)?
- [ ] Flicker <3Hz with an on/off switch?
- [ ] Neon as body text measured ≥4.5:1?
- [ ] Reduce Motion disables scan/glitch motion?
- [ ] Density serves professionalism, not clutter?
- [ ] No crossover (soft shadows / large radii / warm colors = S1/S6 residue)?

## Suitable for
Monitoring dashboards, game UI, AI tools, sci-fi concepts, data visualization.
