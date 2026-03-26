---
name: client-profile-generator
description: "Generate a structured client profile document (.docx) from onboarding call notes and/or a completed questionnaire. Use this skill whenever the user mentions 'client profile', 'onboarding synthesis', 'client intake', 'new client', or provides raw onboarding notes/transcripts and wants them turned into a structured profile. Also trigger when the user uploads call transcripts, questionnaire responses, or client intake forms and wants a clean summary document produced. This is the first step in the web design workflow — everything downstream (copywriting, content briefs) depends on a solid client profile. Trigger even when the user just says something like 'process this onboarding' or 'synthesize this client info' or drops a CSV with questionnaire data."
---

# Client Profile Generator

## What This Skill Does

This skill takes raw client onboarding materials — call transcripts, filled questionnaires (including CSV exports), intake notes, emails, or any combination — and synthesizes them into a clean, structured client profile document (.docx). The profile is ready to upload into Notion or hand off to team members.

The profile captures everything needed for downstream web copy and design work: who the client is, what they do, who they serve, how they're different, and what their brand should feel like.

## Why Each Section Matters

The profile isn't just a summary — it's the foundation the copywriter and designer build on. Every section exists because it directly feeds a downstream decision:

- **Client Overview & Mission** → Sets the strategic frame for all messaging
- **Services/Products** → Defines the sitemap and page structure
- **Why They Hired Us** → Keeps the project focused on outcomes, not scope creep
- **Target Audience** → This is who the website copy speaks to — pain points, desires, language
- **Unique Value Proposition & Differentiators** → The core argument every page makes
- **Brand Voice & Tone** → How the copy should sound — the copywriter needs this to write
- **Competitors** → Positioning depends on knowing what the audience is comparing against
- **Social Proof Inventory** → What credibility assets exist to weave into the site
- **Color Palette & Visual Direction** → The designer needs this alongside the copy

## Process

### Step 0: Set Up Client Folder

Before generating anything, create the client's folder structure in the workspace:

```
Clients/[Client Name]/
├── Client Information/    ← profile doc goes here
└── Deliverables/          ← content briefs, copy docs go here later
```

Check if the folder already exists first. If it does, use it. If not, create it. The client name should match how they refer to their business (e.g., "Demarciano" not "Nathaniel Epps").

### Step 1: Understand What You're Working With

When the user provides onboarding materials, read through everything before doing anything else. Common input formats:

**CSV questionnaire exports:** These often contain multiple clients in rows. Ask the user which client to process, or identify the correct row by matching the business name. CSV columns may have generic headers like "Untitled short answer field" — use context to figure out what each column represents. The column order typically follows: contact info → mission/values → services → differentiators → scaling plans → ideal customer → demographics → challenges → competitors → brand preferences → design choices → page selections.

**Call transcripts (Fathom, Otter, etc.):** These are gold for context that doesn't appear in questionnaires — the *why* behind answers, nuances about competitors, design preferences discussed live, and the client's actual voice/language. Cross-reference with the questionnaire to fill gaps and add depth.

**Loose notes or emails:** Treat as supplementary. Extract what's useful and flag if critical info is missing.

