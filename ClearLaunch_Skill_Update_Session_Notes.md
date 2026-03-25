# ClearLaunch Skill Update — Session Notes
**Last Updated:** March 24, 2026
**Status:** ICP Skill v1.0 Complete — Market Research Skill Next

---

## What We Accomplished Today

### 1. Market Research Frameworks — COMPLETE
All 8 ClearLaunch framework files are built, branded, and living in `ClearThink/Frameworks/`:

| File | Status |
|---|---|
| ClearLaunch_B2B_ICP_Summary_Deck.pptx | ✅ Done (prior session) |
| ClearLaunch_B2B_ICP_Template.docx | ✅ Done (prior session) |
| ClearLaunch_B2C_ICP_Summary_Deck.pptx | ✅ Done (prior session) |
| ClearLaunch_B2C_ICP_Template.docx | ✅ Done (prior session) |
| ClearLaunch_B2B_Market_Research_Summary_Deck.pptx | ✅ Regenerated today (slide 16 spacing fix) |
| ClearLaunch_B2B_Market_Research_Template.docx | ✅ Updated with brand colors today |
| ClearLaunch_B2C_Market_Research_Summary_Deck.pptx | ✅ Regenerated today |
| ClearLaunch_B2C_Market_Research_Template.docx | ✅ Updated with brand colors today |

**Note:** Two stale QA files (`DESIGN_ISSUES_REPORT.txt`, `QUICK_REFERENCE_ISSUES.txt`) are still in the Frameworks folder — need manual deletion (permission issue).

### 2. ICP Skill — COMPLETE (v1.0)
**File:** `Skills/ICP_Skill.md`

**Built from scratch this session** (previous `/tmp/` working copy was lost to session reset). The skill now has:

- Correct Notion data flow: queries Transcripts DB for "Not started" entries with Meeting Type = ICP or Discovery
- Full B2B extraction fields (firmographics, pain points, buying triggers, decision-makers, competitive landscape, beachhead, qualifying criteria, buyer persona)
- Full B2C extraction fields (demographics, psychographics, pain points, buying triggers, decision-making, competitive landscape, beachhead, qualifying criteria, buyer persona)
- Tier 1/2/3 segmentation logic (Tier 1 fully detailed from discovery call, Tiers 2-3 sketched then fleshed out in ICP workshop)
- Workshop follow-up flow for second-pass transcript processing
- Deliverable storage: files go into client portal → Reports → ICP Analysis section
- Fallback handling: Fathom browser → manual input if Notion transcript missing
- Scope boundary: ICP only, does NOT pass data to Market Research (separate skill)
- Notion database IDs hardcoded: Transcripts DB, Client Portals DB
- Template file references for all 4 ICP files (B2B/B2C .docx + .pptx)

**Trigger architecture decided:**
- Fathom → Zapier → Notion (transcript with Status: "Not started") → Zapier notification to Terry → Terry opens Claude Code → "process new transcripts"
- Zapier zap needs notification step added (Slack or email after Notion write)
- Future: replace notification with webhook to hosted service for full automation

### 2b. Client Portal Template — Reports Section Added
- Added a "Reports" section to the Client Portal template in Notion
- Subsections for each ClearLaunch deliverable type: ICP Analysis, Market Research, Value Proposition, Channel Strategy, Metrics & KPIs, Launch Roadmap
- ICP skill stores deliverables in Reports → ICP Analysis when processing is complete

### 2c. GTM Strategy Blueprint — Updated
- `ClearLaunch_GTM_Strategy_Blueprint.md` Step 1 updated with confirmed Notion structure, database IDs, correct trigger flow, and marked ICP Skill as BUILT

### 2d. Skill Architecture Clarified
- **Skill 1 (Onboarding):** Onboarding form → Zapier → creates Client Portal + populates Client Information
- **Skill 2 (ICP):** Discovery call transcript → ICP templates → stored in client portal Reports
- **Skill 3 (Market Research):** Separate skill, gets inputs from onboarding form (keywords, competitor URLs), NOT from ICP output

### 3. Market Research Skill Update — NOT STARTED
**File:** `/tmp/clearlaunch-market-research/SKILL.md` (writable copy ready)

**What needs to happen:**

#### A. Replace "no API" assumption with browser-based data collection
The current skill says *"There is currently no direct API connection to Ahrefs, SEMrush, or Google Keyword Planner."* This needs to be replaced with active browser workflows for:

- **Ahrefs** (https://ahrefs.com) — keyword research, backlink analysis, competitor keyword gaps, content gap analysis, site audit data. The skill should include step-by-step browser workflows for pulling each type of data.
- **SimilarWeb** (https://similarweb.com) — traffic estimates, audience demographics, cross-visitation data, traffic sources, industry benchmarking. The skill should know when to use SimilarWeb vs Ahrefs (they serve different purposes).

#### B. Add framework deliverable references
The skill currently has no awareness of the `.docx` templates or `.pptx` summary decks we built. It needs:
- Instructions to populate the Market Research Templates (B2B/B2C .docx) as the analysis deliverable
- Instructions to generate the Summary Decks (B2B/B2C .pptx) as the presentation deliverable
- Markdown reference files (like the ICP skill has `b2b_icp_template.md`) showing the template structure so the skill knows what fields to fill

#### C. Update the skill description
Add Ahrefs, SimilarWeb, and deliverable-related trigger phrases to the description.

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

---

## Open Questions for Next Session

1. ~~**Fathom → Notion flow:**~~ ✅ RESOLVED — Transcripts DB confirmed. Scheduled Zapier, moving to webhook. Notification step to be added.
2. **Ahrefs workflow specifics:** Which Ahrefs reports does Terry typically pull? (Site Explorer → Organic Keywords? Content Gap? Backlink Profile?) Needed for Market Research skill.
3. **SimilarWeb workflow specifics:** Which SimilarWeb sections are most used? (Traffic Overview? Audience? Competitors?) Needed for Market Research skill.
4. **Competitor Analysis Framework:** Terry explicitly said this hasn't been discussed yet — do NOT start building it.
5. ~~**Zapier notification step:**~~ ✅ RESOLVED — Slack notification added to Fathom→Notion zap. Sends to `#internal-notifications` channel via "Digital VA" bot when a transcript lands in Notion.
6. **Onboarding → Client Portal automation:** Tally form → Zapier → Notion Client Portal creation. Exists conceptually but needs to be confirmed/built.
7. **Client relation on transcripts is manual for now.** Fathom doesn't pass client identity, so the Client relation field on the Notion transcript record cannot be auto-populated by Zapier. Current workflow: Terry manually sets the Client relation in Notion before telling Claude Code to process. Future iteration: explore matching client name from Fathom call title to Client Portals database via a Zapier lookup step.

---

## Working Files Location
- ICP Skill: `Skills/ICP_Skill.md` (permanent location, not in /tmp/)
- GTM Blueprint: `ClearLaunch_GTM_Strategy_Blueprint.md`
- Framework templates: `Frameworks/` (8 files)
- Session notes: this file
