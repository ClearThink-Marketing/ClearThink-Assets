# ClearLaunch GTM Strategy Blueprint

**ClearThink Marketing | Version 3.3 | April 2026**

---

## Purpose

This document is the single-source-of-truth for the ClearLaunch System — ClearThink Marketing's productized go-to-market strategy sprint. It captures:

- The full 7-step process and what each step produces
- What's already built (templates, decks, agent skills) and what's next
- How the agent automation works and how data flows between steps
- The tool stack and infrastructure that powers the system

**Audience:** Terry Robinson (operator), future team members, and any Claude Code session that needs context to continue building skills or templates.

**How to use this:** Hand this file to a new chat session as context. It tells the agent what the ClearLaunch System is, what exists, what needs to be built, and how the pieces connect.

---

## 1. What Is The ClearLaunch System

The ClearLaunch System is an 8-week, industry-agnostic go-to-market strategy sprint priced at $1,000 (or 2 payments of $500). It gives businesses a complete GTM strategy they can execute themselves or hire ClearThink to implement.

**It works for any business type** — AEC firms (architects, engineers, contractors), ecommerce brands, SaaS companies, professional services, or any business that needs a structured path to consistent client acquisition.

**The core promise:** Eliminate marketing guesswork by building a data-backed strategic foundation before spending on campaigns. The client walks away knowing exactly who to target, what message resonates, and where to focus their budget.

### The 7 Steps & Their Deliverables

| Step | Focus | Deliverables Produced |
|---|---|---|
| 1 | Client Onboarding & Portal Setup | Client Portal in Notion — validated intake data, populated Client Information, scaffolded Reports section |
| 2 | Ideal Customer Profile | ICP Analysis document (.docx) + ICP Summary Deck (.pptx) — 1-3 prioritized customer segments, pain point mapping, decision-making criteria, qualifying/disqualifying criteria |
| 3 | Market Landscape Analysis | Market Research document (.docx) + Market Research Summary Deck (.pptx) — keyword research (up to 50 keywords), competitive analysis, audience intelligence, content gap analysis |
| 4 | UVP Development | UVP document (.docx) + UVP Summary Deck (.pptx) — Top 3 differentiators, UVP statement, elevator pitch, positioning statement, 7-section framework |
| 5 | Offer Development | Offer Development document (.docx) — 3-tier offer ladder (Micro/Macro/Core), creative angles, objection handling |
| 6 | Channel Strategy & Customer Journey | Channel Strategy document (.docx) + Summary Deck (.pptx) + Projections Workbook (.xlsx) — two-phase: channel evaluation, budget allocation, projections (Phase A), then customer journey mapping across confirmed channels (Phase B) |
| 7 | Success Metrics & Launch Roadmap | KPI Framework + Implementation Roadmap (.docx) — 5-10 priority metrics, 90-day tactical plan, budget allocation, prioritized actions |

### The 4-Phase Timeline

| Phase | Weeks | Steps | Focus |
|---|---|---|---|
| Phase 1: Onboarding, Discovery & Research | 1-2 | Steps 1-3 | Client onboarding, ICP discovery sessions, market research, keyword analysis, competitive landscape |
| Phase 2: Strategy Development | 3-4 | Steps 4-5 | UVP development, offer engineering (Micro/Macro/Core ladder), messaging framework |
| Phase 3: Channel & Roadmap | 5-6 | Steps 6-7 | Customer journey mapping, channel strategy, success metrics, KPI framework, 90-day implementation roadmap |
| Phase 4: Strategy Delivery & Launch Prep | 7-8 | Delivery | Complete strategy delivery, priority recommendations, tracking activation, first campaign launch support |

---

## 2. The 7-Step Process

This process synthesizes ClearThink's own methodology with GTM best practices. Each step builds on the output of the previous one.

---

### Step 1: Client Onboarding & Portal Setup

**Status: BUILT** (Tally form live, GTM Intake database created, Onboarding Skill v1 complete)

**This is Skill 1** in the ClearLaunch system. It validates the intake data and creates a populated client portal. This step has two workflows:

**Workflow A: Tally Form → Client Portal (automated)**

Takes the client's Tally form submission, validates that all required data is present, duplicates the Client Template Page in Notion, and populates the Client Information sub-page with intake data (Company Overview, Story & Positioning, Target Audience, Competitive Landscape sections).

