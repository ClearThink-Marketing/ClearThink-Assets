# Meta Ads — Service Overview

**What this service is.** Production and iteration of static creative for Meta (Facebook + Instagram) paid social campaigns, built around Meta's Andromeda algorithm. ClearThink writes the strategy and copy; ChatGPT renders the images; the strategist assembles in Meta Ads Manager.

**The system in one sentence.** Generate 25-30 distinct creative concepts, render them in batch, refine, produce a shared rotating copy set, assemble in Ads Manager, critique-and-iterate the 1-3 winners.

**What's in this folder.**

| File | Purpose |
|---|---|
| `Meta-Ads_Methodology.md` | **Canonical (production layer).** Frameworks, vocabulary, vertical playbooks, visual heuristics, banned words, handoff vocabulary, the Andromeda playbook (§9), Three-Axis Articulation Framework (§3). All three skills load this before running. |
| `Campaign-Structure.md` | **Canonical (deployment layer).** Strategist's decision guide for *deploying* campaigns in Meta Ads Manager — budget tiers, campaign structure (broad / interest stack / lookalike stack), Andromeda settings checklist, optimization cadence, reach concentration, the scaling loop, refresh/scale/kill decisions, CAC vs. LTV mindset. Read by humans, not loaded by skills. |
| `CREATIVES_DATABASE.md` | **Workflow doc.** Notion Concepts/Creatives database pattern, schema, status lifecycle, and where the database lives in a client portal. Read by humans when starting a new campaign. |
| `Process/` | The 5-stage production loop. See `Process/overview.md`. |

**The loop in one diagram.**

```
Brief MD
  → Ideation (Claude: strategy + 25-30 concepts)
  → ChatGPT (batch render 25-30 images)
  → [Strategist refines: keeps strong, drops weak]
  → Production (Claude: 5 headlines + 5 body + 5 desc + CTAs — shared copy set)
  → [Strategist assembles in Ads Manager — rotates copy across creatives]
  → Critique (Claude: scores winners; per-creative regen prompt for losers)
  → ChatGPT (per-creative v2 render) → loop
```

This is a **closed loop, not a linear sequence.** Ideation runs once per fresh campaign round; Production runs once per copy refresh; Critique + per-creative regen cycle as many times as needed.

**Trigger phrases that route here.**

- "Meta ads", "Facebook ads", "Instagram ads", "static ad", "paid social creative"
- "Ideate ads", "creative concepts", "brainstorm angles", "competitor ad analysis"
- "Write ad copy", "produce copy set", "headlines for [campaign]"
- "Critique this ad", "score this ad", "review my ad", "iterate on this"
- "Ad brief", "fill out a brief", "static ad brief"

**Routing.**

- Filling out a brief → `Process/1-Brief/`
- Generating the creative concept set → `Process/2-Ideation/`
- Generating the shared copy set → `Process/3-Production/`
- Critiquing or iterating an existing ad → `Process/4-Critique/`
- ChatGPT-side image generation reference → `Process/5-ChatGPT-Context/`

**Inputs.** Filled-in Ad Brief MD (template at `Process/1-Brief/templates/ad-brief-template.md`). Optional: competitor ad images, strategist notes (for Ideation).

**Outputs.** Strategic recommendations + 25-30 creative concepts (Ideation) → rendered images (ChatGPT) → shared rotating copy set (Production) → scored critiques + per-creative regeneration prompts (Critique).

**Pricing.** TBD — see `/CLEANUP.md`.

**Known gaps.**

- Pricing/scope still open (carried from `/CLEANUP.md`).
- No case studies or example briefs filed yet — add real client examples once one ships.
- No Notion database IDs assigned yet for client-side delivery tracking.
- ChatGPT custom GPT vs. Project decision is open (see `Process/5-ChatGPT-Context/overview.md`).
- Andromeda playbook defaults (25-30 / 1-3 winners / 5+5+5 copy set) are Haynes-derived starting points; revisit calibration after several real ClearThink campaigns.
