# ClearLaunch System Diagrams

Visual diagrams of the ClearLaunch GTM System architecture and data flow. These render automatically on GitHub.

---

## System Architecture

How data flows from client engagement through the agent to deliverables:

```mermaid
flowchart TB
    subgraph CLIENT["Client Engagement"]
        ONBOARD["Tally Onboarding Form"]
        CALL["ICP Discovery Call"]
    end
    subgraph CAPTURE["Data Capture"]
        FATHOM["Fathom"]
        TALLY_INT["Tally Native Integration"]
        ZAP2["Zapier: Transcript to Notion"]
        ZAP3["Zapier: Intake to Slack"]
    end
    subgraph NOTIFY["Notifications"]
        SLACK["Slack\n#internal-notifications"]
    end
    subgraph NOTION["Notion: Central Hub"]
        INTAKE_DB["GTM Intake DB"]
        PORTAL["Client Portal"]
        TRANSCRIPTS["Transcripts DB"]
    end
    subgraph AGENT["Claude Code Agent"]
        S1["Step 1: Onboarding Skill"]
        S2["Step 2: ICP Skill"]
        S3["Step 3: Market Research Skill"]
        S4["Step 4: Value Prop + Offer Skill"]
        S5["Step 5: Channel + Journey Skill"]
        S6["Step 6: Metrics + KPI Skill"]
        S7["Step 7: Roadmap Skill"]
    end
    subgraph TOOLS["External Tools"]
        AHREFS["Ahrefs"]
        SIMILAR["SimilarWeb"]
        META["Meta Ad Library"]
    end
    subgraph OUTPUT["Deliverables"]
        DOCX[".docx Templates"]
        PPTX[".pptx Summary Decks"]
    end
    ONBOARD --> TALLY_INT --> INTAKE_DB
    INTAKE_DB --> ZAP3 --> SLACK
    INTAKE_DB --> S1
    S1 -->|"creates"| PORTAL
    CALL --> FATHOM --> ZAP2 --> TRANSCRIPTS
    ZAP2 --> SLACK
    TRANSCRIPTS --> S2
    PORTAL --> S2
    PORTAL --> S3
    S2 -->|ICP data| PORTAL
    S3 -->|Market data| PORTAL
    S4 -->|UVP + Offers| PORTAL
    S5 -->|Channel strategy| PORTAL
    S6 -->|KPI framework| PORTAL
    S7 -->|90-day roadmap| PORTAL
    S3 --> AHREFS
    S3 --> SIMILAR
    S3 --> META
    S2 --> DOCX & PPTX
    S3 --> DOCX & PPTX
    S4 --> DOCX
    S5 --> DOCX
    S6 --> DOCX
    S7 --> DOCX
    style CLIENT fill:#E5F5EC,stroke:#1B9B5E,color:#121718
    style CAPTURE fill:#F0F9F4,stroke:#A8D9BD,color:#121718
    style NOTIFY fill:#F0F9F4,stroke:#A8D9BD,color:#121718
    style NOTION fill:#F6F3EF,stroke:#1B9B5E,color:#121718
    style AGENT fill:#1B9B5E,stroke:#121718,color:#fff
    style TOOLS fill:#F6F3EF,stroke:#A8D9BD,color:#121718
    style OUTPUT fill:#3BEB96,stroke:#1B9B5E,color:#121718
```

---

## Step-by-Step Data Flow

Each step's output becomes the next step's input. Notion is the hub that connects them all:

```mermaid
flowchart LR
    S1["Step 1\nOnboarding"]
    S2["Step 2\nICP"]
    S3["Step 3\nMarket Research"]
    S4["Step 4\nValue Prop + Offers"]
    S5["Step 5\nChannel + Journey"]
    S6["Step 6\nMetrics + KPIs"]
    S7["Step 7\nLaunch Roadmap"]
    S1 -->|"Client Portal\ncreated"| S2
    S2 -->|"pain points, competitors,\nsegments, industry"| S3
    S3 -->|"keywords, gaps,\naudience data"| S4
    S4 -->|"positioning, messaging,\noffer structure"| S5
    S5 -->|"channels, journey,\nbudget allocation"| S6
    S6 -->|"KPIs, baselines,\nmeasurement cadence"| S7
    T0["Tally Form\n+ Notion GTM Intake"]
    T1["Fathom + Notion"]
    T2["Ahrefs + SimilarWeb\n+ Meta Ad Library"]
    T0 -.->|form data| S1
    T1 -.->|ICP Discovery\ntranscript| S2
    T2 -.->|browser data| S3
    style S1 fill:#1B9B5E,stroke:#121718,color:#fff
    style S2 fill:#1B9B5E,stroke:#121718,color:#fff
    style S3 fill:#1B9B5E,stroke:#121718,color:#fff
    style S4 fill:#A8D9BD,stroke:#121718,color:#121718
    style S5 fill:#A8D9BD,stroke:#121718,color:#121718
    style S6 fill:#A8D9BD,stroke:#121718,color:#121718
    style S7 fill:#A8D9BD,stroke:#121718,color:#121718
    style T0 fill:#F0F9F4,stroke:#A8D9BD,color:#121718
    style T1 fill:#F0F9F4,stroke:#A8D9BD,color:#121718
    style T2 fill:#F0F9F4,stroke:#A8D9BD,color:#121718
```

