# ClearLaunch GTM Strategy Blueprint

**ClearThink Marketing | Version 2.0 | March 2026**

---

## Purpose

This document is the single-source-of-truth for the ClearLaunch System — ClearThink Marketing's productized go-to-market strategy sprint. It captures:

- The full 6-step process and what each step produces
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

### The 6 Steps & Their Deliverables

| Step | Focus | Deliverables Produced |
|---|---|---|
| 1 | Ideal Customer Profile | ICP Analysis document (.docx) + ICP Summary Deck (.pptx) — 1-3 prioritized customer segments, pain point mapping, decision-making criteria, qualifying/disqualifying criteria |
| 2 | Market Landscape Analysis | Market Research document (.docx) + Market Research Summary Deck (.pptx) — keyword research (up to 50 keywords), competitive analysis, audience intelligence, content gap analysis |
| 3 | Value Proposition & Offer Engineering | Value Proposition document (.docx) + Offer Engineering document (.docx) — strategic positioning, core messaging, MICRO offer (lead magnets), MACRO offer (core revenue offer) |
| 4 | Channel Strategy & Customer Journey | Customer Journey document (.docx) — journey mapping (awareness to advocacy), channel strategy matrix, budget allocation recommendations |
| 5 | Success Metrics & KPIs | KPI Framework document (.docx) — 5-10 priority metrics, measurement cadence, baseline benchmarks, reporting structure |
| 6 | Implementation Roadmap | Launch Roadmap document (.docx) — 90-day tactical plan with weekly milestones, budget allocation, prioritized actions, clear ownership |

### The 4-Phase Timeline

| Phase | Weeks | Steps | Focus |
|---|---|---|---|
| Phase 1: Discovery & Research | 1-2 | Steps 1-2 | ICP discovery sessions, market research, keyword analysis, competitive landscape |
| Phase 2: Strategy Development | 3-4 | Steps 3-4 | Value proposition, messaging framework, offer engineering, customer journey mapping, channel identification |
| Phase 3: Framework & Roadmap Creation | 5-6 | Steps 5-6 | Success metrics, KPI framework, budget optimization, 90-day implementation roadmap |
| Phase 4: Strategy Delivery & Launch Prep | 7-8 | Delivery | Complete strategy delivery, priority recommendations, tracking activation, first campaign launch support |

---

## 2. The 6-Step Process

This process synthesizes ClearThink's own methodology with GTM best practices. Each step builds on the output of the previous one.

---

### Step 1: Define Ideal Client Profile

**Status: BUILT** (templates complete, agent skill complete)

**This is Skill 2** in the ClearLaunch system. Skill 1 (Onboarding) creates the client portal and populates Client Information from the onboarding form. This ICP skill comes after — it processes the deeper discovery call transcript.

**What it accomplishes:** Creates a detailed picture of who the client should be targeting — firmographics (B2B) or demographics (B2C), behaviors, pain points, buying triggers, and decision-making criteria. Segments prospects into Tier 1 (primary focus), Tier 2 (secondary), and Tier 3 (nurture/monitor).

**How it works in practice:**
1. Terry conducts a discovery call with the client (recorded via Fathom)
2. The call transcript lands in Notion automatically (Fathom → Zapier → Notion Transcripts DB with Status: "Not started")
3. Zapier sends a notification (Slack/email) alerting Terry that a transcript is ready
4. Terry opens Claude Code and says "process new transcripts"
5. The agent queries Notion for "Not started" ICP/Discovery transcripts, sets status to "In progress"
6. Agent reads the transcript from the page body, determines B2B or B2C, and extracts ICP data
7. Tier 1 gets fully fleshed out from the discovery call data
8. Both the .docx template and .pptx summary deck are populated
9. Deliverables are stored in the client's portal (Reports → ICP Analysis section)
10. Notion transcript record updated to "Done" with deliverable filenames and processing notes
11. During a subsequent ICP workshop, Tiers 2 and 3 get fleshed out from the workshop transcript

**What the agent needs as input:**
- A "Not started" transcript in the Notion Transcripts database (Meeting Type: ICP or Discovery)
- The Client relation must be set on the transcript so the agent can find the client's portal

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

### Step 2: Analyze Market Landscape

**Status: PARTIALLY BUILT** (templates complete, agent skill v2 in progress)

**What it accomplishes:** Researches the client's target market size, growth trajectory, competitive landscape, keyword opportunities, and content gaps. Validates that there's real demand for what the client offers and identifies where they have the best chance of winning.

