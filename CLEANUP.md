# CLEANUP — Open Items

Running list of known issues, gaps, and follow-ups across the ClearThink-Assets repo. Items get checked off as they're resolved.

**Last updated:** 2026-05-03 (Deferred to Form.md inventory added)

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

## Deferred to Form.md

Decisions accumulated from `Core/Components/` files (button, input) that defer to `Form.md` for resolution. Form is not yet scoped or built — chat decided (option B per process-observations 2026-05-03) to track an inventory here rather than scope Form prematurely. Each item resolves when `Form.md` is drafted.

- [ ] **HTML `disabled` form-level submission exclusion.** Distinct from `aria-disabled` + `input-disabled` (visual disabled state on the input element). Form will document when to use the HTML attribute for native browser-level submission exclusion vs. the visual state utility for unavailable-but-still-focusable interactions. (Source: `input.md` §5 implementation note, §9 disabled annotation, §12 cross-reference.)
- [ ] **Validation patterns and lifecycle.** When validation runs (on blur, on submit, debounced on change), how errors propagate to `aria-invalid` + `input-error` utility class, how error text replaces helper text. (Source: `input.md` §5 "No success state" + §10 mistake on hardcoded error colors.)
- [ ] **Submission behavior.** Full label-input-helper-error-button composition pattern as a reusable form-field unit. (Source: `input.md` §12 [Form] cross-reference.)
- [ ] **`autocomplete` attribute conventions.** Which values to use on which field types (`email`, `tel`, `name`, `street-address`, etc.). Conversion-rate-relevant for ClearThink lead-gen forms. (Source: `input.md` §10 mistake #5.)
- [ ] **Form-button labeling convention.** "Send proposal" not "Submit" — action verb describing what happens, not generic submit. (Source: `button.md` §10 common mistakes.)

---

*Update the "Last updated" date when items are added, removed, or checked off. When an item is complete, strike through (or delete) rather than leaving a ghost entry.*
