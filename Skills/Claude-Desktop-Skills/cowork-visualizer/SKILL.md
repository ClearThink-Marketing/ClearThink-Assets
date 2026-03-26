---
name: cowork-visualizer
description: Visualize a Claude Cowork system or workflow as a beautiful self-contained HTML diagram. Takes a description of a Cowork setup and generates a visual map of its components, flow, and connections.
allowed-tools:
  - Read
  - Write
  - Bash
---

Visualize this Claude Cowork system or workflow: $ARGUMENTS

## PURPOSE

Turn a description of a Claude Cowork system into a beautiful, self-contained HTML visual — so you can see exactly how a workflow operates before you build it. Think of it as a blueprint generator.

**When to use `/cowork-visualizer`:**
- Before building a new Cowork system — visualize first, build second
- To explain your Cowork setup to someone else
- To audit an existing system and spot gaps
- To map out a new workflow idea end to end

---

## WORKFLOW

### STEP 1: PARSE THE SYSTEM

From the user's description, identify and categorize:

**Components to look for:**
- **Trigger** — what starts the workflow? (user message, scheduled task, webhook, morning briefing)
- **Context** — what does Claude read first? (CLAUDE.md, data files, prior outputs)
- **Tools / Connectors** — what integrations are used? (Google Drive, Gmail, Calendar, Notion, Slack, MCP servers)
- **Skills / Commands** — what slash commands run? (e.g., `/script`, `/morning`, `/publish`)
- **Outputs** — what gets produced? (script, HTML file, Notion page, email draft, pipeline entry)
- **Loop / Repeat** — does it run on a schedule? Daily? Weekly? On demand?

If the description is vague, infer reasonable defaults for a content creator workflow. Don't ask — just visualize.

### STEP 2: DESIGN THE DIAGRAM

Plan a visual layout with these zones, top to bottom:

1. **TRIGGER** — how the system starts (1-2 items)
2. **CONTEXT LOAD** — what Claude reads at the start (CLAUDE.md, data, prior memory)
3. **CORE WORKFLOW** — the main steps Claude takes (3-6 steps in a flow)
4. **TOOLS USED** — integrations and connectors firing during the flow
5. **OUTPUTS** — what comes out the other side

Use these visual components from the design system:

| Component | Use for |
|-----------|---------|
| `.flow` + `.flow-step` | Sequential steps (numbered) |
| `.card-grid` + `.info-card` | Tools, connectors, capabilities |
| `.compare` | Before/after, input/output |
| `.code-panel` + `.code-line` | Commands, file paths, config |
| `.bullet-list` | Capabilities or outputs list |
| `.big-stat` | Key metric or number |
| `.zone-label` | Section headers for each zone |
| `.connector-line` | SVG or CSS arrows between zones |

### STEP 3: GENERATE THE HTML

Create a single self-contained HTML file. All CSS in `<style>`, all JS in `<script>`. No external dependencies.

**File structure:**
```
outputs/diagrams/cowork-[topic-slug]/index.html
```
Topic slug: lowercase kebab-case from the workflow description (e.g., `morning-briefing`, `content-pipeline`, `brand-deal-tracker`)

---

## DESIGN SYSTEM

Use EXACTLY the same design tokens as the slides system:

```
Background: #0a0a0a (main)
Zone backgrounds: rgba(255,255,255,0.03) with 1px solid rgba(255,255,255,0.06) border
Primary text: #f5f5f7 (weight 400)
Bold/headline: #ffffff (weight 700)
Secondary text: #86868b
Accent (Claude brand): #DA7756
Flow step bg: rgba(218,119,86,0.12)
Flow step border: rgba(218,119,86,0.3)
Card bg: rgba(255,255,255,0.05)
Card border: rgba(255,255,255,0.08)
Card radius: 16px
Zone radius: 20px
Font: -apple-system, BlinkMacSystemFont, 'SF Pro Display', sans-serif
Font smoothing: -webkit-font-smoothing: antialiased
Trigger accent: #30D158 (green — system is alive)
Output accent: #0A84FF (blue — data leaving the system)
Tool accent: #FFD60A (yellow — external connection)
```

