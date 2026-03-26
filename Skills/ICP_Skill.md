# ClearLaunch ICP Skill

**Skill 2 in the ClearLaunch System**
**Version:** 1.0 | March 2026

---

## Description

This skill processes discovery call and ICP workshop transcripts to generate complete Ideal Customer Profile deliverables. It reads transcripts from Notion, extracts customer segmentation data, populates ICP templates (.docx) and summary decks (.pptx), and stores the finished deliverables in the client's portal.

**Trigger phrases:** "process ICP", "build ICP", "ICP transcript", "discovery call analysis", "process transcript", "process new transcripts"

---

## Prerequisites

Before this skill runs, the following must already exist:

- **Client Portal** in Notion — created by Skill 1 (Onboarding) when the client's onboarding form is submitted
- **Transcript page** in the Notion Transcripts database — created by the Fathom → Zapier → Notion pipeline after a discovery call or ICP workshop
- **ICP template files** in `Frameworks/` — the .docx and .pptx templates this skill populates

---

## Notion Reference

### Transcripts Database

- **Database ID:** `collection://0f372290-8993-4c7e-b303-13afca181721`
- **Location:** Database Hub - ClearThink → Transcripts

**Fields:**

| Field | Type | How This Skill Uses It |
|---|---|---|
| Meeting Title | title | Identifies the transcript |
| Attendees | text | Captures who was on the call |
| Client | relation | Links to the Client Portals database — used to find the client's portal for deliverable storage |
| Meeting Date | date | When the call happened |
| Meeting Type | select | Filter for "ICP" or "Discovery" entries |
| Duration (min) | number | Reference only |
| Fathom Share URL | url | Fallback if transcript text is missing |
| Recording URL | url | Reference only |
| Notes | text | Skill writes processing notes here |
| Deliverables Generated | text | Skill writes deliverable filenames and summary here |
| Status | status | **"Not started"** = ready for processing. **"In progress"** = skill is working on it. **"Done"** = deliverables complete. |

**Transcript text** lives in the **page body** (not a property). It's formatted as a conversation with speaker labels (e.g., "**Terry:** ...", "**Marcus:** ...").

### Client Portals Database

- **Database ID:** `collection://30e821ad-7ba9-8080-8f38-000ba9c44ad0`
- **Location:** Database Hub - ClearThink → Client Portals

The skill uses the `Client` relation on the transcript record to look up the client's portal page, then navigates to the **Reports** section within that portal to store deliverables.

---

## Workflow

### Step 1: Find Transcripts to Process

1. Query the Transcripts database for entries where:
   - `Status` = "Not started"
   - `Meeting Type` = "ICP" **or** "Discovery"
2. If the user specified a client name, filter results by that name
3. If multiple transcripts are found, present the list and ask which one to process
4. If no transcripts are found, inform the user and offer alternatives (see Fallback Handling)

### Step 2: Claim the Transcript

1. Update the transcript's `Status` to **"In progress"** immediately
   - This prevents another session from processing the same transcript
2. Note the `Client` relation value — you'll need it for deliverable storage

### Step 3: Read the Transcript

1. Fetch the full page body of the transcript page
2. Extract the conversation text — look for the section with speaker-labeled dialogue
3. Also read the property fields (Attendees, Meeting Date, Duration) for metadata

### Step 4: Determine B2B or B2C

1. Analyze the transcript content:
   - If the client discusses **businesses, companies, organizations, contracts, B2B sales cycles, enterprise** → **B2B**
   - If the client discusses **consumers, individuals, households, retail, direct-to-consumer** → **B2C**
2. If unclear from the transcript, **ask the user to confirm** before proceeding
3. This determines which template set to use and which extraction fields apply

### Step 5: Extract ICP Data

Parse the transcript and extract the following data. Mark any field as **[Inferred]** if the transcript doesn't explicitly state it but context suggests a value. Mark as **[Not Discussed]** if there's no basis for inference.

#### If B2B — Extract These Fields:

**Firmographics (Tier 1 Segment)**
- Industry / vertical
- Company size (employee count range)
- Revenue range
- Geography / service area
- Organizational structure (owner-operated, has VP/director level, etc.)

**Pain Points**
- Core business problems expressed
- Operational frustrations
- Cost / efficiency issues
- What's not working with current approach