1. Client fills out the [GTM Strategy Intake Questionnaire](https://tally.so/r/Ekk6dr)
2. Tally sends submission directly to the GTM Intake database in Notion (`collection://476a46cc-8fab-428c-acb2-f82d61cf1fdd`)
3. Zapier fires a Slack notification to `#internal-notifications` via Digital VA bot
4. Terry says "process new intake" or "onboard client"
5. Agent queries GTM Intake for "New" submissions, runs validation checklist
6. Duplicates the Client Template Page, renames it, populates the Client Information sub-page with all intake data
7. Creates the Reports section for downstream skill deliverables
8. Updates intake record status to "Portal Created"

**Workflow B: Onboarding Call (record-keeping only)**

After the portal is created, Terry conducts an onboarding call with the client to walk them through the ClearLaunch process and set expectations.

1. Terry has the onboarding call with the client
2. Fathom records and transcribes the call
3. Transcript lands in the Transcripts DB via Zapier (`collection://0f372290-8993-4c7e-b303-13afca181721`)
4. Slack notification fires (existing Fathom → Notion → Slack zap)
5. Terry sets the Client relation on the transcript record for organizational purposes

This transcript is stored for reference only — **no agent skill processes the onboarding call transcript.** The Onboarding Skill gets all its data from the Tally form (Workflow A). The onboarding call is a client relationship touchpoint, not a data extraction event.

**What it produces:**
- A fully populated Client Portal page in Notion (Client Information filled, Reports section scaffolded)
- Validation report flagging any missing fields
- Onboarding call transcript stored in Transcripts DB (for reference)

**Notion references:**
- GTM Intake DB: `collection://476a46cc-8fab-428c-acb2-f82d61cf1fdd`
- Client Portals DB: `collection://30e821ad-7ba9-8080-8f38-000ba9c44ad0`
- Client Template Page: `310821ad7ba980f294c0e0096effb298`
- Transcripts DB: `collection://0f372290-8993-4c7e-b303-13afca181721`

**Skill file:** `Skills/ClearLaunch_Onboarding_Skill_v1.md`
**Field mapping:** `Skills/ClearLaunch_Onboarding_Field_Mapping.md`

---

### Step 2: Define Ideal Client Profile

**Status: BUILT** (templates complete, agent skill complete)

**This is Skill 2** in the ClearLaunch system. Skill 1 (Onboarding) creates the client portal and populates Client Information from the Tally form. This ICP skill comes after — it processes the ICP Discovery call transcript, which is a separate, later call from the onboarding call.

**What it accomplishes:** Creates a detailed picture of who the client should be targeting — firmographics (B2B) or demographics (B2C), behaviors, pain points, buying triggers, and decision-making criteria. Segments prospects into Tier 1 (primary focus), Tier 2 (secondary), and Tier 3 (nurture/monitor).

**How it works in practice:**
1. Terry conducts an ICP Discovery call with the client — a dedicated call focused on ideal customer profiling, separate from the onboarding call (recorded via Fathom)
2. The call transcript lands in Notion automatically (Fathom → Zapier → Notion Transcripts DB with Status: "Not started")
3. Zapier sends a Slack notification to `#internal-notifications` alerting Terry that a transcript is ready
4. Terry opens Claude Code and says "process new transcripts"
5. The agent queries Notion for "Not started" ICP Discovery transcripts, sets status to "In progress"
6. Agent reads the transcript from the page body, determines B2B or B2C, and extracts ICP data
7. Tier 1 gets fully fleshed out from the ICP Discovery call data
8. Both the .docx template and .pptx summary deck are populated
9. Deliverables are stored in the client's portal (Reports → ICP Analysis section)
10. Notion transcript record updated to "Done" with deliverable filenames and processing notes
11. During a subsequent ICP workshop, Tiers 2 and 3 get fleshed out from the workshop transcript

**What the agent needs as input:**
- A "Not started" transcript in the Notion Transcripts database (Meeting Type: ICP Discovery)
- The Client relation must be set on the transcript so the agent can find the client's portal
- Note: Onboarding call transcripts (from Step 1, Workflow B) are stored in the same Transcripts DB but are NOT processed by this skill

**What it produces:**
- Populated ICP Template (.docx) — B2B version uses firmographics; B2C version uses demographics/psychographics
- Populated ICP Summary Deck (.pptx) — 11-slide presentation ready for client review
- Deliverables stored in client portal Reports section

**Notion references:**
- Transcripts DB: `collection://0f372290-8993-4c7e-b303-13afca181721`
- Client Portals DB: `collection://30e821ad-7ba9-8080-8f38-000ba9c44ad0`

**Skill file:** `Skills/ClearLaunch_ICP_Skill_v2.md` — contains the complete workflow, Notion integration, extraction fields for B2B and B2C, fallback handling, tiering logic, and template references. Also mirrored in `Skills/Claude-Desktop-Skills/clearlaunch-icp/SKILL.md` for the Claude desktop app.

**ICP tiering approach:**
- **Tier 1 (High Priority):** Maximum investment — direct outreach, personalized campaigns, highest LTV potential. This is the beachhead market the client should dominate first.
- **Tier 2 (Potential):** Scaled outreach, good fit but lower urgency or smaller deal size. Expansion market after Tier 1 is proven.
- **Tier 3 (Nurture Only):** Monitor and nurture. May become Tier 2 over time as the market or the client's offering evolves.

**Framework files:**
- `Frameworks/ClearLaunch_B2B_ICP_Template.docx`
- `Frameworks/ClearLaunch_B2B_ICP_Summary_Deck.pptx`
- `Frameworks/ClearLaunch_B2C_ICP_Template.docx`
- `Frameworks/ClearLaunch_B2C_ICP_Summary_Deck.pptx`

**Remaining items:**
- Zapier notification step has been added — Slack notification fires to `#internal-notifications` via "Digital VA" bot when a transcript lands in Notion
- ICP Summary Decks were rebuilt on March 24, 2026 — all layout issues resolved (0 remaining). Build script at `Frameworks/rebuild_icp_decks.py`

---

### Step 3: Analyze Market Landscape

**Status: PARTIALLY BUILT** (templates complete, agent skill v2 in progress)

**What it accomplishes:** Researches the client's target market size, growth trajectory, competitive landscape, keyword opportunities, and content gaps. Validates that there's real demand for what the client offers and identifies where they have the best chance of winning.

**How it works in practice:**
1. Agent reads the ICP output from Step 2 (stored in the client's Notion portal) — specifically the industry, target segments, competitor names, and pain points
2. Agent reads the client portal data that was populated by Onboarding (Step 1) — keywords, competitor URLs, client's own website. This is Tally form data, not ICP Discovery call data.
3. Agent runs Ahrefs browser workflows for SEO/keyword/backlink data
4. Agent runs SimilarWeb browser workflows for traffic/audience/market data
5. Agent synthesizes findings into the Market Research template + summary deck

**What the agent needs as input:**
- ICP data from Step 2 (from Notion)
- Client's website URL
- Competitor URLs (from ICP Discovery call or Tally onboarding form)
- Seed keywords (derived from ICP pain points and industry terms)

**What it produces:**
- Populated Market Research Template (.docx) with: keyword landscape, competitive analysis, audience intelligence, market sizing
- Populated Market Research Summary Deck (.pptx)
- Structured market research data stored in Notion (becomes input for Step 4)

**Ahrefs workflows (what the agent pulls):**
- Site Explorer → Organic Keywords: what the client currently ranks for
- Site Explorer → Backlink Profile: client's link authority
- Content Gap: keywords competitors rank for that the client doesn't
- Keywords Explorer: volume, difficulty, and CPC for seed keywords from ICP
- Site Audit: technical SEO issues (if client has Ahrefs access)

**SimilarWeb workflows (what the agent pulls):**
- Website Analysis → Traffic Overview: traffic estimates for competitors
- Website Analysis → Audience: demographics, geography, interests
- Website Analysis → Competitors & Similar Sites: cross-visitation, referral sources
- Industry Analysis: benchmark the client's vertical

**When to use which:** Ahrefs for search visibility data (keywords, backlinks, content gaps). SimilarWeb for market sizing and audience behavior data (traffic, demographics, industry benchmarks).

**Framework files:**
- `Frameworks/ClearLaunch_B2B_Market_Research_Template.docx`
- `Frameworks/ClearLaunch_B2B_Market_Research_Summary_Deck.pptx`
- `Frameworks/ClearLaunch_B2C_Market_Research_Template.docx`
- `Frameworks/ClearLaunch_B2C_Market_Research_Summary_Deck.pptx`

**Open items:**
- Market Research Skill v2 needs to be built — will replace the outdated `Skills/Claude-Desktop-Skills/clearlaunch-market-research/SKILL.md`
- Ahrefs and SimilarWeb workflows are now defined by the template structure (15 tables across the .docx templates specify exactly which data to pull from which tool)
- Browser workflows for Ahrefs (Keywords Explorer, Site Explorer, Content Gap, Top Pages, Backlinks, Paid Keywords), SimilarWeb (Traffic Sources, Audience, Social), and Meta Ad Library need to be written into the skill

---

### Step 4: UVP Development

**Status: BUILT** (templates complete, agent skill complete, Zapier pipeline documented inline)

**What it accomplishes:** Takes the ICP pain points (from Step 2) and the competitive gaps (from Step 3) and synthesizes them into a unique value proposition — Top 3 differentiators, a UVP statement, an elevator pitch, and a positioning statement. This is the messaging backbone that feeds into offer development, website copy, ad creative, and sales scripts.

**How it works in practice:**
1. Terry conducts a UVP workshop call with the client (recorded via Fathom)
2. The call transcript lands in Notion automatically (Fathom → Zapier → Notion Transcripts DB with Status: "Not started")
3. Zapier sends a Slack notification to `#internal-notifications` via "Digital VA" bot
4. Terry opens Claude Code and says "process UVP transcript"
5. Agent queries Notion for "Not started" transcripts, reads content, classifies as UVP
6. Agent sets status to "In progress", reads the client's completed ICP from their portal
7. Agent extracts data through the 7-section framework (Problem, Methodology, Expertise, Results, Risk, Proof, Synthesis)
8. Agent cross-references ICP Tier 1 pain points to ground differentiators in real audience needs
9. Agent synthesizes: Top 3 Differentiators, UVP Statement, Elevator Pitch, Positioning Statement
10. Both .docx and .pptx deliverables are populated
11. Deliverables stored in client portal (Reports → Value Proposition section)
12. Transcript record updated to "Done"

**What the agent needs as input:**
- A "Not started" transcript in Notion (classified as UVP by agent after reading content)
- Completed ICP deliverable from Step 2 (Tier 1 pain points, buying triggers, competitive landscape)
- The Client relation must be set on the transcript

**What it produces:**
- Populated UVP Template (.docx) — 7-section framework + synthesis outputs
- Populated UVP Summary Deck (.pptx) — 9 slides presenting the refined UVP
- Deliverables stored in client portal Reports section

**The 7-section framework:**
1. Problem & Market Gap — what's broken that this business uniquely fixes
2. Methodology & Approach — HOW they do it differently
3. Expertise & Credibility — what makes them uniquely qualified
4. Results & Outcomes — measurable impact competitors can't match
5. Risk Reduction & Assurance — why the buying decision feels safe
6. Proof & Validation — evidence of differentiation in action
7. UVP Synthesis — Top 3 Differentiators, UVP Statement, Elevator Pitch, Positioning Statement

**Skill file:** `Skills/ClearLaunch_UVP_Skill_v1.md` (includes Zapier pipeline details inline)

**Framework files:**
- `Frameworks/ClearLaunch_UVP_Template.docx`
- `Frameworks/ClearLaunch_UVP_Summary_Deck.pptx`

---

### Step 5: Offer Development

**Status: BUILT** (templates complete, agent skill complete, Zapier pipeline documented inline)

**What it accomplishes:** Designs the client's complete offer stack — a 3-tier ladder from free entry-point (Micro Offer) through initial paid engagement (Macro Offer) to full core engagement (Core Offer). Each tier builds trust and leads naturally to the next.

**What the agent needs as input:**
- Completed ICP (Tier 1 pain points, buying triggers)
- Completed UVP (Top 3 differentiators, positioning)
- Industry/vertical context

**What it should produce:**
- Populated Offer Development Template (.docx) — 3-tier offer ladder, creative angles, objection handling
- Offer Dev Summary Deck (.pptx) — 8-slide branded deck summarizing the ladder
- Deliverables stored in client portal Reports → Offer Development section

**The 3-tier offer ladder:**
- **Micro Offer (Marketing Offer):** Free resource that demonstrates expertise (audit, calculator, guide, quiz, sample kit)
- **Macro Offer (Business Offer):** Entry-point paid offering that proves the relationship works (consultation, starter plan, pilot project)
- **Core Offer (Full Engagement):** Primary revenue driver (retainer, subscription, full implementation)

**Framework files:**
- `Frameworks/ClearLaunch_Offer_Dev_Template.docx`
- `Frameworks/ClearLaunch_Offer_Dev_Summary_Deck.pptx`
- `Frameworks/build_offer_dev_deck.py`
- `Skills/ClearLaunch_Offer_Dev_Skill_v1.md`

---

### Step 6: Channel Strategy & Customer Journey

**Status: BUILT** (all templates complete, agent skill complete, Zapier pipeline documented)

**Key architectural difference from Steps 2–5:** Step 6 is a TWO-PHASE step:
- **Phase A (Internal Analysis):** No Fathom transcript. Terry triggers the skill manually. Reads all 4 upstream deliverables (ICP, MR, UVP, Offer Dev), evaluates 7 channels, scores against ICP, recommends focused channel mix, allocates budget, generates per-channel projections (data-backed + modeled). Terry presents findings to client.
- **Fathom Call:** Client reviews channel strategy, confirms channels, provides industry-specific customer journey insights.
- **Phase B (Journey Build):** Skill reads the Fathom transcript (confirmed channels + journey insights) and completes the customer journey map on top of confirmed channels.

**Channel selection comes BEFORE journey mapping.** The journey map is built on top of the confirmed channels — not the other way around.

**How it works in practice:**

**Phase A:**
1. Terry says `Generate channel strategy for [Client Name]`
2. Agent reads Client Portal → verifies Steps 2–5 are complete
3. Reads ICP (audience, geography, B2B/B2C), Market Research (keywords, CPC, competitors), UVP (positioning, differentiators), Offer Dev (pricing, Revenue Per Client)
4. Scores all 7 channels in the ClearLaunch channel universe (Google Ads, Meta Ads, LinkedIn Ads, TikTok, SEO, Content Marketing, Organic Social)
5. Applies 4 decision rules in order: ICP Presence Gate → Budget Viability Gate → Journey Coverage Check → Data Availability Tiebreaker
6. Recommends 1–2 primary + 0–1 supporting channels
7. Builds budget allocation (retainers fixed, ad spend adjustable)
8. Generates projections: data-backed (from keyword CPC data) and modeled (from CPM/CTR benchmarks)
9. Populates .docx (Sections 1, 3–9), .pptx (Slides 1, 3–8), .xlsx (all 4 tabs)
10. Stores preliminary deliverables in Client Portal → Reports → Channel Strategy

**Phase B:**
1. After the Fathom call, Zapier pipeline fires → transcript in Notion → Slack notification with command `Complete journey map for [Client Name]`
2. Agent reads transcript → extracts confirmed channels, client feedback, journey insights
3. Reads existing Phase A deliverables from portal
4. Builds TOFU/MOFU/BOFU/Purchase journey map using confirmed channels + client insights
5. Completes .docx (adds Section 2: Journey Map), .pptx (adds Slide 2), updates .xlsx if projections adjusted
6. Updates Client Portal with final deliverables

**What the agent needs as input:**
- Phase A: All 4 upstream deliverables (ICP, MR, UVP, Offer Dev) in Client Portal
- Phase B: Fathom transcript from Channel Strategy decision call

**What it produces:**
- Channel Strategy document (.docx) — 9 sections: Executive Summary, Customer Journey Map, Channel Universe Assessment, Recommended Channel Strategy, Investment Overview, Data-Backed Projections, Modeled Projections, Content & SEO Foundation, Key Takeaways & Next Steps
- Channel Strategy Summary Deck (.pptx) — 8 slides: Title, Journey Map, Channel Universe, Channel Recommendation, Investment Overview, Data-Backed Projections, Modeled Projections, Key Takeaways
- Channel Projections Workbook (.xlsx) — 4 tabs with live formulas: Summary (cross-sheet refs), Google Ads (data-backed), Meta Ads (modeled), Content & SEO
- All deliverables stored in client portal Reports section

**ROAS formula architecture:** Both Google Ads and Meta Ads tabs use identical structure — per-service-line `Ad Spend ROAS = Revenue ÷ Ad Spend`, combined `True ROAS = Revenue ÷ (Ad Spend + Retainer)`. No asymmetry between channels.

**Notion references:**
- Transcripts DB: `collection://0f372290-8993-4c7e-b303-13afca181721` (Phase B transcript)
- Client Portals DB: `collection://30e821ad-7ba9-8080-8f38-000ba9c44ad0` (reads/writes deliverables)
- GTM Intake DB: `collection://476a46cc-8fab-428c-acb2-f82d61cf1fdd` (Zapier validation)

**Skill file:** `Skills/ClearLaunch_Step6_ChannelStrategy_Skill_v1.md`
**Reference template:** `Frameworks/channel_strategy_template.md`

**Framework files:**
- `Frameworks/ClearLaunch_Step6_ChannelStrategy_Template.docx`
- `Frameworks/ClearLaunch_Step6_ChannelStrategy_Summary_Deck.pptx`
- `Frameworks/ClearLaunch_Step6_Projections_Template.xlsx`
- `Frameworks/build_step6_templates.py`
- `Frameworks/build_step6_deck.py`
- `Frameworks/build_step6_projections.py`

**Channel strategy principle:** Start focused. Pick 1-2 primary channels that match the audience and the client's capacity. Prove ROI there before expanding. The most common GTM failure is channel sprawl — trying to be everywhere at once and being effective nowhere.

---

### Step 7: Success Metrics & Launch Roadmap

**Status: NOT STARTED** (no template, no skill)

**What it accomplishes:** Defines success metrics and KPIs per channel, then packages everything from Steps 1-6 into a 90-day tactical execution plan with specific tasks, timelines, budget allocations, and clear ownership.

**What the agent needs as input:**
- All outputs from Steps 1-6
- Client's available budget and internal capacity

**What it should produce:**
- Success Metrics & KPI Framework (.docx) — TO BE BUILT
- Implementation Roadmap (.docx) — 90-day plan with weekly milestones, budget allocation, prioritized actions
- Both stored in client portal Reports section

**Key principle:** The roadmap should be actionable regardless of who executes it.

---

## 3. How The Agent Automation Works

The ClearLaunch System uses a single Claude Code agent that plays different roles depending on which step/deliverable is active. It's not 7 separate agents — it's one agent with different skills (context + instructions) for each phase.

### Data Flow

```
TALLY ONBOARDING FORM (Client)            ICP DISCOVERY CALL (Terry + Client)
        |                                          |
        v                                          v
  [Tally Native Integration]                 [Fathom Recording]
        |                                          |
        v                                          v
  [Notion: GTM Intake DB]                   [Zapier Webhook]
        |         |                                |
        |         v                                v
        |   [Zapier: Intake → Slack]         [Notion: Transcripts DB]
        |         |                                |
        |         v                                v
        |   [Slack #internal-notifications]  [Slack #internal-notifications]
        |                                          |
        v                                          v
  ┌─────────────────────────────────────────────────────────┐
  │  AGENT (Claude Code)                                    │
  │                                                         │
  │  Step 1 Role: Onboarding Skill                          │
  │  - Reads intake data from GTM Intake DB                 │
  │  - Validates fields, duplicates Client Template          │
  │  - Creates Client Portal in Notion                      │
  │                                                         │
  │  ONBOARDING CALL (Terry + Client) ──────────────────┐   │
  │  - Fathom records → transcript to Transcripts DB    │   │
  │  - Stored for reference only, NOT agent-processed   │   │
  │                                                         │
  │  Step 2 Role: ICP Skill                                 │
  │  - Reads ICP Discovery call transcript from Notion      │
  │  - Fills ICP template + deck                            │
  │  - Stores structured ICP data in Notion                 │
  │                                                         │
  │  Step 3 Role: Market Research Skill                     │
  │  - Reads ICP data from Notion                           │
  │  - Reads onboarding form data from Client Portal        │
  │  - Runs Ahrefs/SimilarWeb (browser)                     │
  │  - Fills MR template + deck                             │
  │  - Stores structured MR data in Notion                  │
  │                                                         │
  │  Step 4 Role: UVP Skill                                  │
  │  - Reads UVP workshop transcript from Notion            │
  │  - Cross-references ICP pain points                     │
  │  - Synthesizes differentiators, UVP, elevator pitch     │
  │  - Fills UVP template (.docx) + deck (.pptx)            │
  │                                                         │
  │  Step 5 Role: Offer Dev Skill                           │
  │  - Reads ICP + UVP from Notion                          │
  │  - Designs Micro/Macro/Core offer ladder                │
  │  - Fills Offer Dev template                             │
  │                                                         │
  │  Steps 6-7: Same pattern                                │
  │  - Each step reads prior outputs from Notion            │
  │  - Fills its respective template                        │
  │  - Stores structured data for next step                 │
  └─────────────────────────────────────────────────────────┘
```

### Key Concept: Each Step's Output Is The Next Step's Input

- Step 1 creates the Client Portal → all subsequent steps read from and write to it
- Step 2 produces ICP data → Step 3 uses it to know what keywords/competitors to research
- Step 3 produces market data → Step 4 uses it to find positioning opportunities
- Step 4 produces UVP → Step 5 uses it to design offers aligned to differentiators
- Step 5 produces offer stack → Step 6 Phase A uses it for Revenue Per Client projections, funnel structure, and what each channel promotes
- Step 6 Phase A produces channel strategy → Terry presents to client → client confirms channels via Fathom call → Step 6 Phase B reads transcript and completes journey map
- Step 6 produces channel strategy + journey map → Step 7 uses it to define KPIs per channel and build the 90-day launch roadmap

**Notion is the hub.** Every step reads from and writes to Notion. This keeps all client data in one place and makes it accessible to whichever skill the agent is running.

### Workshop Flow (ICP Example)

For the ICP step specifically, there are two agent interactions:

1. **Post-ICP Discovery call:** Agent reads the initial transcript, fills Tier 1 in full detail, sketches Tiers 2-3 with what's available
2. **Post-ICP workshop:** Terry conducts a deeper workshop with the client specifically about customer segments. Agent reads that workshop transcript and fleshes out Tiers 2-3 with the additional detail

This same workshop-then-agent pattern may apply to other steps as Terry refines the process.

---

## 4. Framework File Registry

### Existing Files (COMPLETE)

| File | Type | Location | Used In |
|---|---|---|---|
| `ClearLaunch_B2B_ICP_Template.docx` | Word Template | `Frameworks/` | Step 2 |
| `ClearLaunch_B2B_ICP_Summary_Deck.pptx` | PowerPoint Deck | `Frameworks/` | Step 2 |
| `ClearLaunch_B2C_ICP_Template.docx` | Word Template | `Frameworks/` | Step 2 |
| `ClearLaunch_B2C_ICP_Summary_Deck.pptx` | PowerPoint Deck | `Frameworks/` | Step 2 |
| `ClearLaunch_B2B_Market_Research_Template.docx` | Word Template | `Frameworks/` | Step 3 |
| `ClearLaunch_B2B_Market_Research_Summary_Deck.pptx` | PowerPoint Deck | `Frameworks/` | Step 3 |
| `ClearLaunch_B2C_Market_Research_Template.docx` | Word Template | `Frameworks/` | Step 3 |
| `ClearLaunch_B2C_Market_Research_Summary_Deck.pptx` | PowerPoint Deck | `Frameworks/` | Step 3 |

### Recently Built (Steps 4-5)

| File | Type | Location | Used In |
|---|---|---|---|
| `ClearLaunch_UVP_Template.docx` | Word Template | `Frameworks/` | Step 4 |
| `ClearLaunch_UVP_Summary_Deck.pptx` | PowerPoint Deck | `Frameworks/` | Step 4 |
| `ClearLaunch_Offer_Dev_Template.docx` | Word Template | `Frameworks/` | Step 5 |
| `ClearLaunch_Offer_Dev_Summary_Deck.pptx` | PowerPoint Deck | `Frameworks/` | Step 5 |

### Templates To Be Built (GAPS)

| Template Needed | Used In | Depends On |
|---|---|---|
| Customer Journey Template (.docx) | Step 6 | Steps 2-5 output structure |
| Success Metrics & KPI Template (.docx) | Step 7 | Channel strategy from Step 6 |
| Implementation Roadmap Template (.docx) | Step 7 | All prior templates |

### Other Files in the Project

| File | Purpose |
|---|---|
| `ClearLaunch_Skill_Update_Session_Notes.md` | Session notes from March 24, 2026 — current build status, open questions |
| `Frameworks/rebuild_icp_decks.py` | Python script that rebuilds ICP Summary Decks with ClearThink brand styling |
| `SEO Retainer Model.xlsx` | P&L model for the SEO retainer service |
| `ClearThink Model Projections.xlsx` | Business model projections |
| `SEO_Retainer_Preview.html` | HTML preview of the SEO retainer economics |

---

## 5. What's Built vs. What's Next

### Current Build Status

| Component | Status | Notes |
|---|---|---|
| Tally Onboarding Form | COMPLETE | [GTM Strategy Intake Questionnaire](https://tally.so/r/Ekk6dr) — 29 fields, 6 pages. Business Type field needs to be added. |
| GTM Intake Database (Notion) | COMPLETE | `collection://476a46cc-8fab-428c-acb2-f82d61cf1fdd` — Tally submissions land here via native integration |
| Onboarding Skill v1 | COMPLETE | `Skills/ClearLaunch_Onboarding_Skill_v1.md` — validates intake, duplicates Client Template, populates Client Information |
| Onboarding Field Mapping | COMPLETE | `Skills/ClearLaunch_Onboarding_Field_Mapping.md` — maps all Tally fields to Notion + downstream skills |
| ICP Templates (B2B + B2C) | COMPLETE | 4 files built and branded |
| ICP Summary Decks (B2B + B2C) | COMPLETE | Rebuilt March 24, 2026 — 0 layout issues, ClearThink brand applied |
| ICP Agent Skill v2 | COMPLETE | `Skills/ClearLaunch_ICP_Skill_v2.md` — full Notion integration, Fathom→Notion flow, tiering logic |
| Market Research Templates (B2B + B2C) | COMPLETE | 4 files built and branded (15 data tables each) |
| Market Research Agent Skill v2 | COMPLETE | `Skills/ClearLaunch_Market_Research_Skill_v2.md` — 16-step workflow, Ahrefs/SimilarWeb/Meta Ad Library browser workflows |
| UVP Template (.docx) | COMPLETE | `Frameworks/ClearLaunch_UVP_Template.docx` — 7-section framework, industry-agnostic |
| UVP Summary Deck (.pptx) | COMPLETE | `Frameworks/ClearLaunch_UVP_Summary_Deck.pptx` — 9 slides, ClearThink branded |
| UVP Agent Skill v1 | COMPLETE | `Skills/ClearLaunch_UVP_Skill_v1.md` — full Notion integration, transcript pipeline, ICP cross-reference |
| UVP Zapier Pipeline | COMPLETE | Documented inline in `Skills/ClearLaunch_UVP_Skill_v1.md` — ready for Zapier configuration |
| Offer Dev Template (.docx) | COMPLETE | `Frameworks/ClearLaunch_Offer_Dev_Template.docx` — 3-tier ladder, industry-agnostic |
| Offer Dev Summary Deck (.pptx) | COMPLETE | `Frameworks/ClearLaunch_Offer_Dev_Summary_Deck.pptx` — 8 slides, ClearThink branded |
| Offer Dev Agent Skill v1 | COMPLETE | `Skills/ClearLaunch_Offer_Dev_Skill_v1.md` — full Notion integration, transcript pipeline, ICP + UVP cross-reference |
| Offer Dev Zapier Pipeline | COMPLETE | Documented inline in `Skills/ClearLaunch_Offer_Dev_Skill_v1.md` — Zap configured in Zapier |
| Channel Strategy Reference (.md) | COMPLETE | `Frameworks/channel_strategy_template.md` — 9-section variable map, channel matrix, journey map, projection tables |
| Channel Strategy Template (.docx) | COMPLETE | `Frameworks/ClearLaunch_Step6_ChannelStrategy_Template.docx` — 9 sections, 14 tables, placeholder variables |
| Channel Strategy Summary Deck (.pptx) | COMPLETE | `Frameworks/ClearLaunch_Step6_ChannelStrategy_Summary_Deck.pptx` — 8 slides, ClearThink branded |
| Channel Strategy Projections (.xlsx) | COMPLETE | `Frameworks/ClearLaunch_Step6_Projections_Template.xlsx` — 4 tabs, live formulas, cross-sheet refs |
| Channel Strategy Build Scripts | COMPLETE | `build_step6_templates.py`, `build_step6_deck.py`, `build_step6_projections.py` |
| Channel Strategy Agent Skill v1 | COMPLETE | `Skills/ClearLaunch_Step6_ChannelStrategy_Skill_v1.md` — two-phase, Zapier pipeline (Phase B) |
| Metrics/KPI + Roadmap Templates | NOT STARTED | No template exists |

### Build Priority (Recommended Order)

1. **Build Step 7 (Success Metrics & Launch Roadmap)** — design templates (.docx, .pptx), build production skill, configure Zapier pipeline. The final step in the ClearLaunch system.
2. **Configure Channel Strategy Zapier zap** — spec is documented inline in `ClearLaunch_Step6_ChannelStrategy_Skill_v1.md`, needs to be built in Zapier (same 6-step pattern, filter "Channel Strategy")
3. **End-to-end testing** — full flow from Tally form through all 7 steps with a real client

### Open Questions

1. ~~**Onboarding → Client Portal automation:**~~ **RESOLVED (March 26, 2026).** Tally form submits directly to GTM Intake database in Notion (native integration, no Zapier needed). Onboarding Skill v1 reads intake data, duplicates Client Template Page, populates Client Information, and scaffolds Reports section.
2. **Client relation on transcripts is manual:** Fathom doesn't pass client identity, so the Client relation field on the Notion transcript record is set manually by Terry before processing. Future: Zapier lookup step to match client name from Fathom call title.
3. **Competitor Analysis Framework:** Terry explicitly said this hasn't been discussed yet — do NOT start building it until ready.
4. **Tally form needs Business Type field:** The B2B/B2C/Both question is missing from the form. This is the single most critical gap — both ICP and MR skills branch on this value. Must be added before running the onboarding flow with real clients.

---

## 6. Tool Stack & Infrastructure

### Tools and Their Roles

| Tool | Role in ClearLaunch | Monthly Cost |
|---|---|---|
| **Fathom** | Records and transcribes all client calls (onboarding calls, ICP Discovery calls, and workshops) | $14 |
| **Zapier** | Automates Fathom → Notion transcript pipeline + GTM Intake → Slack notifications | $49 |
| **Notion** | Central data hub — stores transcripts, agent outputs, client records, deliverable files | $20 |
| **Ahrefs** | SEO/keyword research, backlink analysis, competitor keyword gaps, content gap analysis | $99 |
| **SimilarWeb** | Traffic estimates, audience demographics, cross-visitation, industry benchmarking | (check plan) |
| **Google Workspace** | Client-facing deliverable sharing, email, docs | $72 |
| **Figma** | Visual deliverables, deck design | $75 |
| **Surfer SEO** | Content optimization (used in SEO retainer, not ClearLaunch) | $129 |
| **ClearScope** | Content grading (used in SEO retainer, not ClearLaunch) | $129 |

### Infrastructure Architecture

```
[Tally Form]                              [Client Calls]
      │                                     │ (Onboarding + ICP Discovery + Workshops)
      ▼                                     ▼
[Tally Native Integration]           [Fathom] ──record + transcribe──▶ [Zapier] ──▶ [Notion Transcripts DB]
      │                                                                                      │
      ▼                                                                                      │
[Notion GTM Intake DB]                                                                       │
      │         │                                                                            │
      │         ▼                                                                            │
      │   [Zapier → Slack]                                                                   │
      │                                                                                      │
      ▼                                                                                      ▼
  ┌──────────────────────────────────────────────────────────────────────┐
  │  [Claude Code Agent]                                                │
  │  • Step 1: Reads GTM Intake → creates Client Portal                │
  │  • Step 2: Reads ICP Discovery transcript → fills ICP templates    │
  │  • Steps 3-7: Each reads prior outputs from Notion                 │
  │                    │              │                                 │
  │         ┌──────────┘              └──────────┐                     │
  │         ▼                                     ▼                    │
  │  [Browser Tools]                       [File Generation]           │
  │  • Ahrefs                              • .docx templates           │
  │  • SimilarWeb                          • .pptx decks               │
  │  • Client website                      • Notion records            │
  └──────────────────────────────────────────────────────────────────────┘
```

**Notion is the central hub.** All client data lives there. The agent reads inputs from Notion and writes outputs back to Notion. Deliverable files (.docx, .pptx) are generated and can be shared with clients via Google Workspace or directly.

---

## 7. ClearThink Brand Reference

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

## 8. Business Model Context

The ClearLaunch System is the **entry point** to the ClearThink client relationship:

- **ClearLaunch** ($1,000 one-time) → Productized GTM strategy sprint. The client gets a complete strategy.
- **SEO Retainer** ($2,500/month ongoing) → The upsell. ClearThink executes the strategy that ClearLaunch defined.

The ClearLaunch → Retainer conversion funnel is critical. ClearLaunch must produce a strategy compelling enough that clients want ClearThink to execute it.

**Why agent automation matters for unit economics:** At $1,000 per engagement, ClearLaunch needs to be delivered efficiently. If agents handle the research-heavy portions (transcript analysis, keyword research, template population), delivery time drops significantly, making the price point viable while maintaining quality.

**SEO Retainer economics (reference):** Per the current P&L model, the retainer service needs 8+ clients at $2,500/month to break even. At 3 clients, it operates at a -49.5% net margin. At 10 clients, net margin improves to ~9%. At 15 clients, ~17%.

---

*Last updated: April 4, 2026 (v3.2 — Step 5 Offer Development shipped: production skill v1, 8-slide summary deck, Zapier pipeline live. Fixed legacy step labels on UVP + Offer Dev templates. Updated build status and priorities.)*

*Previously: March 31, 2026 (v3.1 — split Step 4 into UVP Development + Offer Development, added full Step 4 UVP build details, updated file registry and build statuses, updated data flow diagram)*
