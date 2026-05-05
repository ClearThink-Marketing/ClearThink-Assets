# Meta Ads Methodology

**Canonical source for the Meta Static Ad system.** This document is the single-source-of-truth for the frameworks, vocabulary, vertical playbooks, and creative loop that govern how ClearThink produces and iterates on Meta and Instagram static ad creative.

The two operational skills (`meta-static-ad-producer`, `meta-static-ad-critic`) and the ChatGPT-side image generation context doc all reference this file. If a framework principle changes, change it here and it propagates everywhere.

---

## Table of contents

1. The production loop
2. Shared vocabulary
3. The frameworks (five copywriting + Three-Axis Articulation)
4. Funnel stage → awareness → hook strategy
5. Vertical playbooks
6. Visual & platform heuristics
7. The handoff vocabulary (Claude ↔ ChatGPT)
8. Banned words for ad copy
9. The Andromeda playbook
10. How the skills consume this doc

---

## 1. The production loop

Meta static ads at ClearThink follow a closed loop built around Meta's Andromeda algorithm (see §9). The system produces a high-volume, messaging-diverse creative set rather than a small number of polished variations. Five stages, two ChatGPT touchpoints, and a tight critique-regenerate cycle.

```
┌──────────────┐
│  1. Brief    │  Ad Brief MD (7 sections + creative volume target)
│  (template)  │
└──────┬───────┘
       │
       ▼
┌────────────────────┐      ┌──────────────────────┐
│  2. Ideation       │ ───► │  ChatGPT             │
│  (Claude)          │      │  (batch image render)│
│                    │      │                      │
│  Outputs:          │      │  Inputs ~25-30 image │
│  • strategy        │      │  prompts from        │
│  • 25-30 concepts  │      │  Ideation            │
│  • image prompts   │      │                      │
│  • angle blurbs    │      └──────────┬───────────┘
└────────────────────┘                 │
                                       ▼
                              ┌────────────────┐
                              │  Strategist    │
                              │  refines:      │
                              │  keeps strong, │
                              │  drops weak    │
                              └────────┬───────┘
                                       │
                                       ▼
                              ┌────────────────┐
                              │ 3. Production  │
                              │  (Claude)      │
                              │                │
                              │  Outputs       │
                              │  copy set:     │
                              │  • 5 headlines │
                              │  • 5 body copy │
                              │  • 5 descs     │
                              │  • CTA picks   │
                              └────────┬───────┘
                                       │
                                       ▼
                              ┌────────────────┐
                              │  Strategist    │
                              │  assembles     │
                              │  in Meta Ads   │
                              │  Manager       │
                              │  (rotates copy │
                              │  across the    │
                              │  creative set) │
                              └────────┬───────┘
                                       │
                                       ▼
                              ┌────────────────┐
                              │ 4. Critique    │
                              │  (Claude)      │
                              │                │
                              │  Outputs:      │
                              │  • scores      │
                              │  • verdict     │
                              │  • regen       │
                              │    prompt      │
                              └────────┬───────┘
                                       │
                       ┌───────────────┴───────────────┐
                       ▼                               ▼
                  Ship as-is              Per-creative regen → ChatGPT v2
```

**Roles:**

- **Brief** is the strategist's input. Encodes company, offer, ICP, UVP, levers, creative specs, campaign context, and creative volume target.
- **Ideation** (Claude) produces strategic recommendations + ~25-30 distinct creative concepts (image prompts + angle blurbs). Drives the divergent exploration phase.
- **ChatGPT** renders the 25-30 images in batch. Does not write copy. Does not invent strategy. Renders pixels.
- **Production** (Claude) produces a single copy set — 5 headlines + 5 body copy + 5 descriptions + CTA picks — written broadly enough to rotate across the full creative set. Driven by Andromeda's messaging-diversification requirement (see §9).
- **Critique** (Claude) scores assembled ads across 6 dimensions, issues a verdict (Ship/Iterate/Kill), and produces a regeneration prompt that closes the loop back to ChatGPT for individual creative iteration.

The loop is the unit of production. A single Ideation or Production pass without Critique is incomplete.

---

## 2. Shared vocabulary

These terms have specific meanings in this system. Both skills, the strategist, and ChatGPT (via its context doc) all use them the same way.

