# ClearLaunch System Diagrams

Visual diagrams of the ClearLaunch GTM System architecture and data flow. These render automatically on GitHub.

---

## System Architecture

How data flows from client engagement through the agent to deliverables:

```mermaid
flowchart TB
    subgraph CLIENT["Client Engagement"]
        ONBOARD["Tally Onboarding Form"]
        CALL["Discovery Call"]
    end
    subgraph CAPTURE["Data Capture"]
        FATHOM["Fathom"]
        ZAP1["Zapier: Form to Notion"]
        ZAP2["Zapier: Transcript to Notion"]
    end
    subgraph NOTION["Notion: Central Hub"]
        PORTAL["Client Portal"]
        TRANSCRIPTS["Transcripts DB"]
    end
    subgraph AGENT["Claude Code Agent"]
        S1["Step 1: ICP Skill"]
        S2["Step 2: Market Research Skill"]
        S3["Step 3: Value Prop + Offer Skill"]
        S4["Step 4: Channel + Journey Skill"]
        S5["Step 5: Metrics + KPI Skill"]
        S6["Step 6: Roadmap Skill"]
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
    ONBOARD --> ZAP1 --> PORTAL
    CALL --> FATHOM --> ZAP2 --> TRANSCRIPTS
    TRANSCRIPTS --> S1
    PORTAL --> S1
    PORTAL --> S2
    S1 -->|ICP data| PORTAL
    S2 -->|Market data| PORTAL
    S3 -->|UVP + Offers| PORTAL
    S4 -->|Channel strategy| PORTAL
    S5 -->|KPI framework| PORTAL
    S6 -->|90-day roadmap| PORTAL
    S2 --> AHREFS
    S2 --> SIMILAR
    S2 --> META
    S1 --> DOCX & PPTX
    S2 --> DOCX & PPTX
    S3 --> DOCX
    S4 --> DOCX
    S5 --> DOCX
    S6 --> DOCX
    style CLIENT fill:#E5F5EC,stroke:#1B9B5E,color:#121718
    style CAPTURE fill:#F0F9F4,stroke:#A8D9BD,color:#121718
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
    S1["Step 1\nICP"]
    S2["Step 2\nMarket Research"]
    S3["Step 3\nValue Prop + Offers"]
    S4["Step 4\nChannel + Journey"]
    S5["Step 5\nMetrics + KPIs"]
    S6["Step 6\nLaunch Roadmap"]
    S1 -->|"pain points, competitors,\nsegments, industry"| S2
    S2 -->|"keywords, gaps,\naudience data"| S3
    S3 -->|"positioning, messaging,\noffer structure"| S4
    S4 -->|"channels, journey,\nbudget allocation"| S5
    S5 -->|"KPIs, baselines,\nmeasurement cadence"| S6
    T1["Fathom + Notion"]
    T2["Ahrefs + SimilarWeb\n+ Meta Ad Library"]
    T1 -.->|transcript| S1
    T2 -.->|browser data| S2
    style S1 fill:#1B9B5E,stroke:#121718,color:#fff
    style S2 fill:#1B9B5E,stroke:#121718,color:#fff
    style S3 fill:#A8D9BD,stroke:#121718,color:#121718
    style S4 fill:#A8D9BD,stroke:#121718,color:#121718
    style S5 fill:#A8D9BD,stroke:#121718,color:#121718
    style S6 fill:#A8D9BD,stroke:#121718,color:#121718
    style T1 fill:#F0F9F4,stroke:#A8D9BD,color:#121718
    style T2 fill:#F0F9F4,stroke:#A8D9BD,color:#121718
```

**Legend:**
- **Dark green nodes** = built (Steps 1-2)
- **Light green nodes** = not yet built (Steps 3-6)
- **Solid arrows** = data handoffs between steps
- **Dotted arrows** = external tool inputs

---

## Tool Responsibility Map

Which tools serve which steps and what data they provide:

```mermaid
flowchart TD
    subgraph S1["Step 1: ICP"]
        S1A["Fathom transcript"]
        S1B["Notion Transcripts DB"]
        S1C["Notion Client Portal"]
    end
    subgraph S2["Step 2: Market Research"]
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
    subgraph S3_6["Steps 3-6: Strategy"]
        S3["Value Prop + Offers"]
        S4["Channel + Journey"]
        S5["Metrics + KPIs"]
        S6["Launch Roadmap"]
    end
    subgraph HUB["Notion: Central Hub"]
        NP["Client Portal\nReads + Writes all steps"]
    end
    S1 --> NP
    S2 --> NP
    NP --> S3_6
    style S1 fill:#1B9B5E,stroke:#121718,color:#fff
    style S2 fill:#1B9B5E,stroke:#121718,color:#fff
    style AHREFS fill:#F6F3EF,stroke:#A8D9BD,color:#121718
    style SWEB fill:#F6F3EF,stroke:#A8D9BD,color:#121718
    style OTHER fill:#F6F3EF,stroke:#A8D9BD,color:#121718
    style S3_6 fill:#A8D9BD,stroke:#121718,color:#121718
    style HUB fill:#F6F3EF,stroke:#1B9B5E,color:#121718
```

---

## Onboarding Flow

The upstream automation that creates the client portal before any skills run:

```mermaid
flowchart LR
    TALLY["Tally\nOnboarding Form"]
    ZAP["Zapier"]
    NOTION["Notion\nClient Portal"]
    REPORTS["Reports Section\n- ICP Analysis\n- Market Research\n- Value Proposition\n- Channel Strategy\n- Metrics + KPIs\n- Launch Roadmap"]
    INFO["Client Information\n- Website URL\n- Competitor URLs\n- Seed Keywords\n- Industry\n- B2B or B2C"]
    TALLY -->|form submitted| ZAP
    ZAP -->|creates page| NOTION
    NOTION --> INFO
    NOTION --> REPORTS
    style TALLY fill:#E5F5EC,stroke:#1B9B5E,color:#121718
    style ZAP fill:#F0F9F4,stroke:#A8D9BD,color:#121718
    style NOTION fill:#F6F3EF,stroke:#1B9B5E,color:#121718
    style REPORTS fill:#F6F3EF,stroke:#A8D9BD,color:#121718
    style INFO fill:#F6F3EF,stroke:#A8D9BD,color:#121718
```
