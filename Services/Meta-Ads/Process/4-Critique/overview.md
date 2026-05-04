# 4 — Critique

**Phase.** Fourth. Scores assembled ads (per-creative or across the rotation), issues a verdict, and produces a regeneration prompt that closes the loop back to ChatGPT for individual creative iteration.

**Produces.**
1. Scored critique across 6 dimensions (1-5 each)
2. Overall verdict: Ship / Iterate / Kill (with one-line rationale)
3. Optimization brief: top 1-2 issues, 3 alt headlines, 1 alt visual direction
4. Regeneration prompt block (paste-into-ChatGPT for v2 image of the specific creative)

**Inputs.** One of three modes:
- **Mode A** — image only (Critic uses vision to extract copy + score)
- **Mode B** — copy only (Critic skips Visual Hierarchy dimension)
- **Mode C** — image + copy (standard, all 6 dimensions scored)

Optionally, the Ad Brief MD as ground truth. Without the brief, Critic infers ICP / lever / funnel stage and flags the limitation.

**Outputs.** Inline markdown.

**Files in this folder.**

| File | Purpose |
|---|---|
| `SKILL.md` | The `meta-static-ad-critic` skill. |

**Required reading.** `Services/Meta-Ads/Meta-Ads_Methodology.md` — framework deep-dives ground each dimension's score. Critic is not self-contained; load the methodology before running.

**The 6 dimensions (each scored 1-5).**

1. **Hook** — first-3-seconds attention capture (Sugarman + funnel mapping)
2. **Clarity** — ICP-readable in <5 seconds (Hopkins specificity + banned words)
3. **ICP Match** — language/imagery/emotional register matches the segment (vertical playbook + brief)
4. **Offer Strength** — Hormozi value equation evaluation
5. **Persuasion Lever Execution** — actual lever vs. declared lever (Cashvertising LF8 + Cialdini)
6. **Visual Hierarchy & Platform Fit** — thumb-stop, mobile-first, AI-tells (visual heuristics)

**Verdict thresholds.**

- **Ship** — 24-30 (or 20-25 if visual skipped). Run it.
- **Iterate** — 15-23 (or 13-19 if visual skipped). Run regen prompt → v2 in ChatGPT.
- **Kill** — under 15 (or under 13). Foundation is wrong. Either the brief itself needs rework (return to `1-Brief/`) or the angle is fundamentally off (return to `2-Ideation/` for a fresh concept set).

**Per-creative vs. set-level critique.**

The Critic operates one ad at a time by default. When evaluating a 25-30 ad rotation:
- Run the Critic on the 1-3 creatives capturing the most reach (per Andromeda's reach concentration; see Methodology §9). Those are the ones worth iterating on.
- Run the Critic on the 1-2 creatives the strategist suspects are dragging the set's overall fitness down. Decide whether to fix or kill.
- Don't run the Critic on every creative in a 30-ad set. Reach concentration means most won't run long enough to be worth scoring individually.

**Trigger phrases.** "Critique this ad", "score this ad", "review my ad", "is this any good", "iterate on this", "what's wrong with this ad."

**Handoff.** When verdict = Iterate, paste the regeneration prompt into ChatGPT (per `5-ChatGPT-Context/`) for a per-creative v2 render. When verdict = Ship, archive the brief + ad as a reference. When verdict = Kill, return upstream — `1-Brief/` if the brief itself is broken, `2-Ideation/` if the brief is fine but the angle is wrong.

**Known gaps.**

- No "Ship" archive folder yet — no place to file completed-and-shipped ads as future reference. Add when first ad ships.
- Scoring scale is 1-5 for now. Revisit moving to 1-10 after several real runs reveal calibration ceiling.
- No set-level scoring rubric (does the rotation have good messaging diversity? are the concept clusters balanced?). Currently inferred from per-creative scores; could formalize.
