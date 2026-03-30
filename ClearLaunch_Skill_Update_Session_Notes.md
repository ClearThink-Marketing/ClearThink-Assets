# ClearLaunch Skill Update — Session Notes
**Last Updated:** March 29, 2026
**Status:** Onboarding infrastructure COMPLETE | Zapier GTM Intake → Slack zap LIVE | ICP Skill v2.0 Complete | Market Research Skill v2.0 Complete | Documentation updated to 7-step process (v3.0) | Ready for end-to-end testing

---

## Current Build Status

| Component | Status | Location |
|---|---|---|
| Tally Onboarding Form | COMPLETE | [tally.so/r/Ekk6dr](https://tally.so/r/Ekk6dr) — Business Type field added |
| GTM Intake Database | COMPLETE | Notion: Database Hub - ClearThink → GTM Intake |
| Onboarding Skill v1 | COMPLETE | `Skills/ClearLaunch_Onboarding_Skill_v1.md` |
| Onboarding Field Mapping | COMPLETE | `Skills/ClearLaunch_Onboarding_Field_Mapping.md` |
| ICP Templates (B2B + B2C) | COMPLETE | `Frameworks/` (4 files) |
| ICP Summary Decks (B2B + B2C) | COMPLETE (rebuilt) | `Frameworks/` (0 layout issues, brand applied) |
| ICP Agent Skill v2 | COMPLETE | `Skills/ClearLaunch_ICP_Skill_v2.md` |
| Market Research Templates (B2B + B2C) | COMPLETE | `Frameworks/` (4 files, 15 tables each) |
| Market Research Agent Skill v2 | COMPLETE | `Skills/ClearLaunch_Market_Research_Skill_v2.md` |
| Zapier: GTM Intake → Slack | COMPLETE | Triggers on new GTM Intake item, posts to #internal-notifications via Digital VA bot |
| GTM Strategy Blueprint | COMPLETE (v3.0) | `ClearLaunch_GTM_Strategy_Blueprint.md` |
| QA Checklist | COMPLETE | `ClearLaunch_QA_Checklist.md` |
| Value Proposition Template | NOT STARTED | — |
| Offer Engineering Template | NOT STARTED | — |
| Customer Journey Template | NOT STARTED | — |
| Metrics/KPI Template | NOT STARTED | — |
| Implementation Roadmap Template | NOT STARTED | — |

---

## What Was Accomplished (March 29, 2026 — Session 4)

### Zapier GTM Intake → Slack Notification

1. **Zapier zap built and tested** — New Database Item trigger on GTM Intake DB → Send Channel Message to `#internal-notifications` via Digital VA bot (🤖). Message format: "📋 New GTM Intake Submission: [Company Name] — [Business Type]. Run process new intake in Claude Code to create the client portal."
2. **End-to-end test passed** — Dummy Tally form submission (Acme Test Co) confirmed landing in GTM Intake DB and Slack notification firing correctly.

### Documentation Overhaul — 7-Step Process

3. **Renumbered from 6 steps to 7 steps** — Onboarding moved from "Step 0" to Step 1. All subsequent steps shifted up by 1 (ICP → Step 2, MR → Step 3, Value Prop → Step 4, Channel → Step 5, KPIs → Step 6, Roadmap → Step 7).
4. **Clarified onboarding vs ICP Discovery call** — Step 1 now documents two workflows: Workflow A (Tally form → portal creation, agent-processed) and Workflow B (onboarding call → transcript stored for reference only, not agent-processed). All "discovery call" references renamed to "ICP Discovery call" across all files.
5. **Blueprint updated to v3.0** — 7-step process, updated data flow diagrams, infrastructure architecture, tool descriptions, framework registry, build priorities, and open questions.
6. **All 4 Mermaid diagrams updated** — System Architecture, Step-by-Step Data Flow, Tool Responsibility Map, and Onboarding Flow all reflect 7-step numbering, ICP Discovery naming, and the Zapier → Slack notification path.
7. **14 skill files updated on Skill-Assets branch** — Onboarding Skill, ICP Skill, MR Skill, Field Mapping, 9 Claude Desktop skill files, and 1 legacy skill file — all renumbered and renamed via git worktree.
8. **QA Checklist created** — `ClearLaunch_QA_Checklist.md` tracks Ahrefs/SimilarWeb subscription requirements, end-to-end flow verification status, and cleanup items.

---

## What Was Accomplished (March 26, 2026 — Session 3)

### Onboarding Infrastructure (Upstream Item #1 Resolved)

1. **GTM Intake database created in Notion** — 31 properties (29 form fields + Status + Submitted), lives in Database Hub - ClearThink. Tally native integration sends form submissions directly here (no Zapier needed).
2. **Onboarding Skill v1 built** — `Skills/ClearLaunch_Onboarding_Skill_v1.md`. Reads intake data, validates fields against a 3-tier checklist (Critical/Important/Context), duplicates the Client Template Page, populates the Client Information sub-page, and scaffolds the Reports section. Two modes: automated (from Tally submissions) and manual (fallback).
3. **Field Mapping Document built** — `Skills/ClearLaunch_Onboarding_Field_Mapping.md`. Maps all 29 Tally fields to Notion properties and identifies which downstream skills consume each field. Documents gaps (Business Type field missing, Company Name should be required, Seed Keywords should be required).
4. **GTM Blueprint updated to v2.1** — Added Step 0 (Onboarding) section, updated build status table, resolved Open Question #1, added new open question about Business Type field.
5. **Notion MCP access confirmed** — The `claude.ai Notion` connector works in VS Code after removing duplicate local MCP server entries. No API token needed.
6. **Notion database IDs documented** — GTM Intake: `collection://476a46cc-8fab-428c-acb2-f82d61cf1fdd`, Client Portals: `collection://30e821ad-7ba9-8080-8f38-000ba9c44ad0`, Transcripts: `collection://0f372290-8993-4c7e-b303-13afca181721`

---

## What Was Accomplished (March 24-26, 2026)

### Session: March 24

1. **Market Research Frameworks** — All 8 ClearLaunch framework files built, branded, living in `Frameworks/`
2. **ICP Skill v1.0** — Built from scratch with Notion data flow, B2B/B2C extraction, tiering logic
3. **Client Portal Template** — Reports section added in Notion with subsections for each deliverable type
4. **GTM Blueprint** — Step 1 updated with Notion structure, database IDs, trigger flow
5. **Skill Architecture** — Clarified: Onboarding (Step 1) → ICP (Step 2) → Market Research (Step 3, separate)
6. **Zapier notification** — Slack notification added to Fathom→Notion zap (`#internal-notifications` via "Digital VA" bot) for transcript arrivals

### Session: March 24-26

1. **ICP Summary Decks rebuilt** — Both B2B and B2C decks regenerated from scratch using python-pptx. Fixed 16 zero-height shapes, cramped Slide 10, Slide 9 gap, missing brand colors. Result: 0 issues. Build script at `Frameworks/rebuild_icp_decks.py`
2. **ICP file permissions fixed** — All 4 ICP files were read-only, now editable
3. **Stale QA files deleted** — `DESIGN_ISSUES_REPORT.txt` and `QUICK_REFERENCE_ISSUES.txt` removed from Frameworks
4. **GTM Blueprint updated to v2.0** — Replaced "7 Deliverables" with "6 Steps & Their Deliverables" to match current process. Cleared all stale references. Updated build statuses. Pushed to `GTM-Strategy` branch.
5. **ICP Skill upgraded to v2.0** — `Skills/ClearLaunch_ICP_Skill_v2.md` with full Notion integration, workshop follow-up flow, fallback handling
6. **Market Research Skill v2.0 built** — `Skills/ClearLaunch_Market_Research_Skill_v2.md`. 16-step workflow mapped to all 15 template tables. Browser workflows for Ahrefs (6 reports), SimilarWeb (4 sections), Meta Ad Library. Notion data flow. Pushed to `Skill-Assets` branch.
7. **Claude Desktop skill updated** — `Skills/Claude-Desktop-Skills/clearlaunch-market-research/SKILL.md` now points to v2 as source of truth
8. **GitHub repo organized** — ClearThink-Assets repo with branches: `Skill-Assets` (skills), `GTM-Strategy` (blueprint, session notes), `Templates` (framework files)

---

## Upstream Items — Must Complete Before Progressing to Step 3

Before building Value Proposition / Offer Engineering templates and skills (Step 3), the following upstream infrastructure needs to be in place. These are the foundations that Steps 1 and 2 depend on to actually run.

### 1. Tally Onboarding Form

**Status:** ✅ RESOLVED (March 26, 2026). Form exists at [tally.so/r/Ekk6dr](https://tally.so/r/Ekk6dr). GTM Intake database created in Notion. Onboarding Skill v1 and Field Mapping built. **Remaining action:** Add Business Type (B2B/B2C/Both) field to the Tally form and make Company Name required.

**What it needs to capture (at minimum):**
- Client business name
- Client website URL
- B2B or B2C (or both)
- Industry / vertical
- Competitor URLs (up to 3)
- Seed keywords (what terms do your customers search for?)
- Primary service/product offered
- Geographic focus
- Contact information

**Why it matters:** The onboarding form captures initial client context (company, industry, URLs, keywords) that populates the Client Portal. The ICP Skill and Market Research Skill later read from this portal — but they are separate workflows triggered by different events (ICP Discovery call transcript for ICP, manual trigger for MR after ICP is complete). Without the form data in the portal, Terry has to manually feed inputs to each skill.

**Action needed:** Add Business Type field to Tally form. Make Company Name required. Optionally split Competitor URLs into 3 separate fields.

### 2. Tally → Notion Client Portal Automation

**Status:** ✅ RESOLVED (March 26, 2026). Using Tally's native Notion integration (no Zapier needed). Tally sends submissions directly to the GTM Intake database. The Onboarding Skill then reads intake data and creates the Client Portal.

**What it actually does (as built):**
- Tally form submission lands in GTM Intake database (Tally native Notion integration)
- Onboarding Skill reads the intake data, validates it, duplicates the Client Template Page, populates Client Information, and scaffolds the Reports section
- This is a separate event from the onboarding call or the ICP Discovery call — the ICP Skill runs later when an ICP Discovery call transcript arrives

**Why it matters:** Everything downstream assumes a client portal exists with populated data. The Onboarding Skill automates this so every new client starts with a consistent, structured portal.

**Action needed:** Test with a dummy form submission to verify end-to-end.

### 3. Notion Client Portal Structure

**Status:** Reports section was added, but full structure needs verification

**What needs to be confirmed:**
- Does the Client Portal template in Notion have all the right sections?
- Is the Client Information section structured so skills can read from it programmatically (via Notion MCP)?
- Are the Reports subsections created automatically by the onboarding zap, or does Terry create them manually?
- Do the database IDs in the skills still match the live Notion databases?

**Database IDs currently hardcoded in skills:**
- Transcripts DB: `collection://0f372290-8993-4c7e-b303-13afca181721`
- Client Portals DB: `collection://30e821ad-7ba9-8080-8f38-000ba9c44ad0`

**Action needed:** Open Notion, verify the structure matches what the skills expect. Test that the Notion MCP can read/write to these databases.

### 4. Client Relation on Transcripts

**Status:** Manual

**Current workflow:** Fathom doesn't pass client identity, so Terry manually sets the Client relation field on the Notion transcript record before telling Claude Code to process. This applies to ALL transcripts in the Transcripts DB — both onboarding call transcripts (stored for reference only) and ICP Discovery call transcripts (processed by the ICP Skill).

**Future improvement:** Zapier lookup step to match client name from Fathom call title to Client Portals database. Not blocking, but worth building once the core flow is solid.

### 5. Ahrefs / SimilarWeb Access Verification

**Status:** Unknown — need to confirm access levels

**What needs to be checked:**
- Does the current Ahrefs plan support all the reports the Market Research skill needs? (Keywords Explorer, Site Explorer, Content Gap, Top Pages, Backlinks, Paid Keywords)
- Does the SimilarWeb plan provide the data the templates expect? (Traffic Sources, Audience Demographics, Audience Interests, Social Traffic). Note: SimilarWeb has limited data for low-traffic sites — this is documented in the skill's fallback handling.

**Action needed:** Verify tool access. If any reports are behind a higher plan tier, note which tables in the template would be affected.

---

## What's Next (After Upstream Is Resolved)

Once the upstream items above are confirmed and working:

1. **Test the full flow end-to-end** — Tally form → GTM Intake DB → Slack notification → Onboarding Skill creates Client Portal → Onboarding call (transcript stored, not processed) → ICP Discovery call → Transcript in Notion → ICP Skill processes → Deliverables stored
2. **Test the Market Research flow** — ICP complete → Read inputs from portal → Run Ahrefs/SimilarWeb workflows → Populate templates → Store in portal
3. **Build Value Proposition Template** — .docx structure for Step 3
4. **Build Offer Engineering Template** — .docx structure for Step 3
5. **Build Value Prop + Offer Skill** — automate Step 3

---

## Open Questions

1. ~~**Tally form:**~~ ✅ RESOLVED. Form exists at [tally.so/r/Ekk6dr](https://tally.so/r/Ekk6dr) with 30+ fields. Business Type field added. Company Name made required. All fields mapped to GTM Intake database via Tally's native Notion integration.
2. ~~**Onboarding Zapier zap:**~~ ✅ RESOLVED. No Zapier needed for Tally → Notion (native integration). Separate Zapier zap built for GTM Intake → Slack notification (March 29, 2026).
3. **Competitor Analysis Framework:** Terry explicitly said this hasn't been discussed yet — do NOT start building it.
4. ~~**Client relation automation:**~~ Staying manual by design. Terry sets the Client relation on transcript records (both onboarding and ICP Discovery) before processing. Not a blocker.

---

## GitHub Repository

**Repo:** [ClearThink-Marketing/ClearThink-Assets](https://github.com/ClearThink-Marketing/ClearThink-Assets)

| Branch | Contents |
|---|---|
| `Skill-Assets` | Skills, skill references, Claude Desktop skill files |
| `GTM-Strategy` | GTM Blueprint, session notes |
| `Templates` | Framework template files (.docx, .pptx), rebuild scripts |
| `main` | (baseline) |

---

## Working Files Location

- ICP Skill v2: `Skills/ClearLaunch_ICP_Skill_v2.md`
- Market Research Skill v2: `Skills/ClearLaunch_Market_Research_Skill_v2.md`
- Claude Desktop Skills: `Skills/Claude-Desktop-Skills/`
- GTM Blueprint v2: `ClearLaunch_GTM_Strategy_Blueprint.md`
- Framework templates: `Frameworks/` (8 template files + rebuild script)
- Session notes: this file

---

## ClearThink Brand Colors (Reference)

| Token | Hex | Usage |
|---|---|---|
| GREEN | `#1B9B5E` | Accent, headers, primary brand |
| BRIGHT | `#3BEB96` | CTAs, highlights, emphasis |
| DARK | `#121718` | Body text |
| CREAM | `#F6F3EF` | Backgrounds |
| LGGREEN | `#E5F5EC` | Light tint areas |
| ALTROW | `#F0F9F4` | Alternating table rows |
| BORDER | `#A8D9BD` | Table/section borders |
