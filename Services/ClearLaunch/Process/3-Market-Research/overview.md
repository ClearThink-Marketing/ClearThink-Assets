# Step 3 — Market Research

**Phase:** Weeks 3–4 · Strategy Development
**Produces:** Market landscape analysis document + summary deck (client-facing deliverables)
**Previous step:** [2. ICP](../2-ICP/)
**Next step:** [4. UVP](../4-UVP/)

---

## What this step does

Conducts a comprehensive market landscape analysis — keyword research, competitive SEO analysis, traffic intelligence, audience insights, and ad strategy review — and produces completed deliverables stored in the client's Notion portal.

Market research answers one fundamental question: **"Where do the opportunities and competitive gaps live?"**

The output directly shapes the UVP (what messaging will resonate), offer development (what people are actually looking for), and channel strategy (where to invest).

---

## Inputs

- **Completed ICP** in the client's Notion portal (from Step 2) — provides industry, target segments, pain points, competitor names
- **Client Portal** in Notion with onboarding data populated — specifically: client website URL, competitor URLs, seed keywords
- **Market Research templates** in [`templates/`](./templates/) (B2B or B2C, based on Business Type)
- **External tools** — Ahrefs and SimilarWeb data (pulled manually during the analysis)

## Outputs

- **Market Research document** (`.docx`) — populated from the appropriate B2B or B2C template, stored in the client's Notion Portal
- **Market Research summary deck** (`.pptx`) — populated from the appropriate B2B or B2C template, stored in the client's Notion Portal

---

## Files in this folder

| File | Purpose |
|---|---|
| [`ClearLaunch_Market_Research_Skill_v2.md`](./ClearLaunch_Market_Research_Skill_v2.md) | Production skill — Market Research Agent |
| [`templates/`](./templates/) | B2B and B2C `.docx` / `.pptx` templates |

---

## Trigger phrases

Invoke the skill with any of: *"market research"*, *"keyword research"*, *"competitive analysis"*, *"market landscape"*, *"SEO research"*, *"competitor audit"*, *"keyword data"*, *"search volume"*, *"Ahrefs"*, *"SimilarWeb"*, *"content gap"*, *"backlink analysis"*, *"look at their keywords"*, *"what are competitors doing"*, *"analyze this keyword data"*, *"run market research for [client]"*.

---

## Reference databases (Notion)

- **Client Portals** (read ICP + onboarding data, write deliverables) — `collection://30e821ad-7ba9-8080-8f38-000ba9c44ad0`

---

## Known gaps

- **No template builder script.** Unlike UVP, Offer Dev, and Channel Strategy (which each have dedicated `build_*_template.py` and deck builder scripts), Market Research has no Python tooling at all. Both `build_market_research_template.py` and `rebuild_market_research_decks.py` are follow-up items.
- **Skill uses old 7-step labels.** The skill's "How This Skill Fits" section merges UVP + Offer as Step 4 and splits Metrics/Roadmap into Steps 6 and 7. Same misalignment as the Onboarding skill. Cleanup pass.
- **Skill file references old template paths.** Points to `Frameworks/...` (the old Templates-branch location). Needs updating to the new `templates/` subfolder path. Cleanup pass.

---

*Step 3 of the 7-step ClearLaunch GTM process. See [`../overview.md`](../overview.md) for the full process flow.*
