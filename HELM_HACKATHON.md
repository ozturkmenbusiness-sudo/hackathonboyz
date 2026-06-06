# HELM - Hackathon and Founding Brief

**Status:** June 6, 2026. Hackathon prototype in a **public repo**. Customer evidence: not yet.

**One line:** Helm tells fabless AI chip companies **what capacity to lock and by when** - turning a 50-week supply black box into one actionable decision.

**Hackathon priority:** Build something real. One recommendation report beats validation theater.

**Public-repo rule:** We ship in the open. Anything static, illustrative, or rule-of-thumb must be **labeled in the product** and **defensible in one sentence** if challenged. Never imply live foundry access, customer data, or TSMC/foundry partnership we do not have.

---

## Product

**Not** a dashboard, data platform, or report you read for fun.

**Is** a **capacity brief**: public supply signals + customer inputs -> **one recommendation** (action, deadline, $ at risk).

```
SOURCES (public, cited, dated)
  -> INDICES (HBM / CoWoS / N3 tightness, 0-100)
    -> GAP (demand vs committed capacity)
      -> RECOMMENDATION
```

**Moat framing:** Decision you act on, not SemiAnalysis-style intel you read manually. Competes with Excel + email to the foundry/OSAT rep.

---

## Wedge

> We tell AI chip companies **what to produce, how much, and what foundry/packaging capacity to reserve** - before the supply window closes.

Customer-facing: _the planning brain for AI chip companies._

---

## Buyer

|              |                                                                                     |
| ------------ | ----------------------------------------------------------------------------------- |
| **Role**     | VP Ops / Head of Supply Chain; at <100 people often **COO or technical co-founder** |
| **Company**  | Series A-C **fabless AI chip** startup (accelerator / ASIC), ~50-300 people         |
| **Examples** | Groq, Cerebras, Etched, Tenstorrent, d-Matrix, Rivos, Positron (stage archetype)    |
| **Geo**      | US first; also Israel, EU custom-silicon                                            |
| **Today**    | Spreadsheet at midnight + emails/calls to foundry/OSAT reps chasing allocation      |

**Not our buyer:** Nvidia, AMD, Intel, TSMC, hyperscalers, or CoreWeave. They have planning armies, insider allocation, or enough leverage to build in-house. We sell to the **~80 challengers** who do not.

---

## Why It Hurts

**Demand hypothesis:** A chip company that misjudges CoWoS/HBM allocation slips product 3-6 months and can lose design wins worth tens of millions. Missing the order window is an existential, board-level event.

**But:** We have not yet seen a buyer be upset, pay, or panic. Compliments, "that's cool," and waitlists do not count.

**Status quo competitor:**

- A planner's **Excel model** + gut feel.
- **Emails and calls** to foundry/OSAT account reps chasing allocation and lead times.
- Expensive **market-intel reports** read manually.
- Hiring an **ex-foundry supply-chain person** and hoping their rolodex covers it.

Our job is to be 10x better than the spreadsheet, not to invent a need.

---

## Why Now

1. **LLMs can now read unstructured supply signals cheaply.** Parsing earnings calls, guidance, and reports into structured tightness signals was impractical/expensive in 2023; inference cost collapse makes "read everything, fuse it" viable.
2. **The allocation crisis is acute post-2023.** CoWoS/HBM constraints are now structural enough that public market, earnings, and trade-press signals matter.
3. **The customer base exploded.** Funded AI-chip challengers multiplied after 2023. The market to sell into did not exist at this size before.

---

## Validation Scorecard

| #   | Question           | Verdict                              |
| --- | ------------------ | ------------------------------------ |
| 1   | Wedge              | Strong                               |
| 2   | Buyer              | Strong                               |
| 3   | Demand             | Hypothesis - unproven                |
| 4   | Status quo         | Strong                               |
| 5   | Why now            | Strong                               |
| 6   | Founder-market fit | Weak - needs an advisor + interviews |
| 7   | Evidence           | None yet - go get one written "yes"  |

**Pass/fail:** We answer more than two honestly and well (1, 2, 4, 5). Keep building. **3, 6, and 7 are the work.**

### Founder-Market Fit

Weak. Background is **Vono (voice AI for tradespeople)**, not semiconductors. We have not personally lived chip supply-chain pain and do not currently have an unfair relationship with fabless ops leaders.

**Honest edge:** speed of building and a sharp data approach, not domain. That is not enough on its own.

**How to fix it:**

