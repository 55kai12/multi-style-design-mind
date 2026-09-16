# Multi-Style Design Mind

A switchable design-style master system with **11 independent style modules**, built as a [WorkBuddy](https://www.workbuddy.cn) Skill (also compatible with any Agent that supports the SKILL.md convention).

Only one style is active at a time (or modules blend by weight). Axioms, design tokens, and effect rules of inactive modules are fully isolated — no "style crossover".

> **This is the English edition.** The Chinese edition lives at the repository root (`SKILL.md` + `references/`). To install the English edition, use the `en/` folder.

## Style modules

| # | Style | Keywords |
|---|---|---|
| S1 | Apple Design Mind | content-first, material depth, Liquid Glass, real physics |
| S2 | Swiss Minimal | grid, whitespace, weight contrast, zero decoration, rational |
| S3 | Glassmorphism Web | colorful gradients, glass cards, glow borders, ambience |
| S4 | Neo-Brutalism | thick black borders, hard shadows, saturated, sticker feel, attitude |
| S5 | Cyber HUD | dark, neon, scanlines, information density, glow |
| S6 | Soft Neumorphism | monochrome, raised/sunken, soft dual shadows |
| S7 | Ins Minimal | black & white, large whitespace, rounded, photo-first |
| S8 | Classic Chinese (dignified) | vermilion/gold/ink/moon-white, symmetry, ink-wash, ceremony |
| S9 | P5R style | pure red/black/white, jagged, graffiti, comic dialogue, kinetic |
| S10 | Minimalist | fewest elements, single focal point, basic shapes, affordance |
| S11 | European Elegance | cream/brown/gold accents, symmetry, elegant, simplified classic |

Every module follows one unified structure:

> Axioms/decision order → Color → Typography → Shape & layout → Material → Shadow → Components → Motion → Effects → **Implementation (SwiftUI / Jetpack Compose / Web CSS)** → **Accessibility (style-specific risks and fallbacks)** → Prohibitions → **Self-check list** → Suitable for

## Highlights

- **Progressive disclosure**: only the active module's file is loaded — zero context pollution.
- **Three-platform implementation code**: every style ships concrete SwiftUI, Jetpack Compose (with equivalence tables and honest cost notes), and Web CSS snippets — not just tokens.
- **Accessibility as hard constraints, not suggestions**: e.g. S3/S6 low-contrast risks and fallbacks, S5 photosensitive flashing limited to <3Hz, S8/S11 gold never as text color, S9 red-background small-text ban — all contrast-measured.
- **Style isolation rules**: when blending, the primary style owns information architecture, motion physics, and prohibitions; the secondary contributes surface visuals only.
- **Honest cost reporting**: e.g. S6 dual shadows are the most expensive in Compose, S8 has no native vertical text — no invented solutions.

## Install (WorkBuddy / compatible Agent)

```bash
git clone https://github.com/55kai12/multi-style-design-mind.git
cp -r multi-style-design-mind/en ~/.workbuddy/skills/multi-style-design-mind
```

Restart the session to take effect. (For the Chinese edition, copy the repo root instead.)

## Usage

| Command | Effect |
|---|---|
| `/style s1` … `/style s11` | Switch style (default S1) |
| `/style s1+s3 7:3` | Blend: primary first, weighted |
| `/styles` | List all styles and keywords |
| `/reset` | Clear current style and context preferences |
| `/lock on` | Lock the current style |

Blend example: `/style s1+s3 7:3` — Apple's structure, hierarchy, and motion physics as the base, layered with Glassmorphism's colors and material ambience; S1's prohibitions win.

## Repository structure

```
multi-style-design-mind/
├── SKILL.md                  # Chinese edition entry
├── references/styles/        # Chinese modules (s1–s11)
├── en/
│   ├── SKILL.md              # English edition entry
│   └── references/styles/    # English modules (s1–s11)
├── README.md                 # Chinese readme
├── README.en.md              # This file
└── LICENSE                   # MIT
```

## License

[MIT](LICENSE)