**Legend:**
- **Dark green nodes** = built (Steps 1-3)
- **Light green nodes** = not yet built (Steps 4-7)
- **Solid arrows** = data handoffs between steps
- **Dotted arrows** = external tool inputs

---

## Tool Responsibility Map

Which tools serve which steps and what data they provide:

```mermaid
flowchart TD
    subgraph S1["Step 1: Onboarding"]
        S1A["Tally Form Data"]
        S1B["Notion GTM Intake DB"]
        S1C["Notion Client Portal"]
    end
    subgraph S2["Step 2: ICP"]
        S2A["Fathom ICP Discovery transcript"]
        S2B["Notion Transcripts DB"]
        S2C["Notion Client Portal"]
    end
    subgraph S3["Step 3: Market Research"]
        direction LR
        subgraph AHREFS["Ahrefs"]
            A1["Keywords Explorer"]
            A2["Site Explorer"]
            A3["Content Gap"]
            A4["Top Pages"]
            A5["Backlinks"]
            A6["Paid Keywords"]
        end
        subgraph SWEB["SimilarWeb"]
            SW1["Traffic Sources"]
            SW2["Audience Demographics"]
            SW3["Audience Interests"]
            SW4["Social Traffic"]
        end
        subgraph OTHER["Other"]
            M1["Meta Ad Library"]
            M2["Manual Social Observation"]
        end
    end
    subgraph S4_7["Steps 4-7: Strategy"]
        S4["Value Prop + Offers"]
        S5["Channel + Journey"]
        S6["Metrics + KPIs"]
        S7["Launch Roadmap"]
    end
    subgraph HUB["Notion: Central Hub"]
        NP["Client Portal\nReads + Writes all steps"]
    end
    S1 --> NP
    S2 --> NP
    S3 --> NP
    NP --> S4_7
    style S1 fill:#1B9B5E,stroke:#121718,color:#fff
    style S2 fill:#1B9B5E,stroke:#121718,color:#fff
    style S3 fill:#1B9B5E,stroke:#121718,color:#fff
    style AHREFS fill:#F6F3EF,stroke:#A8D9BD,color:#121718
    style SWEB fill:#F6F3EF,stroke:#A8D9BD,color:#121718
    style OTHER fill:#F6F3EF,stroke:#A8D9BD,color:#121718
    style S4_7 fill:#A8D9BD,stroke:#121718,color:#121718
    style HUB fill:#F6F3EF,stroke:#1B9B5E,color:#121718
```

---

## Onboarding Flow

The upstream automation that creates the client portal before any skills run:

```mermaid
flowchart LR
    TALLY["Tally\nOnboarding Form"]
    INTAKE["Notion\nGTM Intake DB"]
    ZAP["Zapier\nIntake → Slack"]
    SLACK["Slack\n#internal-notifications\nvia Digital VA"]
    SKILL["Onboarding Skill\n(Step 1)"]
    PORTAL["Notion\nClient Portal"]
    INFO["Client Information\n- Website URL\n- Competitor URLs\n- Seed Keywords\n- Industry\n- B2B or B2C"]
    REPORTS["Reports Section\n- ICP Analysis\n- Market Research\n- Value Proposition\n- Channel Strategy\n- Metrics + KPIs\n- Launch Roadmap"]
    TALLY -->|"native integration"| INTAKE
    INTAKE -->|"new item trigger"| ZAP
    ZAP -->|"notification"| SLACK
    SLACK -.->|"Terry runs\nprocess new intake"| SKILL
    SKILL -->|"reads intake,\nduplicates template"| PORTAL
    PORTAL --> INFO
    PORTAL --> REPORTS
    style TALLY fill:#E5F5EC,stroke:#1B9B5E,color:#121718
    style INTAKE fill:#F6F3EF,stroke:#1B9B5E,color:#121718
    style ZAP fill:#F0F9F4,stroke:#A8D9BD,color:#121718
    style SLACK fill:#F0F9F4,stroke:#A8D9BD,color:#121718
    style SKILL fill:#1B9B5E,stroke:#121718,color:#fff
    style PORTAL fill:#F6F3EF,stroke:#1B9B5E,color:#121718
    style REPORTS fill:#F6F3EF,stroke:#A8D9BD,color:#121718
    style INFO fill:#F6F3EF,stroke:#A8D9BD,color:#121718
```
