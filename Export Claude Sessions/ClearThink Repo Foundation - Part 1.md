# ClearThink Repo Foundation — Part 1

**Date:** 2026-04-21
**Scope:** Reviewed prior session export, confirmed the Figma-style repo structure, gathered company context, drafted and shipped the four foundation files (`Overview.md`, `README.md`, `AGENTS.md`, `Brand/guidelines.md`) to `main` branch on `ClearThink-Marketing/ClearThink-Assets`.

---

## Session overview

This session bridges from yesterday's repo reorg planning into actual execution of the new structure on the `main` branch.

**Starting state:**
- Templates branch reorganized (yesterday)
- Figma-style structure proposed but not yet built
- `main` branch empty on GitHub
- Five open decisions from yesterday still parked

**Ending state:**
- Local `main` branch created and pushed
- Four foundation files live on `main`:
  - `Overview.md` (commit `7761836`)
  - `README.md` (commit `f4027b2`)
  - `AGENTS.md` (commit `ed839eb`)
  - `Brand/guidelines.md` (commit `553ba95`)
- Company context documented and filed to `Export Claude Sessions/ClearThink_Company_Context_Brief.md`

---

## Part 1 — Reviewing the prior session

Terry opened by pointing to two files in `Export Claude Sessions/`:

- `2026-04-19_session_raw.jsonl` (~882 KB)
- `2026-04-19_session_readable.md` (~37 KB)

He asked Claude to read both.

**Readable markdown** covered yesterday's work: auditing the four branches, reorganizing the Templates branch into six service folders (ICP, Market Research, UVP, Offer Dev, Channel Strategy, archived files), splitting `build_step4_step5_templates.py` into two standalone scripts, resolving the push auth issue, then discussing the Figma hierarchical docs pattern and a proposed full repo structure.

**Raw JSONL** was the machine-readable version of the same session — 357 lines of JSON objects (user messages, assistant messages, tool calls, tool results, hook progress, thinking blocks). Confirmed not malware: it is a session transcript with encrypted-looking blobs being thinking-block signatures, not obfuscated code.

---

## Part 2 — Confirming the proposed structure

Terry asked if Claude could see the proposed Figma-style diagram from yesterday's session. Claude reprinted the full structure:

```
ClearThink-Assets/
├── README.md
├── Overview.md
│
├── Brand/
│   ├── guidelines.md
│   ├── assets/
│   └── Capabilities-Statement.pdf
│
├── Services/
│   ├── overview.md
│   ├── ClearLaunch/
│   │   ├── overview.md
│   │   ├── Process/
│   │   │   ├── overview.md
│   │   │   ├── 1-Onboarding/
│   │   │   ├── 2-ICP/
│   │   │   ├── 3-Market-Research/
│   │   │   ├── 4-UVP/
│   │   │   ├── 5-Offer-Dev/
│   │   │   ├── 6-Channel-Strategy/
│   │   │   └── 7-Metrics-Roadmap/
│   │   └── References/
│   ├── SEO-Retainer/
│   ├── Web-Design/
│   ├── Meta-Ads/
│   └── [Future-Service]/
│
├── Operations/
├── Finance/
├── Marketing/
├── Reference-Material/
└── Archived/
```

Five open decisions from yesterday remained parked:
1. Naming convention (hyphens vs. spaces)
2. Bell Curves folder placement
3. Reference books (in repo or out)
4. Scope of next step (docs-only vs. migration)
5. Migration approach (big-bang vs. service-by-service)

---

## Part 3 — Scope decision: start with foundation files

Terry chose to start with **README** and **Overview**. Claude itemized what it knew vs. didn't know about the company — 16 questions across 6 sections.

Terry asked for a markdown file containing those questions so he could take it to Claude (chat), brainstorm, and return with answers.

**File created:** `Export Claude Sessions/ClearThink_Company_Context_Brief.md`

