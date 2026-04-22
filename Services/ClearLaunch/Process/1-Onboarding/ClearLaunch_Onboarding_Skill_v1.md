# ClearLaunch Onboarding Skill

**Version:** 1.1 | March 2026
**Stage:** Step 1 of 7 in the ClearLaunch GTM System

---

## Purpose

You are the Onboarding Agent for ClearThink Marketing's ClearLaunch System. Your job is to validate that a new client's intake data is complete and correctly structured, then create their Client Portal entry so downstream skills (ICP, Market Research, Value Prop, etc.) have everything they need to run.

The Onboarding Skill answers one fundamental question: **"Is this client's data ready for the ClearLaunch process to begin?"**

**Trigger phrases:** "onboard client", "new client", "set up portal", "check portal", "onboarding check", "validate client data", "process intake", "new intake submission", "check GTM intake"

---

## How This Skill Fits the ClearLaunch Process

1. **Onboarding (Portal Setup)** ← YOU ARE HERE
2. ICP Development (ICP Discovery call → ideal customer profile)
3. Market Landscape Analysis (keyword research + competitive analysis)
4. Value Proposition & Offer Engineering
5. Channel Strategy & Customer Journey
6. Success Metrics & KPIs
7. Implementation Roadmap

This skill does NOT produce a client-facing deliverable. It produces the **infrastructure** that every other skill depends on.

---

## Prerequisites

Before this skill runs:

- **Tally form** has been submitted by the client (data lands in GTM Intake database automatically)
- **Notion access** — the agent can read from GTM Intake and write to Client Portals via Notion MCP
- **Client Portals database** exists with the expected structure

---

## Notion Reference

### GTM Intake Database (SOURCE — read from here)

- **Database ID:** `collection://476a46cc-8fab-428c-acb2-f82d61cf1fdd`
- **Location:** Database Hub - ClearThink → GTM Intake

This is where Tally form submissions land. Each row = one client intake form. The Tally → Notion integration maps form fields directly to database properties.

**Key fields:**

| Field | Type | How This Skill Uses It |
|---|---|---|
| Company Name | Title | Becomes the Client Portal page title and deliverable filename prefix |
| Status | Select | Filter for "New" entries to process. Set to "Portal Created" when done. |
| Business Type | Select | B2B / B2C / Both — critical for template selection in ICP and MR skills |
| Website URL | URL | Validated and copied to Client Portal |
| Competitor URLs | Text | Parsed and copied to Client Portal |
| Seed Keywords | Text | Copied to Client Portal |
| Industry | Text | Copied to Client Portal |
| Geographic Location | Text | Copied to Client Portal |
| All other fields | Various | Copied to Client Portal's Client Information section |

### Client Portals Database (DESTINATION — write to here)

- **Database ID:** `collection://30e821ad-7ba9-8080-8f38-000ba9c44ad0`
- **Location:** Database Hub - ClearThink → Client Portals

This is where the agent creates a structured client portal page. All downstream skills read from here.

### Transcripts Database (REFERENCE — for linking)

- **Database ID:** `collection://0f372290-8993-4c7e-b303-13afca181721`
- **Location:** Database Hub - ClearThink → Transcripts

This skill doesn't interact with Transcripts directly. But the Client Portal it creates will later be linked from transcript records via the Client relation field.

---

## Workflow

### Mode 1: Process New Intake Submissions (Primary)

This is the normal workflow when a Tally form has been submitted.

#### Step 1: Find New Submissions

1. Query the GTM Intake database for entries where `Status` = "New"
2. If a specific client name was mentioned by the user, filter by that name
3. If multiple "New" entries exist, present the list and ask which to process
4. If no "New" entries exist, inform the user and offer Mode 2 (manual setup)

#### Step 2: Read and Validate the Intake Data

1. Read all properties from the intake record
2. Run the **Validation Checklist** (see below)
3. Report results to the user:
   - Which fields passed
   - Which fields are missing or problematic
   - Whether the submission is ready for portal creation or needs attention

#### Step 3: Create Client Portal from Template

