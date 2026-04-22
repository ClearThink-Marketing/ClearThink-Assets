# Step 2 — ICP Development

**Phase:** Weeks 3–4 · Strategy Development
**Produces:** Ideal Client Profile document + summary deck (client-facing deliverables)
**Previous step:** [1. Onboarding](../1-Onboarding/)
**Next step:** [3. Market Research](../3-Market-Research/)

---

## What this step does

Takes raw, unstructured client input — call transcripts, onboarding notes, questionnaire responses — and produces a polished Ideal Client Profile with deliverables stored in the client's Notion portal.

The ICP answers one fundamental question: **"Which customers should this client pursue?"**

The ICP is foundational. Every downstream deliverable (Market Research, UVP, Offer, Channel Strategy) depends on getting this right.

---

## Inputs

- **Client Portal** in Notion (created in Step 1)
- **Transcript page** in the Notion Transcripts database (from the Fathom → Zapier → Notion pipeline, after an ICP Discovery call or workshop)
- **ICP templates** in [`templates/`](./templates/) (B2B or B2C, selected based on the client's Business Type field from onboarding)

## Outputs

- **ICP document** (`.docx`) — populated from the appropriate B2B or B2C template, stored in the client's Notion Portal
- **ICP summary deck** (`.pptx`) — populated from the appropriate B2B or B2C template, stored in the client's Notion Portal

---

## Files in this folder

| File | Purpose |
|---|---|
| [`ClearLaunch_ICP_Skill_v2.md`](./ClearLaunch_ICP_Skill_v2.md) | Production skill — ICP Development Agent |
| [`templates/`](./templates/) | B2B and B2C `.docx` / `.pptx` templates and the `rebuild_icp_decks.py` script |

---

## Trigger phrases

Invoke the skill with any of: *"process ICP"*, *"build ICP"*, *"ICP transcript"*, *"ICP Discovery call analysis"*, *"ideal client profile"*, *"ideal customer profile"*, *"target audience definition"*, *"customer segmentation"*, *"who should we target"*, *"figure out their ideal customer"*, *"process new transcripts"*.

---

## Reference databases (Notion)

- **Transcripts** (source — read) — `collection://0f372290-8993-4c7e-b303-13afca181721`
- **Client Portals** (destination — write deliverables) — `collection://30e821ad-7ba9-8080-8f38-000ba9c44ad0`
- **GTM Intake** (read — Business Type + industry context) — `collection://476a46cc-8fab-428c-acb2-f82d61cf1fdd`

---

## Known gaps

- **No `.docx` template builder script.** `rebuild_icp_decks.py` regenerates the `.pptx` summary decks, but the `.docx` templates are crafted artifacts with no regeneration path. Other steps (UVP, Offer Dev, Channel Strategy) have both a deck-builder and a template-builder script. Building a `build_icp_template.py` is a follow-up.
- **Skill file references old template paths.** The skill points to `Frameworks/...` (the old Templates-branch location). Those references will need updating to the new `templates/` subfolder path. Follow-up cleanup pass.

---

*Step 2 of the 7-step ClearLaunch GTM process. See [`../overview.md`](../overview.md) for the full process flow.*
