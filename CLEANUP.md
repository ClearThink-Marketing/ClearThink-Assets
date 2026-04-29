# CLEANUP — Open Items

Running list of known issues, gaps, and follow-ups across the ClearThink-Assets repo. Items get checked off as they're resolved.

**Last updated:** 2026-04-29 (Web-Design Design-System §7 resolved; deferred work added)

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

## Canonical content reconciliation

- [ ] **ClearLaunch pricing mismatch.** `Services/ClearLaunch/ClearLaunch_GTM_Strategy_Blueprint.md` (v3.3) lists ClearLaunch at **$1,000 (or 2 payments of $500)**. Root `Overview.md` lists it at **$1,200 flat**. Overview.md is canonical — update the Blueprint to match.

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

## Web-Design Design-System — open design decisions

~~Surfaced from `Web-Design_Design-System_Context_Brief.md` §7 (2026-04-28).~~ **All six resolved 2026-04-29 in `Web-Design_Design-System_Round-1_Resolutions.md`.** Content commits unblocked.

- [x] ~~**7.1 Token schema philosophy.**~~ Locked: semantic-first, two-layer (primitive + semantic), ~25–30 color tokens. Components reference semantic tokens only.
- [x] ~~**7.2 Override file format.**~~ Locked: `client-tokens.json` canonical; `client-tokens.css` generated from it via small build script.
- [x] ~~**7.3 Where override files live.**~~ Locked: Notion canonical (decision record + archive), local working copy during build (`~/clients/[client-name]/design-tokens/`). No client data in repo (reaffirms Part 2 Decision 2).
- [x] ~~**7.4 AEC scope definition.**~~ Locked: AEC-Commercial = commercial AEC firms + custom residential builders. Specialty-Trades and Home-Services deferred to future verticals. Folder renamed `Verticals/AEC` → `Verticals/AEC-Commercial`.
- [x] ~~**7.5 Component library framework.**~~ Locked: HTML+Tailwind canonical in repo. Figma library + Webflow library are downstream artifacts (Frankee/Terry maintain in parallel).
- [x] ~~**7.6 Reference doc depth per file.**~~ Locked: file structure templates set for Tokens / Components / Universal Patterns / Vertical Patterns / Archetypes. Build `colors.md` first as the working example, refine the template through use, then replicate.

---

## Web-Design Design-System — deferred work

Items deferred from Round 1 resolutions; surface as their triggers arrive.

- [ ] **`Specialty-Trades` vertical scaffold** — when first specialty trades client (cabinetry, masonry, hardscaping, pool builders, etc.) lands.
- [ ] **`Home-Services` vertical scaffold** — when first home services client (HVAC, plumbing, electrical, roofing) lands.
- [ ] **Token JSON→CSS build script** — generates `client-tokens.css` from `client-tokens.json` (and component utility CSS, per §7.5). ~30 lines, Python or Node. Location and language TBD.
- [ ] **Figma library** — Frankee maintains, mirrors HTML reference. Post content commits.
- [ ] **Webflow library** — built from HTML reference. Post content commits.
- [ ] **`Client-Override-Pattern.md` content commit** — documents the lifecycle (Notion canonical → local working copy → archive). After token system completes.

---

*Update the "Last updated" date when items are added, removed, or checked off. When an item is complete, strike through (or delete) rather than leaving a ghost entry.*
