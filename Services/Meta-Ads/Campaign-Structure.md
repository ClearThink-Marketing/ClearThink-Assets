# Campaign Structure & Deployment

**What this doc is.** The strategist's decision guide for *deploying* Meta static ad campaigns once the creative is produced. Covers budget tiers, campaign structure, Andromeda-aligned settings, optimization cadence, the reach-concentration scaling loop, and decision rules for refresh / scale / kill.

**What this doc is not.** It is not the production methodology. The methodology (`Meta-Ads_Methodology.md`) governs how creative is *made* — frameworks, vocabulary, vertical playbooks, the production loop. This doc governs how creative is *deployed and optimized* in Meta Ads Manager.

**Audience.** The strategist running campaigns. Claude skills don't load this doc — they consume the methodology. This doc lives parallel to the methodology and is read by humans making deployment decisions.

**Source synthesis.** Combines small-budget mechanics from Ben Heath with Andromeda scaling mechanics from Jeremy Haynes. The two systems describe different operating tiers of the same underlying model.

---

## Table of contents

1. Pick your budget tier first
2. Pre-launch: campaign structure
3. Pre-launch: Andromeda settings checklist
4. Post-launch: optimization cadence
5. Post-launch: reach concentration
6. Post-launch: the scaling loop
7. Post-launch: refresh, scale, or kill
8. CAC vs. LTV mindset
9. Small-budget specific mechanics
10. When to consult the methodology vs. this doc

---

## 1. Pick your budget tier first

Every other decision in this doc depends on your tier. Pick before launching.

| Tier | Monthly spend | Daily spend | Creative volume target | Operating model |
|---|---|---|---|---|
| **Tiny** | < $600 | < $20 | 10-15 | Heath: consolidate to 1 campaign, 1 ad set, 1 offer. Mine Meta Ads Library + organic content for concepts. Long optimization cycles (10-14 days). |
| **Small** | $600 – $3K | $20 – $100 | 10-15 | Heath: 1 campaign, 1-2 ad sets. Hyper-niche the ICP. Some original creative + heavy reliance on competitor patterns. 7-10 day cycles. |
| **Mid** | $3K – $15K | $100 – $500 | 20-25 | Hybrid. 1 campaign, 2-3 ad sets. Mix of fresh creative + competitor-modeled. 7-day cycles. Approaching full Andromeda model. |
| **Scale** | $15K+ | $500+ | 25-30+ | Full Haynes Andromeda model. 1-2 campaigns, 3 ad sets each (broad + interest stack + lookalike stack). Continuous fresh creative production. Sub-7-day cycles where data supports. |

**Why these brackets.** Below $600/mo there isn't enough conversion volume for Meta's learning phase to exit reliably with anything beyond one tightly-scoped campaign. Above $15K/mo there's enough volume to feed the full Andromeda diversification model. Mid is hybrid territory.

**If your client moves up a tier mid-engagement:** restructure. Don't run a tiny-tier setup at scale spend (you'll be leaving distribution on the table) and don't run a scale-tier setup at tiny spend (you'll be in perpetual learning phase).

---

## 2. Pre-launch: campaign structure

### Tiny / Small tier (< $3K/mo)

```
1 Campaign (objective: Sales or Leads)
└── 1 Ad set (broad targeting; messaging does the work)
    └── 10-15 unique creatives (all the ad set's ads)
        + 5 headlines, 5 body copy, 5 descriptions (rotate)
```

- **One offer only.** Multi-offer briefs fragment learning and almost always lose to single-offer focus at this tier.
- **Broad targeting.** Don't fragment audiences across multiple ad sets at this budget. Messaging controls who Meta serves to.
- **Optional second ad set:** if the strategist has clear retargeting volume (existing site visitors, lead-form starters), a small retarget ad set can run in parallel — but cap its budget at 20-30% of the cold ad set.

### Mid tier ($3K–$15K/mo)

