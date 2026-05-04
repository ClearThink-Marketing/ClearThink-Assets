---
name: meta-static-ad-critic
description: "Critique and optimize Meta and Instagram static ad creative — scoring across hook, clarity, ICP-match, offer strength, persuasion lever execution, and visual hierarchy — and producing a regeneration prompt for the next ChatGPT iteration. Use this skill whenever the user wants an ad reviewed, critiqued, scored, optimized, or iterated on. Triggers include: 'critique this ad', 'review my ad', 'score this ad', 'is this ad any good', 'iterate on this', 'optimize this ad', 'why isn't this converting', 'what's wrong with this ad', 'rate my ad', 'improve this ad', 'analyze this Facebook ad', 'analyze this Instagram ad', or pasting an ad image, ad copy, or both and asking for feedback. Accepts three input modes: image only, copy only, or image + copy. This skill is the downstream half of a production-and-critique loop with the meta-static-ad-producer skill — it grades the output and produces an optimization brief plus a paste-into-ChatGPT regeneration prompt that closes the loop."
---

# Meta Static Ad Critic

## What this skill does

Grades and optimizes static ad creative for Meta (Facebook + Instagram). Given an ad — image only, copy only, or image plus copy — it produces:

1. **A scored critique** across 6 dimensions (1-5 each), with prose feedback per dimension
2. **An overall verdict:** Ship / Iterate / Kill, with one-line rationale
3. **An optimization brief:** top 1-2 issues to fix in priority order, plus 3 alternative headlines and 1 alternative visual direction
4. **A regeneration prompt block** — paste-into-ChatGPT — that closes the generate-critique loop with all the context ChatGPT needs to render v2

The critique is *opinionated*. A 3/5 means "mediocre," not "fine." A 5/5 means "exceptional, ship it." Most working ads land 3-4 across most dimensions on first draft.

## Required reading before running

This skill is **not self-contained**. Before scoring, load the canonical methodology:

- **`Services/Meta-Ads/Meta-Ads_Methodology.md`** — frameworks, vocabulary, funnel mapping, vertical playbooks, visual heuristics, banned words, handoff vocabulary

The framework deep-dives that ground each dimension's score live in the methodology, not here. Without the methodology in working context, dimension scoring lacks anchoring and feedback gets generic.

## Inputs

This skill handles three input modes. Detect the mode from what the user provides.