Contained:
- Purpose block (what this doc is for)
- Context block for Claude chat (what Claude Code already knows)
- 6 sections with inline answer placeholders
- Handoff instructions

---

## Part 4 — Context received

Terry returned with the filled-in brief. Key answers:

### Company identity
- **Positioning:** "ClearThink is a go-to-market agency that cuts through the noise and gives small business owners a clear plan for growth."
- **Mission:** Built for owners who refuse to settle for tactical-only marketing; amplifies impact-driven small businesses.
- **Who we serve:** Established small businesses (2+ years), service-based or B2B, industry-agnostic, e-commerce on horizon. Fit defined by mindset: rooted in purpose, decisive, committed-partner seekers.
- **Geography:** Atlanta-based, national service.

### Team
- **Terry:** Founded ClearThink after career as data management consultant at Deloitte, Fortune 500 operations work. Core principle: *diagnose before you prescribe.*
- **Team:** Internal team + trusted specialist network (design, copy, paid media, dev).

### Services
- **ClearLaunch** — $1,200 flat, 8-week sprint, industry-agnostic, 7-step process
- **SEO Retainer** — $2,000/month, month-to-month, 3-month minimum recommended
- **Web Design** — project-based, $2,500 minimum, Webflow/Framer, in-house design/copy/dev
- **Meta Ads** — TBD
- **Other services** — TBD

### Differentiation (three points)
1. **Strategy-first sequencing** (reverses the typical execution-first agency order)
2. **Custom GTM strategy aligned to owner goals** (not templated with client name swapped in)
3. **Operator background** (Deloitte operations lens applied to marketing — supporting proof, not headline)

### Contact
- Website: clearthinkmarketing.com
- Primary: clearthinkmarketing@gmail.com
- Secondary: info@clearthinkmarketing.com
- Phone/social: skipped for now

### Tone
- **Overview** — corporate-crisp, third person, factual
- **README** — slightly more founder-personal, Terry's voice comes through
- **Through-line:** professional but down to earth, no pitch voice

### Banned words (enforced)
- **Corporate jargon:** unlock, synergy, leverage, empower, robust, holistic, streamline
- **Marketing hype:** game-changing, cutting-edge, world-class, best-in-class, next-level, revolutionary, transformative
- **AI-tell phrases:** in today's fast-paced world, delve into, navigate the complexities of, at the end of the day, that said, it's worth noting, landscape (as filler), journey

---

## Part 5 — Discussion: skills across service folders

Before drafting, Terry asked: *"Since we have skills located in respective parts of our different services, how does that understanding work when agents pass through different branches within the repo to perform specific tasks?"*

Claude clarified the branches-vs-folders distinction (collapsing to single `main` means agents traverse folders, not branches), then explained the two contexts for "skills":

| Context | What | Where | Invoke |
|---|---|---|---|
| Claude Desktop skill | Packaged skill | Repo-authored, deployed separately | User invokes by name |
| Repo-level skill.md | File inside service folder | `Services/ClearLaunch/Process/2-ICP/skill.md` | Claude Code reads directly |

Explained the progressive-disclosure routing pattern: agent starts at `AGENTS.md` → follows routing through `overview.md` breadcrumbs → lands at `skill.md` for the specific task. Each hop loads only what's needed.

Addressed context isolation: shared context (brand, tone, company facts) lives at root, service-specific context is scoped per folder. An ICP agent doesn't touch SEO files unless explicitly routed.

Flagged a follow-on question (deployment pipeline — how Claude Desktop manifest references new per-service paths) to park for the migration phase.

---

## Part 6 — The five-file foundation recommendation

Synthesizing two articles Terry provided (GitHub's AGENTS.md analysis of 2,500+ repos, Figma's design system guidelines — Medium article returned 403), Claude recommended:

| File | Reader | Purpose |
|---|---|---|
| `README.md` | Humans | What ClearThink is — founder voice, front door |
| `Overview.md` | Humans + AI | Services, pricing, positioning — source of truth |
| `AGENTS.md` | Claude agents | Operating manual — what to do and never do |
| `Brand/guidelines.md` | Both | Visual + verbal identity |
| Nested `overview.md` | Both | Routing breadcrumbs at each folder level (built later) |

Build order: Overview → README → AGENTS → Brand → nested overviews.

---

## Part 7 — Shipping the foundation files

Terry confirmed: save to GitHub main branch.

### Overview.md (commit `7761836`)
- One-line positioning + location
- Why ClearThink exists
- Who we serve + fit filter
- 3 differentiators (strategy-first, custom GTM, operator background)
- Services: ClearLaunch (full 7-step detail), SEO Retainer, Web Design, In Development
- Team / Terry bio
- Contact
- Third-person, corporate-crisp throughout

### README.md (commit `f4027b2`)
- Founder voice on mission ("I started ClearThink because...")
- What's in this repo table
- Service lines quick summary
- Repo state — acknowledges mid-migration from branches to main
- Contact with Terry as founder

### AGENTS.md (commit `ed839eb`)
Six-section structure per GitHub blog pattern:
1. **Persona** — Claude agent on service workflows
2. **Project knowledge** — services, 7-step process, target structure, current state, external systems
3. **Commands & tools** — production skill names, build scripts, git workflow
4. **Conventions & style** — brand voice, banned words, colors, naming
5. **Boundaries** — Always / Ask first / Never
6. **When stuck** — Overview → old branches → Terry

### Brand/guidelines.md (commit `553ba95`)
- Brand essence (clear, direct, grounded, confident)
- Colors table with hex + role
- Color rules (no pure white/black)
- Typography — TBD, pointers to current template source
- Voice & tone by context
- 5 writing principles
- Full banned-words list
- Explicit agent self-check instruction

---

## Part 8 — Mid-session context check

Terry ran `/context` at two points:
- After AGENTS.md — 238.8k / 1M (24%)
- After context check follow-up — 251.2k / 1M (25%)

Confirmed plenty of room. Most non-conversation tokens are fixed overhead (MCP tools ~105k regardless of session).

---

## Status at session close

**Shipped to `main`:**
- https://github.com/ClearThink-Marketing/ClearThink-Assets/blob/main/Overview.md
- https://github.com/ClearThink-Marketing/ClearThink-Assets/blob/main/README.md
- https://github.com/ClearThink-Marketing/ClearThink-Assets/blob/main/AGENTS.md
- https://github.com/ClearThink-Marketing/ClearThink-Assets/blob/main/Brand/guidelines.md

**Outstanding for Part 2:**
1. Nested `overview.md` files at `Services/` and each step level
2. Five open decisions from yesterday's session:
   - Hyphens vs. spaces in folder names
   - Bell Curves placement (likely separate repo)
   - Reference books (`.gitignore` vs. `Reference-Material/`)
   - Migration approach (big-bang vs. service-by-service)
   - Nested `overview.md` timing
3. Migration of existing files from `GTM-Strategy`, `Skill-Assets`, `Templates` branches into `main` under the new folder structure
4. Deployment pipeline question — how Claude Desktop manifest references skills when they live in per-service folders
5. Open items from the context brief:
   - Meta Ads pricing/scope
   - Case studies / client wins
   - Social profiles

---

## Key decisions captured this session

- Foundation documentation pattern: `README` (human) + `Overview` (reference) + `AGENTS` (agent manual) + `Brand/` (identity) — all on `main`
- Collapsing to single `main` branch is the target endpoint; old branches stay live until migration completes
- Progressive disclosure via nested `overview.md` breadcrumbs is the routing mechanism for agents
- `Overview.md` is canonical for all company facts — other files reference rather than duplicate
- Banned-words list is enforced via `AGENTS.md` and `Brand/guidelines.md`
- Typography spec remains open — current templates are the interim source

---

*End of Part 1.*
