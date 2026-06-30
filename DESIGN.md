# Design

Visual system for the AirXSpatial brand site. Source of truth for tokens,
type, layout, motion, and imagery. Strategy lives in [PRODUCT.md](PRODUCT.md).

North star: **award-winning architecture.** Glass reflecting sky, structure,
landscape. Gallery-light by default with rationed dark, cinematic moments.
Monumental restraint; engineered precision; trust over hype.

## Theme

Dual-world system:

- **Light (default):** a near-white architectural monograph. Crisp, airy,
  imagery-forward. Most of the site lives here.
- **Dark (cinematic moments):** a deep blue-graphite "glass tower at dusk."
  Reserved for the hero, the closing CTA, and at most one mid-page reveal —
  drama is rationed. Frosted-glass panels (subtle backdrop-blur) are allowed
  here as a material nod; never as decoration.

Color strategy: **Full palette / restrained.** Two named brand colors (sky,
landscape) used deliberately on a disciplined neutral spine. Accent coverage
stays ≤10% of any view — the monumentality comes from space and imagery, not
saturation.

## Color

All values OKLCH. The brand colors carry the mood; surfaces stay near-neutral
(cool architectural graphite), never tinted warm.

### Brand

```css
/* Sky — glass reflecting sky. Primary. Links, primary CTAs, focus. */
--brand-sky-500: oklch(0.55 0.13 240);   /* core */
--brand-sky-600: oklch(0.48 0.13 242);   /* hover / pressed */
--brand-sky-300: oklch(0.72 0.11 238);   /* on-dark, glints */

/* Landscape — foliage green (honors palette seed ~h140). Accent. */
--brand-land-500: oklch(0.56 0.13 142);  /* core accent */
--brand-land-600: oklch(0.49 0.12 144);  /* hover / pressed */
--brand-land-300: oklch(0.72 0.13 145);  /* on-dark */
```

Sky and landscape are separated by ~100° of hue and read as unmistakably
distinct. Text on either filled color is **white** (mid-luminance saturated
fills — Helmholtz-Kohlrausch).

### Light surfaces & ink

```css
--bg:        oklch(1.000 0.000 0);        /* pure gallery white */
--surface:   oklch(0.975 0.004 245);      /* cool concrete panel */
--surface-2: oklch(0.955 0.005 245);      /* sunken / inset */
--ink:       oklch(0.22 0.012 245);       /* graphite — headings & body, >10:1 */
--muted:     oklch(0.50 0.012 245);       /* secondary text, ~4.6:1 */
--hairline:  oklch(0.90 0.006 245);       /* 1px structural rules */
--border:    oklch(0.86 0.007 245);
```

### Dark surfaces & ink

```css
--bg-d:        oklch(0.16 0.013 250);     /* glass-tower dusk, slight cool */
--surface-d:   oklch(0.20 0.015 250);     /* raised panel */
--glass-d:     oklch(0.22 0.018 250 / 0.55); /* frosted panel, with backdrop-blur */
--ink-d:       oklch(0.96 0.004 245);     /* near-white text */
--muted-d:     oklch(0.70 0.012 245);     /* secondary on dark, ≥3.5:1 */
--hairline-d:  oklch(0.30 0.012 250);
--border-d:    oklch(0.34 0.013 250);
```

### Semantic

```css
--success: oklch(0.55 0.12 150);
--warn:    oklch(0.66 0.13 75);
--danger:  oklch(0.55 0.16 25);
--focus:   var(--brand-sky-500);          /* 2px ring, 2px offset */
```

### Contrast contract (must hold)

- `--ink` on `--bg` ≥ 7:1 · `--muted` on `--bg` ≥ 4.5:1
- `--ink-d` on `--bg-d` ≥ 7:1 · `--muted-d` on `--bg-d` ≥ 3.5:1
- White on `--brand-sky-500` / `--brand-land-500` ≥ 4.5:1
- Text over imagery: always on a scrim/panel meeting the above.

## Typography

Pair on a **contrast axis**, not two similar sans. Direction: a tight,
confident **grotesque display** for monumental headlines + a clean,
**neutral humanist sans** for body. Self-hosted only (repo bans Google Fonts /
external requests) via `font-display: optional`.

- **Display / headings:** a tight grotesque. Recommended self-host:
  *Söhne* (licensed) or free alt *Geist* / *Inter Tight*. Weights 600–800.
