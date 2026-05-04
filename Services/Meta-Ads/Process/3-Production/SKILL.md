---
name: meta-static-ad-producer
description: "Generate the shared copy set for a Meta or Instagram static ad campaign — 5 headlines, 5 body copy variations, 5 descriptions, and CTA picks designed to rotate across a 25-30 creative ad set. Use this skill whenever the user wants ad copy written for a Meta campaign once the creative concepts and images are in place. Triggers include: 'write ad copy', 'produce copy set', 'Meta ad copy', 'Facebook ad copy', 'Instagram ad copy', 'headlines for [campaign]', 'body copy for [campaign]', 'finalize copy', 'rotate copy across ads', 'copy variations for the set'. Aligned with Andromeda best practices: outputs a shared copy set that rotates across all creatives in the ad set rather than per-creative copy. Runs after the meta-static-ad-ideator has produced the creative concept set and ChatGPT has rendered the images."
---

# Meta Static Ad Producer

## What this skill does

Generates the **shared copy set** for a Meta/Instagram static ad campaign. Output is the convergent production phase of the loop — the headlines, body copy, descriptions, and CTAs that rotate across the 25-30 creatives Ideation generated and ChatGPT rendered.

Output per run:

- **5 headlines** (~40 chars each) — the bold text below the image
- **5 body copy variations** (~125 chars each before "see more" truncation; can run longer if the hook earns it) — primary text above the image
- **5 descriptions** (~30 chars each) — small subline under the headline (often hidden on mobile but worth using)
- **1-3 CTA button recommendations** — selected from Meta's preset list
- **Rotation guidance** — which copy elements pair best with which concept clusters from Ideation

Why a shared set, not per-creative copy: Andromeda matches on visual+concept diversity. The algorithm doesn't reward 25 unique pieces of body copy — it rewards 25 distinct visual concepts paired with broadly applicable copy. See **Methodology §9 Andromeda playbook**.

## Required reading before running

This skill is **not self-contained**. Before generating, load the canonical methodology:

- **`Services/Meta-Ads/Meta-Ads_Methodology.md`** — frameworks (Hopkins, Sugarman, Hormozi, Cashvertising LF8, Cialdini), funnel mapping, vertical playbooks, banned words, Andromeda playbook (§9 — explains why this is a copy set, not per-creative copy)

If the methodology is not in working context, stop and load it first. Running this skill without the methodology produces generic output.

## Inputs

### Required: Brief MD

The completed Ad Brief MD (template at `Services/Meta-Ads/Process/1-Brief/templates/ad-brief-template.md`). Pulls from:

- Section 1 (Company): brand voice, vertical
- Section 2 (Offer): product, price framing, value equation, risk reversal, bonuses
- Section 3 (ICP): segment, pain/desire, top objections
- Section 4 (UVP): primary differentiator, proof, against-which-alternative
- Section 5 (Persuasion levers): primary Life Force, primary Cialdini principle
- Section 7 (Campaign Context): funnel stage, KPI

If the brief is missing, ask for it. Don't proceed without it.

### Optional but valuable: Ideation output

The full output from `Services/Meta-Ads/Process/2-Ideation/SKILL.md` (the strategy + 25-30 concepts). With it, the copy set can be tuned to rotate intelligently across the concept clusters — same broad headline pool, but rotation guidance that pairs concept clusters with the headlines that fit best.

Without the ideation output, generate the copy set against the brief only and produce generic rotation guidance.

## Process

### Step 1 — Read the brief
Read end-to-end. Push back on missing or vague sections. Common gaps to flag: ICP psychographics, proof points (numbers, named clients, reviews), offer specifics, brand voice.

### Step 2 — Load the lever and funnel stage
Pull the primary Life Force (LF8) and Cialdini principle from Section 5. Pull funnel stage from Section 7. Map funnel stage → emotional register via **Methodology §4**:

- TOF cold → pain-naming, pattern-interrupt copy register
- MOF warm → differentiation, objection-handling register
- BOF retarget → urgency, risk-reversal, closing register

### Step 3 — Apply the vertical playbook
Read the playbook in **Methodology §5** that matches the brief's `Vertical` field. This determines copy emphasis (specificity vs. punchiness vs. ROI focus), default CTAs, and watch-outs for the vertical.

### Step 4 — Read ideation (if available)
If the ideation output is provided, scan the concepts. Note 2-4 concept clusters (e.g., "problem-amplification cluster," "social-proof cluster," "outcome-direct cluster"). The copy set will be designed to rotate across these clusters.

### Step 5 — Draft 5 headlines
Each headline is broad enough to apply across most/all creatives in the rotation but specific enough to land. Constraints:

- ~40 chars (Meta truncation)
- Each headline activates the locked primary lever
- Each headline matches the funnel stage register
- Five must be **meaningfully distinct** — different angle, hook, or framing. Not five rewordings of the same idea.
- Apply Hopkins specificity, Sugarman first-sentence rule, banned words list
- At least one should reference a number, named segment, or specific outcome (Hopkins specificity bonus)

### Step 6 — Draft 5 body copy variations
Each ~125 chars before "see more" (can extend if the hook earns it). Constraints:

- Same lever, same funnel stage register
- Each one is the slippery slide from a different opening — different reasons to convert articulated as different reasons to read on
- Each should pair naturally with multiple headlines and multiple visual concepts
- Apply Hormozi value equation: at least 2 of the 5 should explicitly stack the value (outcome + proof + risk reversal); others can be lighter
- Address the top objection from Section 3 in at least 1-2 of the body copy variations
- Banned words list applies

### Step 7 — Draft 5 descriptions
~30 chars each. Often hidden on mobile but used on desktop and some placements. Constraints:

