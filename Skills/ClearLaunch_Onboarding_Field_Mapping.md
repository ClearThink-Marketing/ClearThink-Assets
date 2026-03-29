# ClearLaunch Onboarding Field Mapping

**Version:** 1.0 | March 2026
**Purpose:** Maps every Tally onboarding form field to its Notion destination and downstream skill consumers. Use this as the reference for Tally → Notion integration setup and Zapier/automation configuration.

**Tally Form:** [GTM Strategy Intake Questionnaire](https://tally.so/r/Ekk6dr)
**Notion Database:** GTM Intake (`collection://476a46cc-8fab-428c-acb2-f82d61cf1fdd`) inside Database Hub - ClearThink

---

## Field Mapping

### Page 1: Contact Information

| # | Tally Field | Notion Property | Type | Required | Consumed By | Notes |
|---|---|---|---|---|---|---|
| 1 | First Name | First Name | Text | Yes | Portal identification | Combined with Last Name for contact display |
| 2 | Last Name | Last Name | Text | Yes | Portal identification | Combined with First Name for contact display |
| 3 | Phone Number | Phone | Phone | Yes | Ops/communication only | Not consumed by any skill directly |
| 4 | E-mail Address | Email | Email | Yes | Ops/communication only | Not consumed by any skill directly |
| 5 | Company Name | Company Name | Title | **CHANGE TO REQUIRED** | ALL skills | Portal page title. Appears in every deliverable filename (`[ClientName]_ICP_B2B.docx`). Currently optional in Tally — must be required. |

### Page 2: Business Information

| # | Tally Field | Notion Property | Type | Required | Consumed By | Notes |
|---|---|---|---|---|---|---|
| 6 | Company Website URL | Website URL | URL | Yes | ICP Skill (industry context), MR Skill (Ahrefs Site Explorer Steps 5-8, SimilarWeb Steps 9-11) | **Critical input.** MR Skill states: "Do not proceed without at least: client URL." |
| — | **NEW: Business Type** | Business Type | Select | **ADD TO FORM** | ICP Skill (Step 4: template selection), MR Skill (Step 15: template selection) | **CRITICAL MISSING FIELD.** Both skills branch on B2B vs B2C to select template sets. Options: "B2B (I sell to businesses)", "B2C (I sell to consumers)", "Both". |
| 7 | Core mission and values | Mission & Values | Text | Yes | Value Prop Skill (Step 4, future) | Useful context for positioning |
| 8 | Company story | Company Story | Text | Yes | Value Prop Skill (Step 4, future) | Brand narrative context |
| 9 | Products/services offered | Products & Services | Text | Yes | ICP Skill (industry adaptation, meta-framework), MR Skill (keyword derivation from pain points) | Important for both skills |
| 10 | What makes business unique | Unique Differentiators | Text | Yes | Value Prop Skill (Step 4, future) | Core positioning input |
| 11 | Plans to scale | Growth Plans | Text | Yes | Implementation Roadmap Skill (Step 7, future) | Growth context for roadmap |

### Page 3: Target Audience

| # | Tally Field | Notion Property | Type | Required | Consumed By | Notes |
|---|---|---|---|---|---|---|
| 12 | Who is your ideal customer | Ideal Customer | Text | Yes | ICP Skill (initial context before ICP Discovery call), MR Skill (validates keyword intent classification) | Important context field |
| 13 | Age Range | Age Range | Text | Yes | ICP Skill (B2C demographics section) | Maps directly to B2C ICP Template Section 2 |
| 14 | Geographic Location | Geographic Location | Text | Yes | ICP Skill (Geography section, B2B + B2C), MR Skill (Ahrefs country filter Step 3, SimilarWeb geography Step 10) | Important for both skills |
| 15 | Industry/Profession | Industry | Text | Yes | ICP Skill (Section 1 Overview, B2B firmographics), MR Skill (SimilarWeb Industry Analysis, keyword framing Step 2) | Important for both skills |
| 16 | Other relevant demographics | Other Demographics | Text | Yes | ICP Skill (additional extraction context) | Nice-to-have context |
| 17 | Challenges target audience faces | Challenges Solved | Text | Yes | ICP Skill (Pain Points section, meta-framework), MR Skill (ICP-derived keyword generation Step 2) | Important for both skills — "how to [solve pain point]" keyword patterns |
| 18 | Keywords ideal customer would type | Seed Keywords | Text | **Optional (strengthen)** | MR Skill (PRIMARY input for Step 2 Keyword Discovery and Step 3 Ahrefs Keywords Explorer) | **Strongly recommended to make required.** MR Skill states: "Do not proceed without at least: 5 seed keywords." The fallback (deriving from ICP) is a degraded path. Add helper text: "List 5-10 words or phrases your ideal customer would type into Google. Example: 'commercial roofing contractor Dallas'" |

### Page 4: Competitive Landscape

| # | Tally Field | Notion Property | Type | Required | Consumed By | Notes |
|---|---|---|---|---|---|---|
| 19 | 3-5 competitor websites | Competitor URLs | Text | Optional | MR Skill (Steps 5-12 — every competitive analysis table uses these URLs in Ahrefs Site Explorer and SimilarWeb) | **Recommend improving.** Add helper text: "Enter full website URLs (e.g., https://competitor.com). We use these to analyze their SEO, traffic, and ad strategy." Consider splitting into 3 separate URL fields for cleaner Zapier mapping. |
| 20 | What you like about competitors | Competitor Likes | Text | Optional | Value Prop Skill (Step 4, future), MR Skill (contextual insight) | Competitive context |
| 21 | What to avoid from competitors | Competitor Dislikes | Text | Optional | Value Prop Skill (Step 3, future — positioning against weaknesses) | Competitive context |

### Page 5: Current Marketing & Sales

| # | Tally Field | Notion Property | Type | Required | Consumed By | Notes |
|---|---|---|---|---|---|---|
| 22 | Marketing channels currently using | Marketing Channels | Multi-select | Yes | Channel Strategy Skill (Step 5, future), MR Skill (validates SimilarWeb traffic source data) | No change needed |
| 23 | What's working well | Whats Working | Text | Optional | Channel Strategy Skill (Step 5, future) | No change needed |
| 24 | What's not working / underperformed | Whats Not Working | Text | Optional | Channel Strategy Skill (Step 5, future) | No change needed |
| 25 | Current sales process | Sales Process | Text | Yes | Customer Journey Skill (Step 5, future), KPI Skill (Step 6 — funnel stage definitions) | No change needed |
| 26 | Main conversion points | Conversion Points | Text | Yes | KPI Skill (Step 6, future — what to measure) | No change needed |

### Page 6: Team & Operations

| # | Tally Field | Notion Property | Type | Required | Consumed By | Notes |
|---|---|---|---|---|---|---|
| 27 | Team structure | Team Structure | Text | Yes | Implementation Roadmap Skill (Step 7, future — capacity constraints, "who does what") | No change needed |
| 28 | Current tech stack | Tech Stack | Text | Yes | Implementation Roadmap Skill (Step 7 — tool recommendations), KPI Skill (Step 6 — what can be measured) | No change needed |
| 29 | Content or marketing assets you have | Existing Assets | Text | Yes | MR Skill (context for content gap analysis Step 7), Channel Strategy Skill (Step 5 — existing content inventory) | No change needed |

### Tracking Properties (Not from Tally)

| Property | Type | Purpose |
|---|---|---|
| Status | Select: `New`, `Reviewed`, `Portal Created` | Tracks intake processing. "New" = just submitted. "Reviewed" = Terry has reviewed. "Portal Created" = Onboarding Skill has created the Client Portal entry. |
| Submitted | Date | Auto-set by Tally integration on form submission. |

---

## Gaps: Missing Fields

### CRITICAL — Must Add Before Running Skills

| Field | Type | Why It's Critical | Recommendation |
|---|---|---|---|
| **Business Type** (B2B / B2C / Both) | Select | ICP Skill Step 4 branches entirely on this value to select B2B vs B2C templates. MR Skill Step 15 uses it for template selection. Without it, the agent must infer from context (unreliable) or ask Terry (adds manual step). | Add as Radio/Dropdown on Tally Page 2, right after Company Name. Options: "B2B (I sell to businesses)", "B2C (I sell to consumers)", "Both B2B and B2C". |

### STRONGLY RECOMMENDED — Improves Skill Quality

| Field | Type | Why It Matters | Recommendation |
|---|---|---|---|
| Company Name required | — | Currently optional. It's the Notion page title and every deliverable filename. | Change from optional to required in Tally. |
| Seed Keywords required | — | MR Skill's primary input for keyword research. Fallback (deriving from ICP) produces lower-quality results. | Make required, or add strong helper text with examples. |
| Competitor URLs structured | — | Free-text area makes it hard for the agent and Zapier to parse. MR Skill processes up to 3 competitors individually. | Split into 3 separate URL fields in Tally, or add helper text specifying "full URLs, one per line." |

### NICE TO HAVE — Feeds Future Skills

| Field | Type | Feeds | Recommendation |
|---|---|---|---|
| Monthly Marketing Budget | Select/Dropdown | Channel Strategy (Step 5), Implementation Roadmap (Step 7) | Options: "Under $1K/mo", "$1K-$3K/mo", "$3K-$5K/mo", "$5K-$10K/mo", "$10K+/mo", "Not sure yet" |
| Revenue Model | Select/Dropdown | Offer Engineering (Step 4) | Options: "Subscription/recurring", "One-time purchase", "Retainer/ongoing service", "Project-based", "Mixed/other" |

---

## Notion Database Reference

| Database | ID | Purpose |
|---|---|---|
| **GTM Intake** | `collection://476a46cc-8fab-428c-acb2-f82d61cf1fdd` | Tally form submissions land here |
| **Client Portals** | `collection://30e821ad-7ba9-8080-8f38-000ba9c44ad0` | Onboarding Skill creates portal entries here from intake data |
| **Transcripts** | `collection://0f372290-8993-4c7e-b303-13afca181721` | Fathom call transcripts (ICP Skill reads from here) |

---

## Data Flow Summary

```
Tally Form → Notion GTM Intake DB (automatic via Tally integration)
                    ↓
        Onboarding Skill reads intake
                    ↓
        Creates Client Portal entry (Client Portals DB)
        - Copies critical fields (URL, B2B/B2C, competitors, keywords, industry)
        - Creates Reports section structure
        - Sets portal status to "Ready"
                    ↓
        ICP Skill reads from Client Portal + Transcripts DB
                    ↓
        MR Skill reads from Client Portal + ICP output
                    ↓
        Steps 4-7 continue the chain
```
