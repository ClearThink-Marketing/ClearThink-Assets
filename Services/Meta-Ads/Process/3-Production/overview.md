# 3 — Production

**Phase.** Third. Convergent production phase. Generates the shared copy set that rotates across the creative concepts Ideation generated and ChatGPT rendered.

**Produces.** A copy set per run:
- 5 headlines (~40 chars each)
- 5 body copy variations (~125 chars each)
- 5 descriptions (~30 chars each)
- 1-3 CTA button recommendations (Meta preset)
- Rotation guidance — which copy elements pair best with which concept clusters

Why a copy set, not per-creative copy: per Andromeda best practices (see Methodology §9), the algorithm needs visual+concept diversity, not 25 unique pieces of copy. Five strong, broadly-applicable headlines outperform 25 specific ones.

**Inputs.**

- **Required:** Completed Ad Brief MD from `1-Brief/`.
- **Optional but valuable:** Ideation output from `2-Ideation/` (the strategy + concept set). With it, rotation guidance is concrete; without it, rotation guidance is generic.

**Outputs.** Inline markdown by default. Save to `.docx` or `.pdf` if the user asks.

**Files in this folder.**

| File | Purpose |
|---|---|
| `SKILL.md` | The `meta-static-ad-producer` skill. Drives copy set generation. |

**Required reading.** `Services/Meta-Ads/Meta-Ads_Methodology.md` — frameworks (especially Hopkins, Sugarman, Hormozi), funnel mapping (§4), vertical playbooks (§5), banned words (§8), Andromeda playbook (§9 — explains the copy-set model). Producer is not self-contained.

**Process.**

1. Read the brief end-to-end. Push back on missing or vague sections.
2. Load lever (Section 5) + funnel stage (Section 7) → emotional register via Methodology §4.
3. Apply the matching vertical playbook (Methodology §5).
4. Read Ideation output (if provided); cluster concepts.
5. Draft 5 headlines (~40 chars, broadly applicable, distinct angles).
6. Draft 5 body copy variations (~125 chars, slippery slide, value equation).
7. Draft 5 descriptions (~30 chars, proof/clarity supporters).
8. Recommend 1-3 CTAs matched to commitment level.
9. Write rotation guidance — map copy to concept clusters.
10. Render output.

**Trigger phrases.** "Write ad copy", "produce copy set", "Meta ad copy", "headlines for [campaign]", "body copy for [campaign]", "finalize copy", "rotate copy across ads."

**Handoff to next stage.** Strategist assembles the copy set + rendered creatives in Meta Ads Manager. Once assembled and running, individual ads (or the set as a whole) go to `4-Critique/` for scoring.

**Known gaps.**

- No A/B testing harness — Producer generates the copy pool, but tracking which combinations win in Ads Manager is manual. Build a tracking template if volume warrants.
- No vertical-specific reference files in this folder yet (e.g., a pasted-in DTC swipe library or B2B copy bank). Consider adding `references/` subfolder if useful.
- The 5/5/5 default is a Haynes-derived starting point. Revisit after several real campaigns reveal whether 3/5/3 (lower bandwidth) or 7/7/5 (higher diversification) work better for ClearThink's client mix.
