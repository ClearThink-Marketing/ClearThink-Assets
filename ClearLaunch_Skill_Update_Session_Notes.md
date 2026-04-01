# ClearLaunch Skill Update — Session Notes
**Last Updated:** March 31, 2026
**Status:** Step 4 (UVP) BUILT — templates, skill v1, summary deck, Zapier zap configured | Step 5 (Offer Dev) templates built | Blueprint updated to v3.1 | 7-step process finalized

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
| UVP Template (.docx) | COMPLETE | `Frameworks/ClearLaunch_UVP_Template.docx` (Templates branch) |
| UVP Summary Deck (.pptx) | COMPLETE | `Frameworks/ClearLaunch_UVP_Summary_Deck.pptx` (Templates branch) |
| UVP Agent Skill v1 | COMPLETE | `Skills/ClearLaunch_UVP_Skill_v1.md` (Skill-Assets branch) |
| UVP Zapier Zap | CONFIGURED (draft) | 6-step: Fathom → Filter → Notion → Formatter → Find Page → Slack |
| UVP Workshop Reference | COMPLETE | `Frameworks/uvp_workshop_template.md` (Templates branch) |
| Offer Dev Template (.docx) | COMPLETE | `Frameworks/ClearLaunch_Offer_Dev_Template.docx` (Templates branch) |
| Offer Dev Reference | COMPLETE | `Frameworks/offer_dev_template.md` (Templates branch) |
| Offer Dev Agent Skill | NEEDS UPGRADE | Claude Desktop skill exists, needs production build like UVP |
| Customer Journey Template | NOT STARTED | — |
| Metrics/KPI + Roadmap Templates | NOT STARTED | — |

---

## What Was Accomplished (March 31, 2026 — Session 5)

### Step 4 (UVP) — Full Production Build

1. **UVP Template (.docx) built** — Industry-agnostic 7-section discovery workshop template with adaptive agent notes per business type (SaaS, services, ecommerce, B2B/B2C). ClearThink branded with python-docx.
2. **UVP Summary Deck (.pptx) built** — 9-slide branded deck: Title, Problem & Market Gap, Methodology & Approach, Expertise & Credibility, Results & Outcomes, Risk Reduction & Assurance, Proof & Validation, Top 3 Differentiators, UVP Statement + Elevator Pitch.
3. **UVP Skill v1 built** — `Skills/ClearLaunch_UVP_Skill_v1.md`. Full Notion-integrated workflow matching ICP skill pattern: reads transcripts, classifies meeting type, cross-references ICP, extracts through 7-section framework, synthesizes (Top 3 Differentiators, UVP Statement, Elevator Pitch, Positioning Statement), generates .docx + .pptx deliverables, uploads to Client Portal → Reports → Value Proposition.
4. **UVP Zapier zap configured** — 6-step pipeline: Fathom → Filter ("UVP" in title) → Notion Create Data Source Item → Formatter (split meeting title on " - " to extract client name) → Find Page By Title (GTM Intake lookup) → Slack notification with copy-paste command including client name.
5. **Fathom call naming convention established** — `Type - Client Name` (e.g., "UVP Workshop - Greenfield Landscaping"). Formatter splits on " - " and takes last segment for GTM Intake lookup.

### Step 5 (Offer Dev) — Templates Built

6. **Offer Dev Template (.docx) built** — Industry-agnostic 3-tier offer ladder (Micro/Macro/Core) with creative angles and objection handling sections. ClearThink branded.
7. **Offer Dev reference template built** — `Frameworks/offer_dev_template.md` with adaptive notes per business type.

### Process & Organization Updates

8. **7-step process finalized** — Confirmed split: Step 4 = UVP, Step 5 = Offer Dev. Previously these were combined as one step.
9. **Blueprint updated to v3.1** — Split UVP/Offers, added full Step 4 workflow details, updated data flow diagram, file registry, build statuses, and priorities.
10. **Zapier spec folded into skill file** — No separate Zapier spec documents. Pipeline details documented inline in the skill file (matching ICP pattern).
11. **Reference templates moved to Templates branch** — `uvp_workshop_template.md` and `offer_dev_template.md` now live in `Frameworks/` on the Templates branch, not in Skill-Assets Claude Desktop skill folders.
12. **UVP workshop template updated to agnostic language** — Replaced "firm"→"business", "services"→"offerings", "clients"→"customers" throughout.

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

## What's Next

1. **Publish UVP Zapier zap** — configured as draft, ready to go live when Terry is ready
2. **Build Offer Dev Skill v1** — production upgrade with Notion integration, following UVP skill pattern
3. **Build Offer Dev Summary Deck (.pptx)** — matching UVP deck pattern
4. **Build Offer Dev Zapier zap** — same 6-step pipeline pattern, filter for "Offer" in title
5. **Build Step 6 (Channel Strategy)** — templates, skill, Zapier zap
6. **Build Step 7 (Success Metrics & Launch Roadmap)** — templates, skill, Zapier zap
7. **End-to-end testing** — full flow from Tally form through all 7 steps

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

**Skill-Assets branch:**
- Onboarding Skill: `Skills/ClearLaunch_Onboarding_Skill_v1.md`
- ICP Skill v2: `Skills/ClearLaunch_ICP_Skill_v2.md`
- Market Research Skill v2: `Skills/ClearLaunch_Market_Research_Skill_v2.md`
- UVP Skill v1: `Skills/ClearLaunch_UVP_Skill_v1.md`
- Field Mapping: `Skills/ClearLaunch_Onboarding_Field_Mapping.md`
- Claude Desktop Skills: `Skills/Claude-Desktop-Skills/`

**Templates branch:**
- Framework templates: `Frameworks/` (ICP, MR, UVP, Offer Dev .docx + .pptx files)
- Reference templates: `Frameworks/uvp_workshop_template.md`, `Frameworks/offer_dev_template.md`
- Build scripts: `Frameworks/rebuild_icp_decks.py`, `Frameworks/build_step3_step4_templates.py`, `Frameworks/build_uvp_deck.py`

**GTM-Strategy branch:**
- GTM Blueprint v3.1: `ClearLaunch_GTM_Strategy_Blueprint.md`
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
