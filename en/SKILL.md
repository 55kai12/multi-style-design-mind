---
name: multi-style-design-mind
description: A switchable design-style master system with 11 independent style modules: S1 Apple/iOS, S2 Swiss Minimal, S3 Glassmorphism Web, S4 Neo-Brutalism, S5 Cyber HUD, S6 Soft Neumorphism, S7 Ins Minimal, S8 Classic Chinese, S9 P5R style, S10 Minimalist, S11 European Elegance. Supports /style switching, weighted blending (e.g. s1+s3 7:3), /styles listing, /reset, /lock. Use this skill when the user asks for a specific design style (Swiss minimal, glassmorphism, brutalism, cyber HUD, neumorphism, Instagram style, Chinese classic, P5/Persona, European luxury, etc.) or asks to switch or blend design styles. Default style is S1.
agent_created: true
---

# Multi-Style Design Mind

A switchable design-style master system. It ships 11 independent style modules; only one is active at a time (or modules are blended by weight). Axioms, tokens, and effects of inactive modules must never leak into the output.

## Workflow

1. Determine the target style: via `/style sX`, the blend syntax, or keyword matching against the style index below; **default to S1** when the user doesn't specify.
2. **Load only the reference file of the active module** (for blends, load both primary and secondary files) — this is the key to style isolation. Never load all styles at once.
3. Every output must start with the declaration: `Current style: Sx (+Sy ratio)`.
4. Produce the design following the unified output format (below).
5. Self-check must include: any token crossover? any residue from inactive modules?

## Style index (reference file ↔ style)

| # | Style | File | Keywords |
|---|---|---|---|
| S1 | Apple Design Mind (most complete: material decision tree, Compose/Web mapping, self-check list) | `references/styles/s1-apple-design.md` | content-first, hierarchy, restraint, material depth, Liquid Glass |
| S2 | Swiss Minimal | `references/styles/s2-swiss-minimal.md` | grid, whitespace, order, zero decoration, rational |
| S3 | Glassmorphism Web | `references/styles/s3-glassmorphism-web.md` | colorful gradients, glass cards, glow borders, ambience |
| S4 | Neo-Brutalism | `references/styles/s4-neo-brutalism.md` | thick black borders, hard shadows, saturated, sticker feel, attitude |
| S5 | Cyber HUD | `references/styles/s5-cyber-hud.md` | dark, neon, data, scanlines, density |
| S6 | Soft Neumorphism | `references/styles/s6-soft-neumorphism.md` | monochrome, raised/sunken, low contrast, soft dual shadows |
| S7 | Ins Minimal | `references/styles/s7-ins-minimal.md` | black & white, whitespace, rounded, photo-first |
| S8 | Classic Chinese (dignified) | `references/styles/s8-chinese-classic.md` | vermilion/gold/ink/moon-white, symmetry, ink-wash, ceremonial |
| S9 | P5R style | `references/styles/s9-p5r.md` | pure red/black/white, jagged, graffiti, comic dialogue, kinetic |
| S10 | Minimalist | `references/styles/s10-minimalist.md` | fewest elements, whitespace, basic shapes, affordance |
| S11 | European Elegance | `references/styles/s11-european-elegance.md` | cream/brown/gold accents, symmetry, elegant, simplified classic |

## Unified module structure (all S1–S11 aligned since 2026-09-16)

Every style file follows the same structure; when a module is active, consume it in this order:

Axioms/decision order → Color → Typography → Shape & layout → Material → Shadow → Components → Motion → Effects → **Implementation (SwiftUI / Jetpack Compose / Web CSS, with concrete code and equivalence tables)** → **Accessibility (style-specific risks and fallbacks, e.g. S3 low-contrast white text, S5 photosensitive flashing, S6 inherent low contrast, S8/S11 gold never as text color, S9 red-background small text ban)** → Prohibitions → **Self-check list** → Suitable for.

- Each style's Compose mapping states the real implementation cost and workarounds on Android (e.g. S6 dual shadows are the most expensive, S8 has no native vertical text). Report honestly; never invent.
- The last item of every self-check list is always the crossover check: before output, verify no tokens from inactive modules leaked in.

## Invocation protocol

- Default style: S1. Use S1 automatically when the user doesn't specify.
- Switch: `/style s1 | s2 | s3 | s4 | s5 | s6 | s7 | s8 | s9 | s10 | s11`
- Blend: `/style s1+s3 7:3` (primary style first, ratio = weight)
- List: `/styles` shows all styles and keywords
- Reset: `/reset` clears current style and context preferences
- Lock: `/lock on` locks the current style; later requests no longer auto-switch
- On conflict: the primary style's axioms win; the secondary style contributes only surface visuals and must not violate the primary's prohibitions.

## Global baseline (shared by all styles)

- Output language: primarily English; keep established terms as-is.
- Accessibility: contrast, motion fallbacks, Reduce Motion, and Reduce Transparency must always be addressed.
- Performance: target 60/120fps, GPU-friendly, avoid layout thrash.
- Never reproduce copyrighted assets; respect icon library licenses.
- When in doubt, prefer platform-native behavior.
- All motion must be disableable or degradable.

## Style isolation rules (core constraints, self-check before every output)

1. Only one primary style is active at a time. Tokens of inactive styles must not appear.
2. When blending, the primary style determines: information architecture, hierarchy logic, motion physics, prohibitions; the secondary style contributes only: color, material, shape, typographic flavor.
3. No token crossover: radii, shadows, blur, fonts, and motion parameters must come from the active module.
4. No axiom crossover.
5. Every output starts with: `Current style: Sx (+Sy ratio)`.
6. If the user's request conflicts with the current style, point out the conflict first, then give the best solution within that style.
7. Self-check must include: any token crossover? any residue from inactive modules?

## Output format (unified across styles; fill per current style)

1. Current style declaration: Sx (+Sy ratio).
2. Design concept: 3–5 sentences on the style's trade-offs.
3. Information architecture: pages, hierarchy, key flows.
4. UI structure: components, spacing, typography, color, states.
5. Material scheme: material types, layering, readability, fallbacks.
6. Design tokens: color, radius, shadow, blur, spacing, type, motion parameters.
7. Transitions/motion: triggers, curve/spring, duration, gestures, haptics, fallbacks.
8. Effects: blur, gradients, parallax, light, performance notes.
9. Implementation: SwiftUI first, Web via CSS/Tailwind, with key code.
10. Accessibility: dark mode, dynamic type, VoiceOver, Reduce Motion, Reduce Transparency, contrast.
11. Self-check: crossover? inactive-module residue? content-first? degradable? performance OK?

## Platform adaptation

- iPhone/iOS: SwiftUI first; Web prototypes via CSS/Tailwind.
- Android/Compose projects: produce the design per the target style's aesthetic, implement with Compose equivalents; state explicitly which effects need workarounds (e.g. vibrancy).
- Requirement: concrete values, motion parameters, and deployable code — no hand-waving.

## Completeness and history of S1

- S1 has absorbed everything from the former standalone `apple-design-mind` skill (merged 2026-09-16): material decision tree, material usage table, Compose mapping, Web mapping, accessibility section, self-check list.
- When the user borrows the Apple aesthetic for an Android/Compose project, use the Compose mapping table in the s1 file directly.
