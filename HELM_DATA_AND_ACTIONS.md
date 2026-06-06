# HELM — Data Sources & Recommended Actions (Build Spec)

Companion to `PROJECT_HELM.md`. This is the "what data in, what decision out" spec to build from.

---

## Core principle
**Forecast is the INPUT. The action is the PRODUCT.**
Every external source collapses to a normalized time-series signal → signals blend into the pressure index → the index meets the customer's *own* position → out comes a specific action with a dollar figure and a traceable reason. Nothing is vibes; everything traces back to a number.

```
[External signals]  +  [Customer internal data]  ->  [Forecast]  ->  [Recommended action + $ + confidence]
  (supply weather)        (their order book)          (the gap)        (what to do this week)
```

---

## PART 1 — Data we collect

### A. External signals (public — what we scrape)

| Category | Source | Access | Becomes (quantified) | Hackathon-ready |
|---|---|---|---|---|
| Equity momentum | TSMC, SK Hynix, Micron, Samsung, ASML, AMAT, Lam, KLA, NVDA, AMD, AVGO, MRVL | yfinance (free) | % change, volatility, z-score | ✅ done |
| Memory spot/contract price | DRAM / NAND / HBM | TrendForce / DRAMeXchange (partly paid) | $ price index, YoY | ⚠️ partial |
| Capex & fundamentals | Foundry/memory capex, inventory days, purchase commitments, guidance | SEC EDGAR API (free, XBRL) | $ capex, inventory-days, YoY delta | ✅ |
| Earnings-call language | Transcripts of suppliers + buyers | FMP / API Ninjas (free tier) → LLM | 0–10 "tight vs expanding" score | ✅ |
| Trade flows | Taiwan + South Korea monthly semiconductor exports | Govt sites (free, scrape) | export volume YoY (leading indicator) | ✅ |
| Macro | Semiconductor PPI, electronics inventory/sales, industrial production | FRED API (free) | indexed series | ✅ |
| News + sentiment | Global news tone on "shortage/allocation/capacity" | GDELT API (free) | tone score + event counts over time | ✅ |
| Demand (forward) | Hyperscaler capex (MSFT/GOOG/AMZN/META), GPU rental prices, CHIPS/EU grants, fab job postings | Filings, vast.ai API, gov announcements | $ capex, $/GPU-hr, MW, headcount | ✅ partial |
| Alt-data (moat, later) | Satellite fab-construction, customs bill-of-lading, distributor lead-time feeds, grid interconnection queues | Planet / Panjiva / ImportGenius (paid) | progress %, shipment counts, lead-time wks | ❌ post-hackathon |

### B. Internal signals (from the customer — the personalization layer)
Collected once they're a customer; this is the lock-in.
- Order book / demand pipeline (units by SKU, by customer)
- Committed capacity (wafer-starts, CoWoS slots, HBM allocation already secured)
- BOM + long-lead component list
- Current inventory / safety stock
- Target margins and customer commitments (design wins)

**The magic = fusing external supply tightness with the customer's specific position.** External data alone is a market report (commodity). External × internal = *their* decision (defensible, sticky).

---

## PART 2 — Signal → index → forecast (the pipeline)
1. **Ingest** each source on a schedule.
2. **Normalize** each to a comparable scale (z-score / 0–10) and align to a monthly timeline.
3. **LLM layer** turns unstructured text (calls, news) into scores.
4. **Blend** into the **Supply Pressure Index** (weighted; weights tunable, backtested).
5. **Project** the customer's demand vs. their committed capacity → the **gap** by quarter, by component.

---

## PART 3 — The ACTIONS we recommend (the product)

A fabless AI chip company controls these supply levers. Helm recommends across all of them:

| # | Lever | Example recommendation |
|---|---|---|
| 1 | Wafer-starts | "Pre-book 1,500 N3 wafer-starts now (47-wk lead) — protects $38M Q3 revenue." |
| 2 | Advanced packaging (CoWoS) | "Reserve +12% CoWoS slots this week; packaging is the binding constraint." |
| 3 | HBM procurement | "Raise HBM3E 12-hi order 8%; SK Hynix allocation tightening (+281%/6mo)." |
| 4 | Long-lead components | "Add 3 weeks substrate buffer — lead-time volatility rising." |
| 5 | Safety stock | "Hold 2 wks extra finished buffer on N1; supply variance high." |
| 6 | Demand commitments | "Cap new design-win promises at 28k units this quarter — can't be supplied." |
| 7 | Pricing | "Raise N1 list price 6%; demand +14% over capacity — capture margin, ration scarce supply." |
| 8 | Second-sourcing | "Qualify Amkor as backup packaging — single-source risk at pressure 9.9." |

### Every recommendation carries 4 fields + a reason
- **What** (the action) · **How much** (quantity) · **By when** (timing/window) · **$ impact** (protected or at-risk)
- **Show-your-work chain:** which signals triggered it (e.g., "memory momentum + spot price + allocation language in last call"). This traceability is what makes Helm bulletproof, not a black box.

### Output tiers (roadmap)
1. **Forecast** — demand-vs-capacity gap by quarter/component. *(foundation)*
2. **Decision** — the lever recommendations above, with $ and timing. *(the product)*
3. **Autopilot** — auto-drafts the PO / capacity reservation, routes to procurement; **human approves**. *(the vision — "planners stay in charge")*

---

## PART 4 — Bulletproofing
- **Explainability:** never output a number without its inputs. Every action links to its signals.
- **Confidence score:** attach a % to each recommendation; low-confidence → flag as "watch," not "act."
- **Honesty about the model:** the pressure index is a transparent proxy from public signals, **not** a peek inside foundries. Say so. Explainable beats black-box.
- **Backtest everything:** show the index would have flagged the last crunch early. Re-run as new data lands.
- **Human-in-the-loop:** Helm recommends; the customer commits. This is both safer and an easier sell.

---

## Hackathon build order (fastest path to a credible demo)
1. yfinance ✅ → momentum + pressure index (done)
2. GDELT → quantified news sentiment line
3. SEC EDGAR → capex + inventory deltas
4. One earnings-transcript API → LLM tightness score
5. Fuse → index → meet a sample customer's gap → output 2–3 ranked actions with $ + reason
