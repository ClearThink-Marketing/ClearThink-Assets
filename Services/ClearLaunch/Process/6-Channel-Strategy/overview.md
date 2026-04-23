# Step 6 — Channel Strategy & Customer Journey

**Phase:** Weeks 5–6 · Channel & Roadmap
**Produces:** Channel strategy document + summary deck + projections workbook (client-facing deliverables)
**Previous step:** [5. Offer Dev](../5-Offer-Dev/)
**Next step:** [7. Metrics & Roadmap](../7-Metrics-Roadmap/) *(not yet built)*

---

## What this step does

Analyzes all upstream deliverables (ICP, Market Research, UVP, Offer Dev), evaluates viable marketing channels, recommends a focused channel mix with budget allocation and performance projections, and — after a client decision call — maps the complete customer journey across the confirmed channels.

The Channel Strategy answers one fundamental question: **"Where should we show up, and what should we expect?"**

---

## Two-phase workflow

This is the only ClearLaunch step that runs in **two phases**:

| Phase | What happens | Input | Output |
|---|---|---|---|
| **A — Internal Analysis** | Terry runs the skill to generate the channel strategy (matrix, scoring, projections, budget). No client call yet. Terry presents findings. | Upstream deliverables (ICP, MR, UVP, Offer) | Channel matrix, projections workbook, recommendations |
| **Client Decision Call** | Client reviews the strategy, decides where to focus resources, provides industry-specific customer journey insights. Call runs through the 6-step Fathom → Zapier → Notion pipeline. | Call conversation | Fathom transcript in Notion Transcripts DB |
| **B — Journey Build** | Skill reads the Fathom transcript and completes the customer journey map on top of the confirmed channels. | Transcript + confirmed channels | Full customer journey deliverable |

Channel selection comes **before** journey mapping. The journey is built on top of the confirmed channels — not the other way around.

---

## Inputs

- **All upstream deliverables** (Steps 1–5) in the client's Notion Portal
- **Phase B only:** Channel Strategy transcript in the Notion Transcripts database (from the Fathom → Zapier → Notion pipeline)
- **Templates** in [`templates/`](./templates/) (single set — no B2B/B2C split)

## Outputs

- **Channel Strategy document** (`.docx`) — channel matrix, scoring, recommendations, journey map
- **Channel Strategy summary deck** (`.pptx`)
- **Projections workbook** (`.xlsx`) — channel-level budget allocation and performance projections

---

## Files in this folder

| File | Purpose |
|---|---|
| [`ClearLaunch_Step6_ChannelStrategy_Skill_v1.md`](./ClearLaunch_Step6_ChannelStrategy_Skill_v1.md) | Production skill — Channel Strategy & Customer Journey Agent (two-phase) |
| [`templates/ClearLaunch_Step6_ChannelStrategy_Template.docx`](./templates/ClearLaunch_Step6_ChannelStrategy_Template.docx) | Channel strategy document template (Word) |
| [`templates/ClearLaunch_Step6_ChannelStrategy_Summary_Deck.pptx`](./templates/ClearLaunch_Step6_ChannelStrategy_Summary_Deck.pptx) | Summary deck template (PowerPoint) |
| [`templates/ClearLaunch_Step6_Projections_Template.xlsx`](./templates/ClearLaunch_Step6_Projections_Template.xlsx) | Projections workbook template (Excel) |
| [`templates/channel_strategy_template.md`](./templates/channel_strategy_template.md) | Reference template — channel strategy discovery structure |
| [`templates/build_step6_templates.py`](./templates/build_step6_templates.py) | Regenerates the `.docx` template |
| [`templates/build_step6_deck.py`](./templates/build_step6_deck.py) | Regenerates the `.pptx` deck |
| [`templates/build_step6_projections.py`](./templates/build_step6_projections.py) | Regenerates the `.xlsx` projections workbook |

---

## Trigger phrases

**Phase A (internal analysis):** *"generate channel strategy"*, *"build channel strategy for"*, *"channel analysis for"*, *"evaluate channels for"*, *"Step 6 for"*, *"where should they advertise"*, *"which channels"*, *"channel recommendation"*.

**Phase B (journey build after call):** *"complete journey map"*, *"build journey map for"*, *"process channel strategy transcript"*, *"journey map for"*, *"finish Step 6 for"*.

**Revision:** *"revise channel strategy for"*, *"update channel strategy for"*.

---

## Reference databases (Notion)

- **Client Portals** (read all upstream deliverables, write all three Step 6 deliverables) — `collection://30e821ad-7ba9-8080-8f38-000ba9c44ad0`
- **Transcripts** (Phase B only — read channel strategy call transcript) — `collection://0f372290-8993-4c7e-b303-13afca181721`

---

## Known gaps

- **Skill file references old template paths.** Points to `Frameworks/...` (the old Templates-branch location). Needs updating to the new `templates/` subfolder path. Cleanup pass (same as all prior steps).

**Naming note:** this skill's filename uses `Step6_ChannelStrategy` (PascalCase, numbered prefix) while other skills use descriptive names like `Offer_Dev` or `Market_Research`. Consider normalizing in a future cleanup pass — not blocking.

---

*Step 6 of the 7-step ClearLaunch GTM process. See [`../overview.md`](../overview.md) for the full process flow.*