```
1 Campaign (objective: Sales or Leads)
├── Ad set 1: Broad
├── Ad set 2: Interest stack (large stack of interests + behaviors + demographics)
└── (Optional) Ad set 3: Lookalike stack (1% lookalikes from highest-value customers)
    └── Each ad set runs the same 20-25 creatives + same 5/5/5 copy set
```

- **Same creatives in every ad set.** This is critical. Don't try to run different creatives per ad set — Andromeda needs the same creative pool exposed to different audience signals.
- **Use ABO (ad-set budgets), not CBO.** Better distribution control across the three ad sets.

### Scale tier ($15K+/mo)

```
Test campaign (objective: Sales or Leads)
├── Ad set 1: Broad
├── Ad set 2: Interest stack
└── Ad set 3: Lookalike stack
    └── Each ad set runs the same 25-30 creatives + same 5/5/5 copy set

Foundational campaign (after winners scale-out)
├── Foundational ad set: same audience structure as test ad set, only the proven 1-3 winners
    └── Scaled budget; the test campaign continues to feed it
```

- **Test campaign feeds the foundational campaign.** When 1-3 winners emerge from the test campaign and scale to a ceiling, they "graduate" into a separate foundational ad set with dedicated scaled budget. The test campaign then refreshes (see §6 scaling loop) and keeps producing the next generation of winners.

### Always

- **Skip awareness, engagement, and traffic objectives.** Run Sales or Leads only. Brand awareness on Meta requires scale this system isn't built for.
- **One campaign per offer.** Don't run multi-offer experiments inside a single campaign.

---

## 3. Pre-launch: Andromeda settings checklist

Before launching any ad set, check these settings. Most of them defeat Andromeda when left on.

**Turn OFF:**

- **Advantage+ Creative.** Don't let Meta auto-generate copy/visual variations. Breaks the strategist's intentional diversification.
- **Site Links.** Adds clutter under your CTA that the algorithm wasn't optimized for.
- **Music suggestions** (where applicable).
- **Comment suggestions / engagement nudges** that aren't the positive-comment-highlight feature.
- **Auto-translation** unless explicitly running a multi-language campaign.

**Leave ON (or selectively use):**

- **Positive comment highlighting.** Only Advantage+ feature worth keeping — surfaces strong social proof in the ad unit.

**Budget settings:**

- **ABO (ad-set budget optimization), not CBO.** Cleaner data per ad set, better distribution control.
- **Accelerated delivery: OFF.** Standard delivery only.

**Placements:**

- **Manual placements** for static ads. Auto placements include video-only surfaces that waste static-ad spend.
- For static ads specifically: Feed (Facebook + Instagram) + Stories + Reels (when 9:16 is rendered) + Marketplace where relevant. Skip Audience Network unless tested and proven.

**Optimization event:**

- **The most-conversion-volume event the campaign can support.** Sales > Add to Cart > View Content > Lead. If you're under ~50 conversions/week of your top-tier event, optimize for the next event up the funnel and let Meta's modeling fill in.

---

## 4. Post-launch: optimization cadence

### Set a cycle, stick to it

Every change to a campaign or ad set re-enters the learning phase. Tiny constant tweaks = perpetual learning phase = wasted spend. Set an optimization schedule and respect it.

| Tier | Cycle | Why |
|---|---|---|
| Tiny | 10-14 days | Low conversion volume → long learning phase. Need patience. |
| Small | 7-10 days | Some volume, still want stability. |
| Mid | 7 days | Standard. |
| Scale | 3-7 days | High volume = fast learning phase exit. Can iterate faster. |

**During the cycle, you can still:** produce fresh creative, write new copy, analyze data, plan adjustments. You just don't *make* the adjustments mid-cycle.

### Use a statistical-significance check before declaring winners

Before deciding "this ad is the winner" and acting on it, confirm with a free statistical-significance calculator. Default threshold: 90%+ significance. Without that, you're chasing noise.

### What to do during a cycle if performance tanks