- Each is a one-line proof-or-clarity supporter (e.g., "Atlanta — same-day quote", "1,200+ five-star reviews", "Free guarantee — no obligation")
- These rotate independently of headline/body — so each description should make sense paired with most headlines
- Specific over clever

### Step 8 — Recommend 1-3 CTAs
From the Meta preset list, pick 1-3 that match the offer commitment level (per the vertical playbook in **Methodology §5**):

- Free / low-commit: Learn More, Get Quote, Download
- Medium-commit: Sign Up, Book Now, Get Started, Get Estimate
- High-commit: Shop Now, Buy Now, Order Now

If recommending more than one, explain when each applies (e.g., "Get Quote for the awareness ads, Book Now for the deeper-funnel ones").

### Step 9 — Write rotation guidance
Tell the strategist how to map the copy set to the creative set:

- Which 1-2 headlines pair best with which concept clusters from Ideation
- Which body copy variation is the workhorse (pairs with most concepts) vs. the specialist (pairs with one cluster)
- Whether one description should run universally vs. rotated
- Which CTA goes with which funnel-stage concepts (if recommending more than one)

If no Ideation output was provided, give generic rotation guidance ("rotate freely; keep an eye on which combinations win in Ads Manager and concentrate spend there").

### Step 10 — Render output
Inline structured markdown. See output format below.

## Output format

```
# Copy Set: [client name] — [campaign / round identifier]

## Context

- **Vertical:** [vertical from brief]
- **Funnel stage:** [TOF cold / MOF warm / BOF retarget]
- **Primary lever:** LF#X — [name] + Cialdini [principle]
- **Volume target:** [N creatives the copy will rotate across]

## Headlines (5)

1. **[headline]** — [1-line note on what this hooks]
2. **[headline]** — [note]
3. **[headline]** — [note]
4. **[headline]** — [note]
5. **[headline]** — [note]

## Body copy (5)

### Body 1
[~125 char primary text]
*Pairs best with:* [headline #s + concept clusters]

### Body 2
[~125 char primary text]
*Pairs best with:* [...]

### Body 3
[~125 char primary text]
*Pairs best with:* [...]

### Body 4
[~125 char primary text]
*Pairs best with:* [...]

### Body 5
[~125 char primary text]
*Pairs best with:* [...]

## Descriptions (5)

1. **[~30 char description]** — [purpose: clarity / proof / urgency / etc.]
2. **[~30 char description]** — [purpose]
3. **[~30 char description]** — [purpose]
4. **[~30 char description]** — [purpose]
5. **[~30 char description]** — [purpose]

## CTAs

- **[CTA button]** — [when to use]
- **[CTA button]** — [when to use, if recommending more than one]

## Rotation guidance

[2-4 paragraphs explaining how to map the copy set to the creative set in Meta Ads Manager. Reference Ideation concept clusters by name if available. Cover: which headlines pair with which concepts, which body copy is the workhorse, whether descriptions rotate freely or stay fixed, CTA mapping by funnel stage or concept cluster.]
```

If the user asks for a `.docx` or `.pdf` archive, save one. Default is inline.

## Writing guidelines (apply to all copy)

**Lead with benefits, not features.** "Sleep through the night" not "memory foam construction."

**Be specific.** Numbers, names, places, timeframes. "Atlanta homeowners" beats "homeowners." "14 days" beats "fast."

**Match the funnel stage.** TOF copy should feel like a stranger talking; BOF copy should feel like a friend reminding you.

**Voice match the brief.** Pull from Section 1 (Brand voice). If the brief says "warm and direct," don't write corporate.

**Address the top objection from Section 3.** If the objection is price, lead with value or risk reversal. If it's trust, lead with proof. If it's time, lead with speed.

**One idea per copy element.** Don't try to say everything in one headline. The headline's job is the click; the body copy's job is to support it; the description's job is to add a proof point or clarifier.

**Banned words.** Do not use any word on the banned-words list in **Methodology §8**. If a draft contains one, rewrite.

**CTA matches commitment level.** Don't put "Buy Now" on a free-quote offer.

## What to push back on

If the brief or ideation has any of the following, flag before writing:

- **Brief locked but no Ideation output and no rough creative direction.** Without it, rotation guidance is generic — flag as a limitation.
- **Lever mismatch.** If the declared primary lever doesn't fit the offer/ICP, say so before writing 5 headlines around the wrong lever.
- **Missing proof points.** Body copy and descriptions need specifics. If Section 4 (UVP) and Section 2 (Offer) lack numbers, named clients, or review counts, ask.
- **Funnel stage doesn't match ICP description.** If the brief says BOF retarget but the ICP description sounds cold (no awareness of the brand), the funnel stage is probably wrong.

It's better to send the strategist back for 5 minutes of clarification than produce a copy set built on shaky inputs.

## Important notes

- **The copy set rotates — it doesn't pair 1:1 with creatives.** A 25-creative ad set with 5 headlines × 5 body × 5 descriptions = 625 theoretical combinations. The strategist (and Ads Manager's automatic combination logic when used carefully) decides what's actually live.
- **Don't write 25 unique headlines.** That defeats the Andromeda model and the strategist's bandwidth. 5 strong, broad-but-grounded headlines outperform 25 specific ones.
- **The rotation guidance is the most valuable part for the strategist.** Without it, they're guessing at combinations. With it, they have a defensible mapping that ties each piece of copy to the concepts it was written for.
- **Banned words are non-negotiable.** No exceptions. If a sharp line uses one, rewrite it.
- **Paired with the Critic.** Once ads are assembled and running, individual creatives should run through `Services/Meta-Ads/Process/4-Critique/SKILL.md` for scoring and per-creative iteration.
