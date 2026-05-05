# Creatives Database Pattern (Notion)

**Status:** v1 — first formalized May 2026. Expect schema and lifecycle to evolve as we run more campaigns and learn what holds vs. what doesn't.

This doc specifies the Notion database pattern ClearThink uses to track creatives across a Meta Ads campaign. Concepts ideated by the `meta-static-ad-ideator` skill and regen prompts written by the `meta-static-ad-critic` skill all flow into this database, which becomes the source of truth for the campaign's creative round.

## When to use it

Whenever a campaign produces ≥10 creatives (Andromeda standard) and renders flow through ChatGPT then assemble in Meta Ads Manager. Don't bother for one-off creatives — overhead exceeds benefit.

## Schema

| Column | Type | Purpose |
|---|---|---|
| **Title** | Title | Concept name (e.g., "Concept 1: The 90-Minute Flip" or "v1 Ad 3 (Regen): Lock In Turnover Rates") |
| **Hook direction** | Rich text | The on-image hook (5-15 words) |
| **Angle blurb** | Rich text | Strategic reasoning — what angle, why this concept, what makes it distinct from neighbors |
| **Image generation prompt** | Rich text | Paste-and-go for ChatGPT (Methodology §7 format) |
| **Notes** | Rich text | What changed across iterations, render notes, design decisions |
| **Ad creative** | Files | Final rendered image (drag-drop the PNG/JPG) |
| **Status** | Select | Lifecycle tracking (see below) |

## Status lifecycle

| Value | Color | Meaning |
|---|---|---|
| Pending render | gray | Concept exists in the database, image not yet rendered |
| Rendered v1 | yellow | First render produced; may need iteration |
| Rendered v2 | orange | Refined render produced (from a regen prompt or edit-mode iteration) |
| Approved | green | Render is locked, ready for Meta Ads Manager assembly |
| Killed | red | Concept deemed not worth pursuing — preserve the row for context (Andromeda may revive a killed angle later in a future round) |

## Workflow

1. Strategist runs Ideation skill → 25-30 concepts (or 10-15 for low-budget pilot)
2. Each concept gets a database row with: Title, Hook direction, Angle blurb, Image generation prompt
3. Status defaults to **Pending render**
4. Strategist copies the `Image generation prompt` cell → pastes into ChatGPT → renders
5. Drag rendered image into the **Ad creative** column on the row
6. Status → **Rendered v1**
7. If iteration needed, strategist asks ChatGPT for refinements (edit mode, see ChatGPT context doc §10) or runs the Critique skill for a regen prompt
8. Once render is right, Status → **Rendered v2** (if iterated) → eventually **Approved**
9. Strategist assembles approved creatives in Meta Ads Manager

## Where it lives in Notion

Inside the client's portal in Notion, as a sub-page of the campaign-level strategy doc. Suggested tree:

```
[Client Name] (Client Portal)
└── Meta Ads Strategy — [Campaign Name]
    ├── 📋 Ad Brief — [Audience Segment]
    ├── 💡 Ideation v[N] — [Audience Segment]
    │   └── Concepts — Ideation v[N] (database)
    └── (future: Critique v[N], Production copy set, etc.)
```

The database can also live as a sibling to the Ideation page rather than nested — strategist's call.

## What this database is NOT

- **Not a project tracker.** It tracks creatives, not tasks. Use a separate Notion task database for client deliverables.
- **Not a copy library.** Headlines, body copy, and descriptions from the Production skill live in a separate document — this database is image-prompt-and-render only.
- **Not Brand Library.** Logos, brand colors, etc. live in `/Brand/` — don't store assets here.

## Known gaps

- No template database in the ClearThink Notion workspace yet — strategist creates the schema by hand each campaign. Consider building a duplicable template once a 2nd-3rd campaign confirms the schema is stable.
- No automated sync between the Concepts database and Meta Ads Manager — manual copy-paste at assembly time. Possible future improvement.
