# Step 1 — Onboarding

**Phase:** Weeks 1–2 · Onboarding & Discovery
**Produces:** Client Portal infrastructure (not a client-facing deliverable)
**Next step:** [2. ICP](../2-ICP/)

---

## What this step does

Validates that a new client's intake data is complete and structured correctly, then creates their Client Portal entry in Notion so every downstream step (ICP, Market Research, UVP, etc.) has what it needs to run.

This step produces **infrastructure, not deliverables.** No document, deck, or report goes to the client. What it creates is the foundation every other step depends on.

---

## Inputs

- **Tally form submission** from the client (lands automatically in the GTM Intake Notion database)
- **Notion access** — read from GTM Intake, write to Client Portals

## Outputs

- **Client Portal page** in Notion, structured for all downstream skills
- **GTM Intake row** status flipped to `Portal Created`

---

## Files in this folder

| File | Purpose |
|---|---|
| [`ClearLaunch_Onboarding_Skill_v1.md`](./ClearLaunch_Onboarding_Skill_v1.md) | Production skill — the agent that validates intake and creates the portal |
| [`ClearLaunch_Onboarding_Field_Mapping.md`](./ClearLaunch_Onboarding_Field_Mapping.md) | Reference — every Tally form field mapped to its Notion property and downstream consumer |

---

## Trigger phrases

Invoke the skill with any of: *"onboard client"*, *"new client"*, *"set up portal"*, *"check portal"*, *"onboarding check"*, *"validate client data"*, *"process intake"*, *"new intake submission"*, *"check GTM intake"*.

---

## Reference databases (Notion)

- **GTM Intake** (source — read) — `collection://476a46cc-8fab-428c-acb2-f82d61cf1fdd`
- **Client Portals** (destination — write) — `collection://30e821ad-7ba9-8080-8f38-000ba9c44ad0`
- **Transcripts** (linked later by downstream skills) — `collection://0f372290-8993-4c7e-b303-13afca181721`

---

*Step 1 of the 7-step ClearLaunch GTM process. See [`../overview.md`](../overview.md) for the full process flow.*