| Term | Meaning |
|---|---|
| **Brief** | The 7-section markdown file that drives every decision. Located at `Process/1-Brief/templates/ad-brief-template.md`. |
| **Vertical** | One of three: `dtc_ecom`, `b2c_local_service`, `b2b_lead_gen`. Routes which playbook applies. |
| **Funnel stage** | One of three: `TOF cold`, `MOF warm`, `BOF retarget`. Operational decision (which audience am I buying?). Maps internally to awareness level. |
| **Awareness level** | Schwartz's framework: unaware, problem-aware, solution-aware, product-aware, most-aware. Inferred from funnel stage; not declared in the brief. |
| **Primary lever** | The one Life Force (Cashvertising LF8) the ad pulls hardest on. Declared in brief Section 5. |
| **Cialdini principle** | The dominant persuasion principle (one of six). Declared in brief Section 5. |
| **Concept** | A distinct creative idea attacking the chosen lever from a specific angle. Ideation produces 25-30 of these per run. Each concept = one image prompt + one angle blurb + one hook direction. |
| **Angle** | The specific framing within a concept (e.g., "the slow damage you don't see" vs. "the neighbor who waited too long"). Concepts differ by angle. |
| **Copy set** | The shared 5 headlines + 5 body copy + 5 descriptions + CTA picks Production outputs once per campaign. Written broadly enough to rotate across all 25-30 creatives. |
| **Creative volume target** | The number of unique creatives the strategist commits to producing this round. Declared in brief Section 7. Defaults: 25-30 (Andromeda standard), 20-25 (mid-budget), 10-15 (low-budget pilot). |
| **Pocket audience** | The micro-segment Andromeda's algorithm matches an ad to. Each creative tends to find its own pocket. 1-3 creatives out of 25-30 typically capture nearly all the reach. |
| **Three-Axis Articulation** | Framework for generating distinct concepts within a chosen lever: Problems / Circumstances / Outcomes. See §3. |
| **Batch render** | The ChatGPT pass that renders all 25-30 image prompts from Ideation in one session. Distinct from per-creative regen rendering driven by Critic. |
| **Hook** | The first 3 seconds. Headline + opening line + visual focal point combined. The thing that decides whether the scroll stops. |
| **Image prompt** | The structured paste-into-ChatGPT block the Producer outputs for each variation. Self-contained — does not reference the brief. |
| **Regeneration prompt** | The structured paste-into-ChatGPT block the Critic outputs to drive a v2 image. Includes explicit v1 failures. |
| **Ship / Iterate / Kill** | Critic's three-tier verdict. Ship = run it. Iterate = one more cycle. Kill = brief is broken, go back to brief not v2. |

When a skill or human references one of these terms, it means *exactly* this. Do not redefine inline.

---

## 3. The frameworks

The canonical references. The first five are copywriting fundamentals applied by Producer and Critic. The sixth (Three-Axis Articulation) is the angle-generation framework Ideation uses to produce 25-30 distinct concepts from a single chosen lever.

### Hopkins — *Scientific Advertising*

Foundational principles for evidence-based copy.

- **Specificity beats cleverness.** "Saved 47 minutes per workout" beats "saves you time." Numbers, named places, specific outcomes always outperform vague claims.
- **Reason-why copy.** Don't just claim — explain *why* the claim is true. Every claim should carry its own justification or be paired with one.
- **Test the offer, not the cleverness.** The copy serves the offer; the offer is what wins. Clever copy on a weak offer loses to plain copy on a strong offer.
- **Headlines are filters.** A good headline pre-qualifies the right reader, not the most readers. Filtering down to the right ICP is a feature, not a bug.

### Sugarman — *The Adweek Copywriting Handbook*

Psychology of reading and persuasion in long-form direct response, applied to short-form ad copy.

- **The slippery slide.** Every line exists to make the reader read the next. Headlines pull to body, body pulls to CTA. If a line doesn't pull forward, cut it.
- **First sentence rule.** The only job of the headline (or first line of body copy) is to get the reader to read the second line. Nothing more.
- **Sell on emotion, justify with logic.** Lead with how it feels (relief, pride, safety, belonging). Back it up with proof (numbers, credentials, social proof). Logic-only ads underperform on cold traffic.
- **Seeds of curiosity.** Hint at a benefit you'll reveal lower down. Keep the reader scrolling.
- **Sell the concept, not the product.** "Peace of mind" not "polyurethane coating." Translate features into the experience or identity the buyer is actually purchasing.

