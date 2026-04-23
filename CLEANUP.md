# CLEANUP — Open Items

Running list of known issues, gaps, and follow-ups across the ClearThink-Assets repo. Items get checked off as they're resolved.

**Last updated:** 2026-04-22

---

## Skill files

### Path references to update (migration follow-up)

All six ClearLaunch skills reference old `Frameworks/...` template paths. After migration, templates live at `Services/ClearLaunch/Process/<step>/templates/`. Skills need their path references updated — decide convention first (relative paths like `templates/foo.docx` vs. full repo paths like `Services/ClearLaunch/Process/4-UVP/templates/foo.docx`).

- [ ] `Services/ClearLaunch/Process/1-Onboarding/ClearLaunch_Onboarding_Skill_v1.md`
- [ ] `Services/ClearLaunch/Process/2-ICP/ClearLaunch_ICP_Skill_v2.md`
- [ ] `Services/ClearLaunch/Process/3-Market-Research/ClearLaunch_Market_Research_Skill_v2.md`
- [ ] `Services/ClearLaunch/Process/4-UVP/ClearLaunch_UVP_Skill_v1.md`
- [ ] `Services/ClearLaunch/Process/5-Offer-Dev/ClearLaunch_Offer_Dev_Skill_v1.md`
- [ ] `Services/ClearLaunch/Process/6-Channel-Strategy/ClearLaunch_Step6_ChannelStrategy_Skill_v1.md`

### Step-label alignment

Two skills use the old framework labels (merge UVP + Offer Dev as "Step 4: Value Proposition & Offer Engineering"; split Metrics/Roadmap into Steps 6 and 7). Update to match the current 7-step framework in `AGENTS.md` (and ICP v2, UVP v1, Offer Dev v1, Channel Strategy v1, which are already correct).

- [ ] `Services/ClearLaunch/Process/1-Onboarding/ClearLaunch_Onboarding_Skill_v1.md`
- [ ] `Services/ClearLaunch/Process/3-Market-Research/ClearLaunch_Market_Research_Skill_v2.md`

### Naming consistency

- [ ] Rename `ClearLaunch_Step6_ChannelStrategy_Skill_v1.md` → `ClearLaunch_Channel_Strategy_Skill_v1.md` to match descriptive naming pattern used by other skills (Offer_Dev, Market_Research, etc.)

---

## Missing Python tooling

- [ ] **ICP — build `build_icp_template.py`.** `rebuild_icp_decks.py` regenerates the `.pptx` summary decks but there's no equivalent for the `.docx` templates. Other steps (UVP, Offer Dev, Channel Strategy) have both deck and template builders.
- [ ] **Market Research — build Python tooling from scratch.** No build scripts exist at all — neither `build_market_research_template.py` nor `rebuild_market_research_decks.py`.

---

## Missing structure

### ClearLaunch Step 7

- [ ] Build Step 7 (Metrics-Roadmap) end-to-end: folder, skill, templates (`.docx` + `.pptx`), build scripts, `overview.md`

### Service lines

- [ ] SEO-Retainer — folder scaffold + skills + templates + overview
- [ ] Web-Design — folder scaffold + skills + templates + overview
- [ ] Meta-Ads — pricing/scope decision first (see Open context items), then folder + content

### Top-level folders

- [ ] `Operations/` — cross-service workflows (Notion, Zapier, portals)
- [ ] `Finance/` — pricing models, projections
- [ ] `Marketing/` — ClearThink-as-a-company marketing assets (Capabilities Statement, etc.)
- [ ] `Archived/` — deprecated content

---

## Branch retirement

- [ ] **Retire legacy `Skills/ICP_Skill.md`** (pre-v2 draft) still living on the `Skill-Assets` branch
- [ ] **Archive old branches after verification.** Once everything is confirmed migrated and working on `main`: archive `GTM-Strategy`, `Skill-Assets`, and `Templates` branches (probably via tag + delete, so history is preserved but branches don't confuse agents)

---

## Open questions

- [ ] **Claude Desktop skill deployment pipeline.** When skills live in per-step folders on `main` instead of `Skill-Assets/Skills/` root, how does the Claude Desktop deployment flow find them? Confirm current flow and document.
- [ ] **Path convention for skill updates.** When updating skill files in the path-references item above, decide: relative paths (`templates/foo.docx`) or full repo paths (`Services/ClearLaunch/Process/4-UVP/templates/foo.docx`)? Convention needs to be set before the fix is applied uniformly.

---

## Open context items (from Part 1 session brief)

- [ ] Meta Ads pricing/scope — currently TBD in `Overview.md`
- [ ] Case studies / client wins — to be added as engagements conclude and results are documented
- [ ] Social profiles — skipped initially; add when profiles are active
- [ ] Typography in `Brand/guidelines.md` — currently TBD; sourced from existing `.docx` / `.pptx` template fonts

---

*Update the "Last updated" date when items are added, removed, or checked off. When an item is complete, strike through (or delete) rather than leaving a ghost entry.*