**Buying Triggers**
- What events cause them to seek a solution
- Examples: new project, failed vendor, regulation change, growth milestone, seasonal cycle

**Decision-Makers**
- Who signs the contract (title/role)
- Who influences the decision
- Buying committee structure (if applicable)
- Approval process and timeline
- Number of proposals/vendors they typically evaluate

**Current Solutions**
- What they use now
- Why it's insufficient
- Switching costs or barriers

**Competitive Landscape**
- Who else the client competes against
- What competitors do well / poorly
- What differentiates this client from competitors

**Beachhead Analysis**
- Which specific niche or segment to dominate first
- Why this segment (highest LTV, easiest to win, strongest differentiator)
- Expansion path after beachhead is proven

**Qualifying Criteria**
- Must-haves: minimum requirements for a good-fit customer
- Nice-to-haves: bonus traits that indicate higher value
- Disqualifiers: red flags, deal-breakers, walk-away criteria

**Buyer Persona**
- Primary buyer role/title
- Their goals and motivations
- Their frustrations and objections
- How they research solutions (Google, referrals, LinkedIn, industry associations, etc.)
- Preferred communication channels
- Trust signals they look for (case studies, references, certifications, etc.)

#### If B2C — Extract These Fields:

**Demographics (Tier 1 Segment)**
- Age range
- Income level
- Location / geography
- Education level
- Household composition (single, family, etc.)

**Psychographics**
- Values and beliefs
- Lifestyle characteristics
- Interests and hobbies
- Attitudes and aspirations

**Pain Points**
- Personal frustrations and unmet needs
- Emotional triggers
- What they've tried that didn't work

**Buying Triggers**
- Life events that create the need
- Seasonal or cyclical needs
- Social influence (friends, family, influencers, reviews)

**Decision-Making**
- Solo decision or household/group decision
- Research behavior (where they look, how long they take)
- Price sensitivity
- Brand loyalty factors

**Current Solutions**
- What they currently use
- Alternatives they've tried
- Why existing options fall short

**Competitive Landscape**
- Direct alternatives
- Substitute products/services
- Indirect competitors

**Beachhead Analysis**
- Which specific niche to dominate first
- Why this segment
- Expansion path

**Qualifying Criteria**
- Must-haves, nice-to-haves, disqualifiers

**Buyer Persona**
- Lifestyle profile
- Goals and aspirations
- Frustrations and objections
- Media consumption habits
- Preferred channels (social, email, search, etc.)

### Step 6: Tier the Segments

- **Tier 1 (High Priority):** Fully detailed from transcript data. This is the beachhead market — maximum investment, direct outreach, personalized campaigns, highest LTV potential.
- **Tier 2 (Potential):** Sketch with available info. Good fit but lower urgency or smaller deal size. Flag as "Needs workshop follow-up for full detail."
- **Tier 3 (Nurture Only):** Sketch with available info. Monitor and nurture. Flag as "Needs workshop follow-up for full detail."

If this is a first-pass discovery call, Tier 1 should be fully detailed. Tiers 2-3 will be fleshed out after a subsequent ICP workshop (see Workshop Follow-Up below).

### Step 7: Populate Deliverables

1. **Select the correct template:**
   - B2B: `Frameworks/ClearLaunch_B2B_ICP_Template.docx` + `Frameworks/ClearLaunch_B2B_ICP_Summary_Deck.pptx`
   - B2C: `Frameworks/ClearLaunch_B2C_ICP_Template.docx` + `Frameworks/ClearLaunch_B2C_ICP_Summary_Deck.pptx`

2. **Fill every placeholder** in the template with extracted data. Use the field labels in the template as guides. If a field was not discussed, write "[Not Discussed — Follow up in ICP Workshop]".

3. **Name the output files:**
   - `[ClientName]_ICP_[B2B/B2C].docx` — e.g., `Greenfield_Landscaping_ICP_B2B.docx`
   - `[ClientName]_ICP_Summary_[B2B/B2C].pptx` — e.g., `Greenfield_Landscaping_ICP_Summary_B2B.pptx`

4. **Save files** to the ClearThink project directory initially.

### Step 8: Store Deliverables in Client Portal

1. Use the `Client` relation from the transcript record to find the client's portal page in the Client Portals database
2. Navigate to the **Reports** section within that client portal
3. Find or create an **"ICP Analysis"** subpage inside Reports
4. Link or embed the .docx and .pptx deliverables in that subpage
5. Include a brief summary: what was extracted, which tiers are complete, what needs follow-up

