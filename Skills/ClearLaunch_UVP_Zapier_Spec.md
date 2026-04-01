# ClearLaunch UVP — Zapier Zap Specification

**Version:** 1.0 | March 2026
**Purpose:** Automate the flow of UVP workshop transcripts from Fathom into Notion and notify the team via Slack.

---

## Zap Overview

| Field | Value |
|---|---|
| **Zap Name** | ClearLaunch: UVP Transcript → Notion + Slack |
| **Trigger App** | Fathom |
| **Filter** | Meeting title contains "UVP" |
| **Action 1** | Create page in Notion Transcripts DB |
| **Action 2** | Send Slack message to #internal-notifications |

---

## Step 1: Trigger — Fathom New Recording

- **Trigger Event:** New Recording (or New Call Summary — whichever Fathom trigger provides the transcript text)
- **Output fields needed:**
  - Meeting Title
  - Transcript Text (full content)
  - Attendees
  - Meeting Date
  - Duration
  - Fathom Share URL
  - Recording URL

---

## Step 2: Filter — Meeting Title Contains "UVP"

- **Filter condition:** Meeting Title → Text Contains → "UVP" (case-insensitive)
- **Purpose:** Only process meetings that are UVP workshops. Other meeting types (ICP, Offer Dev, etc.) are handled by their own zaps.
- **Note:** This is a routing filter only — the agent does the formal meeting type classification after reading the transcript content.

---

## Step 3: Action — Create Page in Notion Transcripts DB

- **Notion Database:** Transcripts (`collection://0f372290-8993-4c7e-b303-13afca181721`)
- **Location:** Database Hub - ClearThink → Transcripts

**Field mapping:**

| Notion Field | Zapier Source | Notes |
|---|---|---|
| Meeting Title | Fathom: Meeting Title | Title property |
| Attendees | Fathom: Attendees | Text — comma-separated names |
| Client | *(Manual or Zapier lookup)* | Relation field — see note below |
| Meeting Date | Fathom: Meeting Date | Date property |
| Meeting Type | *(Leave blank)* | Agent classifies after reading content |
| Duration (min) | Fathom: Duration | Number property |
| Fathom Share URL | Fathom: Share URL | URL property |
| Recording URL | Fathom: Recording URL | URL property |
| Notes | *(Leave blank)* | Agent fills during processing |
| Deliverables Generated | *(Leave blank)* | Agent fills after generating deliverables |
| Status | "Not started" | Status property — agent picks up from here |

**Page body:** Paste the full transcript text as the page content (speaker-labeled conversation format).

### Client Relation Note

The `Client` relation field links transcripts to Client Portals. Options:

1. **Manual:** Terry sets the Client relation manually after the transcript lands in Notion (current ICP pattern)
2. **Zapier lookup:** Add a lookup step that matches the meeting title or attendee name to an existing Client Portal and auto-sets the relation (future improvement)

---

## Step 4: Action — Slack Notification

- **Slack Channel:** `#internal-notifications`
- **Bot Name:** Digital VA
- **Message Template:**

```
📋 UVP Discovery transcript created for *[Client Name]*

Meeting: [Meeting Title]
Date: [Meeting Date]
Duration: [Duration] min
Attendees: [Attendees]

Status: Ready for processing
Fathom: [Fathom Share URL]
```

- **Note:** If the Client relation is set manually (not by Zapier), the Slack message may use the meeting title instead of the client name. Adjust once the client lookup is automated.

---

## Testing Checklist

- [ ] Trigger fires when a Fathom recording with "UVP" in the title is created
- [ ] Filter correctly skips recordings without "UVP" in the title
- [ ] Notion page is created in the correct Transcripts database
- [ ] All field mappings populate correctly
- [ ] Transcript text appears in the page body (not a property)
- [ ] Status is set to "Not started"
- [ ] Slack message posts to `#internal-notifications`
- [ ] Slack message includes meeting title, date, and Fathom link

---

## Relationship to Other Zaps

This zap follows the same pattern as the ICP transcript zap:

| Zap | Filter | Transcript DB | Slack Message |
|---|---|---|---|
| ICP Transcript | Title contains "ICP" or "Discovery" | Same DB | "ICP Discovery transcript created for [Client]" |
| **UVP Transcript** | **Title contains "UVP"** | **Same DB** | **"UVP Discovery transcript created for [Client]"** |
| Offer Dev Transcript *(future)* | Title contains "Offer" | Same DB | "Offer Dev transcript created for [Client]" |

All transcripts land in the **same Transcripts database** — the agent uses the Meeting Type field (set during classification) to determine which skill processes them.
