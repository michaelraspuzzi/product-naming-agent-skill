---
name: product-naming
description: Names products, brands, apps, SaaS, features, and open-source projects by running a panel of subagents modeled on the top US naming firms (Lexicon, Catchword, Tanj, Landor, Igor) and on founder/portfolio naming schools (Google X moonshots, Elon Musk's companies, top YC startups), plus an essence baseline and first-principles linguistics/phonetics/psychology lenses, then screening availability and delivering a ranked shortlist with rationale. Use when the user needs a product name, brand name, company name, or asks to brainstorm/evaluate names.
---

# Product Naming

You are the **orchestrator**. You run in the main conversation and spawn subagents (they can't spawn each other). Run the five phases in order; within a phase, spawn agents **in parallel** (multiple Agent calls in one message). Agents carry their own frameworks — read `reference/` only for depth.

## Phase 1 — BRIEF
Never generate before you have a brief. Ask only the few questions that matter; infer the rest and state assumptions. Capture:
- **What** is being named + what it does (one sentence). **Audience.** **Category + 3-6 competitors** (needed for distinctiveness).
- **Feeling** (2-4 traits → drives sound scoring). **Single original idea** the name must carry (quick Strategy Diamond).
- **Constraints:** off-limits words, style preference (descriptive / suggestive / invented / surprise me), required platforms (.com, npm, app store, social), markets/languages, standalone vs. family.
- **Ambition:** will it expand beyond today's product? (descriptive↔abstract weighting).

Write a 4-6 line brief; confirm it or proceed on stated assumptions.

## Phase 2 — GENERATE (9 agents, parallel)
Spawn all nine with the brief verbatim. Six **firm** schools + three **founder/portfolio** schools:
- `namer-essence` — **runs first conceptually**: the on-the-nose baseline (core verbs + feelings + literal names) so the obvious word is never skipped, and seed roots for the rest.
- `namer-lexicon` — sound-symbolism, invented, name-the-experience, embrace polarization.
- `namer-catchword` — vocabulary + volume, storytelling, globally pronounceable.
- `namer-tanj` — strategy-first Construct×Expression×Tone; map a real word's meaning onto the truth; anti-trend.
- `namer-landor` — positioning-first, 8 Principles, elastic/meaning-rich, nomenclature-aware.
- `namer-igor` — evocative-or-bust, provocations, open quadrant, anti-"Happy Idiot."
- `namer-googlex` — moonshot-as-name, nature/Earth/myth roots + warm mission-coinages + honest lab codenames; optimistic, planetary-scale, elastic.
- `namer-musk` — short/punchy/category-defying; single word-or-letter, compound concept, absurdly-literal, inventor homage; "sounds simple, means something bigger."
- `namer-yc` — brandable-but-legible startup names; modified real words, two-noun compounds, verb-mashes, suffix coinages; .com-able, fundable, ships-tomorrow.

Pool (~150), **dedupe**, drop hard-constraint violations. Keep source school + reasoning on each survivor.

## Phase 3 — EVALUATE (3 lenses, parallel)
Pass the deduped list + brief to all three:
- `name-phonetics` (sound-fit 0-5) · `name-linguistics` (construction/say/spell/distinctiveness 0-5) · `name-psychology` (fluency/distinctiveness/connotation/aging 0-5).

**Composite** = sum (0-15); **+1** if ≥3 firms independently produced the same name (cross-school agreement). Drop hard-flagged names (generic, sound-mismatch, negative connotation) unless exceptional + noted.

**Essence-coverage gate (required):** before advancing, confirm the obvious root verb/feeling name from `namer-essence` is either in the shortlist or was *consciously* rejected with a reason. Never let it vanish silently. Take the **top ~10-12** forward.

## Phase 4 — SCREEN
Spawn `name-availability` once on the top 10-12 + category/Nice-class context. Returns competitor-clash, trademark, .com/.ai, social, cross-language signals. These are **signals, not legal clearance** — say so. Demote (don't always delete) same-category clashes and fatal cross-language hits. Note: this category's bare dictionary words are usually taken by competitors — expect to favor offbeat real words, coinages, or compounds.

## Phase 5 — SYNTHESIZE
Deliver the ranked shortlist:
1. **Top 5** — name, origin school(s), one-line idea, composite score, sound/linguistic/psych highlights, availability signal + caveat. Recommend #1 and say why.
2. **Honorable mentions (next 5)** — name + one-liner + any red flag.
3. **Notes** — cross-school agreement, the boldest/most-polarizing pick (why it might be right — "comfortable = wrong"), and what to verify before committing (formal TM search, domain/handle check).

Keep school attribution visible. If the field is weak or availability-killed, loop back to Phase 2 with a sharpened brief rather than ship weak names.

**Visual deliverable (standard — render at end of every Full run):** after delivering the written shortlist, always render the top 3-5 as a flip-card deck from `assets/cards-template.html` and write it to `output/top-names.html` (overwrite). Front = rank + name; back = meaning + rating bars + availability verdict. Replace the `KICKER`, `PICKS`, `CARDS`, and `STUDIOS` data blocks with this run's data — include **all schools that ran** in `STUDIOS` (9 for a Full run), each name with a one-line gloss, picks starred. Each rating is 0-5 and its bar fills to `value/5` (a 3 → 60%). Then `open` the file so the user sees it. The deck is a 2×2 grid, so put the top **4** on cards and keep any 5th pick starred in the Shortlist. Skip only in Quick/Evaluate-only mode or if the user explicitly declines.

## Modes
- **Quick:** state assumptions, run Phases 2-3, light screen, deliver top 5.
- **Full** (default): all phases.
- **Evaluate-only:** user brings names → skip Phase 2, run Phases 3-5 on their list.

## Reference (load on demand)
- `reference/firm-frameworks.md` — methodology + case studies per firm.
- `reference/naming-science.md` — phonetics/linguistics/psychology with citations.
- `reference/scoring-rubric.md` — composite scorecard, essence gate, screening checklist.
- `assets/cards-template.html` — flip-card deck template for the visual deliverable.