### Step 9: Update Notion Transcript Record

1. Set `Status` → **"Done"**
2. Fill `Deliverables Generated` with:
   - Filenames of both deliverables
   - Brief summary of what was extracted (e.g., "Primary ICP: Mid-Size Property Management Companies ($50K-$200K annual contracts). Processed automatically on [date].")
3. Fill `Notes` with:
   - Processing notes
   - Items marked [Inferred] that need client verification
   - Fields marked [Not Discussed] that should be covered in the ICP workshop

---

## Workshop Follow-Up Flow

When a **second** transcript comes in with Meeting Type = "ICP" for the **same client:**

1. The agent recognizes this is a follow-up workshop (same client, second ICP-type transcript)
2. Read the existing deliverables from the first pass (the Tier 1 data stored in the client portal)
3. Use the workshop transcript to flesh out **Tiers 2 and 3** with full detail
4. Update the existing deliverable files with the additional tier data
5. Update the Notion records accordingly

---

## Fallback Handling

**If no "Not started" transcripts exist in Notion:**
- Ask the user if they have a Fathom Share URL — if yes, navigate to it via browser and extract the transcript
- If no Fathom access, ask the user to paste the transcript text directly into the chat
- Create a manual transcript record in Notion to maintain tracking

**If the transcript is thin or unclear:**
- Mark specific fields as **[Inferred]** with a note explaining what was assumed and why
- Mark missing fields as **[Not Discussed]** with a recommendation to cover them in the ICP workshop
- Never fabricate data — if it's not in the transcript, flag it

---

## Scope Boundary

This skill **ONLY** handles ICP generation. Its job:

**Transcript in → ICP templates out → stored in client portal. That's it.**

It does NOT:
- Pass data to the Market Research skill or any other step
- Run keyword research or competitive analysis
- Modify the Client Information page (that's Skill 1 — Onboarding)
- Create the client portal (that's Skill 1 — Onboarding)

Market Research (Skill 3) is a completely separate skill that gets its inputs independently from the client onboarding form (keywords, competitor URLs, etc.).

---

## Template Files Reference

### B2B Templates
- `Frameworks/ClearLaunch_B2B_ICP_Template.docx` — Word template with all ICP sections
- `Frameworks/ClearLaunch_B2B_ICP_Summary_Deck.pptx` — 11-slide PowerPoint deck

### B2C Templates
- `Frameworks/ClearLaunch_B2C_ICP_Template.docx` — Word template with all ICP sections
- `Frameworks/ClearLaunch_B2C_ICP_Summary_Deck.pptx` — 11-slide PowerPoint deck

### ICP Summary Deck Slide Structure (11 slides)
1. Title Slide — Client name & intro
2. Your Customer Types — Tier 1, 2, 3 overview
3. Tier 1 Deep Dive — Primary ICP profile
4. Firmographics (B2B) / Demographics (B2C) — Quantitative segment data
5. Needs / Pain Points — Core problems, pain drivers, buying triggers
6. Beachhead & Competitive Landscape — Initial market focus strategy
7. Scenario-Based Profile — Before/After customer journey
8. Qualifying Criteria — Must-haves, nice-to-haves, disqualifiers
9. Tiering Summary — Brief overview of all tiers
10. Primary Buyer Persona — Goals, pain points, decision process, channels
11. Next Steps — Call to action

---

## Example: Successful Run (Greenfield Landscaping)

For reference, here's what a completed ICP processing looks like:

- **Transcript:** "ICP Deep Dive - Greenfield Landscaping"
- **Meeting Type:** ICP
- **Attendees:** Terry Robinson, Marcus Greenfield
- **Status:** Done
- **Deliverables Generated:** "ICP Document (B2B) — Greenfield_Landscaping_ICP_B2B.docx saved to Greenfield Landscaping folder. Primary ICP: Mid-Size Property Management Companies ($50K-$200K annual contracts). Processed automatically on 2026-03-22."
- **Notes:** "Transcript clearly identified B2B segment. Primary ICP targets mid-size property management companies managing 10-50 properties. Key differentiator: dedicated crew model. Items marked [Inferred] should be verified with Marcus Greenfield."

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
