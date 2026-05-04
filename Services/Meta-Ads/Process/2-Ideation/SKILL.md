---
name: meta-static-ad-ideator
description: "Generate the creative concept set for a Meta or Instagram static ad campaign — strategic recommendations + 25-30 distinct creative concepts with image prompts and angle directions. Use this skill whenever the user wants to brainstorm ad concepts, explore creative angles, analyze competitor ads, or generate the upfront creative set for a Meta campaign. Triggers include: 'ideate ads', 'creative concepts for [client]', 'brainstorm ad angles', 'explore creative directions', 'analyze competitor ads', 'generate ad ideas', 'creative angle exploration', 'what should we test on Meta', 'ad concepts', 'creative set for [campaign]'. Designed around Andromeda's messaging-diversification requirement: produces a high-volume creative concept set, not a small number of polished variations. The image prompts feed forward to ChatGPT for batch rendering; the concepts then route to the meta-static-ad-producer skill which generates the shared copy set."
---

# Meta Static Ad Ideator

## What this skill does

Generates the upfront **creative concept set** for a Meta/Instagram static ad campaign. Output is the divergent-exploration phase of the loop — the 25-30 distinct angles the campaign will test, each with an image prompt for ChatGPT and an angle blurb explaining the creative thinking.

Output per run:

1. **Strategic recommendations** — Claude's reasoning about lever choice, top angles, competitor patterns, what to test vs. what to avoid
2. **N creative concepts** (where N = brief's Creative volume target, default 25-30):
   - Concept name (5-10 words)
   - Angle blurb (1-2 sentences explaining what this concept is going for)
   - Hook direction (one-line headline/hook idea)
   - Image generation prompt (paste-into-ChatGPT, formatted per Methodology §7)

The image prompts get rendered in batch by ChatGPT. The concepts then feed forward to the Producer skill, which generates the shared copy set (5 headlines + 5 body copy + 5 descriptions) that rotates across the rendered creatives.

## Required reading before running

This skill is **not self-contained**. Before generating, load the canonical methodology:

- **`Services/Meta-Ads/Meta-Ads_Methodology.md`** — frameworks (especially the Three-Axis Articulation Framework in §3), Andromeda playbook (§9), funnel mapping, vertical playbooks, visual heuristics, banned words, handoff vocabulary

The Andromeda playbook (§9) explains why we generate 25-30 concepts and not 3. The Three-Axis Articulation Framework (§3) is the structured way to generate that many distinct concepts from a single chosen lever. Without these in working context, the skill produces a small number of generic concepts.

## Inputs

This skill flexibly accepts any combination of three input types. Use whatever the strategist provides; ask for more only if there's a critical gap.

### Input A: Brief (any state — partial or full)

The Ad Brief MD (template at `Services/Meta-Ads/Process/1-Brief/templates/ad-brief-template.md`). Ideation can run on:
- A **fully completed brief** — generate concepts directly against the locked lever, vertical, ICP, and funnel stage
- A **partial brief** — Ideation may *recommend* the primary lever (Section 5) and/or specific angles based on the rest of the brief, the competitor evidence, and the strategist notes. The strategist confirms before locking.
- A **raw company-context paste** with no formal brief — treat as partial; flag missing fields.

The brief's `Creative volume target` field (Section 7) determines how many concepts to generate.

### Input B: Competitor ad images / screenshots

Optional. Strategist pastes or uploads competitor ads. Use vision to extract:
- The lever each competitor is pulling
- The angle/concept of each ad
- Hook construction and visual style
- What's working (steal these patterns) vs. what's not (avoid)

Output a competitor pattern observation in the strategy section explaining what the market is doing and where the gaps are.

### Input C: Strategist notes / creative angles

Optional. Free-form notes from the strategist on:
- Hypotheses they want to test
- Angles they're already considering
- Voice or visual constraints from the client
- Trends or seasonal context they've observed

Treat these as priors. If a strategist-suggested angle is strong, include it (and credit the source in the strategy section). If a strategist-suggested angle is weak (wrong lever, wrong funnel stage, generic), say so.

## Process

### Step 1 — Read everything
Read the brief end-to-end, then any competitor ads, then strategist notes. Identify what's locked vs. what's open.

### Step 2 — Determine or confirm the primary lever
If the brief's Section 5 has a primary Life Force locked, work with it. If it's blank or ambiguous:
- Read ICP (Section 3), offer (Section 2), and competitor evidence
- Recommend a primary lever with reasoning
- Note 1-2 alternative levers worth considering
- Flag this as "for strategist confirmation before locking" in the output

### Step 3 — Map funnel stage to concept register
Use the funnel → awareness → hook strategy table in **Methodology §4**. The 25-30 concepts should all match the declared funnel stage's emotional register (TOF cold = pain-naming, pattern interrupts; MOF warm = differentiation, objection-handling; BOF retarget = urgency, risk reversal).

### Step 4 — Apply the vertical playbook
Read the playbook in **Methodology §5** that matches the brief's `Vertical` field. This determines visual direction defaults, which levers tend to win, and what to avoid. Do not blend playbooks across verticals.

### Step 5 — Run the Three-Axis Articulation exercise
This is the core of the skill. For the locked primary lever, generate concept seeds across three axes (per **Methodology §3 Three-Axis Articulation Framework**):

- **Problems** — list 8-12 specific problems the ICP has *right now*. Concrete and named, not abstract.
- **Circumstances** — list 8-12 situations, life stages, recent changes, seasons, or contexts that make the offer relevant *right now*.
- **Outcomes** — list 8-12 specific dream states, transformations, or measurable endpoints the ICP wants.

Don't optimize for novelty inside this list — exhaustive over clever. The next step culls.

### Step 6 — Cull and combine into N concepts
From the three-axis lists, build N distinct concepts (where N = creative volume target). Each concept is a tight pairing of one specific axis-item with a creative angle. Examples:

- *Problem axis × Visual angle*: "The slow damage you don't see" — pairs the Problem ("UV damage building under the surface") with a visual angle (close-up before/after under macro lens).
- *Circumstance axis × Social proof angle*: "Your neighbor just had this done" — pairs the Circumstance (it's spring, neighbors are visibly servicing their homes) with a social proof angle (a real Atlanta street photo).
- *Outcome axis × Direct angle*: "Back to brand-new in 3 hours" — pairs the Outcome (specific time-to-result) with a direct visual of the finished work.

Each concept must be **meaningfully distinct** from the others. Two concepts with the same hook idea reworded are one concept, not two. Aim for genuine messaging diversity — that's what Andromeda needs.

### Step 7 — Write the image generation prompt per concept
Use the exact "Ideation → ChatGPT (batch)" template from **Methodology §7**. Include the `CONCEPT [N of 25-30]` field naming the concept so ChatGPT (and the strategist) can track which render is which.

### Step 8 — Write the strategy section
Synthesize:
- **Locked lever** (or recommended, if brief was open)
- **Reasoning**: why this lever for this ICP at this funnel stage
- **Top 3-5 angles ranked**: which concepts you most expect to win, with rationale
- **Competitor patterns observed**: what the market is doing, what to steal, what to avoid
- **What to test vs. avoid**: explicit guidance on the most-vs-least-likely-to-work directions

### Step 9 — Render output
Strategy section first, then numbered concepts. See output format below.

## Output format

```
# Ideation Output: [client name] — [campaign / round identifier]

## Strategy

**Primary lever (locked / recommended):** [LF#X — name]
[Reasoning: 2-3 sentences on why this lever for this ICP at this funnel stage]

**Top 3-5 angles ranked (by expected performance):**
1. Concept #[N] — [reason]
2. Concept #[N] — [reason]
3. Concept #[N] — [reason]
[etc.]

**Competitor patterns observed:**
- [Pattern 1 — what to steal or avoid]
- [Pattern 2 — what to steal or avoid]
- [Gap in market — direction nobody's running]

**What to test vs. avoid:**
- ✅ Test: [direction] — because [reason]
- ✅ Test: [direction] — because [reason]
- ❌ Avoid: [direction] — because [reason]
- ❌ Avoid: [direction] — because [reason]

## Concepts ([N total])

### Concept 1: [name in 5-10 words]

**Angle blurb:** [1-2 sentences explaining what this concept is going for]

**Hook direction:** "[one-line headline/hook idea]"

**Image generation prompt:**
[full structured block per Methodology §7 Ideation → ChatGPT format]

---

### Concept 2: [name in 5-10 words]

[same structure]

---

[continue through Concept N]
```

If the user wants the output in a `.docx` or `.pdf` for handoff, save one. Default is inline.

## What to push back on

If the strategist provides any of the following, flag before generating:

- **No ICP definition.** The whole skill is built on articulating angles for a specific pocket. Without an ICP, you're guessing.
- **Vertical not declared.** The vertical playbook drives visual direction defaults — you can't generate good image prompts without knowing whether this is DTC, local services, or B2B.
- **Funnel stage not declared.** TOF, MOF, and BOF concepts look fundamentally different. Without it, half the concepts will be wrong-register.
- **Creative volume target not set.** Default to 25-30 if missing, but flag — the strategist should have made this call based on budget.
- **Competitor ads provided but they're all from the same brand.** One competitor isn't a market read. Push for 3+ competitors before drawing pattern conclusions.

It's better to send the strategist back for 5 minutes of clarification than produce 25 concepts built on a shaky brief.

## Important notes

- **Volume over polish.** This skill produces concepts, not finished ads. The image prompts are paste-and-go for ChatGPT; the angle blurbs are for the strategist's understanding. Don't optimize each concept like you're shipping it — the next step (refinement + Production copy set) does the polish.
- **Three-axis ≠ three concepts per axis.** The framework is a generation tool, not a quota. A campaign might end up with 18 problem-axis concepts, 8 circumstance-axis, and 4 outcome-axis if that's where the strongest angles land.
- **Don't invent levers the brief explicitly excluded.** Section 5 has an "Explicitly avoid" field. Respect it.
- **Concepts must be genuinely distinct.** "Tired of dirty windows?" and "Sick of dirty windows?" are one concept. Reuse of structural patterns across all 25-30 means you've generated 5 concepts and 25 wrappers. That defeats the Andromeda purpose.
- **The image prompts are the handoff.** Each must be self-contained. Don't reference the brief inside them.
- **Paired with the Producer.** Once concepts ship and ChatGPT renders the images, the strategist refines (drops weak renders, iterates on borderline ones), then runs the Producer (`Services/Meta-Ads/Process/3-Production/SKILL.md`) to generate the shared copy set that rotates across the final image set.