1. Recruit a semiconductor supply-chain advisor or co-founder: ex-foundry, ex-OSAT, or ex-fabless ops/procurement.
2. Do 20 customer interviews this week. Ask about their last allocation crunch, not about our idea.
3. In the pitch, be honest: "We're not chip veterans - we're builders who saw a $X problem and shipped a working tool in 9 hours. Here is our advisor, and here is what 20 ops leaders told us."

### Evidence Plan

Goal within ~7 days: one VP Ops / COO says, in writing, **"when can I try it?"** or **"can you do this for our N3 allocation?"**

1. Build a 30-name target list of VP Ops / COOs at fabless AI-chip startups.
2. Cold outreach with a 20-second Loom of the Helm demo.
3. Convert demand from hypothesis to a real, paying, panicking user.
4. Stretch: one paid pilot LOI.

---

## What We Build Today

**Minimum shippable:** one **capacity brief** for a fixed **illustrative scenario** - cited public sources where real, clearly marked synthetic inputs elsewhere, optional demand slider.

### Deliverable Structure

**Page 1 - Recommendation (hero)**

```
ACTION: Lock additional 8,000 CoWoS-L slots + 3,500 N3 wafer starts
BY:     14 August 2026
WHY:    HBM + CoWoS binding constraints (both >85/100)
RISK:   ~$18.2M revenue at risk if ~4mo slip (40k units @ $4.2k ASP)
```

**Page 2 - Gap**

|                            |                  |
| -------------------------- | ---------------- |
| 18mo demand (input)        | 40,000 units     |
| Committed capacity (input) | 12,000 equiv.    |
| Gap                        | 28,000           |
| Bottleneck                 | HBM3E allocation |

**Page 3 - Signal table** with named sources, dates, and tags.

**Page 4 - Methodology** with three bullets: indices from public data; bottleneck = worst link; not insider fab data.

### Demo Scenario

Series B inference ASIC, **N3 + CoWoS-L + HBM3E**, 40k unit plan, 12k committed.

**Demo beat:** drag demand slider -> recommendation flips from HOLD to LOCK + deadline + $ at risk.

---

## Public Disclosure

We post publicly. Separate three data classes. **Tag every field** in the brief and its underlying data.

| Class               | Tag                   | Meaning                                            | Example                                                       |
| ------------------- | --------------------- | -------------------------------------------------- | ------------------------------------------------------------- |
| **Verified public** | `source:public`       | Real citation, link, date; anyone can check        | TrendForce CoWoS ramp article; TSMC earnings line             |
| **Derived**         | `source:derived`      | Computed from verified public inputs; show formula | HBM tightness score from stock momentum + earnings keywords   |
| **Illustrative**    | `source:illustrative` | Scenario inputs for demo only; not a real customer | "ChipCo", 40k units, 12k committed, $4.2k ASP                 |

**Never tag illustrative data as public.** If a number is not traceable, it is illustrative.

### In-Product Copy

> **Hackathon prototype.** Supply signals cite public sources where noted. Customer scenario, gap math, and some index weights are **illustrative** to show the recommendation format - not a forecast for a real company or foundry allocation.

### README One-Liner

> Proof-of-concept built for AI BEAVERS June 2026. Demonstrates how public supply signals could fuse into one capacity decision. Not production forecasting software; no TSMC/foundry partnership; scenario data clearly labeled in the product.

### Say / Don't Say

| Don't say (public or pitch)             | Say instead                                                                 |
| --------------------------------------- | --------------------------------------------------------------------------- |
| "Live data from this morning"           | "Built from public sources cited in the brief" (only if actually refreshed) |
| "Real-time foundry intelligence"        | "Transparent proxies from public market and earnings data"                  |
| "Our customers" / "we forecasted for X" | "Illustrative scenario: a Series B fabless AI chip company"                 |
| "TSMC told us..."                       | "Public earnings and trade press indicate..."                               |
| "85/100 tightness" as fact              | "Model score 85/100 (derived from sources listed below)"                    |

### If Someone Pushes Back

Recover in one breath:

1. **Acknowledge:** "The scenario company and order book are illustrative - it is a hackathon demo."
2. **Anchor what's real:** "These six rows are public - here is the link and date."
3. **Point at the product:** "The product is the decision format: one action, deadline, $ at risk, from fused signals. Production version ingests real order books and refreshes sources on a schedule."
4. **Offer transparency:** "Every field carries a disclosure tag — public, derived, or illustrative — so you can see exactly what is cited vs. scenario."

Do not argue that illustrative numbers are "basically true." Either cite them or label them.

---

## Data Sources

Six buckets. For hackathon: compile once, cite source + date on every **public** row, and label **derived** and **illustrative** rows explicitly.

### 1. Foundry & Packaging

