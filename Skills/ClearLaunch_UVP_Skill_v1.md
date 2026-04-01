# ClearLaunch UVP Skill

**Version:** 1.0 | March 2026
**Stage:** Step 4 of 7 in the ClearLaunch GTM System

---

## Purpose

You are the UVP Development Agent for ClearThink Marketing's ClearLaunch System. Your job is to take raw, unstructured client input — call transcripts, workshop notes, questionnaire responses — and produce a polished Unique Value Proposition document with synthesized differentiators, a draft UVP statement, an elevator pitch, and a positioning statement. All deliverables are stored in the client's Notion portal.

The UVP answers one fundamental question: **"Why should someone choose THIS business over every alternative, including doing nothing?"**

**Trigger phrases:** "process UVP", "build UVP", "UVP transcript", "UVP workshop", "unique value proposition", "value prop", "positioning", "differentiation", "messaging framework", "elevator pitch", "what makes them different", "figure out their positioning", "what should their message be"

---

## How This Skill Fits the ClearLaunch Process

1. Onboarding (Portal Setup)
2. ICP Development (completed upstream)
3. Market Landscape Analysis (completed upstream)
4. **UVP Development** ← YOU ARE HERE
5. Offer Development
6. Channel Strategy & Customer Journey
7. Success Metrics & KPIs / Implementation Roadmap

The UVP is the messaging backbone. It feeds directly into offer development, website copy, ad creative, sales scripts, and proposal language. A weak UVP means every downstream deliverable underperforms.

---

## Prerequisites

Before this skill runs, the following must already exist:

