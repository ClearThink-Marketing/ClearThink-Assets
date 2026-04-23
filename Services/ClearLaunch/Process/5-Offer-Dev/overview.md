# Step 5 — Offer Development

**Phase:** Weeks 3–4 · Strategy Development
**Produces:** Offer Development document + summary deck (client-facing deliverables)
**Previous step:** [4. UVP](../4-UVP/)
**Next step:** [6. Channel Strategy](../6-Channel-Strategy/)

---

## What this step does

Takes raw, unstructured client input — offer workshop transcripts, ICP and UVP context — and produces a polished Offer Development document with a complete 3-tier offer ladder (Micro → Macro → Core), creative angles mapped to ICP pain points, and objection-handling frameworks grounded in the UVP.

The Offer Ladder answers one fundamental question: **"How do we turn a stranger into a loyal customer through a series of low-risk, high-value steps?"**

The Offer Ladder turns messaging into revenue. The Micro Offer becomes the lead magnet for awareness-stage channels, the Macro Offer defines what consideration-stage content needs to exist, and the Core Offer anchors long-term revenue and retention strategy.

---

## Inputs

- **Client Portal** in Notion (from Step 1)
- **Completed ICP** (from Step 2) — pain points, customer segments
- **Completed Market Research** (from Step 3) — demand and pricing context
- **Completed UVP** (from Step 4) — differentiators, positioning, objection handling
- **Offer workshop transcript** in the Notion Transcripts database (from the Fathom → Zapier → Notion pipeline)
- **Offer Dev templates** in [`templates/`](./templates/)

## Outputs

- **Offer Development document** (`.docx`) — populated with the Micro/Macro/Core ladder, stored in the client's Notion Portal
- **Offer Development summary deck** (`.pptx`) — populated from the deck template, stored in the client's Notion Portal

Single template — no B2B/B2C split.

---

## Files in this folder

| File | Purpose |
|---|---|
| [`ClearLaunch_Offer_Dev_Skill_v1.md`](./ClearLaunch_Offer_Dev_Skill_v1.md) | Production skill — Offer Development Agent |
| [`templates/ClearLaunch_Offer_Dev_Template.docx`](./templates/ClearLaunch_Offer_Dev_Template.docx) | Offer document template (Word) |
| [`templates/ClearLaunch_Offer_Dev_Summary_Deck.pptx`](./templates/ClearLaunch_Offer_Dev_Summary_Deck.pptx) | Offer summary deck template (PowerPoint) |
| [`templates/offer_dev_template.md`](./templates/offer_dev_template.md) | Reference template — offer workshop discovery structure |
| [`templates/build_offer_dev_template.py`](./templates/build_offer_dev_template.py) | Regenerates the `.docx` template |
| [`templates/build_offer_dev_deck.py`](./templates/build_offer_dev_deck.py) | Regenerates the `.pptx` deck |

---

## Trigger phrases

Invoke the skill with any of: *"process Offer Dev"*, *"process Offer"*, *"build offer ladder"*, *"offer development"*, *"offer transcript"*, *"offer workshop"*, *"3-tier ladder"*, *"Micro Macro Core"*, *"design the offer"*, *"what should they sell"*, *"build their offer stack"*, *"offer strategy"*.

---

## Reference databases (Notion)

- **Transcripts** (source — read offer workshop transcript) — `collection://0f372290-8993-4c7e-b303-13afca181721`
- **Client Portals** (read ICP/MR/UVP context, write deliverables) — `collection://30e821ad-7ba9-8080-8f38-000ba9c44ad0`

---

## Known gaps

- **Skill file references old template paths.** Points to `Frameworks/...` (the old Templates-branch location). Needs updating to the new `templates/` subfolder path. Cleanup pass (same as all prior steps).

Note: Offer Dev v1 skill uses the correct 7-step labels (matches ICP v2, UVP v1). No step-label misalignment.

---

*Step 5 of the 7-step ClearLaunch GTM process. See [`../overview.md`](../overview.md) for the full process flow.*