| Source                                                                                                                                                             | Use                                                      |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------- |
| TSMC quarterly earnings + investor deck                                                                                                                            | Capex, advanced packaging revenue %, capacity commentary |
| [TrendForce - CoWoS capacity ramp](https://www.trendforce.com/news/2024/12/13/news-tsmc-ramps-up-cowos-capacity-across-taiwan-projected-to-nearly-triple-by-2026/) | ~35k -> 90k wafers/mo trajectory                         |
| Trade press (CoWoS booked ~2 years, AP8/AP6 ramps)                                                                                                                 | Allocation window closing                                |
| Public allocation writeups (e.g. Silicon Analysts Q1 2026)                                                                                                         | N3 fully booked; CoWoS 52-78wk lead times                |

Output: CoWoS tightness index (0-100)

### 2. HBM / Memory

| Source                                  | Use                                     |
| --------------------------------------- | --------------------------------------- |
| SK Hynix / Micron / Samsung earnings    | HBM mix, capex, allocation language     |
| TrendForce HBM/DRAM press releases      | HBM3E allocation, price YoY             |
| Public equity performance (memory suppliers) | 6mo momentum as price-confirms-scarcity |

Output: HBM tightness index (0-100)

### 3. Leading-Edge Logic

| Source                            | Use                             |
| --------------------------------- | ------------------------------- |
| TSMC earnings                     | N3 utilization, ASIC/TPU demand |
| Public foundry allocation reports | "N3 fully booked"               |

Output: N3 tightness index (0-100)

### 4. OSAT / Substrate

| Source                                   | Use                                     |
| ---------------------------------------- | --------------------------------------- |
| ASE, Amkor earnings                      | Utilization, advanced packaging revenue |
| Sell-side notes via finance press        | ABF substrate bottleneck                |

Output: substrate tightness index (0-100, optional fourth line)

### 5. Demand Proxy

| Source                                        | Use                                          |
| --------------------------------------------- | -------------------------------------------- |
| Hyperscaler capex (META, MSFT, GOOG earnings) | AI infra pull                                |
| NVIDIA datacenter revenue trend               | Downstream accelerator demand                |
| AI chip startup funding / launch activity     | More challengers competing for same capacity |

Output: demand pressure index (0-100)

### 6. Customer Inputs

- Target units (18 mo)
- Already committed wafer starts / CoWoS slots
- Stack: N3 + CoWoS-L + HBM3E
- ASP assumption (sensitivity range)

---

## Recommendation Logic

Normalize each bucket to a 0-100 tightness score (document rules in the methodology section).

The bottleneck is whichever constraint scores highest among HBM, CoWoS, and N3.

Gap = required capacity (from demand + yield assumption) minus committed capacity.

Recommend increasing capacity commitment when gap is positive and the bottleneck score is high (tune thresholds so the demo flips convincingly). When triggered: set a deadline roughly six weeks out when the bottleneck is severe, and estimate revenue at risk from the gap fraction, demand volume, and ASP.

---

## Pitch

> "This is Helm - a planning brief for fabless AI chip companies. Everyone not named Nvidia is flying blind on 50-week allocation queues. We fuse public supply signals into one decision: what capacity to lock, and by when. This demo uses an illustrative scenario - the cited sources are real; drag demand to see how the recommendation changes."

Demo move: drag the slider or use the pre-filled scenario, then point at signal table citations and disclosure tags.

---

## Today Checklist

- [ ] Every data field tagged as public, derived, or illustrative.
- [ ] One capacity brief with disclosure footer.
- [ ] README disclaimer (see Public Disclosure).
- [ ] Optional: demand slider that flips HOLD -> LOCK.
- [ ] 3-slide deck: problem -> brief demo -> market/ask; slide 2 footnote "illustrative scenario".
- [ ] 30-name outreach list.

---

## This Week Checklist

- [ ] Recruit 1 semiconductor supply-chain advisor.
- [ ] Run 20 Mom-Test customer interviews.
- [ ] Cold outreach -> 1 written "when can I try it?"
- [ ] Convert demand from hypothesis to real buyer evidence.

---

## Explicitly Out of Scope

- OEM / industrial buyers (Festo-type procurement)
- "All chips" or distributor catalog forecasting
- Nvidia / hyperscaler / CoreWeave as ICP
- Live TSMC API, user accounts, ERP integration
- Full dashboard or 12-chart analytics

---

## Open Questions

- **Data freshness:** Do not claim "live data" unless sources were actually refreshed. Cite refreshed public data only when verified; otherwise label as illustrative or derived.
- **Company examples:** The examples are treated as stage archetypes, not customers or evidence.