### Hormozi — *$100M Offers*

How to construct an offer that converts.

- **Value equation:** `(Dream Outcome × Perceived Likelihood of Achievement) ÷ (Time Delay × Effort & Sacrifice)`. Maximize the top, minimize the bottom. Every line of ad copy should push at least one of these four levers.
- **Lead with outcome, not process.** "Lawn back to green in 14 days" beats "our 7-step lawn care system." Buyers buy outcomes; they tolerate processes.
- **Risk reversal converts fence-sitters.** If the brief has a guarantee, surface it. A money-back guarantee, satisfaction promise, or no-risk trial often does more work than another bullet point.
- **Stack value before naming price.** When price is mentioned, the perceived value should already exceed it. Bonuses, guarantees, and proof stack the value side of the equation.

### Cashvertising (Whitman) — Life Force 8

The eight primal motivators every ad ultimately hooks into. Match the primary Life Force declared in brief Section 5.

1. **Survival, enjoyment of life, life extension.** Health, longevity, vitality, safety from death.
2. **Enjoyment of food and beverages.** Taste, satisfaction, indulgence.
3. **Freedom from fear, pain, and danger.** Safety, security, removal of threat. (Often #1 in B2C local services — pressure washing, pest control, plumbing.)
4. **Sexual companionship.** Romantic and sexual desire.
5. **Comfortable living conditions.** Ease, convenience, comfort, quality of life. (Strong in home services, DTC home goods.)
6. **To be superior, winning, keeping up with the Joneses.** Status, achievement, competition. (Strong in DTC apparel, B2B SaaS.)
7. **Care and protection of loved ones.** Family, kids, pets, parents. (Strong in B2C local services framed around family safety.)
8. **Social approval.** Belonging, fitting in, being well-regarded. (Strong in DTC fashion, lifestyle.)

If the brief says "care of loved ones" but the draft executes on "be superior," the draft is wrong even if it sounds good.

### Cialdini — *Influence*: Six Principles

The dominant persuasion principle the ad activates. One declared in brief Section 5; do not stack all six.

- **Reciprocity** — give value first. Free guide, free quote, useful tip in the ad itself.
- **Commitment & consistency** — micro-yes ladders. "If you've ever ___, then you know ___."
- **Social proof** — reviews, counts, testimonials. "Join 1,200+ Atlanta homeowners."
- **Authority** — credentials, named experts, years in business, media mentions, license/insurance.
- **Liking** — shared identity, founder face, relatable language, in-group references.
- **Scarcity** — limited spots, limited time, limited inventory. (Use sparingly; cold traffic distrusts urgency unless it's specific and credible.)

### Three-Axis Articulation Framework (per Haynes)

The framework Ideation uses to generate 25-30 distinct concepts within a single chosen lever. For each ICP pocket, list as many reasons as possible across three axes:

- **Problems** — what's actively wrong, broken, painful, frustrating, expensive, embarrassing, or fragile in the ICP's current state. Concrete and specific. Not "frustration" — "the third tab crash this week with 12 unsaved drafts."
- **Circumstances** — the situation, role, context, season, life stage, or recent change that makes the offer relevant *right now*. Not general traits — specific moments. "Just took on her first direct report." "Roof is 14 years old going into hurricane season." "Switched from in-house to agency-supported and the agency just churned."
- **Outcomes** — the dream state, transformation, or specific endpoint the ICP wants. Concrete and measurable where possible. Not "growth" — "first $50K month without working weekends."

Each axis-and-pocket combination is a **concept seed**. A small ICP that can convert through 25-30 different angles is a small ICP being articulated from many angles, not a small ICP scaled by audience expansion. This is the core of Andromeda's messaging-as-targeting model (see §9).

**Use:** Ideation runs this exercise across the brief's ICP, plus any additional pocket audiences the strategist surfaces. The output is the angle list that becomes the 25-30 concepts.

---

## 4. Funnel stage → awareness level → hook strategy

The brief declares funnel stage in Section 7. Internally, both skills map it to awareness level and hook strategy via this table.

| Funnel stage | Default awareness (Schwartz) | Hook job |
|---|---|---|
| **TOF cold** | Problem-aware (or unaware if ICP signals it) | Name the pain, pattern interrupt, call out the audience |
| **MOF warm** | Solution-aware | Differentiate, prove, handle the top objection |
| **BOF retarget** | Product-aware / most-aware | Urgency, risk reversal, final close |

**Override rule.** If the brief's "Pain or desire being targeted" (Section 3) suggests the ICP doesn't yet recognize the problem, treat TOF as unaware and lead with a pattern-interrupt observation rather than a pain statement. Example: a productivity tool for owners who don't yet know they're losing 2 hours/day to context-switching → unaware, not problem-aware.

**Why we don't ask for awareness level explicitly.** Funnel stage is the operational decision the strategist makes when buying audiences in Ads Manager. Awareness is mostly a consequence of it. Asking for both adds friction and creates room for inconsistency.

---

## 5. Vertical playbooks

The brief's `Vertical` field (Section 1) routes which sub-playbook to apply. **Do not mix vertical playbooks** — each has different defaults for visual direction, copy emphasis, common offers, default CTAs, and which Life Force levers tend to win.

### DTC E-commerce (`dtc_ecom`)

- **Visual direction defaults:** product hero on clean background, lifestyle in-context, UGC-style "real person holding it," before/after for transformative products. Avoid stocky/corporate compositions.
- **Copy emphasis:** short, punchy, benefit-first. Lead with the transformation or the identity ("built for runners who hate running"). Stack social proof early (review counts, ratings, press mentions).
- **Common offers:** % off first order, free shipping threshold, bundle discount, BOGO, free gift with purchase.
- **Default CTAs:** Shop Now, Get Yours, Order Now, Buy Now.
- **Common winning levers:** LF6 (be superior / keep up), LF8 (social approval), LF1 (longevity for health/wellness). Cialdini: social proof + scarcity.
- **Watch-outs:** ecommerce ads die fast — variations should diverge sharply in *angle*, not just swap headlines. Don't make 3 variations the same idea reworded.

### B2C Local Services (`b2c_local_service`)

- **Visual direction defaults:** before/after of real work, photo of the team or owner, work-in-progress shot showing competence, branded truck/equipment with a real home in the background. Avoid stocky "happy contractor" stock photos — they read fake and tank trust.
- **Copy emphasis:** trust + clarity + proximity. Lead with service area, response time, or named local trust signal. Specificity is everything: "Atlanta," "same-day," "licensed and insured" beat generic claims.
- **Common offers:** free quote, $X off first service, satisfaction guarantee, same-day or next-day availability, no-obligation estimate.
- **Default CTAs:** Get Quote, Book Now, Get Estimate, Learn More, Call Now.
- **Common winning levers:** LF3 (freedom from pain/danger — "before this becomes a bigger problem"), LF7 (care of loved ones — "keep your family safe"), LF5 (comfortable living). Cialdini: authority + social proof (Google review counts, years in business, license/insurance).
- **Watch-outs:** local services have a high "BS detector." Vague claims like "best service in town" are negative signal. Always cite a number, a year, or a named credential. If the brief lacks proof, flag it.

### B2B Lead Gen (`b2b_lead_gen`)

- **Visual direction defaults:** clean professional composition, founder/team headshot, problem visualization (the messy spreadsheet, the alert dashboard, the calendar full of meetings), data viz that hints at outcome, named client logos in the layout. Avoid clichéd "shaking hands" or "diverse boardroom" stock.
- **Copy emphasis:** specific, ROI-focused, objection-handling. Lead with the unfair-advantage outcome ("close 23% more deals without adding headcount"). Reference role/title explicitly to pre-qualify ("for B2B SaaS founders doing $1M-$10M ARR").
- **Common offers:** free audit, free strategy call, downloadable resource (guide, template, calculator), demo, ROI assessment, free trial.
- **Default CTAs:** Book a Call, Get the Audit, Download, Sign Up, Learn More.
- **Common winning levers:** LF6 (winning, beating competitors), LF1 (business survival — "stop losing deals to ___"), LF3 (fear of falling behind, missing the trend). Cialdini: authority + social proof (named client logos, named results, case study mentions).
- **Watch-outs:** B2B buyers are skeptical of cleverness. Lean specific over witty. Numbers and named clients beat metaphors.

---

## 6. Visual & platform heuristics

Practitioner heuristics for what wins on Meta static, regardless of vertical. Apply across all three playbooks.

- **Thumb-stop logic.** The focal point must be obvious within 1 second at thumbnail size. If the image requires squinting on a phone, it's already lost.
- **Mobile-first composition.** 9:16 and 4:5 dominate. Never frame for desktop.
- **Text overlay — the rule has nuance.** ChatGPT image generation handles text inconsistently, *and* high-text-density ads lose thumb-stop on mobile. But "minimal" is not "zero." Two principles:

  - **A short hook earns on-image space.** A headline that filters the right reader (Hopkins' "headlines are filters") is the image's job — don't strip the hook trying to be minimalist. Use judgment on length; the principle is "the hook deserves space," not a fixed word count.
  - **No supporting copy on the image.** CTA buttons (Meta adds its own), feature panels, redundant decorative banners ("Spaces filling fast," etc.) — all of that is body-copy work. Strip them. The image qualifies; the body copy delivers.

- **Pick one trust display layout.** Vertical column OR horizontal strip — never both. Visual repetition without information gain hurts thumb-stop. Each row in the chosen layout should have equal visual weight.

- **Lever determines density tolerance.** The same on-image text-density rule does not apply equally across all ads:

  - **Loss-frame ads** can earn quantitative on-image elements (specific numbers, deadlines) because those numbers ARE the lever's argument made concrete. Without them, the loss-frame is abstract.
  - **Burden-relief and proof-driven ads** should stay leaner — the visual itself is the proof; on-image quantification competes with the relief promise.

  This is a principle, not a rule with fixed thresholds. Apply judgment per ad — what does this specific lever need on the image vs. what belongs in the copy?

- **Forward-looking language for upcoming events.** When a campaign launches before its anchor event, use *"ahead of"* or *"Ready for"* — not *"during"* or *"at"*. Pre-event "during" is grammatically off (the event hasn't happened yet) and loses the scarcity nudge that "ahead of" creates naturally.

- **Spell out abbreviations for cold traffic.** TOF cold viewers haven't earned the right to decode jargon. Industry shorthand belongs on MOF/BOF creative where context exists.

- **The image's primary job is Hopkins-aligned.** *Scientific Advertising* (1923) is explicit: the image's purpose is to **qualify the reader and pull them into the copy** — not deliver the entire pitch. Every on-image element should answer one question: "does this make the right reader more likely to read the body copy?" If the answer is no, strip it.

> **Note on patterns vs. principles.** Specific design patterns observed in individual campaigns (3-tier banner hierarchies, productized pricing tier cards on image, particular layout templates) need validation across multiple campaigns before being codified here. The methodology stays principle-level; patterns earn methodology status only after battle-testing proves them.
- **Safe zones for stories/reels.** Top ~14% and bottom ~20% are obscured by UI. Keep critical content in the middle 66%.
- **Contrast and color isolation.** A single bright/saturated focal element on a quieter background outperforms balanced compositions.
- **Faces work.** Especially direct eye contact and expressive faces. UGC aesthetic outperforms studio aesthetic for cold audiences across most verticals (especially DTC and local services).
- **Native-feeling beats polished.** "Looks like a friend posted it" beats "looks like an ad" for cold traffic.

**AI-image tells to avoid (must include in image prompts as MUST AVOID).** Extra fingers, garbled text, melted features, illegible signage, warped logos, asymmetric eyes, fused limbs, plastic skin texture, identical faces in a group, inconsistent lighting on the focal subject.

---

## 7. The handoff vocabulary (Claude ↔ ChatGPT)

The system has two AI roles with one shared vocabulary. ChatGPT receives image-generation work from two Claude sources: Ideation (batch, fresh concepts) and Critique (per-creative regen). Production never talks to ChatGPT — it produces copy that the strategist assembles in Ads Manager. The handoffs are structured prompt blocks — paste-and-go, no inference required.

### Ideation → ChatGPT (batch image prompts)

The Ideator outputs ~25-30 of these blocks in one run, one per concept. ChatGPT renders all of them in a batch session. Each block is self-contained; ChatGPT does not need to know what's in the brief.

```
Generate a Meta static ad image for [company name].

CONCEPT [N of 25-30]: [concept name / angle in 5-10 words]

SUBJECT: [the main thing in frame]
SETTING: [where, with context]
COMPOSITION: [framing — centered, rule-of-thirds, close-up, wide]
LIGHTING/MOOD: [natural daylight, golden hour, moody, bright]
STYLE: [photorealistic, UGC iPhone shot, editorial, illustrated]
ASPECT RATIO: [from brief Section 6]
TEXT OVERLAY: [either "none — text added separately" OR "max 3-5 words: '[text]'"]
COLOR PALETTE: [from brand or scene]
MUST INCLUDE: [list]
MUST AVOID: [list — including stocky, generic, AI-tells]
```

### Critique → ChatGPT (regeneration prompt)

The Critic outputs this block when the verdict is Iterate on a specific creative. ChatGPT reads it and renders v2 of that one creative. Same structure as the Ideation prompt, plus an explicit `CONTEXT` block declaring v1 failures.

```
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
```

The ChatGPT-side context doc (`Process/5-ChatGPT-Context/chatgpt-image-gen-context.md`) is the mirror of this section — it teaches ChatGPT how to read both prompt formats and how to handle batch render sessions vs. single-creative regen.

---

## 8. Banned words for ad copy

These words signal lazy copy, AI-generated copy, or "marketing speak" that erodes trust on Meta. Both Producer and Critic enforce this list. Brand-level banned words (from `/Brand/guidelines.md`) also apply.

**Corporate jargon:** comprehensive, robust, leverage, synergy, facilitate, methodology, holistic, streamline, empower.

**Marketing hype:** cutting-edge, innovative, groundbreaking, seamless, next-generation, transformative, best-in-class, game-changing, world-class, revolutionary, take to the next level.

**Filler / AI-tell:** intriguing, noteworthy, remarkable, harness, revolutionize, unleash, "unlock the power of," "in today's fast-paced world," "delve into," "navigate the complexities of," "at the end of the day," "that said," "it's worth noting," landscape (as filler), journey.

If a draft contains any of these, the skill must rewrite. The Critic deducts on the Clarity dimension.

---

## 9. The Andromeda playbook

This section explains *why* the system is structured the way it is. The 25-30 creative model, the shared copy set, the per-creative regen loop, and the Ideation→Production split are all consequences of how Meta's Andromeda algorithm distributes ads. Skip this and the rest of the system looks like overkill.

### What Andromeda changed

Meta's Andromeda algorithm (rolled out late 2024 through mid-2025, now active across all accounts) is an upstream creative-selection layer that pre-filters ads before Meta's traditional retrieval/ranking algo (Lattice) ever sees them. Practical implications:

- **Messaging is targeting.** Ad-set-level audience targeting (interests, lookalikes, demographics) is now suggestive, not deterministic. The algorithm matches *creative messaging* to micro-segment "pocket audiences" within the broader audience signal. One word in a hook can shift who sees the ad.
- **Pocket audiences are small and exhaust fast.** Andromeda finds tight micro-segments where a specific message resonates, then exhausts that pocket within hours-to-days. The algorithm needs a deep bench of distinct messages to keep finding new pockets.
- **Reach concentration is the norm, not a bug.** Out of 25-30 creatives in an ad set, 1-3 will get nearly all the reach. The other 22-29 sit ready to absorb spend when (a) the winners exhaust their pocket, (b) the algorithm finds a new pocket that one of them matches, or (c) the strategist refreshes the set.
- **AI Advantage Creative settings hurt.** Meta's automatic creative variations, site links, and "improvements" interfere with Andromeda's matching by introducing copy/visual permutations the strategist didn't intend. Turn them off — except positive comment highlighting, which is fine.

### What this requires of the production system

To work with Andromeda rather than against it, the production system must produce:

1. **High-volume, messaging-diverse creative sets.** 25-30 unique reasons to convert per ad set. Each creative is its own message — different concept, different angle, different hook, different visual. **Not** the same body copy with a swapped headline.
2. **A shared copy set, not per-creative copy.** 5 headlines + 5 body copy + 5 descriptions written broadly enough to rotate across all 25-30 creatives. Andromeda needs visual+concept diversification; it doesn't need 25 unique pieces of body copy.
3. **A scaling loop that respects reach concentration.** When the 1-3 winners exhaust, duplicate the ad set, pull the winners (they'll be the foundation of a separate scaled campaign), and replace with 1-3 fresh creatives. Test the remaining 22-29 + new ones against the next pocket.
4. **Refresh fuel on the bench.** Always have 5-10 unused creatives ready to deploy when the loop calls for refresh. The bottleneck is creative speed, not algorithm capability.

### The scaling loop in practice

```
Launch 25-30 → Identify 1-3 winners → Scale winners
   ↓                                       ↓
   ↓                              Hit ceiling on winner
   ↓                                       ↓
   ↓                              Convert to foundational
   ↓                              campaign (or ad set)
   ↓
   Duplicate ad set
   ↓
   Turn off the 1-3 winners (they live in the foundation)
   ↓
   Add 1-3 fresh creatives from the bench
   ↓
   Loop back to test the 22-29 + 3 new
```

If the 1-3 winners produced low-quality leads (per sales team feedback or call data), they don't get scaled — they get killed and the system loops with fresh angles.

### What the brief's "Creative volume target" means

Ideation generates against this target:

- **25-30+** — Andromeda standard. Default for $15K+/month Meta budgets.
- **20-25** — mid-budget. Slightly compressed but still respects the diversification principle.
- **10-15** — low-budget pilot. Acknowledges that you'll get fewer pockets matched but you preserve the messaging-diversity discipline.

Never go below 10 unique creatives. Below that, the Andromeda matching layer doesn't have enough signal to find pockets, and you're back to pre-Andromeda dynamics where a single hero ad can carry a campaign — which is no longer reliable.

### Source

Synthesized from Jeremy Haynes' 2025-2026 Meta best-practices content. Treat the principles as load-bearing; treat the specific numbers (25-30, 1-3 winners, 5+5+5 copy set) as well-tested defaults, not laws.

---

## 10. How the skills consume this doc

All three skills assume this methodology is loaded into working context before they run. They reference sections of this doc by number rather than re-embedding content.

**Ideator skill** loads:
- Section 1 (loop) — to know its position in the system
- Section 2 (vocabulary) — for shared term definitions
- Section 3 (frameworks, especially Three-Axis Articulation) — applied to generate distinct concepts
- Section 4 (funnel mapping) — to determine hook strategy across concepts
- Section 5 (vertical playbook) — only the playbook matching the brief's `Vertical` field
- Section 6 (visual heuristics) — to inform image prompt construction
- Section 7 (Ideation → ChatGPT batch format) — to format the batch image prompts correctly
- Section 9 (Andromeda playbook) — drives the volume target and three-axis approach

**Producer skill** loads:
- Section 2 (vocabulary) — for shared term definitions
- Section 3 (frameworks, especially Hopkins/Sugarman/Hormozi) — applied during copy drafting
- Section 4 (funnel mapping) — to determine copy register from declared funnel stage
- Section 5 (vertical playbook) — only the playbook matching the brief's `Vertical` field
- Section 8 (banned words) — enforced at draft time
- Section 9 (Andromeda playbook) — drives the copy-set model (5+5+5) instead of per-creative copy

**Critic skill** loads:
- Section 2 (vocabulary) — for shared term definitions
- Section 3 (frameworks) — used to ground each dimension's score
- Section 4 (funnel mapping) — to evaluate hook against expected awareness level
- Section 6 (visual heuristics) — used for the Visual Hierarchy & Platform Fit dimension
- Section 7 (Critique → ChatGPT regen format) — to format the regeneration prompt block correctly
- Section 8 (banned words) — applied as a Clarity penalty trigger

**Operator routing.** When an agent enters this folder via `Services/Meta-Ads/overview.md`, the routing instruction is: load this methodology first, then the relevant skill (Ideator, Producer, or Critic). Do not run a skill without the methodology in context.

---

*End of methodology.*