You're looking for:
- How complete is the information? Are there obvious gaps?
- What industry/business type is this?
- Does the transcript add context beyond the questionnaire? (It usually does — especially around competitors, design direction, and the client's real motivations)

### Step 2: Ask Before You Assume

Before generating the profile, check for gaps. If any of the following are missing or unclear, ask the user directly — don't guess:

**Must-haves (do not proceed without these):**
- What the business does (services/products)
- Who their target audience is
- What makes them different from competitors

**Should-haves (ask if missing, but can proceed with a flag):**
- Brand voice/tone preferences
- Competitor names
- Specific results or social proof

Ask focused, specific questions — not a laundry list. For example:
- "I can see they offer three services, but the notes don't mention who their ideal client is. Do you have that, or should I flag it as a gap?"
- "There's no mention of competitors. Do you know who they're up against?"

### Step 3: Generate the Profile Document

Create a .docx file using the `docx` skill's approach (docx-js via Node). The document should be clean, professional, and easy to scan.

**Document Structure:**

```
CLIENT PROFILE: [Client Name]
Generated: [Date]  |  Prepared by: ClearThink Marketing

1. CLIENT OVERVIEW
   Table format with key facts:
   - Business name, owner, contact info
   - Industry/niche, location, year founded
   - Social media presence
   Then 2-3 sentence summary paragraph

2. MISSION & VISION
   - Mission statement (synthesized from their words — not corporate speak)
   - Core values (as bullet points)
   - Long-term vision (where they're headed)

3. SERVICES / PRODUCTS
   For each major service/product line:
   - Name as subheading
   - Description paragraph (what it is, who it's for)
   Then list product categories as bullets

4. PROJECT SCOPE — WHY THEY HIRED US
   - The Problem (what's broken or missing — use their words)
   - What Success Looks Like (bullet list of concrete outcomes)
   - Future Goals (what comes after this project)

5. TARGET AUDIENCE / IDEAL CUSTOMER
   - Demographics table (gender, age, location, income, occupation)
   - Psychographics paragraph (mindset, values, style)
   - Pain points (bullet list)
   - How they currently buy (current customer journey)
   Include direct quotes from the client when available —
   the copywriter needs to hear the client's voice

6. UNIQUE VALUE PROPOSITION & DIFFERENTIATORS
   - Core UVP (one statement)
   - Primary message (the tagline or key takeaway)
   - Key differentiators (3-5 bullets with detail)

7. BRAND VOICE & TONE
   - Tone description (paragraph)
   - Brand personality traits (bullets)
   - Voice guidelines (bullets — how to write for this brand)
   - Words/phrases to lean into
   - Words/phrases to avoid

8. COMPETITORS
   For each competitor:
   - Name as subheading
   - What they do well (paragraph)
   - Where the client has an advantage (paragraph)

9. SOCIAL PROOF INVENTORY
   - Bullet list of all credibility assets
   - Note at end flagging what's missing (e.g., "No testimonials provided")

10. COLOR PALETTE & VISUAL DIRECTION
    - Brand colors table (name + hex code)
    - Typography preferences
    - Design style description
    - Template selection (if applicable)
    - Imagery notes (current state + what's needed)
```

**Followed by:**

```
GAPS & FOLLOW-UPS
- Specific bullet list of everything that couldn't be filled in
- Each gap should say what's missing AND why it matters
```

### Step 4: Formatting & Design

The .docx should feel like a professional internal document — clean enough to share but not fussy:

- **Page size:** US Letter (8.5 x 11) with 1-inch margins
- **Font:** Arial throughout — 11pt body (22 half-points), headings scaled up
- **Colors:** Use the client's brand color as an accent (section dividers, header bar). Fall back to a gold (#D9B829) accent if no brand color is provided.
- **Header:** "CLIENT PROFILE | [CLIENT NAME]" with a colored underline
- **Footer:** Page numbers, right-aligned
- **Tables:** Use for structured data (client overview, demographics, colors). Light gray backgrounds on label cells, thin borders.
- **Section dividers:** A colored horizontal rule between major sections for visual breathing room
- **Bullets:** Use docx-js LevelFormat.BULLET — never unicode bullet characters

Read the docx SKILL.md for technical implementation details (docx-js setup, table formatting, page breaks, validation).

### Step 5: Save and Present

1. Save the .docx to `Clients/[Client Name]/Client Information/[ClientName]_Client_Profile.docx`
2. Validate the file using the docx validation script
3. Provide a computer:// link so the user can open it directly
4. Briefly mention any critical gaps that need follow-up — don't over-explain the document

## Important Notes

- **Never invent information.** If the onboarding materials don't mention something, either ask or flag it — don't fill in plausible-sounding details. This is the single most important rule.
- **Use the client's language.** If they described their audience as "dream chasers, freedom fighters, and faith-based carriers," capture that exact phrasing. The copywriter needs to hear the client's voice. Direct quotes are valuable.
- **Keep it synthesis, not transcription.** The profile should be organized and concise, not a rehash of the raw notes. Distill, don't dump.
- **Cross-reference sources.** When you have both a questionnaire and a transcript, the transcript almost always adds important nuance — design preferences, competitor analysis, the client's real motivations vs. what they wrote in a form. Synthesize across both.
- **One profile per client.** Each run produces one complete profile document.
- **Call transcripts have action items.** You may see lines like "ACTION ITEM: ..." in transcripts. Don't include these in the profile — they're project management notes, not client profile content.
