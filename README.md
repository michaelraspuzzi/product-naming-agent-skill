# product-naming — a Claude Code naming skill

Names products, brands, apps, SaaS, features, and open-source projects by orchestrating a **panel of subagents** modeled on the top US naming firms, then screening availability and delivering a ranked shortlist with rationale — optionally as an interactive flip-card deck.

![Ranked name candidates rendered as flip cards with a studio explorer](docs/cover.png)

## How it works

A panel of subagents, orchestrated by `SKILL.md` through five phases (**brief → generate → evaluate → screen → synthesize**):

- **6 generators** — five modeled on top naming firms (`namer-lexicon`, `namer-catchword`, `namer-tanj`, `namer-landor`, `namer-igor`), each carrying that firm's distilled framework + case studies, plus `namer-essence`, an on-the-nose baseline (core verbs + feelings) so the obvious word is never silently skipped.
- **3 first-principles evaluators** — `name-phonetics` (sound symbolism), `name-linguistics` (construction/pronounceability), `name-psychology` (fluency/distinctiveness/aging).
- **1 availability screener** — `name-availability` (domain / trademark / cross-language signals).

Candidates are scored on a composite rubric (with a cross-school agreement bonus and an essence-coverage gate), screened, and ranked. The orchestrator runs in the main conversation and spawns the subagents in parallel.

## Structure
```
SKILL.md                                   # the orchestrator skill (source copy)
reference/                                 # deep reference, loaded on demand
  firm-frameworks.md  naming-science.md  scoring-rubric.md
.claude/
  agents/*.md                              # the 10 subagents
  skills/product-naming/                   # installed (project-scoped) copy
    SKILL.md  reference/  assets/cards-template.html
output/top-names.html                      # example rendered card deck
```

## Install

**Option A — personal (available in every project):**
```bash
mkdir -p ~/.claude/skills/product-naming ~/.claude/agents
cp -R SKILL.md reference .claude/skills/product-naming/assets ~/.claude/skills/product-naming/
cp .claude/agents/*.md ~/.claude/agents/
```

**Option B — project-scoped (checked into one repo):**
```bash
mkdir -p /path/to/project/.claude/skills/product-naming
cp -R SKILL.md reference .claude/skills/product-naming/assets /path/to/project/.claude/skills/product-naming/
cp .claude/agents/*.md /path/to/project/.claude/agents/
```

Then run `/reload-plugins` (or restart Claude Code) so it picks up the new skill and agents.

## Use
Just ask in natural language — the skill auto-triggers on naming requests:
> "Help me name a B2B AI agent that automates finance-team workflows."

Or invoke explicitly: `/product-naming a calm sleep-tracking app for new parents`

Claude collects a short brief, runs the panel, and returns a ranked shortlist. Say **"quick mode"** to skip the interview, or paste your own list of names to only evaluate/screen them. Ask for a **card deck** to render the top picks as the flip-card visual above (`assets/cards-template.html`) — front shows the name, tap to flip for meaning + score bars, with a studio explorer below.

## Notes
- Availability results are **best-effort screening signals, not legal clearance** — always do a formal trademark search before committing.
- Firm attributions stay visible in the output — you see which school produced each name and why.

## License
[MIT](LICENSE) © 2026 Michael Raspuzzi
