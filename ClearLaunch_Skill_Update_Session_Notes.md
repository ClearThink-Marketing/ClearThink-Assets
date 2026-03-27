# ClearLaunch Skill Update — Session Notes
**Last Updated:** March 26, 2026
**Status:** Onboarding infrastructure COMPLETE | ICP Skill v2.0 Complete | Market Research Skill v2.0 Complete | Ready for end-to-end testing

---

## Current Build Status

| Component | Status | Location |
|---|---|---|
| Tally Onboarding Form | COMPLETE | [tally.so/r/Ekk6dr](https://tally.so/r/Ekk6dr) (needs Business Type field added) |
| GTM Intake Database | COMPLETE | Notion: Database Hub - ClearThink → GTM Intake |
| Onboarding Skill v1 | COMPLETE | `Skills/ClearLaunch_Onboarding_Skill_v1.md` |
| Onboarding Field Mapping | COMPLETE | `Skills/ClearLaunch_Onboarding_Field_Mapping.md` |
| ICP Templates (B2B + B2C) | COMPLETE | `Frameworks/` (4 files) |
| ICP Summary Decks (B2B + B2C) | COMPLETE (rebuilt) | `Frameworks/` (0 layout issues, brand applied) |
| ICP Agent Skill v2 | COMPLETE | `Skills/ClearLaunch_ICP_Skill_v2.md` |
| Market Research Templates (B2B + B2C) | COMPLETE | `Frameworks/` (4 files, 15 tables each) |
| Market Research Agent Skill v2 | COMPLETE | `Skills/ClearLaunch_Market_Research_Skill_v2.md` |
| GTM Strategy Blueprint | COMPLETE (v2.1) | `ClearLaunch_GTM_Strategy_Blueprint.md` |
| Value Proposition Template | NOT STARTED | — |
| Offer Engineering Template | NOT STARTED | — |
| Customer Journey Template | NOT STARTED | — |
| Metrics/KPI Template | NOT STARTED | — |
| Implementation Roadmap Template | NOT STARTED | — |

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
5. **Skill Architecture** — Clarified: Onboarding (Skill 1) → ICP (Skill 2) → Market Research (Skill 3, separate)
6. **Zapier notification** — Slack notification added to Fathom→Notion zap (`#internal-notifications` via "Digital VA" bot)

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

**Why it matters:** The onboarding form is the data source for both the ICP skill (industry context) and the Market Research skill (client URL, competitor URLs, seed keywords). Without it, Terry has to manually feed all inputs.

**Action needed:** Add Business Type field to Tally form. Make Company Name required. Optionally split Competitor URLs into 3 separate fields.

### 2. Tally → Notion Client Portal Automation

**Status:** ✅ RESOLVED (March 26, 2026). Using Tally's native Notion integration (no Zapier needed). Tally sends submissions directly to the GTM Intake database. The Onboarding Skill then reads intake data and creates the Client Portal.

**What it should do:**
- Tally form submission triggers Zapier
- Zapier creates a new page in the Client Portals database in Notion
- Populates Client Information section with form responses
- Creates the Reports section structure (ICP Analysis, Market Research, Value Proposition, Channel Strategy, Metrics & KPIs, Launch Roadmap)

**Why it matters:** This is "Skill 1 (Onboarding)" — everything downstream assumes a client portal exists with populated data. If this automation doesn't work, every client engagement starts with manual Notion setup.

**Action needed:** Build or verify the Zapier zap. Test with a dummy form submission.

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

**Current workflow:** Fathom doesn't pass client identity, so Terry manually sets the Client relation field on the Notion transcript record before telling Claude Code to process.

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

1. **Test the full ICP flow end-to-end** — Onboarding form → Client Portal → Discovery call → Transcript in Notion → ICP Skill processes → Deliverables stored
2. **Test the Market Research flow** — ICP complete → Read inputs from portal → Run Ahrefs/SimilarWeb workflows → Populate templates → Store in portal
3. **Build Value Proposition Template** — .docx structure for Step 3
4. **Build Offer Engineering Template** — .docx structure for Step 3
5. **Build Value Prop + Offer Skill** — automate Step 3

---

## Open Questions

1. **Tally form:** Does it exist? What fields does it currently have? Does it need to be updated to capture all the inputs the skills need?
2. **Onboarding Zapier zap:** Is this built? If so, what does it currently create in Notion?
3. **Competitor Analysis Framework:** Terry explicitly said this hasn't been discussed yet — do NOT start building it.
4. **Client relation automation:** Worth building a Zapier lookup step, or stay manual for now?

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
