# 1 — Brief

**Phase.** First. Brief is the input that drives every downstream decision.

**Produces.** A completed Ad Brief MD — the 7-section structured input passed to the Producer skill.

**Inputs.** Strategist-filled answers across:
1. Company (name, vertical, industry, geography, brand voice)
2. Offer (product, price, Hormozi value equation, risk reversal, bonuses)
3. ICP (segment, demographics, psychographics, pain/desire, top objections)
4. UVP / Positioning (differentiator, proof, against which alternative)
5. Persuasion Levers (primary LF8, primary Cialdini, secondary, avoid)
6. Creative Specs (placement, aspect ratio, format, char targets, CTA, must-haves/avoids)
7. Campaign Context (funnel stage, audience, KPI, test variable)

**Outputs.** A filled-in `.md` file the strategist hands to the Producer.

**Files in this folder.**

| File | Purpose |
|---|---|
| `templates/ad-brief-template.md` | Empty template. Copy and fill per ad concept. |

**How to use.**

1. Copy `templates/ad-brief-template.md` to a working location (or paste into chat).
2. Rename to `<client>-<campaign>-brief.md`.
3. Fill every field. Write `N/A — [reason]` rather than leave blank.
4. Pass to `2-Ideation/SKILL.md` (Ideator) to generate the creative concept set, then to `3-Production/SKILL.md` (Producer) to generate the shared copy set.

**Trigger phrases.** "Ad brief", "Meta ad brief", "fill out a brief", "static ad brief template."

**Required reading before running downstream.** Both Producer and Critic load `Services/Meta-Ads/Meta-Ads_Methodology.md`. The brief's enum fields (vertical, funnel stage, primary lever, Cialdini principle) are defined there.

**Intended workflow (in progress).** The brief is designed to be **semi-automated**, not fully manual. Plan:

1. Client completes the **Meta Ads onboarding form** (lives in the ClearThink Forms Hub in Notion) — captures company, offer, ICP demographics, brand voice, and campaign context.
2. Form responses **auto-populate Sections 1 (Company), 2 (Offer), most of 3 (ICP), parts of 6 (Creative Specs)**, and parts of 7 (Campaign Context).
3. Strategist completes the **strategic sections** that require judgment, not intake: Section 4 (UVP / positioning), Section 5 (Persuasion levers — primary LF8, primary Cialdini), and the open fields in Sections 6 and 7 (test variable, creative volume target).
4. Filled brief routes to the Ideation skill.

The PTN brief was filled fully manually because the onboarding form hasn't shipped yet. Future briefs should follow the semi-automated path once the form is in place.

**Known gaps.**

- **Onboarding form not yet built.** Until it ships, briefs are filled manually end-to-end. Priority: build the form in the Forms Hub and wire it to auto-populate the brief template's mechanical fields.
- No automated brief-generator skill (downstream of the onboarding form). Reconsider once the form is in place and we have multiple campaigns of data on which fields strategists routinely override vs. accept as-is.
