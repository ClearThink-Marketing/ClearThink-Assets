# Step 4 — UVP Development

**Phase:** Weeks 3–4 · Strategy Development
**Produces:** Unique Value Proposition document + summary deck (client-facing deliverables)
**Previous step:** [3. Market Research](../3-Market-Research/)
**Next step:** [5. Offer Dev](../5-Offer-Dev/)

---

## What this step does

Takes raw, unstructured client input — UVP workshop transcripts, ICP and Market Research context — and produces a polished Unique Value Proposition document with synthesized differentiators, a draft UVP statement, an elevator pitch, and a positioning statement.

The UVP answers one fundamental question: **"Why should someone choose this business over every alternative, including doing nothing?"**

The UVP is the messaging backbone. It feeds into offer development, website copy, ad creative, sales scripts, and proposal language. A weak UVP means every downstream deliverable underperforms.

---

## Inputs

- **Client Portal** in Notion (from Step 1)
- **Completed ICP** — the ICP Analysis deliverable from Step 2 (the UVP must speak to a specific audience's specific pain points)
- **Completed Market Research** — landscape context from Step 3 (validates which differentiators will actually land)
- **UVP workshop transcript** in the Notion Transcripts database (from the Fathom → Zapier → Notion pipeline)
- **UVP templates** in [`templates/`](./templates/)

## Outputs

- **UVP document** (`.docx`) — populated from the single UVP template, stored in the client's Notion Portal
- **UVP summary deck** (`.pptx`) — populated from the single UVP deck template, stored in the client's Notion Portal

Unlike ICP and Market Research, UVP uses **a single template** (no B2B/B2C split) — positioning is business-specific, not audience-type-specific.

---

## Files in this folder

| File | Purpose |
|---|---|
| [`ClearLaunch_UVP_Skill_v1.md`](./ClearLaunch_UVP_Skill_v1.md) | Production skill — UVP Development Agent |
| [`templates/ClearLaunch_UVP_Template.docx`](./templates/ClearLaunch_UVP_Template.docx) | UVP document template (Word) |
| [`templates/ClearLaunch_UVP_Summary_Deck.pptx`](./templates/ClearLaunch_UVP_Summary_Deck.pptx) | UVP summary deck template (PowerPoint) |
| [`templates/uvp_workshop_template.md`](./templates/uvp_workshop_template.md) | Reference template — UVP workshop discovery questions |
| [`templates/build_uvp_template.py`](./templates/build_uvp_template.py) | Regenerates the `.docx` template |
| [`templates/build_uvp_deck.py`](./templates/build_uvp_deck.py) | Regenerates the `.pptx` deck |

---

## Trigger phrases

Invoke the skill with any of: *"process UVP"*, *"build UVP"*, *"UVP transcript"*, *"UVP workshop"*, *"unique value proposition"*, *"value prop"*, *"positioning"*, *"differentiation"*, *"messaging framework"*, *"elevator pitch"*, *"what makes them different"*, *"figure out their positioning"*, *"what should their message be"*.

---

## Reference databases (Notion)

- **Transcripts** (source — read UVP workshop transcript) — `collection://0f372290-8993-4c7e-b303-13afca181721`
- **Client Portals** (read ICP/MR context, write deliverables) — `collection://30e821ad-7ba9-8080-8f38-000ba9c44ad0`

---

## Known gaps

- **Skill file references old template paths.** Points to `Frameworks/...` (the old Templates-branch location). Needs updating to the new `templates/` subfolder path. Cleanup pass.

Note: unlike Steps 1–3, the UVP v1 skill **uses the correct 7-step labels** (matches ICP v2). No step-label misalignment.

---

*Step 4 of the 7-step ClearLaunch GTM process. See [`../overview.md`](../overview.md) for the full process flow.*
