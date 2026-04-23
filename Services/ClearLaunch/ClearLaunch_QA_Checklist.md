# ClearLaunch QA Checklist

**Last Updated:** March 29, 2026
**Purpose:** Track verification items and blockers before running the ClearLaunch system with real clients.

---

## Blocker: Ahrefs / SimilarWeb Subscriptions

**Status:** BLOCKED — paid subscriptions needed before Market Research Skill (Step 3) can run.

### Ahrefs — Reports Required by Step 3

| Report | What the MR Skill Uses It For | Plan Tier Needed |
|---|---|---|
| Keywords Explorer | Seed keyword expansion (Also Rank For, Related Terms, Questions), keyword metrics (volume, KD, CPC) | Lite or higher |
| Site Explorer — Organic Keywords | Client's current rankings, competitor top keywords | Lite or higher |
| Site Explorer — Backlink Profile | Client + competitor domain rating, backlink counts | Lite or higher |
| Content Gap | Keywords competitors rank for that client doesn't | Standard or higher |
| Top Pages | Competitor's highest-traffic pages | Lite or higher |
| Paid Keywords | Competitor PPC activity | Standard or higher |

**Action needed:** Confirm which Ahrefs plan Terry subscribes to and whether Content Gap and Paid Keywords are available. If on Lite, those two reports may be limited or unavailable — the MR Skill has fallback handling but output quality degrades.

### SimilarWeb — Reports Required by Step 3

| Report | What the MR Skill Uses It For | Access Level Needed |
|---|---|---|
| Traffic Overview | Competitor traffic estimates | Free (limited) or Pro |
| Traffic Sources | Where competitor traffic comes from (organic, paid, social, referral) | Free (limited) or Pro |
| Audience Demographics | Competitor audience age, gender, geography | Pro |
| Audience Interests | Cross-visitation, affinity categories | Pro |
| Social Traffic | Which social platforms drive traffic | Free (limited) or Pro |

**Note:** SimilarWeb is browser-only (no API). Free tier provides limited data — low-traffic sites may show no data at all. Pro subscription required for full audience demographics and interests.

**Action needed:** Determine if SimilarWeb Pro is needed or if free tier is sufficient for initial clients. Low-traffic client competitors may return empty data regardless of plan.

---

## Verification: End-to-End Flow Test

### Step 1: Onboarding (Tally → Portal)

| Check | Status | Notes |
|---|---|---|
| Tally form submission lands in GTM Intake DB | ✅ PASS | Acme Test Co submission confirmed March 29 |
| Zapier fires Slack notification | ✅ PASS | Digital VA bot posted to #internal-notifications |
| Onboarding Skill creates Client Portal | ⬜ NOT TESTED | Run "process new intake" against Acme Test Co |
| Client Information sections populated correctly | ⬜ NOT TESTED | Verify after portal creation |
| Reports section has all 7 subsections | ⬜ NOT TESTED | Verify after portal creation |
| Intake record status updated to "Portal Created" | ⬜ NOT TESTED | Verify after portal creation |

### Step 2: ICP (Transcript → Deliverables)

| Check | Status | Notes |
|---|---|---|
| ICP Discovery call transcript lands in Transcripts DB | ⬜ NOT TESTED | Requires a Fathom-recorded call |
| Slack notification fires for transcript arrival | ✅ PASS | Existing Fathom → Notion → Slack zap confirmed working |
| Client relation set on transcript | ⬜ NOT TESTED | Manual step by Terry |
| ICP Skill processes transcript | ⬜ NOT TESTED | Run "process new transcripts" |
| B2B/B2C template selection works | ⬜ NOT TESTED | Depends on Business Type from portal |
| Deliverables stored in portal Reports section | ⬜ NOT TESTED | Verify after ICP Skill runs |

### Step 3: Market Research

| Check | Status | Notes |
|---|---|---|
| MR Skill reads ICP output from portal | ⬜ BLOCKED | Needs Step 2 to complete first |
| Ahrefs browser workflows produce data | ⬜ BLOCKED | Needs Ahrefs subscription |
| SimilarWeb browser workflows produce data | ⬜ BLOCKED | Needs access verification |
| Template population works | ⬜ BLOCKED | Needs tool access |

---

## Cleanup: Acme Test Co Dummy Data

After testing is complete, clean up the test artifacts:

- [ ] Delete or archive the Acme Test Co record from GTM Intake DB
- [ ] Delete the Acme Test Co Client Portal (if created during testing)
- [ ] Delete any test transcripts from Transcripts DB

---

## Infrastructure Items (Non-Blocking)

| Item | Status | Notes |
|---|---|---|
| Client relation automation on transcripts | DEFERRED | Manual by design for now. Future: Zapier lookup to match client name from Fathom call title |
| Competitor Analysis Framework | NOT STARTED | Terry explicitly said not to build yet |
| Meta Ad Library browser workflow | DOCUMENTED | In MR Skill but untested — no subscription needed (free tool) |