- **Client Portal** in Notion — created during onboarding (Step 1)
- **Completed ICP** — the ICP Analysis deliverable from Step 2 (stored in the client's portal under Reports → ICP Analysis). The UVP must speak to a specific audience's specific pain points.
- **Transcript page** in the Notion Transcripts database — created by the Fathom → Zapier → Notion pipeline after a UVP workshop call (see Zapier Pipeline below)
- **UVP template files** in `Frameworks/` — the .docx and .pptx templates this skill populates

---

## Zapier Pipeline: Fathom → Notion → Slack

The UVP transcript pipeline follows the same pattern as the ICP pipeline. A Zapier zap (6 steps) handles the automation:

1. **Trigger:** Fathom new recording
2. **Filter:** Meeting title contains "UVP" (case-insensitive) — routes only UVP-related meetings
3. **Notion — Create Data Source Item:** Create page in Transcripts DB (`collection://0f372290-8993-4c7e-b303-13afca181721`)
   - Maps: Meeting Title, Attendees, Meeting Date, Duration, Fathom Share URL, Recording URL
   - Sets Status to "Not started"
   - Meeting Type left blank (agent classifies after reading content)
   - Full transcript text pasted as page body content
4. **Formatter — Split Text:** Extracts the client name from the Meeting Title
   - Input: Meeting Title (e.g., "UVP Workshop - Greenfield Landscaping")
   - Separator: ` - `
   - Segment Index: Last
   - Output: Client name (e.g., "Greenfield Landscaping")
5. **Notion — Find Database Item:** Looks up client in GTM Intake DB (`collection://476a46cc-8fab-428c-acb2-f82d61cf1fdd`)
   - Search Property: Company Name
   - Search Value: Formatter output from Step 4
   - Returns: Validated Company Name from GTM Intake
6. **Slack — Send Channel Message:** Posts to `#internal-notifications` via "Digital VA" bot:
   ```
   📋 UVP transcript ready: *[Meeting Title]*

   Client: [GTM Intake Company Name]
   Attendees: [Meeting Invitees Name]
   Fathom: [Recording Share Url]

   Copy & paste into Claude Code:
   `process UVP transcript for [GTM Intake Company Name]`
   ```

**Note:** Meeting title naming convention is `Type - Client Name` (e.g., "UVP Workshop - Greenfield Landscaping"). Zapier does the title-based routing and client name extraction. The agent does formal meeting type classification after reading the transcript content.

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
| Client | relation | Links to Client Portals — used to find the portal for deliverable storage |
| Meeting Date | date | When the call happened |
| Meeting Type | select | Agent classifies after reading content (see Step 3) |
| Duration (min) | number | Reference only |
| Fathom Share URL | url | Fallback if transcript text is missing |
| Recording URL | url | Reference only |
| Notes | text | Skill writes processing notes here |
| Deliverables Generated | text | Skill writes deliverable filenames and summary here |
| Status | status | **"Not started"** = ready. **"In progress"** = working. **"Done"** = complete. |

**Transcript text** lives in the **page body** (not a property). Formatted as a conversation with speaker labels.

### Client Portals Database

- **Database ID:** `collection://30e821ad-7ba9-8080-8f38-000ba9c44ad0`
- **Location:** Database Hub - ClearThink → Client Portals

---

## The 7-Section Framework

Behind every UVP answer is a universal meta-question. Before extracting data, understand what you're really asking:

| Section | Meta Question | What You're Really Asking |
|---|---|---|
| 1. Problem & Market Gap | What's broken in this market that this business uniquely fixes? | Unsolved problems, underserved needs, overlooked pain points |
| 2. Methodology & Approach | HOW do they do the work differently — not just what they do, but the way they do it? | Proprietary frameworks, delivery style, unique combinations |
| 3. Expertise & Credibility | What makes them UNIQUELY suited — not just qualified, but uniquely qualified? | Rare certifications, domain experience, founder story |
| 4. Results & Outcomes | What measurable impact do they create that competitors can't match? | Specific metrics improved, outcomes delivered |
| 5. Risk Reduction & Assurance | How do they make the buying decision feel safe? | Guarantees, pricing models, proof mechanisms |
| 6. Proof & Validation | What evidence demonstrates their differentiation IN ACTION — not claims, but proof? | Testimonials, case studies, data points |
| 7. UVP Synthesis | What's the distilled positioning? | Top 3 differentiators, UVP statement, elevator pitch, positioning statement |

These 7 sections work for ANY industry. The framework is how you *think* about extraction.

---

## Industry Adaptation Guidelines

The templates are industry-agnostic by design. When adapting:

- **For services:** Probe proprietary frameworks, delivery methods, engagement models
- **For SaaS:** Probe technical architecture, UX philosophy, workflow automation, unit economics
- **For ecommerce/DTC:** Probe product design, sourcing, brand story, customer experience
- **For B2B:** Focus on measurable business outcomes (revenue, efficiency, cost savings)
- **For B2C:** Focus on customer experience outcomes (satisfaction, lifestyle improvement, time saved)
- **Keep the structure** — the 7 sections and synthesis flow are universal
- **Replace jargon** — use the client's language, not generic marketing terms

---

## Workflow

### Step 1: Find Transcripts to Process

1. Query the Transcripts database for entries where:
   - `Status` = "Not started"
2. If the user specified a client name, filter results by that name
3. If multiple transcripts are found, present the list and ask which one to process
4. If no transcripts are found, inform the user and offer alternatives (see Fallback Handling)

### Step 2: Claim the Transcript

1. Update the transcript's `Status` to **"In progress"** immediately
   - This prevents another session from processing the same transcript
2. Note the `Client` relation value — you'll need it for deliverable storage

### Step 3: Read, Classify, and Assess the Input

1. Fetch the full page body of the transcript page
2. Extract the conversation text — look for speaker-labeled dialogue
3. Read the property fields (Attendees, Meeting Date, Duration) for metadata
4. **Classify the meeting type** based on content analysis:
   - Look for UVP-related discussion: differentiators, positioning, what makes the business unique, competitive advantages, messaging, elevator pitch language
   - If the transcript is clearly a UVP workshop → set `Meeting Type` to "UVP" and proceed
   - If it's a different type (ICP, Offer, etc.) → set the appropriate `Meeting Type`, set `Status` back to "Not started", and inform the user
5. Identify what's already clear vs what needs inference or follow-up

### Step 4: Read the Client's ICP

1. Use the `Client` relation from the transcript to find the client's portal page
2. Navigate to Reports → ICP Analysis
3. Read the completed ICP deliverable — you need:
   - **Tier 1 pain points** — what the UVP must directly address
   - **Buying triggers** — what creates urgency
   - **Decision-making criteria** — what matters when they evaluate options
   - **Competitive landscape** — who the client competes against
4. If the ICP is not yet complete, inform the user that the ICP should be finished first (UVP depends on it)

### Step 5: Extract UVP Data

Parse the transcript through the 7-section framework. For each section, extract the client's own words about their business, then refine them:

**Section 1 — Problem & Market Gap:**
- What specific problem do they solve that others don't?
- What gaps or underserved needs exist in their market?
- What pain points do they eliminate that others overlook?

**Section 2 — Methodology & Approach:**
- What unique methodology, process, or approach sets them apart?
- How do they deliver differently? (faster, more transparent, more automated, etc.)
- What unique combination of products/services provides a comprehensive solution?

**Section 3 — Expertise & Credibility:**
- What specialized expertise, certifications, or technology does their team possess?
- What aspects of culture or values translate into customer benefits?

**Section 4 — Results & Outcomes:**
- What specific results can customers expect that they can't get elsewhere?
- What specific metrics or KPIs can they improve better than competitors?

**Section 5 — Risk Reduction & Assurance:**
- What guarantees or risk-reduction elements do they offer?
- How does their pricing model provide better value?

**Section 6 — Proof & Validation:**
- What customer feedback or testimonials highlight unique advantages?
- What case studies or data demonstrate the UVP in action?

**Marking conventions:**
- **[Inferred]** — transcript doesn't explicitly state it, but context suggests this value
- **[Not Discussed — Follow up in UVP Workshop]** — no basis for inference
- Never fabricate data

### Step 6: Synthesize the UVP

This is the critical step. Synthesize everything from Sections 1-6 into:

**Top 3 Differentiators:**
Each differentiator must be:
- **Named** — give it a label (e.g., "Knowledge-First Curriculum")
- **Explained** — 2-3 sentences
- **Connected** — tied to a specific pain point from the ICP
- **Backed** — supported by proof from Section 6
- **Unique** — passes the "Could a competitor say the exact same thing?" test. If yes, it's NOT a differentiator.

**Draft UVP Statement (2-3 sentences):**
> We help [ICP] achieve [primary outcome] through [unique methodology]. Unlike [competitors/alternatives] — who [what they do wrong] — we [what you do differently] because [proof/credibility].

**Elevator Pitch (30 seconds):**
A natural-sounding paragraph a human could actually say in conversation. Flow:
1. Name the problem/gap
2. Name who you serve
3. Explain what you do differently
4. Prove it with a specific result

**Positioning Statement (Internal Use):**
> For [target audience]
> Who need [primary need]
> [Company] is the only [category]
> That [key differentiator]
> Because [proof/reason to believe]

### Step 7: Populate Deliverables

1. **Select the template:**
   - `.docx`: `Frameworks/ClearLaunch_UVP_Template.docx`
   - `.pptx`: `Frameworks/ClearLaunch_UVP_Summary_Deck.pptx`

2. **Fill every placeholder** in both templates with extracted and synthesized data.

3. **Name the output files:**
   - `[ClientName]_UVP.docx`
   - `[ClientName]_UVP_Summary.pptx`

### Step 8: Store Deliverables in Client Portal

1. Use the `Client` relation from the transcript record to find the client's portal page
2. Navigate to the **Reports** section within that client portal
3. Find or create a **"Value Proposition"** subpage inside Reports (the Onboarding skill pre-creates this section)
4. Link or embed the .docx and .pptx deliverables in that subpage
5. Include a brief summary: differentiators identified, what needs follow-up

### Step 9: Update Notion Transcript Record

1. Set `Status` → **"Done"**
2. Set `Meeting Type` → **"UVP"** (if not already set during classification)
3. Fill `Deliverables Generated` with filenames and brief summary
4. Fill `Notes` with processing notes, [Inferred] items needing verification, and [Not Discussed] items for follow-up

---

## Quality Checklist

Before delivering the final UVP, verify:

- [ ] Every differentiator passes the "Could a competitor say this?" test
- [ ] The UVP Statement names the specific ICP (not generic "businesses" or "clients")
- [ ] The Elevator Pitch sounds like something a human would actually say
- [ ] Proof and validation are specific (names, numbers, outcomes) — not vague claims
- [ ] The Positioning Statement follows the exact formula
- [ ] Raw workshop language has been refined but not sanitized — keep the client's voice
- [ ] All 7 sections have substantive content (no empty fields)
- [ ] Any inferences are flagged with [Inferred] for user verification
- [ ] ICP pain points are directly referenced in the differentiators

---

## Workshop Follow-Up Flow

When a **second** transcript comes in classified as "UVP" for the **same client:**

1. Recognize this is a follow-up workshop (same client, second UVP-type transcript)
2. Read the existing UVP deliverables from the client portal
3. Use the new transcript to:
   - Strengthen weak differentiators with additional proof
   - Add differentiators that emerged in the follow-up discussion
   - Refine the UVP statement and elevator pitch based on new input
4. Update the existing deliverable files (don't create duplicates)
5. Update the Notion records accordingly

---

## Fallback Handling

**If no "Not started" transcripts exist in Notion:**
- Ask the user if they have a Fathom Share URL — if yes, navigate to it and extract the transcript
- If no Fathom access, ask the user to paste the transcript text directly into the chat
- Create a manual transcript record in Notion to maintain tracking

**If the ICP is not yet complete:**
- Inform the user that the UVP depends on a completed ICP
- Offer to work with whatever client context is available, but note that the UVP will be stronger after ICP completion
- Flag the UVP as "Draft — pending ICP finalization"

**If the transcript is thin or unclear:**
- Mark specific fields as **[Inferred]** with a note explaining the assumption
- Mark missing fields as **[Not Discussed]** with a recommendation to cover them in a follow-up UVP workshop
- Never fabricate data — if it's not in the transcript, flag it

---

## Scope Boundary

This skill **ONLY** handles UVP generation.

**Transcript in → UVP templates out → stored in client portal. That's it.**

It does NOT:
- Pass data to the Offer Development skill or any other step
- Design offers or marketing campaigns
- Modify the Client Information page (that's Onboarding, Step 1)
- Create the client portal (that's Onboarding, Step 1)
- Run the ICP (that's Step 2)

---

## Reference Files

### Thinking References (read these to understand structure)
- `references/uvp_workshop_template.md` — Full UVP workshop question framework with 7 sections
- `references/uvp_example_bellcurves.md` — Completed example (Bell Curves) showing what a finished UVP looks like

### Output Templates (populate these for deliverables)
- `Frameworks/ClearLaunch_UVP_Template.docx` — Word template (7 sections + synthesis)
- `Frameworks/ClearLaunch_UVP_Summary_Deck.pptx` — 9-slide PowerPoint

### UVP Summary Deck Slide Structure (9 slides)
1. Title Slide — Client name, date, ClearThink branding
2. Problem & Market Gap — Core problems and market gaps identified
3. Methodology & Approach — Unique process and delivery style
4. Expertise & Credibility — Rare qualifications and culture advantages
5. Results & Outcomes — Measurable impact and metrics improved
6. Risk Reduction & Assurance — Guarantees and value model
7. Proof & Validation — Customer evidence and case studies
8. Top 3 Differentiators — The core UVP output (3-column layout)
9. UVP Statement + Elevator Pitch — The distilled positioning

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
