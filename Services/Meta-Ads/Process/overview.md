# Meta Ads — Process Overview

**The loop.** Meta static ad production at ClearThink runs as a closed loop with five stages, built around Meta's Andromeda algorithm. Stages 2 and 5 cycle on the front end (Ideation → batch render → refine); stages 4 and 5 cycle on the back end (Critique → per-creative regen).

```
1. Brief
   ↓
2. Ideation (Claude)        →   5. ChatGPT (batch render of 25-30)
                                       ↓
                                 [Strategist refines]
                                       ↓
3. Production (Claude)        ←        ↓
   ↓
[Strategist assembles in Ads Manager]
   ↓
4. Critique (Claude)
   ↓                         ↘
   Ship                       5. ChatGPT (per-creative regen) → loop
```

| Stage | Folder | Responsible | Produces |
|---|---|---|---|
| 1. Brief | `1-Brief/` | Strategist | Filled-in Ad Brief MD (7 sections + creative volume target) |
| 2. Ideation | `2-Ideation/` | Claude (Ideator skill) | Strategy + 25-30 creative concepts (image prompts + angle blurbs) |
| 3. Production | `3-Production/` | Claude (Producer skill) | Shared copy set: 5 headlines + 5 body copy + 5 descriptions + CTAs + rotation guidance |
| 4. Critique | `4-Critique/` | Claude (Critic skill) | Per-creative scored critique + verdict + regeneration prompt |
| 5. ChatGPT context | `5-ChatGPT-Context/` | ChatGPT (custom GPT or Project) | Rendered images (batch from Ideation; per-creative from Critique regen) |

**Read this first.** Before running any skill in this Process folder, load `Services/Meta-Ads/Meta-Ads_Methodology.md`. All three skills assume it's in working context.

**The unit of work is the loop, not the stage.** A single Ideation pass without Production and Critique is incomplete. Critique decides whether to ship a creative or iterate; if iterate, its regeneration prompt feeds back into ChatGPT for v2 of that specific creative.

**When stages run.**

- **Stage 1** runs once per ad concept (per ICP / offer / funnel-stage combination).
- **Stage 2** runs once per fresh campaign round — produces the full creative concept set (default 25-30).
- **Stage 5 batch** runs once per Ideation output — ChatGPT renders all 25-30 image prompts.
- **Stage 3** runs once per copy refresh — produces the shared 5+5+5 copy set that rotates across the creative set.
- **Stage 4** runs per individual creative being evaluated. Typically focused on the 1-3 reach winners and 1-2 suspected drags (per Andromeda's reach concentration; see Methodology §9).
- **Stage 5 per-creative regen** runs once per "Iterate" verdict from Critique.

**Trigger phrases that route to a specific stage.**

- "Fill out a brief," "ad brief template" → `1-Brief/`
- "Ideate ads," "creative concepts," "brainstorm angles," "competitor analysis" → `2-Ideation/`
- "Write ad copy," "produce copy set," "headlines for [campaign]" → `3-Production/`
- "Critique this," "score this ad," "iterate on this" → `4-Critique/`
- "Image generation," "ChatGPT prompt," "DALL-E reference," "batch render" → `5-ChatGPT-Context/`

**Known gaps.**

- No completed example brief on file yet — first real client run should be archived as a reference.
- No deployment pipeline for the ChatGPT side (custom GPT vs. Project decision still open).
- Batch render sessions of 25-30 prompts may hit ChatGPT plan limits — test before relying on a single-session batch.
- See `/CLEANUP.md` for service-level open items.