**How it works in practice:**
1. Agent reads the ICP output from Step 1 (stored in Notion) — specifically the industry, target segments, competitor names, and pain points
2. Agent also takes data from the client onboarding form (keywords, competitor URLs, client's own website)
3. Agent runs Ahrefs browser workflows for SEO/keyword/backlink data
4. Agent runs SimilarWeb browser workflows for traffic/audience/market data
5. Agent synthesizes findings into the Market Research template + summary deck

**What the agent needs as input:**
- ICP data from Step 1 (from Notion)
- Client's website URL
- Competitor URLs (from discovery call or onboarding form)
- Seed keywords (derived from ICP pain points and industry terms)

**What it produces:**
- Populated Market Research Template (.docx) with: keyword landscape, competitive analysis, audience intelligence, market sizing
- Populated Market Research Summary Deck (.pptx)
- Structured market research data stored in Notion (becomes input for Step 3)

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

### Step 3: Craft Value Proposition & Messaging

**Status: NOT STARTED** (no template, no skill)

**What it accomplishes:** Takes the ICP pain points (from Step 1) and the competitive gaps (from Step 2) and synthesizes them into a unique value proposition and messaging framework. Also designs the client's offer structure — both MICRO offers (low-commitment entry points like lead magnets, free audits, downloadable guides) and MACRO offers (the core paid service/product that generates revenue).

**How it should work:**
1. Agent reads ICP data + Market Research data from Notion
2. Cross-references: what does the target audience need (pain points) that competitors aren't adequately serving (gaps)?
3. Generates UVP candidates — positioning statements that answer "Why us, why now?"
4. Designs MICRO offer: the entry point that proves value and captures leads
5. Designs MACRO offer: the core engagement that generates revenue
6. Builds messaging framework: headlines, proof points, objection handlers, CTAs

**What the agent needs as input:**
- ICP data (Tier 1 pain points, buying triggers, decision-making criteria)
- Market research data (competitive weaknesses, content gaps, keyword opportunities)

**What it should produce:**
- Value Proposition Template (.docx) — TO BE BUILT
- Offer Engineering Template (.docx) — TO BE BUILT
- Messaging framework with headlines, proof points, objection handlers
- Structured value proposition data stored in Notion (becomes input for Steps 4-6)

**Key principle:** The value proposition must translate what the client does into the outcomes their customers care about — not just features or capabilities, but results. This is especially important for technical businesses that tend to describe services in jargon rather than benefits.

---

### Step 4: Design Channel Strategy & Customer Journey

**Status: NOT STARTED** (no template, no skill)

**What it accomplishes:** Maps the complete customer journey from first awareness through decision and advocacy. Identifies which marketing channels serve which journey stages. Creates a channel strategy matrix that tells the client exactly where to invest their time and budget.

**How it should work:**
1. Agent reads all prior step outputs from Notion
2. Maps journey stages: Awareness → Consideration → Decision → Onboarding → Retention → Advocacy
3. For each stage, identifies: what the customer needs, what content/touchpoints should exist, which channels deliver them
4. Applies a channel fit matrix — evaluating each potential channel by audience fit, cost efficiency, scalability, and measurability
5. Recommends a focused starting set of channels (2-3 primary) with expansion path

**What the agent needs as input:**
- ICP data (where the audience spends time, how they research, preferred content formats)
- Market research data (which channels competitors use, traffic sources)
- Value proposition data (what message to deliver through each channel)

**What it should produce:**
- Customer Journey Template (.docx) — TO BE BUILT
- Channel strategy matrix with budget allocation recommendations
- Journey data stored in Notion (becomes input for Steps 5-6)

**Channel strategy principle:** Start focused. Pick 1-2 primary channels that match the audience and the client's capacity. Prove ROI there before expanding. The most common GTM failure is channel sprawl — trying to be everywhere at once and being effective nowhere.

---

### Step 5: Define Success Metrics & KPI Framework

**Status: NOT STARTED** (no template, no skill)

**What it accomplishes:** Defines what success looks like for the client's GTM strategy before the launch roadmap is built. Establishes KPIs per channel, measurement cadence, and baseline metrics so the 90-day plan in Step 6 is built around measurable outcomes, not just activities.

**How it should work:**
1. Agent reads all prior outputs — especially the channel strategy from Step 4
2. For each channel selected, defines: primary KPI, secondary metrics, measurement frequency, target benchmarks
3. Establishes baseline metrics (where the client is now) vs. target metrics (where they should be in 90 days)
4. Defines the reporting cadence — what gets measured weekly, monthly, quarterly
5. Identifies what tools/tracking need to be in place before launch

**What the agent needs as input:**
- Channel strategy (from Step 4)
- Current client metrics (if available — website traffic, lead volume, conversion rates)
- Budget constraints

**What it should produce:**
- Success Metrics & KPI Template (.docx) — TO BE BUILT
- KPI dashboard structure with 5-10 priority metrics
- Metrics data stored in Notion (becomes input for Step 6)

**Note:** Sales/marketing alignment and CRM capabilities may factor into this step for clients who have sales teams. For now, this is not a formal sub-step, but it's worth noting that some clients will need funnel stage definitions (MQL, SQL, etc.) and lead handoff criteria documented here.

---

### Step 6: Deliver Launch Roadmap

**Status: NOT STARTED** (no template, no skill)

**What it accomplishes:** Packages everything from Steps 1-5 into a 90-day tactical execution plan with specific tasks, timelines, budget allocations, and clear ownership. This is the final deliverable — the client's roadmap for taking action.

**How it should work:**
1. Agent reads all prior outputs from Notion
2. Translates strategy into weekly/monthly action items for the first 90 days
3. Assigns priorities: what delivers fastest results vs. what builds long-term foundation
4. Allocates budget across channels based on the metrics framework from Step 5
5. Creates the roadmap document + final presentation

**What the agent needs as input:**
- All outputs from Steps 1-5
- Client's available budget
- Client's internal capacity (team size, who does what)

**What it should produce:**
- Implementation Roadmap Template (.docx) — TO BE BUILT
- 90-day plan with weekly milestones
- Budget allocation matrix
- Prioritized action items with ownership

**Key principle:** The roadmap should be actionable regardless of who executes it. Whether the client implements it themselves, hires ClearThink for the SEO retainer, or brings in another partner — the strategy stands on its own.

---

## 3. How The Agent Automation Works

The ClearLaunch System uses a single Claude Code agent that plays different roles depending on which step/deliverable is active. It's not 5 separate agents — it's one agent with different skills (context + instructions) for each phase.

### Data Flow

```
DISCOVERY CALL (Terry + Client)
        |
        v
  [Fathom Recording]
        |
        v
  [Zapier Webhook] ──── triggers when call ends
        |
        v
  [Notion: Client Database] ──── transcript stored as a page/record
        |
        v
  ┌─────────────────────────────────────────────┐
  │  AGENT (Claude Code)                        │
  │                                             │
  │  Step 1 Role: ICP Skill                     │
  │  - Reads transcript from Notion             │
  │  - Fills ICP template + deck                │
  │  - Stores structured ICP data in Notion     │
  │                                             │
  │  Step 2 Role: Market Research Skill         │
  │  - Reads ICP data from Notion               │
  │  - Reads onboarding form data               │
  │  - Runs Ahrefs/SimilarWeb (browser)         │
  │  - Fills MR template + deck                 │
  │  - Stores structured MR data in Notion      │
  │                                             │
  │  Step 3 Role: Value Prop Skill              │
  │  - Reads ICP + MR data from Notion          │
  │  - Generates UVP, offers, messaging         │
  │  - Fills VP template                        │
  │  - Stores VP data in Notion                 │
  │                                             │
  │  Steps 4-6: Same pattern                    │
  │  - Each step reads prior outputs from Notion│
  │  - Fills its respective template            │
  │  - Stores structured data for next step     │
  └─────────────────────────────────────────────┘
```

### Key Concept: Each Step's Output Is The Next Step's Input

- Step 1 produces ICP data → Step 2 uses it to know what keywords/competitors to research
- Step 2 produces market data → Step 3 uses it to find positioning opportunities
- Step 3 produces value prop → Step 4 uses it to determine channel messaging
- Step 4 produces channel strategy → Step 5 uses it to define per-channel KPIs
- Step 5 produces metrics framework → Step 6 uses it to build the measured roadmap

**Notion is the hub.** Every step reads from and writes to Notion. This keeps all client data in one place and makes it accessible to whichever skill the agent is running.

### Workshop Flow (ICP Example)

For the ICP step specifically, there are two agent interactions:

1. **Post-discovery call:** Agent reads the initial transcript, fills Tier 1 in full detail, sketches Tiers 2-3 with what's available
2. **Post-ICP workshop:** Terry conducts a deeper workshop with the client specifically about customer segments. Agent reads that workshop transcript and fleshes out Tiers 2-3 with the additional detail

This same workshop-then-agent pattern may apply to other steps as Terry refines the process.

---

## 4. Framework File Registry

### Existing Files (COMPLETE)

| File | Type | Location | Used In |
|---|---|---|---|
| `ClearLaunch_B2B_ICP_Template.docx` | Word Template | `Frameworks/` | Step 1 |
| `ClearLaunch_B2B_ICP_Summary_Deck.pptx` | PowerPoint Deck | `Frameworks/` | Step 1 |
| `ClearLaunch_B2C_ICP_Template.docx` | Word Template | `Frameworks/` | Step 1 |
| `ClearLaunch_B2C_ICP_Summary_Deck.pptx` | PowerPoint Deck | `Frameworks/` | Step 1 |
| `ClearLaunch_B2B_Market_Research_Template.docx` | Word Template | `Frameworks/` | Step 2 |
| `ClearLaunch_B2B_Market_Research_Summary_Deck.pptx` | PowerPoint Deck | `Frameworks/` | Step 2 |
| `ClearLaunch_B2C_Market_Research_Template.docx` | Word Template | `Frameworks/` | Step 2 |
| `ClearLaunch_B2C_Market_Research_Summary_Deck.pptx` | PowerPoint Deck | `Frameworks/` | Step 2 |

### Templates To Be Built (GAPS)

| Template Needed | Used In | Depends On |
|---|---|---|
| Value Proposition Template (.docx) | Step 3 | ICP + MR templates finalized |
| Offer Engineering Template (.docx) | Step 3 | Value Proposition template |
| Customer Journey Template (.docx) | Step 4 | Steps 1-3 output structure |
| Success Metrics & KPI Template (.docx) | Step 5 | Channel strategy from Step 4 |
| Implementation Roadmap Template (.docx) | Step 6 | All prior templates |

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
| ICP Templates (B2B + B2C) | COMPLETE | 4 files built and branded |
| ICP Summary Decks (B2B + B2C) | COMPLETE | Rebuilt March 24, 2026 — 0 layout issues, ClearThink brand applied |
| ICP Agent Skill v2 | COMPLETE | `Skills/ClearLaunch_ICP_Skill_v2.md` — full Notion integration, Fathom→Notion flow, tiering logic |
| Market Research Templates (B2B + B2C) | COMPLETE | 4 files built and branded (15 data tables each) |
| Market Research Agent Skill | IN PROGRESS | Old skill in Claude Desktop is outdated — v2 being built to match current templates |
| Value Proposition Template | NOT STARTED | No template exists |
| Offer Engineering Template | NOT STARTED | No template exists |
| Customer Journey Template | NOT STARTED | No template exists |
| Metrics/KPI Template | NOT STARTED | No template exists |
| Implementation Roadmap Template | NOT STARTED | No template exists |

### Build Priority (Recommended Order)

1. **Build Market Research Skill v2** — map to the 15 template tables, add Ahrefs/SimilarWeb/Meta Ad Library browser workflows, Notion data flow
2. **Build Value Proposition Template** — design the .docx structure for Step 3
3. **Build Offer Engineering Template** — design the .docx structure for Step 3
4. **Build Value Prop + Offer Skill** — automate Step 3 using ICP + MR output
5. **Build Customer Journey Template** — design the .docx structure for Step 4
6. **Build Channel Strategy + Journey Skill** — automate Step 4
7. **Build Metrics/KPI Template** — design .docx structure for Step 5
8. **Build Implementation Roadmap Template** — design .docx structure for Step 6
9. **Build final skills for Steps 5-6** — complete the automation chain

### Open Questions

1. **Onboarding → Client Portal automation:** Tally form → Zapier → Notion Client Portal creation. Exists conceptually but needs to be confirmed/built.
2. **Client relation on transcripts is manual:** Fathom doesn't pass client identity, so the Client relation field on the Notion transcript record is set manually by Terry before processing. Future: Zapier lookup step to match client name from Fathom call title.
3. **Competitor Analysis Framework:** Terry explicitly said this hasn't been discussed yet — do NOT start building it until ready.

---

## 6. Tool Stack & Infrastructure

### Tools and Their Roles

| Tool | Role in ClearLaunch | Monthly Cost |
|---|---|---|
| **Fathom** | Records and transcribes discovery calls and workshops | $14 |
| **Zapier** | Automates Fathom → Notion transcript pipeline (scheduled or webhook trigger) | $49 |
| **Notion** | Central data hub — stores transcripts, agent outputs, client records, deliverable files | $20 |
| **Ahrefs** | SEO/keyword research, backlink analysis, competitor keyword gaps, content gap analysis | $99 |
| **SimilarWeb** | Traffic estimates, audience demographics, cross-visitation, industry benchmarking | (check plan) |
| **Google Workspace** | Client-facing deliverable sharing, email, docs | $72 |
| **Figma** | Visual deliverables, deck design | $75 |
| **Surfer SEO** | Content optimization (used in SEO retainer, not ClearLaunch) | $129 |
| **ClearScope** | Content grading (used in SEO retainer, not ClearLaunch) | $129 |

### Infrastructure Architecture

```
[Client Calls]
      │
      ▼
[Fathom] ──record + transcribe──▶ [Zapier] ──webhook──▶ [Notion Client DB]
                                                              │
                                                              │ Agent reads from / writes to
                                                              ▼
                                                    [Claude Code Agent]
                                                         │    │
                                           ┌─────────────┘    └──────────────┐
                                           ▼                                  ▼
                                    [Browser Tools]                   [File Generation]
                                    • Ahrefs                          • .docx templates
                                    • SimilarWeb                      • .pptx decks
                                    • Client website                  • Notion records
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

*Last updated: March 24, 2026 (v2.0 — aligned deliverables with 6-step process, updated all build statuses, cleared stale references)*