---

## HTML TEMPLATE

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>[System Name] — Cowork Visualizer</title>
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }
    body {
      background: #0a0a0a;
      color: #f5f5f7;
      font-family: -apple-system, BlinkMacSystemFont, 'SF Pro Display', sans-serif;
      -webkit-font-smoothing: antialiased;
      min-height: 100vh;
      padding: 48px 32px;
    }

    /* PAGE HEADER */
    .page-header {
      text-align: center;
      margin-bottom: 64px;
    }
    .system-label {
      font-size: 12px;
      font-weight: 600;
      letter-spacing: 2px;
      text-transform: uppercase;
      color: #DA7756;
      margin-bottom: 12px;
    }
    .page-title {
      font-size: 42px;
      font-weight: 700;
      color: #fff;
      line-height: 1.1;
      margin-bottom: 12px;
    }
    .page-subtitle {
      font-size: 17px;
      color: #86868b;
      max-width: 480px;
      margin: 0 auto;
    }

    /* ZONES */
    .zone {
      background: rgba(255,255,255,0.03);
      border: 1px solid rgba(255,255,255,0.06);
      border-radius: 20px;
      padding: 32px;
      margin-bottom: 24px;
      max-width: 900px;
      margin-left: auto;
      margin-right: auto;
    }
    .zone-label {
      font-size: 11px;
      font-weight: 700;
      letter-spacing: 2px;
      text-transform: uppercase;
      margin-bottom: 24px;
      display: flex;
      align-items: center;
      gap: 8px;
    }
    .zone-label.trigger { color: #30D158; }
    .zone-label.context { color: #DA7756; }
    .zone-label.workflow { color: #f5f5f7; }
    .zone-label.tools { color: #FFD60A; }
    .zone-label.output { color: #0A84FF; }
    .zone-dot {
      width: 6px;
      height: 6px;
      border-radius: 50%;
      background: currentColor;
    }

    /* CONNECTOR ARROW */
    .zone-connector {
      display: flex;
      justify-content: center;
      margin: -8px auto 16px;
      color: #48484a;
      font-size: 22px;
    }

    /* FLOW STEPS */
    .flow {
      display: flex;
      flex-direction: column;
      gap: 12px;
    }
    .flow-row {
      display: flex;
      align-items: center;
      gap: 12px;
    }
    .flow-step {
      background: rgba(218,119,86,0.10);
      border: 1px solid rgba(218,119,86,0.25);
      border-radius: 14px;
      padding: 16px 20px;
      flex: 1;
      display: flex;
      align-items: flex-start;
      gap: 14px;
    }
    .step-num {
      width: 28px;
      height: 28px;
      border-radius: 50%;
      background: rgba(218,119,86,0.2);
      border: 1px solid rgba(218,119,86,0.4);
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 12px;
      font-weight: 700;
      color: #DA7756;
      flex-shrink: 0;
    }
    .step-content {}
    .step-title {
      font-size: 15px;
      font-weight: 600;
      color: #fff;
      margin-bottom: 4px;
    }
    .step-desc {
      font-size: 13px;
      color: #86868b;
      line-height: 1.5;
    }
    .flow-arrow {
      color: #48484a;
      font-size: 18px;
      flex-shrink: 0;
    }

    /* CARD GRID */
    .card-grid {
      display: grid;
      gap: 12px;
    }
    .card-grid.cols-2 { grid-template-columns: repeat(2, 1fr); }
    .card-grid.cols-3 { grid-template-columns: repeat(3, 1fr); }
    .card-grid.cols-4 { grid-template-columns: repeat(4, 1fr); }
    .info-card {
      background: rgba(255,255,255,0.05);
      border: 1px solid rgba(255,255,255,0.08);
      border-radius: 16px;
      padding: 18px;
    }
    .card-icon {
      font-size: 24px;
      margin-bottom: 10px;
    }
    .card-label {
      font-size: 14px;
      font-weight: 600;
      color: #fff;
      margin-bottom: 4px;
    }
    .card-desc {
      font-size: 12px;
      color: #86868b;
      line-height: 1.5;
    }
    .card-tag {
      display: inline-block;
      margin-top: 8px;
      font-size: 10px;
      font-weight: 600;
      letter-spacing: 1px;
      text-transform: uppercase;
      padding: 3px 8px;
      border-radius: 6px;
    }
    .card-tag.trigger { background: rgba(48,209,88,0.15); color: #30D158; }
    .card-tag.tool { background: rgba(255,214,10,0.15); color: #FFD60A; }
    .card-tag.output { background: rgba(10,132,255,0.15); color: #0A84FF; }
    .card-tag.skill { background: rgba(218,119,86,0.15); color: #DA7756; }

    /* CODE PANEL */
    .code-panel {
      background: rgba(0,0,0,0.4);
      border: 1px solid rgba(255,255,255,0.08);
      border-radius: 12px;
      padding: 16px 20px;
      font-family: 'SF Mono', 'Menlo', 'Cascadia Code', monospace;
      font-size: 13px;
    }
    .code-line {
      display: flex;
      gap: 12px;
      margin-bottom: 6px;
      align-items: baseline;
    }
    .code-line:last-child { margin-bottom: 0; }
    .code-line .key { color: #86868b; min-width: 120px; }
    .code-line .val { color: #f5f5f7; }
    .code-line .accent { color: #DA7756; }
    .code-line .green { color: #30D158; }
    .code-line .blue { color: #0A84FF; }
    .code-line .yellow { color: #FFD60A; }

    /* TRIGGER PILL */
    .trigger-pill {
      display: inline-flex;
      align-items: center;
      gap: 8px;
      background: rgba(48,209,88,0.12);
      border: 1px solid rgba(48,209,88,0.25);
      border-radius: 100px;
      padding: 10px 20px;
      font-size: 15px;
      font-weight: 600;
      color: #30D158;
    }
    .trigger-pulse {
      width: 8px;
      height: 8px;
      border-radius: 50%;
      background: #30D158;
      box-shadow: 0 0 8px #30D158;
      animation: pulse 2s infinite;
    }
    @keyframes pulse {
      0%, 100% { opacity: 1; }
      50% { opacity: 0.3; }
    }
    .trigger-row {
      display: flex;
      gap: 12px;
      flex-wrap: wrap;
    }

    /* CONTEXT ROW */
    .context-row {
      display: flex;
      gap: 12px;
      flex-wrap: wrap;
    }
    .context-chip {
      background: rgba(218,119,86,0.10);
      border: 1px solid rgba(218,119,86,0.2);
      border-radius: 10px;
      padding: 10px 16px;
      font-size: 13px;
      font-weight: 600;
      color: #DA7756;
      display: flex;
      align-items: center;
      gap: 8px;
    }

    /* OUTPUT LIST */
    .output-list {
      display: flex;
      flex-direction: column;
      gap: 10px;
    }
    .output-item {
      display: flex;
      align-items: center;
      gap: 14px;
      background: rgba(10,132,255,0.08);
      border: 1px solid rgba(10,132,255,0.18);
      border-radius: 12px;
      padding: 14px 18px;
    }
    .output-icon { font-size: 20px; flex-shrink: 0; }
    .output-name {
      font-size: 14px;
      font-weight: 600;
      color: #fff;
    }
    .output-desc {
      font-size: 12px;
      color: #86868b;
      margin-top: 2px;
    }

    /* SCHEDULE BADGE */
    .schedule-badge {
      display: inline-flex;
      align-items: center;
      gap: 6px;
      background: rgba(255,255,255,0.06);
      border: 1px solid rgba(255,255,255,0.1);
      border-radius: 8px;
      padding: 6px 12px;
      font-size: 12px;
      font-weight: 600;
      color: #86868b;
      margin-top: 12px;
    }

    /* FOOTER */
    .page-footer {
      text-align: center;
      margin-top: 48px;
      font-size: 12px;
      color: #48484a;
    }
  </style>
</head>
<body>

  <div class="page-header">
    <div class="system-label">Claude Cowork System</div>
    <h1 class="page-title">[SYSTEM NAME]</h1>
    <p class="page-subtitle">[One sentence describing what this system does and why it matters]</p>
  </div>

  <!-- ZONE 1: TRIGGER -->
  <div class="zone">
    <div class="zone-label trigger">
      <div class="zone-dot"></div>
      Trigger
    </div>
    <div class="trigger-row">
      <!-- Add trigger pills here -->
    </div>
  </div>

  <div class="zone-connector">↓</div>

  <!-- ZONE 2: CONTEXT LOAD -->
  <div class="zone">
    <div class="zone-label context">
      <div class="zone-dot"></div>
      Context Load
    </div>
    <div class="context-row">
      <!-- Add context chips here -->
    </div>
  </div>

  <div class="zone-connector">↓</div>

  <!-- ZONE 3: CORE WORKFLOW -->
  <div class="zone">
    <div class="zone-label workflow">
      <div class="zone-dot" style="background:#f5f5f7"></div>
      Workflow
    </div>
    <div class="flow">
      <!-- Add flow steps here -->
    </div>
  </div>

  <div class="zone-connector">↓</div>

  <!-- ZONE 4: TOOLS USED -->
  <div class="zone">
    <div class="zone-label tools">
      <div class="zone-dot"></div>
      Tools & Connectors
    </div>
    <div class="card-grid cols-3">
      <!-- Add info cards here -->
    </div>
  </div>

  <div class="zone-connector">↓</div>

  <!-- ZONE 5: OUTPUTS -->
  <div class="zone">
    <div class="zone-label output">
      <div class="zone-dot"></div>
      Outputs
    </div>
    <div class="output-list">
      <!-- Add output items here -->
    </div>
  </div>

  <div class="page-footer">
    Generated by /cowork-visualizer — Claude Cowork
  </div>

</body>
</html>
```

---

### STEP 4: POPULATE THE TEMPLATE

Fill in ALL zones from the user's description. Every zone must have content. If the user didn't specify something (like connectors), infer sensible defaults based on the workflow type.

**Common connectors by workflow type:**
- Content creation: Google Drive, Gmail, YouTube
- Morning briefing: Gmail, Google Calendar, WebSearch
- Brand deals: Notion, Gmail
- Publishing: Blotato, ManyChat, Instagram
- Research: WebSearch, Apify

**Common CLAUDE.md context chips:**
- `📋 CLAUDE.md` (always include)
- `📊 top_performing_content.json` (if content creation)
- `🗂️ scripts.json` (if publishing/pipeline)
- `🧠 Competitor data` (if research)

### STEP 5: SAVE AND OPEN

Save to: `outputs/diagrams/cowork-[topic-slug]/index.html`

Then open in browser:
```bash
open outputs/diagrams/cowork-[topic-slug]/index.html
```

---

## OUTPUT FORMAT

After generating, say:

```
## COWORK SYSTEM VISUALIZED

**System:** [System name]
**File:** outputs/diagrams/cowork-[slug]/index.html

**Zones mapped:**
- Trigger: [what starts it]
- Context: [what Claude reads]
- Workflow: [N steps]
- Tools: [list]
- Outputs: [list]

Want to adjust anything? Describe the change and I'll update the diagram.
```

---

## RULES

- Always generate a complete, working HTML file — never a skeleton or placeholder
- Every zone must have content — never leave a zone empty
- Use the exact design tokens from the design system (colors, fonts, radii)
- Keep text tight — card labels 1-4 words, descriptions 1 sentence max
- The visual should be readable at a glance — not a wall of text
- Never add external CSS/JS dependencies — everything self-contained
- Open the file automatically after saving