If results are clearly broken (cost-per-conversion 3x+ baseline for 3+ days), treat it as an emergency, not a tweak. Pause the ad set, investigate (creative fatigue? landing page issue? Meta bug?), then re-launch with the fix. This is different from "I don't like the numbers, let me tweak" — that's helicopter parenting.

---

## 5. Post-launch: reach concentration

**Expect 1-3 of your creatives to capture nearly all the reach.** Out of 25-30 ads in an ad set, the other 22-29 will spend pennies. This is the algorithm working correctly — Andromeda found the pockets that match those specific creatives.

**Do not respond to this by:**

- Duplicating ad sets to force individual creatives into distribution. Inflates CPA, fragments learning.
- Pausing the "non-distributing" creatives. They're your bench for the next cycle.
- Convincing yourself the algorithm is broken. It's not.

**Do respond by:**

- Running the Critic skill on the 1-3 winners and the 1-2 you suspect are dragging set fitness. Score them.
- Letting the bench sit. They'll get their shot when the winners exhaust their pocket and you refresh (see §6).
- Watching for *who* is converting from the winners, not just *how many*. If lead quality is bad, the winners are losers — see §7.

---

## 6. Post-launch: the scaling loop

When 1-3 winners emerge and continue performing, follow this loop. Source: Haynes' Andromeda scaling pattern.

```
Step 1: Identify winners
   ↓
Step 2: Scale spend on the ad set
   ↓
Step 3: Hit a ceiling (CPR climbs, volume drops past it)
   ↓
Step 4: Pull spend back to the ceiling (this is your new equilibrium)
   ↓
Step 5: Convert this ad set into a "foundational ad set"
   (or duplicate it into a foundational campaign at scale tier)
   ↓
Step 6: Duplicate the original ad set → "test ad set v2"
   ↓
Step 7: In test v2, pause the 1-3 winners (they live in foundational now)
   ↓
Step 8: Add 1-3 fresh creatives from the bench to test v2
   ↓
Step 9: Test v2 returns to test budget; the loop repeats
```

**The unit of scaling is the ad set, not the individual creative.** When a creative wins, it's the ad set's lever you pull (more budget → ceiling → foundational), then you reset the test ad set and look for the next generation of winners.

**Always have 5-10 unused creatives on the bench.** Refresh fuel is the bottleneck — never the algorithm. If you've exhausted the bench, run the Ideator skill again to generate the next batch.

---

## 7. Post-launch: refresh, scale, or kill

Decision matrix for what to do with a winning creative once it's clearly winning.

| Lead quality from winner | Volume/CPR | Action |
|---|---|---|
| Good (sales team likes the leads) | Hitting target CPR | **Scale** — push budget, watch for ceiling, eventually move to foundational. |
| Good | CPR climbing past target | **Hold + watch** — pull spend slightly, see if it stabilizes. If not, pocket may be exhausted; refresh. |
| Bad (low-quality leads, wrong-fit customers) | Any CPR | **Kill the winner.** It's matching the wrong pocket. Pause it, do *not* scale, and run the loop with fresh creatives that target the right segment more precisely. |
| Mixed | Any CPR | **Investigate** — listen to sales calls, look at lead form responses. Decide based on signal, not aggregate metrics. |

**The "good CPR with bad leads" case is the most expensive failure mode.** Don't optimize toward it. The Critic skill flags this when you run it on a winner that pulled the wrong lever (declared LF7 "care of loved ones," ad executed on LF6 "be superior" — pulls in a different audience entirely).

---

## 8. CAC vs. LTV mindset

Most small-budget advertisers cap their willingness to pay for a customer below their actual customer LTV. This is the single biggest constraint on small-budget growth.

### The math you should run before launching

1. **Customer LTV (12-month or business-appropriate window).** What is one customer worth to you in revenue, net of cost of goods/service?
2. **Acceptable CAC (customer acquisition cost).** Some businesses can spend up to 100% of LTV on acquisition (high-LTV recurring revenue, high-margin SaaS, financial services). Most service businesses operate in 20-40% of LTV. Goods businesses with COGS often need 10-20%.
3. **Acceptable CPL (cost per lead).** Acceptable CAC ÷ your lead-to-customer conversion rate.

