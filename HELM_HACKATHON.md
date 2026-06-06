# HELM — Hackathon brief

**Status:** June 6, 2026. Working toward one controlled demo/report. Static data is fine.

**One line:** Helm tells fabless AI chip companies **what capacity to lock and by when** — turning a 50-week supply black box into one actionable decision.

**Hackathon priority:** Build something real. One recommendation report beats validation theater.

---

## Product

**Not** a dashboard, data platform, or report you read for fun.

**Is** a **capacity brief**: public supply signals + customer inputs → **one recommendation** (action, deadline, $ at risk).

```
SOURCES (public, cited, dated)
  → INDICES (HBM / CoWoS / N3 tightness, 0–100)
    → GAP (demand vs committed capacity)
      → RECOMMENDATION
```

**Moat framing:** Decision you act on — not SemiAnalysis-style intel you read manually. Competes with Excel + email to the TSMC rep.

---

## Buyer

| | |
|---|---|
| **Role** | VP Ops / Head of Supply Chain; at &lt;100 people often **COO or technical co-founder** |
| **Company** | Series A–C **fabless AI chip** startup (accelerator / ASIC), ~50–300 people |
| **Examples** | Groq, Cerebras, Etched, Tenstorrent, d-Matrix, Rivos, Positron (stage archetype) |
| **Geo** | US first; also Israel, EU custom-silicon |
| **Today** | Spreadsheet at midnight + emails to foundry/OSAT reps chasing allocation |

**Not our buyer:** Nvidia, AMD, Intel, TSMC — planning armies and insider allocation. We sell to the **~80 challengers** who don't have that.

---

## Wedge

> We tell AI chip companies **what to produce, how much, and what foundry/packaging capacity to reserve** — before the supply window closes.

Customer-facing: *the planning brain for AI chip companies.*

---

## What we build today

**Minimum shippable:** one **HTML or PDF capacity brief** for a fixed scenario — real citations, controlled numbers, optional demand slider.

### Deliverable structure

**Page 1 — Recommendation (hero)**

```
ACTION: Lock additional 8,000 CoWoS-L slots + 3,500 N3 wafer starts
BY:     14 August 2026
WHY:    HBM + CoWoS binding constraints (both >85/100)
RISK:   ~$18.2M revenue at risk if ~4mo slip (40k units @ $4.2k ASP)
```

**Page 2 — Gap**

| | |
|---|---|
| 18mo demand (input) | 40,000 units |
| Committed capacity (input) | 12,000 equiv. |
| Gap | 28,000 |
| Bottleneck | HBM3E allocation |

**Page 3 — Signal table** (named sources + dates)

**Page 4 — Methodology** (3 bullets: indices from public data; bottleneck = worst link; not insider fab data)

### Demo scenario (pre-fill)

Series B inference ASIC · **N3 + CoWoS-L + HBM3E** · 40k unit plan · 12k committed.

**Demo beat:** drag demand slider → recommendation flips from HOLD to LOCK + deadline + $ at risk.

### Tech stack (hackathon)

- `signals.json` — 8–12 signals `{name, source, url, date, reading, tightness_contribution}`
- Template (HTML/PDF) — fills recommendation from JSON + 2 inputs (demand, committed)
- Rules engine — no ML required; optional LLM for prose polish only

**Model honesty:** Tightness indices are **transparent proxies** from public data — not a peek inside foundries. Say that if pushed.

---

## Data sources

Six buckets. Bake numbers once; cite source + date on every row.

### 1. Foundry & packaging (primary constraint)

| Source | Use |
|--------|-----|
| TSMC quarterly earnings + investor deck | Capex, advanced packaging revenue %, capacity commentary |
| [TrendForce — CoWoS capacity ramp](https://www.trendforce.com/news/2024/12/13/news-tsmc-ramps-up-cowos-capacity-across-taiwan-projected-to-nearly-triple-by-2026/) | ~35k → 90k wafers/mo trajectory |
| Trade press (CoWoS booked ~2 years, AP8/AP6 ramps) | Allocation window closing |
| Public allocation writeups (e.g. Silicon Analysts Q1 2026) | N3 fully booked; CoWoS 52–78wk lead times |

→ **`CoWoS_Tightness`** (0–100)

### 2. HBM / memory

| Source | Use |
|--------|-----|
| SK Hynix / Micron / Samsung earnings | HBM mix, capex, allocation language |
| TrendForce HBM/DRAM press releases | HBM3E allocation, price YoY |
| yfinance `000660.KS`, `MU`, `005930.KS` | 6mo momentum as price-confirms-scarcity |

→ **`HBM_Tightness`**

### 3. Leading-edge logic

| Source | Use |
|--------|-----|
| TSMC earnings | N3 utilization, ASIC/TPU demand |
| Public foundry allocation reports | “N3 fully booked” |

→ **`N3_Tightness`**

### 4. OSAT / substrate (tertiary — mention in report)

| Source | Use |
|--------|-----|
| ASE (`3711.TW`), Amkor (`AMKR`) earnings | Utilization, advanced packaging revenue |
| Sell-side notes via finance press | ABF substrate bottleneck |

→ **`Substrate_Tightness`** (optional fourth line)

### 5. Demand proxy (context, not customer order book)

| Source | Use |
|--------|-----|
| Hyperscaler capex (META, MSFT, GOOG earnings) | AI infra pull |
| NVIDIA datacenter revenue trend | Downstream accelerator demand |
| AI chip startup funding / launch activity | More challengers competing for same capacity |

→ **`Demand_Pressure`**

### 6. Customer inputs (only private layer)

- Target units (18 mo)
- Already committed wafer starts / CoWoS slots
- Stack: N3 + CoWoS-L + HBM3E
- ASP assumption (sensitivity range)

---

## Merge logic

**Normalize** each bucket to 0–100 tightness (document rules in appendix).

**Bottleneck** = `max(HBM_Tightness, CoWoS_Tightness, N3_Tightness)`

**Gap** = required capacity (from demand + yield assumption) − committed

**Recommend when** `gap > 0` AND `bottleneck ≥ 70` (tune thresholds for demo flip):

```
→ INCREASE_CAPACITY_COMMIT
→ deadline = today + ~6 weeks (when bottleneck ≥ 80)
→ revenue_at_risk = gap_fraction * demand * ASP
```

---

## Pitch (15 seconds → demo)

> "This is Helm — the planning brain for AI chip companies. Everyone not named Nvidia is flying blind on a 50-week supply black box. We tell them exactly what capacity to lock and by when. Here's a live brief built from this morning's public signals — watch what happens when demand runs hot."

*(slider or pre-filled scenario)*

---

## Today checklist

- [ ] `signals.json` with 8–12 cited signals (dated 6 Jun 2026 or latest available)
- [ ] One capacity brief (HTML or PDF) for demo scenario
- [ ] Optional: demand slider that flips HOLD → LOCK
- [ ] 3-slide deck: problem → brief demo → market (one slide)
- [ ] 30-name outreach list (post-hackathon; not blocking demo)

---

## Explicitly out of scope

- OEM / industrial buyers (Festo-type procurement)
- "All chips" or distributor catalog forecasting
- Nvidia / hyperscaler / CoreWeave as ICP
- Live TSMC API, user accounts, ERP integration
- Full dashboard or 12-chart analytics

---

## Open gaps (known, not blocking build)

- Founder-market fit: weak without ex-foundry / fabless ops advisor
- Customer evidence: none yet — demo manufactures credibility; written "when can I try it" is post-hackathon work
