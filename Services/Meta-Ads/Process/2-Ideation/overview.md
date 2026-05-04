# 2 — Ideation

**Phase.** Second. Divergent exploration phase. Generates the creative concept set the campaign will test.

**Produces.**
1. Strategic recommendations — locked or recommended primary lever, top 3-5 angles ranked, competitor pattern observations, what to test vs. avoid
2. N creative concepts (default 25-30) — each with name, angle blurb, hook direction, and image generation prompt for ChatGPT

**Inputs.** Three flexible input types, used in any combination:

- **A: Brief MD** (any state — partial or full). If the lever in Section 5 is open, Ideation may recommend one based on ICP, offer, and competitor evidence.
- **B: Competitor ad images/screenshots.** Optional. Vision analysis extracts lever, angle, hook construction; output includes pattern observations.
- **C: Strategist notes.** Optional. Free-form hypotheses, angle ideas, voice or visual constraints, seasonal context.

**Outputs.** Inline markdown by default. Save to `.docx` or `.pdf` if the strategist asks.

**Files in this folder.**

| File | Purpose |
|---|---|
| `SKILL.md` | The `meta-static-ad-ideator` skill. Drives concept generation. |

**Required reading.** `Services/Meta-Ads/Meta-Ads_Methodology.md` — especially the Three-Axis Articulation Framework (§3), the Andromeda playbook (§9), the funnel mapping (§4), the vertical playbooks (§5), and the Ideation → ChatGPT handoff format (§7). Ideator is not self-contained.

**Process.**

1. Read brief + competitor ads + strategist notes
2. Confirm or recommend the primary lever
3. Map funnel stage → concept register
4. Apply the matching vertical playbook
5. Run Three-Axis Articulation (Problems × Circumstances × Outcomes) — generate 24-36 concept seeds
6. Cull and combine into N final concepts (where N = brief's Creative volume target)
7. Write the image generation prompt per concept (Methodology §7 format)
8. Write the strategy section
9. Render output

**Trigger phrases.** "Ideate ads", "creative concepts", "brainstorm angles", "explore creative directions", "analyze competitor ads", "generate ad ideas", "what should we test on Meta", "creative set for [campaign]."

**Handoff to next stages.**

- Image prompts → ChatGPT (see `5-ChatGPT-Context/`) for batch render of all N images
- After strategist refines the rendered set → Production (`3-Production/`) generates the shared copy set that rotates across the refined creatives

**Known gaps.**

- No competitor ad library or swipe file maintained yet — Ideation has to work from whatever the strategist pastes in. Consider building a curated reference folder per vertical.
- Three-Axis Articulation outputs are not yet captured as a separate artifact for client deliverable purposes (currently embedded in the strategy section). Reconsider if strategists want it as a standalone deliverable.
