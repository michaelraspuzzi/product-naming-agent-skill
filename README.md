# product-naming — a Claude Code naming skill

Names products, brands, apps, SaaS, features, and open-source projects by orchestrating a **panel of subagents**:

- **5 firm generators** modeled on the top US naming firms — `namer-lexicon`, `namer-catchword`, `namer-tanj`, `namer-landor`, `namer-igor`
- **3 first-principles evaluators** — `name-phonetics` (sound symbolism), `name-linguistics` (construction/pronounceability), `name-psychology` (fluency/distinctiveness/aging)
- **1 availability screener** — `name-availability` (domain / trademark / cross-language signals)

The `product-naming` skill is the orchestrator: brief → generate (parallel) → evaluate (parallel) → screen → ranked top-5 with rationale.

## Structure
```
SKILL.md                    # the orchestrator skill
.claude/agents/*.md         # the 9 subagents
reference/                  # deep reference (loaded on demand)
  firm-frameworks.md
  naming-science.md
  scoring-rubric.md
```

## Install

**Option A — personal (available in every project):**
```bash
mkdir -p ~/.claude/skills/product-naming ~/.claude/agents
cp -R SKILL.md reference ~/.claude/skills/product-naming/
cp .claude/agents/*.md ~/.claude/agents/
```

**Option B — project-scoped (checked into one repo):**
```bash
mkdir -p /path/to/project/.claude/skills/product-naming
cp -R SKILL.md reference /path/to/project/.claude/skills/product-naming/
cp .claude/agents/*.md /path/to/project/.claude/agents/
```

Then run `/reload-plugins` (or restart Claude Code) so it picks up the new skill and agents.

## Use
Just ask in natural language — the skill auto-triggers on naming requests:
> "Help me name a B2B AI agent that automates finance-team workflows."

Or invoke explicitly: `/product-naming a calm sleep-tracking app for new parents`

Claude will collect a short brief, then run the panel and return a ranked shortlist. Say "quick mode" to skip the interview, or paste your own list of names to only evaluate/screen them.

## Notes
- Availability results are **best-effort screening signals, not legal clearance** — always do a formal trademark search before committing.
- The firm attributions are part of the output — you see which school produced each name and why.
