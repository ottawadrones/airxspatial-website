---
target: homepage (src/pages/index.astro)
total_score: 24
p0_count: 1
p1_count: 2
timestamp: 2026-06-30T17-29-37Z
slug: src-pages-index-astro
---
# Impeccable Critique — AirXSpatial Homepage (`src/pages/index.astro`)

Method: dual-agent (A: design-review · B: detector + browser evidence)

## Design Health Score

| # | Heuristic | Score | Key issue |
|---|-----------|-------|-----------|
| 1 | Visibility of System Status | 2 | No visible interactivity affordance on cards; anchor CTAs give no scroll feedback |
| 2 | Match System / Real World | 3 | Domain-fluent copy ("ground truth", "orthomosaics"); minor jargon ("the funnel") |
| 3 | User Control & Freedom | 3 | Skip-link + nav present; no back-to-top on long mobile scroll |
| 4 | Consistency & Standards | 3 | Coherent tokens — but kicker-above-every-heading is monotonously consistent |
| 5 | Error Prevention | 2 | Both closing CTAs point to the same `about` URL — misleading duplication |
| 6 | Recognition Rather Than Recall | 3 | Clear linear narrative; 4 near-identical grids blur together in memory |
| 7 | Flexibility & Efficiency | 2 | One path/one pace; two-sided audience not given distinct doors |
| 8 | Aesthetic & Minimalist Design | 2 | Minimal to the point of austerity — reads unfinished against a luxury brief |
| 9 | Error Recovery | 2 | Few interactive states shown; not richly evaluable |
| 10 | Help & Documentation | 2 | No proof, FAQ, or "how matching works" depth |
| **Total** | | **24/40** | **Acceptable — solid IA & copy; sags on aesthetic ambition, differentiation, dual-audience flexibility** |

## Anti-Patterns Verdict

**LLM assessment: YES, this reads as AI-made.** It trips two reflex-reject lanes at once — (a) editorial-typographic mono-kicker scaffolding (`01 · What we do` / `02 · How it works` / `03 · For firms & pilots` above every heading), and (b) generic corporate block-grid (four sequential grids of hairline-bordered rounded-rect cells). The "monumental" headlines render in the **OS system font** (no display face exists), and the page ships **zero imagery** on a brief whose entire product *is* pictures of the world.

**Deterministic scan: CLEAN (0 findings)** across `index.astro`, `src/components`, `src/layouts`. This is the important gap: the detector catches token/markup slop, not *compositional* slop. The page is technically tidy and aesthetically generic — exactly the failure mode a rule scanner misses and a design director doesn't. Console is silent (0 errors/0 warnings).

**Browser evidence:** bottom **3 consecutive dark sections** (partners → CTA → footer) = **1,644px (1.83 viewports), the bottom ~37% of the page is one continuous dark band.** Computed `font-family` on `h1` and `body` = system-ui stack, no webfont. **All interactive tap targets < 44px** (nav links 17px; hero CTAs 40–42px; CTA button 40px). Mobile: no horizontal overflow.

## Overall Impression

The bones are good and the *words* are genuinely luxurious; the *visuals* are a competent wireframe wearing the brand's clothes. The single biggest opportunity: the brand promises "award-winning architecture" but renders in the system font with no imagery and no material richness — closing that gap (typeface + one monumental architectural gesture + real spatial imagery) is what moves it from "fine" to "ooh."

## What's Working

1. **Copywriting is above-grade and domain-credible** — "Ground truth", "measure twice and deliver to standard", "precision is the price of entry". The voice carries more credibility than the visuals do.
2. **Disciplined OKLCH token system & color restraint** — brand color genuinely stays <10% per view; real a11y scaffolding (skip-link, focus-visible, reduced-motion, ink-400 banned).
3. **The single mid-page dark reveal is the right instinct** — rationing one dark "supply-side" section to flip register for firms/pilots is smart composition; it's only undermined by the dark stack that follows it.

## Priority Issues

**[P0] No display typeface — the monument renders in the OS system font.**
Why: the entire thesis is monumental typography; `system-ui` headlines cap the ceiling on everything else and are the loudest slop tell. Fix: self-host a distinctive architectural display face (NOT Inter/DM Sans/Space Grotesk — reflex-reject) wired as `--font-display`, separate from a clean body sans. Command: **typeset**

**[P1] Bottom three dark slabs stack with no variety or crescendo (1.83 viewports of dark).**
Why: partners→CTA→footer merge into one flat dark zone; the closing CTA — the intended end-peak — drowns (peak-end failure). Fix: return to gallery-light before the CTA OR sculpt a curved/architectural divider between the dark planes OR give the CTA a full-bleed spatial backdrop so it's a *moment*. De-duplicate the two CTAs both pointing to `about`. Command: **layout** (+ **delight** on the divider)

**[P1] Every interactive tap target is under 44px (nav links 17px).**
Why: fails WCAG 2.5.5 / mobile usability for Casey & Sam; nav is effectively unusable one-handed. Fix: raise nav link hit areas (padding), hero/CTA buttons to ≥44px min-height. Command: **harden**

**[P2] Four near-identical bordered-cell grids flatten the middle.**
Why: discipline band, Platform 6-up, Steps 3-up, Partner 2×2 are the same object repeated — the "rigid grid of blocks" / Confluence feel. Fix: differentiate by *composition* — asymmetric editorial Platform layout, Steps as a drawn connected journey, and introduce one architectural curve per scroll-third. Command: **layout** → **bolder**

**[P2] Zero imagery on a brief that sells imagery.**
Why: a LiDAR/photogrammetry marketplace with no point cloud, orthomosaic, or site capture forfeits all the richness/"ooh". Fix: art-directed spatial visuals treated as gallery prints — large, edge-bled, rationed. Command: **overdrive**

**[P3] Repeated numbered mono kickers above every heading = AI scaffolding.**
Why: textbook generative-template rhythm; monotone. Fix: drop the kicker on half the sections; let scale and space carry hierarchy. Command: **polish**

## Persona Red Flags

- **Jordan (first-timer):** hero forces a side-choice ("See how it works" / "For firms & pilots") before they know which side they're on; buyer and supplier hit the same undifferentiated grids.
- **Riley (stress-tester):** both closing CTAs point to the same `about` page; anchor CTAs only jump down the same page; **no proof artifact anywhere** (no numbers, logos, case) to substantiate the credibility claim.
- **Casey (mobile):** 17px nav links; an extended triple-dark bottom scroll with no landmark or back-to-top; grid monotony at 1 column.

## Minor Observations

- Duplicated `.site-accent` blur backdrop CSS (base vs `--sky/--land` modifiers) — dead/overlapping rules.
- `--shadow-pop` defined but unused — the one richness primitive goes unused.
- DESIGN.md's "glass reflecting sky" metaphor is asserted in comments but nothing on the page is glassy/material/reflective.
- Discipline band repeats "Survey-grade" sublabel four times — filler.
- Legacy compat aliases (teal→sky, zinc→ink) are retrofit residue.

## Questions to Consider

1. What if the page sold the *deliverable* (a survey-grade point cloud / digital twin of a real building) as the monument, instead of copy over a dot-grid?
2. What is the ONE architectural curve that earns the whole page — a single Burj-style sweeping radiused edge — with everything else kept hairline-rigid as foil?
3. Should the two-sided marketplace be a deliberate fork — a luminous "demand" world and a darker instrument-grade "supply" world — turning the dark-stack problem into a designed duality?