### Common small-budget mistake

Strategist convinces themselves they should pay $20/lead because that "feels right." Real math says LTV is $2,000, conversion rate is 1-in-10, acceptable CAC is 25% of LTV ($500), acceptable CPL is $50. They were leaving 60% of headroom on the table.

### Counter-mistake

Strategist gets the LTV math right, blows budget on a campaign without proof of concept first. Establish that the campaign converts at small scale before authorizing a CPL ceiling that lets it scale.

### The principle

**Higher willingness to pay = wider audience the algorithm can fish from = more growth.** Capping CPL too low strangles the campaign before Andromeda finds the pockets that would convert.

---

## 9. Small-budget specific mechanics

If you're in the Tiny or Small tier, three Heath-derived mechanics matter more than usual:

### Hyper-niche the ICP

Don't try to compete for broad market against bigger competitors. Pick the 1-5% slice of the market you can serve best, and re-engineer messaging to speak only to them. Most small-budget failures aren't budget failures — they're identity failures (trying to be everything to everyone with $50/day).

### Mine the Meta Ads Library

Free tool. Search competitors. Find ads that have been running for 6+ months — those are proven winners. Pass them to the Ideator skill as Input B (existing creative evidence). Model from them rather than re-discovering what works through expensive testing.

### Mine your own organic content

If you (or the client) have an Instagram or Facebook presence, look at which posts got disproportionate engagement. Those concepts already passed an organic A/B test for free. Pass them to the Ideator as concept seeds. Often the strongest small-budget creatives are organic posts with a CTA appended.

### Consolidate to one offer

Multi-offer fragmentation is the small-budget killer. If the client has multiple products or service tiers, pick the one with the best margin × highest conversion rate × clearest ICP and run that. Add others only after the primary offer is profitable and scaling.

---

## 10. When to consult the methodology vs. this doc

| Question | Doc |
|---|---|
| What lever should this ad pull? | `Meta-Ads_Methodology.md` §3 (frameworks) + §5 (vertical) |
| How do I write the headline? | `Meta-Ads_Methodology.md` §4 (funnel mapping) + Producer skill |
| How many creatives should I produce? | This doc §1 (budget tier) |
| Why are 27 of my 30 ads getting no reach? | This doc §5 (reach concentration) |
| When should I scale spend on a winner? | This doc §6 (scaling loop) |
| What's the right CPL for my campaign? | This doc §8 (CAC vs. LTV) |
| How do I generate 25 distinct concepts? | `Meta-Ads_Methodology.md` §3 (Three-Axis Articulation) + Ideator skill |
| Should I run a brand awareness campaign? | This doc §2 (no — skip awareness/engagement/traffic) |
| Why isn't this ad converting? | Critic skill (`Process/4-Critique/SKILL.md`) |

---

## Known gaps

- **Lookalike source heuristics.** Haynes recommends lookalikes from highest-value customers, qualified leads, leads-that-showed-up-to-calls, etc. Worth codifying which sources work best per vertical once we have ClearThink data.
- **Statistical significance calculator recommendation.** Heath references one but doesn't name a specific tool. Add a vetted recommendation when one is chosen.
- **Foundational campaign mechanics at scale tier.** When test campaign winners "graduate" to foundational, the budget allocation logic (what % of total budget goes to foundational vs. test) is open. Refine after first scale-tier client run.
- **Multi-language campaigns.** Heath references auto-translation; this doc doesn't yet cover when a separate per-language campaign vs. one campaign with auto-translation is the right call.
- **Retargeting structure.** Mentioned briefly under Tiny/Small tier (cap at 20-30%) but not detailed. Worth a dedicated subsection once we run real retargeting campaigns.

---

*End of Campaign Structure & Deployment.*
