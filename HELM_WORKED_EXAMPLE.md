# HELM — Worked Example: One Real Order, In Real Numbers

Purpose: lock the scope. This is exactly what Helm computes for one customer, one quarter, with real parts, suppliers, prices, and lead times.

> **Sourcing note:** unit prices, suppliers, lead-time status, and the example company's chip specs are from public reporting (sources at bottom). Quantities, yields, and totals are **Helm-modeled estimates** built on those anchors — not the company's confidential data.

---

## The customer (real profile)
**A challenger like Etched** — maker of the **Sohu** transformer-inference ASIC.
- Process: **TSMC N4 (4nm)**
- Die: **~800 mm²** (reticle-limit)
- Memory: **144 GB HBM3E** (= 4 × 36GB 12-hi stacks per chip)
- Packaging: **CoWoS-L** (logic die + HBM on interposer + ABF substrate)
- Sold as: **8-chip server**
- Funding: **$625M raised, ~$5B valuation**
- Tell: **no public ship date 20+ months post-announcement** → supply/execution is the risk that defines them.

This is the bullseye buyer: tons of capital committed to silicon, a brutal multi-supplier ramp, and a small ops team.

---

## The Bill of Materials — 40,000-chip quarter

| Input | Spec | Supplier(s) | Unit price | Qty (40k chips) | Subtotal | % of BOM | Lead / status |
|---|---|---|---|---|---|---|---|
| Logic wafers | N4, 800 mm² die, ~45 good die/wafer | **TSMC** | ~$18,500/wafer (+10% YoY) | ~900 wafers | **$16.7M** | 14% | 3–4 mo cycle; book 1–2 Q ahead |
| HBM3E memory | 36GB 12-hi, 4 per chip | **SK Hynix** (primary), Micron, Samsung | ~$340/stack (→ ~$408 in 2026) | 160,000 stacks | **$54.4M** | **46%** | **SOLD OUT through 2026** |
| Advanced packaging | CoWoS-L interposer slot | **TSMC** (backup: ASE, Amkor) | ~$1,050/package | 40,000 | **$42.0M** | 36% | **FULLY BOOKED**, ~40+ wk |
| Substrate | 20-layer, 100×100 mm ABF (FC-BGA) | **Ibiden** (70–80% share), Unimicron, Shinko, AT&S | ~$120 ea (est.) | 44,000 | **$5.3M** | 4% | ~20+ wk |
| **TOTAL** | | | | | **~$118M** | 100% | ~$2,950/chip |

**Key truths this reveals:**
- **HBM is 46% of cost** — memory, not logic, drives AI-chip economics. (H100 ≈ $3,320 mfg; B200 ≈ $6,400, HBM ~45%.)
- **Wafers are only 14%** — the thing founders obsess over is the cheap part.
- **CoWoS-L is the binding constraint** — fully booked; it gates everything downstream.
- **The substrate is the sneaky killer** — 4% of cost, but a 20-week shortfall idles $100M+ of finished die.

---

## The planning nightmare (why Helm exists)
**Four scarce inputs. Four different lead times. All committed months before real demand is known.**

```
Order horizon (must commit BEFORE you know Q3 demand):
HBM3E      |==================== sold out through 2026 ====================|
CoWoS-L    |=============== ~40+ weeks, fully booked ===============|
N4 wafers  |======== ~3-4 mo cycle, book 1-2Q ahead ========|
ABF subst. |========= ~20+ weeks =========|
                                                          ^ you are here, guessing
```
Get any one wrong and you either **miss orders (lost revenue)** or **freeze cash in parts you can't use**.

---

## Helm's 6 recommendations — made concrete (this quarter)

1. **Wafer-starts —** Place **900 N4 wafer-starts now** (~45 good 800 mm² die/wafer → 40,000 dies). Under-ordering by 100 wafers = ~4,500 chips you can't recover this quarter.
2. **CoWoS-L slots (binding constraint) —** Reserve **44,000 slots immediately** (40k + 10% buffer). It's fully booked; without slots, your wafers and HBM are worthless.
3. **HBM3E (lock the price) —** Commit **160,000 stacks now** with SK Hynix primary + Micron secondary. Locking at ~$340 vs the announced 2026 ~$408 saves **~$10.9M** on this order alone.
4. **ABF substrate (cheap part, huge stall risk) —** Order **44,000 high-layer Ibiden substrates now**, qualify Unimicron as backup. $5.3M of substrate protects $100M+ of finished die.
5. **Safety stock —** Hold **2 weeks buffer on HBM + substrates** (high variance, pressure 9.9). Don't buffer wafers — that's cash you control.
6. **Second-source —** Qualify **ASE/Amkor** (packaging) and **Micron/Samsung** (HBM). At pressure 9.9, single-source = existential.

Every recommendation = **what · how much · by when · $ impact · which signal triggered it.**

---

## Why now (specific, 2026)
- HBM3E **sold out through 2026**; Samsung/SK Hynix raising prices **~20%** for 2026.
- TSMC **CoWoS-L and -S fully booked**; wafer prices up ~10% (N4 ~$18.5k).
- Number of funded challengers (Etched $625M, plus Groq/Cerebras/Tenstorrent/d-Matrix...) exploded post-2023 — the buyer base now exists at scale.

## Sources
- ABF substrates / Ibiden share: nikhs.substack.com/p/ibiden-the-hidden-bottleneck-beneath ; digitimes ABF expansion (2025)
- HBM3E pricing & 2026 hikes: trendforce.com (Dec 2025) ; videocardz / ServeTheHome (SK Hynix 12-hi 36GB)
- CoWoS-L specs & booking: tomshardware (Super Carrier) ; trendforce (CoWoS fully booked, Dec 2025)
- Wafer pricing: tomshardware (TSMC +10% 2025) ; siliconanalysts.com wafer-pricing
- AI-chip BOM (H100/B200): siliconanalysts.com cost-bridge / B200 breakdown
- Etched Sohu specs/funding: techpowerup ; spheron.network ; jonpeddie.com