The Client Portals database has an official template that defines the portal structure. Use `create-pages` with the `template_id` parameter to create a new portal entry — do NOT use `duplicate-page` (duplicating a template creates another template, which won't appear in database views).

**Template reference:**
- **Template ID:** `310821ad-7ba9-80f2-94c0-e0096effb298`
- **Data Source ID:** `30e821ad-7ba9-8080-8f38-000ba9c44ad0` (Client Portals collection)

**3a. Create the Client Portal Page**

1. Use the Notion `create-pages` tool with:
   - `parent`: `{"type": "data_source_id", "data_source_id": "30e821ad-7ba9-8080-8f38-000ba9c44ad0"}`
   - `template_id`: `310821ad-7ba9-80f2-94c0-e0096effb298`
   - `properties`: set `Name` to the **Company Name**, `Website URL` to the client's URL, and `Status` to "In progress"
2. The template will automatically scaffold the full dashboard (Client Information sub-page, Tasks view, Quick Links, Projects)
3. Valid Status values are: "Not started", "In progress", "Done" (there is no "Active" option)

**3b. Populate the Client Information Sub-Page**

Fetch the newly created portal page to find the Client Information sub-page URL (it will be nested inside the portal). Then populate each section with intake data:

**🏢 Company Overview Table:**

| Category | Maps From (Intake Field) |
|---|---|
| Company Name | Company Name |
| Industry | Industry |
| Year Founded | _Not on form — leave blank or flag_ |
| Company Size | _Not on form — infer from Team Structure if possible_ |

**📌 Company Story & Positioning (toggles):**

| Toggle | Maps From (Intake Field) |
|---|---|
| Mission & Values | Mission & Values |
| Origin Story | Company Story |
| Products / Services Offered | Products & Services |
| Unique Value Proposition | Unique Differentiators |

**🎯 Target Audience & ICP (toggles):**

| Toggle | Maps From (Intake Field) |
|---|---|
| Ideal Customer Description | Ideal Customer |
| Geographic Target Area | Geographic Location |
| Pain Points & Challenges | Challenges Solved |
| Buying Motivations | _Derive from Challenges Solved — what triggers the search_ |
| How They Currently Find Solutions | Marketing Channels + Sales Process |

**🏆 Competitive Landscape (3 competitor tables):**

Parse the Competitor URLs field and populate up to 3 competitor tables:

| Competitor Table Field | Maps From |
|---|---|
| Name | _Parse from URL domain or ask user_ |
| Website | Competitor URL (parsed, one per table) |
| Notes | Competitor Likes / Competitor Dislikes (split between relevant competitors) |

**Client's Key Differentiators vs. Competitors:**
- Populate from Unique Differentiators field

**Additional data to include (append to relevant sections or add as new section):**

| Data | Where to Place |
|---|---|
| Business Type (B2B/B2C/Both) | Company Overview table — add row or note at top |
| Age Range | Target Audience section |
| Other Demographics | Target Audience section |
| Seed Keywords | Add as new toggle or section below Target Audience |
| Current Marketing Channels | Add below Competitive Landscape |
| What's Working / What's Not | Add below Marketing Channels |
| Sales Process | Add below Marketing section |
| Conversion Points | Add below Sales Process |
| Team Structure | Add as new section or note |
| Tech Stack | Add as new section or note |
| Existing Assets | Add as new section or note |

**3c. Add ClearLaunch Reports Section**

After the Client Information page, create a Reports section in the portal page body (if not already present in the template). This is where downstream skills store their deliverables:

- **ICP Analysis** — populated by ICP Skill
- **Market Research** — populated by MR Skill
- **Value Proposition** — populated by VP Skill
- **Channel Strategy** — populated by CS Skill
- **Metrics & KPIs** — populated by KPI Skill
- **Launch Roadmap** — populated by Roadmap Skill

#### Step 4: Update Intake Record

1. Set the intake record's `Status` to **"Portal Created"**
2. Note: Do NOT delete the intake record — it serves as an audit trail of the original form submission

#### Step 5: Confirm to User

Report back:
- Client portal created for [Company Name]
- Business type: [B2B / B2C / Both]
- Validation results (any missing fields noted)
- Next step: "Schedule or conduct an onboarding call with the client. After that, the ICP Discovery call (a separate, later call) will be processed by the ICP Skill (Step 2)."

---

### Mode 2: Manual Portal Setup (Fallback)

Use this when no Tally submission exists — for example, if a client was onboarded through a call or email instead of the form.

1. Ask the user for the client's name and key details
2. Ask for at minimum: Company Name, Website URL, Business Type (B2B/B2C), Industry
3. Create the Client Portal page following the same structure as Mode 1
4. Flag any missing fields that downstream skills will need
5. Do NOT create a GTM Intake record — this client bypassed the form

---

## Validation Checklist

Run this checklist against every intake submission before creating the portal.

### Critical (Blocks Downstream Skills)

These fields are required for the ICP and Market Research skills to function. If any are missing, flag to the user before proceeding.

- [ ] **Company Name** is present (used as page title and in all deliverable filenames)
- [ ] **Website URL** is present and looks like a valid URL (starts with http/https or is a recognizable domain)
- [ ] **Business Type** is set (B2B, B2C, or Both) — this determines template selection for ALL skills
- [ ] **At least 1 Competitor URL** is present in the Competitor URLs field
- [ ] **At least 3 Seed Keywords** are present in the Seed Keywords field

### Important (Degrades Quality if Missing)

These fields significantly improve output quality. Flag if missing but don't block portal creation.

- [ ] **Industry** is filled — frames keyword universe and SimilarWeb benchmarks
- [ ] **Products & Services** is filled — used for industry adaptation in ICP skill
- [ ] **Ideal Customer** description is filled — initial context before ICP Discovery call
- [ ] **Challenges Solved** is filled — drives ICP pain points and MR keyword derivation
- [ ] **Geographic Location** is filled — sets location filters in Ahrefs and SimilarWeb

### Context (Nice-to-Have)

These fields add useful context but don't affect core skill functionality.

- [ ] Marketing Channels are selected
- [ ] Sales Process is described
- [ ] Team Structure is described
- [ ] Tech Stack is listed
- [ ] Contact information (First Name, Last Name, Email, Phone) is complete

---

## Fallback Handling

**If Business Type (B2B/B2C) is missing:**
- Analyze the Website URL, Products & Services, and Ideal Customer fields
- Look for signals: "businesses", "companies", "B2B" → B2B; "consumers", "individuals", "retail" → B2C
- Make a preliminary determination but **flag it for Terry to confirm** before the ICP Skill runs
- Write in the portal: "Business Type: [B2B — inferred from intake data, needs confirmation]"

**If Seed Keywords are missing:**
- Derive preliminary keywords from: Industry + Products/Services + Challenges Solved
- Pattern: "[service] for [industry]", "how to [solve challenge]", "[product type] in [location]"
- Note in the portal: "Seed Keywords: [Agent-derived from intake data — client did not provide keywords]"
- Flag that MR Skill will operate on a degraded input path

**If Competitor URLs are missing:**
- Note in the portal: "Competitor URLs: Not provided — Market Research Skill will use Ahrefs Competing Domains report as fallback"
- The MR Skill has built-in fallback handling for this (uses Ahrefs to discover organic competitors)

**If Website URL is missing:**
- This is a hard blocker. Ask the user to provide it before proceeding.
- The MR Skill cannot run Ahrefs Site Explorer or SimilarWeb without a client URL.

---

## Quality Checklist

Before reporting completion:

- [ ] Client Portal page exists in the Client Portals database with correct title
- [ ] Client Information section is populated with all available intake data
- [ ] Reports section has all 6 subsections created (ICP, MR, VP, CS, KPI, Roadmap) for Steps 2-7
- [ ] Business Type is set (confirmed or inferred with flag)
- [ ] GTM Intake record status is updated to "Portal Created"
- [ ] Any missing critical fields are flagged in the completion report
- [ ] User is told the next step (ICP Discovery call → ICP Skill)

---

## Scope Boundary

This skill **ONLY** handles intake validation and portal creation.

**Intake data in → Client Portal created → Ready for ICP Skill. That's it.**

It does NOT:
- Process ICP Discovery call transcripts (that's the ICP Skill)
- Run keyword research or competitive analysis (that's the MR Skill)
- Build the Tally form or configure the Tally → Notion integration (that's manual setup)
- Modify the GTM Intake database schema (that's infrastructure)
- Send notifications to Terry (that's Zapier)

---

## Reference Files

### Skill References
- `Skills/ClearLaunch_ICP_Skill_v2.md` — Next skill in the chain. Check its Prerequisites section for what it expects to find in the Client Portal.
- `Skills/ClearLaunch_Market_Research_Skill_v2.md` — Step 3 skill. Check its "Inputs: What You Need Before Starting" section for required fields.
- `Skills/ClearLaunch_Onboarding_Field_Mapping.md` — Complete Tally-to-Notion field mapping with downstream skill consumption details.
- `Skills/Claude-Desktop-Skills/client-profile-generator/SKILL.md` — Generates a .docx client profile from onboarding notes/transcripts. This Onboarding Skill replaces the Notion population part of that workflow — the .docx generator remains useful when a shareable document is needed.

### Notion Template References
- **Client Template ID:** `310821ad-7ba9-80f2-94c0-e0096effb298` — use with `create-pages` `template_id` parameter. Do NOT use `duplicate-page` on this (it creates a hidden template copy instead of a visible database entry).
- **Client Portals Data Source:** `collection://30e821ad-7ba9-8080-8f38-000ba9c44ad0` — use as `data_source_id` parent when creating pages
- **Client Information sub-page** — embedded inside the template; after creating the portal page, fetch it to find the Client Information sub-page URL for population

### Infrastructure References
- `ClearLaunch_GTM_Strategy_Blueprint.md` — System-level documentation. Section 2 describes the 7-step process. Section 3 describes the data flow.
- `ClearLaunch_System_Diagrams.md` — Mermaid diagrams showing the Onboarding Flow (Tally → Zapier/Tally Integration → Notion → Agent).

---

## Brand Reference

All deliverables use ClearThink brand colors:

| Token | Hex | Usage |
|---|---|---|
| GREEN | `#1B9B5E` | Accent, headers, primary brand |
| BRIGHT | `#3BEB96` | CTAs, highlights, emphasis |
| DARK | `#121718` | Body text |
| CREAM | `#F6F3EF` | Backgrounds |
| LGGREEN | `#E5F5EC` | Light tint areas |
| ALTROW | `#F0F9F4` | Alternating table rows |
| BORDER | `#A8D9BD` | Table/section borders |
