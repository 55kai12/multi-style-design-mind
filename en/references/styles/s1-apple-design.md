# S1 · Apple Design Mind (Native iOS)

Keywords: content-first, hierarchy, restraint, material depth, real physics, high fidelity, Liquid Glass.
Axioms: content is the interface; hierarchy is space; motion is causality; material is depth; feedback is trust; restraint is sophistication; accessibility is design.
Decision order: information architecture → visual hierarchy → material → motion → effects. Never start from effects; never add frosted glass before thinking about hierarchy.

## Color system
- Semantic colors first: label / secondaryLabel / tertiaryLabel / quaternaryLabel.
- Backgrounds: systemBackground / secondarySystemBackground / tertiarySystemBackground / systemGroupedBackground / secondarySystemGroupedBackground.
- Fills: systemFill / secondarySystemFill / tertiarySystemFill / quaternarySystemFill.
- Separators: separator / opaqueSeparator.
- Accent: tint (default systemBlue #007AFF), only for key actions.
- System colors: systemRed #FF3B30, systemOrange #FF9500, systemYellow #FFCC00, systemGreen #34C759, systemTeal #5AC8FA, systemBlue #007AFF, systemIndigo #5856D6, systemPurple #AF52DE, systemPink #FF2D55.
- Dark mode: backgrounds #000000 / #1C1C1E / #2C2C2E; text auto-inverts.
- High contrast: increase stroke and text contrast under Increase Contrast.
- Prohibited: abused high-saturation clashes, abused colored glass, gradient text.

## Typography
- Families: SF Pro Display (≥20pt), SF Pro Text (<20pt).
- Sizes: Large Title 34 Bold, Title1 28 Regular, Title2 22 Regular, Title3 20 Regular, Headline 17 Semibold, Body 17 Regular, Callout 16 Regular, Subheadline 15 Regular, Footnote 13 Regular, Caption1 12 Regular, Caption2 11 Regular.
- Line height: Body 22, Title 34/41, Caption 16.
- Tracking: large titles -0.4 to -0.8, body 0.
- Must support Dynamic Type up to AX5.
- Numbers use the monospacedDigit variant.
- Prohibited: gimmicky fonts, art text, more than 2 mixed typefaces.

## Shape & layout
- 8pt grid. Spacing: 4/8/12/16/20/24/32/40/48/64.
- Safe areas: top 59pt (with Dynamic Island), bottom 34pt.
- Card radius 16–28, buttons 10–14 or capsule, Sheet top 10–16 (continuous curvature, avoid harsh right angles).
- Grouped lists: insetGrouped, side margins 16–20, group spacing 32–36.
- Content margins: 16 or 20.
- Icons: SF Symbols, unified weight (regular/medium/semibold), sizes (17/20/24/28), hierarchy (hierarchical/palette/multicolor). No clashing custom icons.
- Touch: minimum 44x44pt. Key actions thumb-reachable; provide haptic feedback.
- Layout: safe areas, optical alignment, edge-to-edge content, grouped lists, large titles, scroll edge effects.

## Material system

### Material family
- **Material**: classic translucent blur, used to establish hierarchy.
- **Vibrancy**: text/icon effect on glass, letting content "show through" from the background.
- **Liquid Glass** (iOS 26+): the new glass language — lensing, refraction, edge highlights, adaptive tinting, interactive morphing. For system-level controls and floating actions only, never full-screen.

### Material types and usage
| Material | Translucency | Usage |
|---|---|---|
| ultraThinMaterial | Most translucent | Temporary controls over photos/media, short-lived HUDs. Background must be simple or scrimmed |
| thinMaterial | Light | Search suggestions, floating chips, lightweight cards |
| regularMaterial | Standard | Sheets, popovers, sidebars, floating cards |
| thickMaterial | Low | High-readability panels, settings groups, long-reading overlays |
| bar / chrome | — | Navigation bars, tab bars, toolbars. Keeps content readable while scrolling |
| Liquid Glass | Interactive | Floating buttons, Control Center, Dynamic Island, system actions. Supports morph, press, focus |

### Material decision tree (run before every use of glass)
1. Does this layer float above content? No → no frosted glass.
2. Is it a system bar? Yes → bar / chrome.
3. High readability needed? Yes → regular / thick; no → thin / ultraThin.
4. Is the background busy, bright, high-contrast? Yes → add scrim + vibrancy.
5. iOS 26+ and interactive morphing needed? Yes → Liquid Glass.
6. Reduce Transparency enabled? Yes → fall back to opaque systemBackground / secondarySystemBackground.

### Frosted glass rules
- Max 1–2 glass layers per screen; never glass-on-glass; floating layers only (NavigationBar, TabBar, Toolbar, Sheet, Popover, ContextMenu, Widget, FAB, search bar).
- Never for: body backgrounds, large scrolling areas, behind low-contrast text, per-row blur in lists.
- Text on glass uses vibrancy semantic colors; contrast ≥4.5:1.
- Continuous-curvature corners; outer radius = inner radius + padding.
- Top 1px highlight opacity 0.20–0.40; bottom 1px dark edge 0.08–0.15; outer shadow y 8–24, blur 24–60, opacity 0.06–0.18; scrim black 0.12–0.28 on busy backgrounds.
- Dark mode glass is darker and thinner (avoid gray fog); light mode brighter (avoid dirty gray). Tinting: low-saturation adaptive tint only, opacity 0.08–0.16.
- On scroll, nav bar transitions from transparent to bar material; material fades in as large title collapses.
- Sheet push-up: background scales 0.92–0.96 + blur + dim; reverses on pull-down dismiss.
- Pressed glass controls: scale 0.96–0.98, brighter highlight, light haptic. Liquid Glass interactions (press/focus/morph/drag) must be interruptible and reversible.
- Performance: prefer system materials, monitor offscreen rendering, never blur per list row, target 60/120fps.

## Shadow & hierarchy
- Soft shadows: y 8–24, blur 24–60, opacity 0.06–0.18.
- Hierarchy via material, blur, opacity, parallax — not borders.
- Prohibited: heavy shadows, thick borders, neon.

## Components
- NavigationBar: large title + scroll collapse + toolbarBackground(.ultraThinMaterial).
- TabBar: bottom-fixed, icon + label, tint for selected state.
- Sheet: grabber + detents + background scale 0.92–0.96 + blur/dim.
- Alert: centered card + frosted glass + two buttons.
- ContextMenu: long-press + frosted glass + preview zoom.
- List: insetGrouped + separators + swipe actions.
- Card: radius + material + soft shadow.
- Toggle / Segmented / Picker: native controls first.
- Widget / Dynamic Island / Live Activity: system-level extensions.

## Transitions & motion
- Default spring: response 0.35–0.55 / damping 0.75–0.9.
- Fast interactions: response 0.25–0.35 / damping 0.82–0.9.
- Push/Pop: hierarchical slide + slight fade/scale, edge-back gesture support.
- Sheet: bottom push-up + radius + grabber + background scale + pull-down dismiss + detents.
- FullScreen: fade/push-up, minimal movement.
- Hero / Matched Geometry: shared-element morphing, zoom from card to detail.
- Timing: enter 250–400ms, exit 200–300ms, list stagger 20–50ms. Deeper levels are slower.
- Physics: velocity projection, rubber-banding, damping, slight overshoot. Must track the finger, be interruptible and reversible.
- Press: scale 0.96–0.98, opacity 0.9, light haptic.
- Reduce Motion: degrade to crossfade or instant switch.

## Effects
- Soft gradients, Mesh Gradient, glass highlights, edge light, low-saturation noise, parallax, symbol animations.
- Particles only for celebration or status, never persistent.
- Performance: prefer system materials, no per-row blur in lists, target 60/120fps.

## Implementation

### SwiftUI (first)
- Materials: .ultraThinMaterial / .thinMaterial / .regularMaterial / .thickMaterial / .bar / .chrome.
- System bars: .toolbarBackground(.ultraThinMaterial, for: .navigationBar) + .toolbarBackground(.visible, for: .navigationBar).
- Glass container: RoundedRectangle(cornerRadius: 24, style: .continuous).fill(.regularMaterial).
- Fallback: @Environment(\.accessibilityReduceTransparency) → Color(.secondarySystemBackground).
- UIKit: UIVisualEffectView + UIBlurEffect(style: .systemThinMaterial) + UIVibrancyEffect.
- iOS 26+: .glassEffect / GlassEffectContainer (per current SDK).

### Compose mapping (borrowing the Apple aesthetic on Android)
| iOS concept | Compose equivalent | Notes |
|---|---|---|
| Material (ultraThin–thick) | Modifier.blur() background + translucent surface overlay, or RenderEffect.createBlurEffect (API 31+) | No system vibrancy; never blur per list row — use a pre-blurred background image |
| Semantic colors | Custom ColorScheme (Material 3), label/surface/separator sets per light/dark | Low-saturation neutral palette to mimic systemGray series |
| SF Pro | Default Roboto/SansSerif or a commercially licensed lookalike | SF Pro can't be bundled (license) |
| SF Symbols | Material Symbols / one unified icon set, unified weight & size | Keep a single weight hierarchy |
| Spring motion | spring(dampingRatio = 0.75–0.9f, stiffness); response 0.35s ≈ stiffness ≈ 300–350 | animateFloatAsState / AnimatedContent |
| Reduce Motion | Read Settings.Global.TRANSITION_ANIMATION_SCALE or in-app toggle | Degrade to tween(fade) |
| Continuous-curvature corners | Custom smooth corner shape (cubic Bézier approximating a superellipse) | Plain RoundedCornerShape acceptable, depends on fidelity needs |
| Large title collapse | CollapsingTopBar (custom NestedScrollConnection) | Material fades in on scroll |

### Web / HTML mapping
- Material: backdrop-filter: blur(20px) saturate(1.8) + layered rgba(...) backgrounds; watch offscreen-render cost, avoid large/nested layers.
- Fallbacks: @media (prefers-reduced-motion: reduce) disables motion; @supports not (backdrop-filter: blur(1px)) falls back to opaque backgrounds.
- Springs: approximate with CSS transitions (e.g. cubic-bezier(0.32, 0.72, 0, 1)); complex springs via Web Animations API or a motion library.

## Accessibility (default, not a patch)
- Dark mode: all colors/materials defined for both appearances; glass darker and thinner in dark.
- Dynamic type: text scales with system settings; never hardcode pt for fixed layouts; up to AX5.
- VoiceOver / TalkBack: every interactive element has a semantic label; focus order matches visual order.
- Reduce Motion: all motion disableable or degraded to crossfade.
- Reduce Transparency: all frosted glass degradable to opaque materials.
- Contrast: body ≥ 4.5:1, large type ≥ 3:1.

## Prohibitions
Neon, heavy shadows, thick borders, gimmicky fonts, full-screen frosted glass, glass-on-glass, abused colored glass, low-contrast text on glass, pointless showing off, ignoring Reduce Transparency.

## Self-check list
- [ ] Content-first?
- [ ] Motion disableable (Reduce Motion fallback)?
- [ ] Touch targets ≥ 44pt?
- [ ] Semantic colors used?
- [ ] Native (prefer system behavior, no invented interactions)?
- [ ] 120fps / 60fps?
- [ ] Frosted glass only on floating layers?
- [ ] Glass-on-glass avoided?
- [ ] Readability ≥ 4.5:1?
- [ ] All frosted glass degradable to opaque?

## Suitable for
iOS, iPadOS, watchOS, macOS, system-level products, high-fidelity prototypes; Android projects can borrow the aesthetic via the Compose mapping.