- **Body / UI:** a neutral humanist sans. Recommended: *Inter* (variable).
- **Data / specs / coordinates:** mono — *Geist Mono* / *JetBrains Mono*.
  Use `font-variant-numeric: tabular-nums` for any figures, dimensions, dates.

Rules:
- Display letter-spacing floor **-0.03em** (never tighter — letters must
  breathe; monumental ≠ cramped).
- Hero display max **≤ 5.5rem** via `clamp()`. Restraint over shouting.
- `text-wrap: balance` on h1–h3; `text-wrap: pretty` on prose.
- Body measure **65–72ch**.
- Eyebrows/kickers: mono, uppercase, `letter-spacing: 0.14em`, `--muted`.

Scale (clamp, fluid): hero `clamp(2.75rem, 6vw, 5.5rem)` ·
display `clamp(2rem, 4vw, 3.25rem)` · h2 `clamp(1.6rem, 3vw, 2.25rem)` ·
body `1.0625rem/1.65` · small `0.875rem`.

## Layout

- **Strict 12-column grid**, max content `72rem`, wide `84rem`, prose `68ch`.
  Gutters `clamp(1.25rem, 4vw, 2rem)`.
- **Spacing scale (8px base):** 4 8 12 16 24 32 48 64 96 128 192. Vary section
  rhythm deliberately — not every section is the same height.
- **Vast vertical space:** section padding `clamp(5rem, 12vh, 10rem)`. The calm
  between moments is the point.
- **Hairline structure:** 1px `--hairline` rules and a faint architectural
  baseline grid (very low opacity) evoke drafting/precision. Optional, sparse.
- Full-bleed imagery breaks the grid intentionally; text never floats over
  image without a scrim or solid panel.
- Radii: small and architectural. `--r-sm: 4px · --r-md: 8px · --r-lg: 12px`.
  No pill-shaped marketing blobs. Glass panels may go to 16px.

## Components

- **Hero (dark):** full-bleed site imagery, dusk-dark scrim, monumental
  headline, one primary CTA. The page's biggest "ooh."
- **Section:** kicker (mono) + headline + lede, generous top padding. Light by
  default; `variant="dark"` for a rationed cinematic break.
- **Proof / credibility row:** logos, certifications, stat figures (tabular
  mono). Quiet, evenly spaced, hairline-separated.
- **How-it-works (two-sided):** explains customer ↔ supply without gig-app
  casualness. Numbered, precise, restrained.
- **Feature/capability card:** flat, hairline-bordered, no drop-shadow soup;
  sky or landscape used only as a thin top-rule or icon tint, ≤10% coverage.
- **CTA strip (dark):** glass panel, closing "ooh," single action.
- **Footer:** structural, hairline-divided, monospaced meta.

Buttons: primary = filled `--brand-sky-500`, white text; secondary = ink
outline; ghost = text + underline-on-hover. Focus ring always `--focus`.

## Motion

Intentional, engineered, calm. Ease-out exponential curves (no bounce/elastic).

- **Reveal:** content is visible by default; motion *enhances* (subtle
  rise+fade, 400–600ms, staggered per list — never gates visibility).
- **Imagery:** slow, restrained parallax / scale on hero only.
- **Glass:** dark panels may animate backdrop-blur/opacity on enter.
- Durations: fast 150ms · base 300ms · slow 600ms. Easing
  `cubic-bezier(0.16, 1, 0.3, 1)` (ease-out-expo-ish).
- **Reduced motion:** every effect has a crossfade/instant fallback under
  `@media (prefers-reduced-motion: reduce)`.

## Imagery

The emotional engine. Real architecture, aerial sites, glass, LiDAR/point-cloud
and photogrammetry artifacts that look like *craft*, not stock.

- Prefer: monumental buildings & infrastructure, drone/aerial vantage,
  point-cloud and mesh renders (these are the product made visible), dusk glass.
- Avoid: handshake/headset stock, generic "tech" abstractions, emoji, clip art.
- Treatment: high contrast, cool grade aligning to sky/graphite; consistent
  dark scrim for overlaid text. Point-cloud accents may tint toward sky/land.

## Migration note

This replaces the repo's neon-halo system. Retheme `src/styles/global.css`
tokens to the above; remove the `.site-accent` conic/radial neon halos and the
`.site-glow` neon shapes (or repurpose `.site-glow` as a very subtle
architectural grid). Keep BEM, token-only values, and the lint gates.