### Mode A: Image only
- User pasted/uploaded an image of an ad (their own draft, a competitor's ad, an inspiration ref)
- Read the image with vision; extract any visible text (headline, body, CTA) directly from the image
- Score all 6 dimensions, but note that "Clarity" is partially limited because you're reading the rendered ad rather than the source copy fields

### Mode B: Copy only
- User provided ad copy text (primary text, headline, description, CTA) without an image
- Skip dimension 6 (visual hierarchy) — can't score what you can't see
- Score the other 5 dimensions
- In the optimization brief, note that visual review is pending

### Mode C: Image + copy (the standard)
- User provided both. Score all 6 dimensions.
- Most useful mode — copy fields aren't always legible at thumbnail size, so having them separately removes ambiguity.

### Brief MD (optional but valuable)

If the user also provides the **Ad Brief MD** (template at `Services/Meta-Ads/Process/1-Brief/templates/ad-brief-template.md`), use it as ground truth for ICP, primary lever, funnel stage, and offer. Without it, you have to *infer* what the ad is trying to do — which limits how sharp the critique can be. If the brief is missing, ask if one is available before scoring; if not, proceed with inferred context but flag the limitation in the optimization brief.

## How frameworks ground each dimension

The frameworks (Hopkins, Sugarman, Hormozi, Cashvertising LF8, Cialdini) are detailed in **Methodology §3**. Dimensions cite them as follows:

- **Hook** ← Sugarman first-sentence rule + funnel mapping (Methodology §4)
- **Clarity** ← Hopkins specificity + banned words (Methodology §8)
- **ICP Match** ← Vertical playbook (Methodology §5) + ICP from brief
- **Offer Strength** ← Hormozi value equation
- **Persuasion Lever Execution** ← Cashvertising LF8 + Cialdini
- **Visual Hierarchy & Platform Fit** ← Visual heuristics (Methodology §6)

When penalizing, **cite the framework**: "Hook scored 2/5 because it violates Sugarman's first-sentence rule — the headline depends on body copy to make sense" is more useful than "Hook is weak."

## The 6 dimensions

Each scored 1-5. Use these anchors:

- **1** — broken, this dimension is actively hurting the ad
- **2** — weak, would need significant work
- **3** — mediocre, common-denominator ad
- **4** — good, working
- **5** — exceptional, hard to improve

Don't hand out 4s and 5s freely. Most working ads score 3-4 on most dimensions. Scoring everything 4+ defeats the point.

### 1. Hook (first 3 seconds)

**What you're scoring:** Does the headline + opening line + visual focal point stop the scroll for *this specific funnel stage*?

**Funnel-stage lens (from Methodology §4):**
- TOF cold → expect a pattern interrupt, audience call-out, or pain-naming statement
- MOF warm → expect differentiation or top-objection handling
- BOF retarget → expect urgency, risk reversal, or specific close

**Penalties:**
- Generic opener ("Tired of ___?", "Are you ready to ___?") = -1
- Headline that requires reading body copy to make sense = -1
- "We're excited to announce" / "Introducing" for cold audiences = -2
- Hook doesn't match funnel stage (BOF urgency on cold = wrong audience temp) = -1 to -2

**Bonus:**
- Specific number, named segment, or unexpected angle in the first 5 words = +1
- Hook that pre-qualifies the right reader and filters out the wrong reader = +1

### 2. Clarity

**What you're scoring:** Can the ICP understand what's being offered in under 5 seconds?

**Penalties:**
- Vague benefits without specifics ("save time," "grow your business") = -1 each
- Jargon the ICP wouldn't use = -1
- Multiple competing ideas in one ad (says it's about A, then B, CTA is about C) = -2
- Banned-word density (per Methodology §8) = -1

**Bonus:**
- Numbers, named credentials, specific outcomes = +1
- Reading-level matches ICP (B2B SaaS founder ≠ same vocabulary as homeowner researching pressure washing) = +1

### 3. ICP Match

**What you're scoring:** Does the language, imagery, and emotional register match the ICP segment from the brief (or inferred ICP)?

**Penalties:**
- Generic "everyone" framing when the brief specifies a segment = -1 to -2
- Visual cues signaling the wrong identity (corporate stock photo aimed at homeowners, polished studio aimed at "real moms") = -1
- Pain or desire framed at the wrong life stage / role / situation = -2

**Bonus:**
- Direct call-out of the segment by role, situation, or shared identity ("Atlanta homeowners with a brick exterior") = +1
- Emotional register matches (urgency for pain-aware, relief for solution-aware, validation for product-aware) = +1

### 4. Offer Strength

**What you're scoring:** Run the Hormozi value equation against the offer as presented. Is the dream outcome vivid? Is perceived likelihood elevated by proof? Is time delay minimized or addressed? Is effort/sacrifice handled? Is risk reversal visible?

**Penalties:**
- No clear offer (just brand awareness with no ask) = -1 (unless intentional for top-of-funnel awareness, which is rare)
- Offer is generic for category ("free quote" with no differentiator) = -1
- No proof of likelihood (no reviews, numbers, named results) = -1
- Time-to-value implied to be slow or unclear = -1
- Risk reversal exists in the brief but isn't surfaced in the ad = -1

**Bonus:**
- Stack of 2+ value elements (offer + bonus + guarantee) = +1
- Specific, near-term outcome ("by next Tuesday," "in 14 days") = +1

### 5. Persuasion Lever Execution

**What you're scoring:** Did the ad actually activate the primary Life Force and Cialdini principle from the brief? If no brief, does it activate *any* one lever well, or does it default to claim+CTA with nothing pulled?

**Penalties:**
- Declared primary lever ≠ actual executed lever (brief says "care of loved ones," ad executes on "be superior") = -2
- 3+ levers stacked weakly instead of 1 executed well = -1
- No identifiable Cialdini principle activated = -1 (unless the offer alone is doing the work)
- Social proof claimed but not specific ("trusted by many" instead of "1,247 reviews, 4.8 stars") = -1

**Bonus:**
- Primary lever is clearly the dominant emotional thread = +1
- Cialdini principle is integrated naturally, not bolted on = +1

### 6. Visual Hierarchy & Platform Fit

*(Skip this dimension in Mode B / copy-only.)*

**What you're scoring:** Does the visual work at thumb-stop scale and on the declared placement? Heuristics in Methodology §6.

**Penalties:**
- Focal point unclear within 1 second = -2
- Text on image illegible at thumbnail size = -1
- Composition framed for desktop (small subject, lots of negative space, centered logo competing with message) = -1
- Safe zones violated (critical content in top 14% or bottom 20% for stories/reels) = -1
- Stocky / corporate / "obviously an ad" aesthetic for cold traffic = -1
- AI-image tells (extra fingers, garbled text, melted hands, illegible signage) = -2

**Bonus:**
- Native-feeling composition that "looks like a friend posted it" = +1
- Single bright/saturated focal element on a quieter background = +1
- Faces with direct eye contact or expressive emotion = +1

## Output format

Render the critique inline as structured markdown. Use this exact structure:

```
# Ad Critique: [short identifier — vertical or angle]

## Scores

| Dimension | Score | One-line takeaway |
|---|---|---|
| Hook | X/5 | ... |
| Clarity | X/5 | ... |
| ICP Match | X/5 | ... |
| Offer Strength | X/5 | ... |
| Persuasion Lever Execution | X/5 | ... |
| Visual Hierarchy & Platform Fit | X/5 (or N/A) | ... |

**Overall: X/30** (or X/25 if visual skipped)

## Verdict: [Ship / Iterate / Kill]

[One-line rationale]

## Dimension Detail

### Hook — X/5
[2-4 sentences of prose feedback. What works, what's broken, what to change. Cite framework.]

### Clarity — X/5
[same]

### ICP Match — X/5
[same]

### Offer Strength — X/5
[same]

### Persuasion Lever Execution — X/5
[same — explicitly call out actual vs declared lever if there's a brief]

### Visual Hierarchy & Platform Fit — X/5
[same — or "N/A — copy-only mode"]

## Optimization Brief

**Top issue to fix (priority 1):** [the single biggest unlock]

**Secondary issue (priority 2):** [the next thing to fix after #1]

**3 alternative headlines** (matched to funnel stage):
1. [headline option]
2. [headline option]
3. [headline option]

**Alternative visual direction:** [1-2 sentences describing a different visual angle that addresses the issues above]

## Regeneration Prompt for ChatGPT

Paste this into ChatGPT to generate v2. Format per Methodology §7 ("Critic → ChatGPT").

\`\`\`
Generate a Meta static ad image for [company].

CONTEXT:
- ICP: [pulled from brief or inferred]
- Funnel stage: [from brief or inferred]
- This is v2 — the previous version had these issues: [issue 1], [issue 2]

VISUAL DIRECTION (NEW):
SUBJECT: [...]
SETTING: [...]
COMPOSITION: [...]
LIGHTING/MOOD: [...]
STYLE: [...]
ASPECT RATIO: [from brief]
TEXT OVERLAY: [none / max 3-5 words: "..."]
COLOR PALETTE: [...]

MUST INCLUDE: [list]
MUST AVOID:
- [the failures from v1]
- AI-image tells (extra fingers, garbled text, melted features)
- Generic stock-photo composition
- [other failures specific to this ad]
\`\`\`
```

## Verdict thresholds

Use total score to anchor the verdict, but apply judgment.

- **Ship (24-30 / 20-25):** Working ad. Run it. Maybe A/B test against a variation but don't block on it.
- **Iterate (15-23 / 13-19):** Has good bones. Regeneration brief should produce a meaningfully better v2. Worth one more cycle.
- **Kill (under 15 / under 13):** Foundation is wrong. Either the brief itself is broken, the angle is fundamentally off, or the ad is solving a different problem than the campaign needs. Go back to the brief, not to v2.

A score of 4-5 on Hook with everything else at 3 can be Ship — a strong hook covers a lot of sins. Conversely, a 5 across the board with a 1 on ICP Match is still Iterate, because targeting the wrong audience drowns everything else.

## Important notes

- **Be honest.** The user wants critique, not flattery. If the ad is mediocre, say so. The whole point of the loop is to *improve*, which requires accurate diagnosis.
- **The regeneration prompt is the handoff.** Self-contained. ChatGPT won't have the brief — copy the relevant details into the prompt itself.
- **Cite the framework when you penalize.** Anchor each dimension's score in Methodology §3.
- **Don't critique the brief unless asked.** If the brief has problems, mention them in the optimization section but don't relitigate the brief itself — that's a separate conversation.
- **Image-only mode is the hardest.** Without copy fields, you're inferring intent. Be explicit about what you can and can't see, and weight Visual Hierarchy more heavily since that's what you actually have data on.
- **If the user pastes a competitor ad and asks "what makes this work?"** — same skill, same dimensions, but the optimization brief becomes "what to steal" instead of "what to fix."
- **Paired with the upstream skills.** When the verdict is Iterate on a specific creative, the regeneration prompt closes the loop back to ChatGPT for a per-creative v2 render. The user runs the prompt, assembles v2 in Meta Ads Manager, and brings it back here. When the verdict is Kill, return to `Services/Meta-Ads/Process/1-Brief/` if the brief itself needs rework, or to `Services/Meta-Ads/Process/2-Ideation/` if the brief is sound but the angle is wrong.
- **Per-creative, not per-set, by default.** The Critic scores individual ads. When evaluating a 25-30 ad rotation, score the 1-3 creatives capturing reach (per Andromeda's reach concentration; see Methodology §9) and the 1-2 the strategist suspects are dragging set fitness. Don't score every ad in a 30-ad set — most won't run long enough to be worth scoring.
