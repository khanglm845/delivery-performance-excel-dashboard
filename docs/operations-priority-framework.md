# Operations Priority Framework
## Delivery Operations & SLA Diagnostic — Excel

This document translates the rebuilt analysis into an evidence-driven operating framework.

---

## 1. Network baseline

| KPI | Result |
| --- | ---: |
| Total Orders | 49,996 |
| Completion Rate | 80.16% |
| Cancellation Rate | 6.84% |
| SLA-Eligible Deliveries | 40,077 |
| On-Time Rate | 50.57% |
| Late Rate | 49.43% |
| Avg Delivery Time | 112.6 h |
| Avg Late Duration | 57.3 h |

---

## 2. Final mile is the primary diagnostic focus

Late orders take **60.4 hours longer** than on-time orders.

Of that gap:

- Confirmation: +0.3 h
- Pickup: +1.3 h
- Transit: +4.4 h
- **Final Mile: +54.4 h**

Final mile therefore contributes approximately **90%** of the observed lead-time difference between late and on-time deliveries.

### Action

Build a final-mile scorecard by:

- region
- province
- shipper
- route / lane if available
- peak vs normal period
- SLA-eligible volume
- final-mile hours
- Late Rate
- Late Orders

### Guardrail

This identifies where delay accumulates. It does not prove why.

---

## 3. Peak-period operating stress

Peak months are defined using a reproducible volume rule:

> monthly orders > 1.5× median monthly volume

Peak months:

- Nov 2022
- Dec 2022
- Jan 2023
- Nov 2023

Comparison:

| Metric | Normal | Peak | Difference |
| --- | ---: | ---: | ---: |
| Total Delivery | 107.1 h | 121.7 h | +14.6 h |
| Final Mile | 63.0 h | 77.7 h | +14.7 h |

The deterioration is concentrated almost entirely in final mile.

### Action hypothesis

Test pre-peak carrier / route capacity planning on the highest-exposure lanes.

Measure:

- final-mile hours
- Late Rate
- Late Orders
- backlog / delivering volume

---

## 4. Region: severity vs exposure

### Severity hotspots

| Region | Late Rate | Avg Delivery | Late Orders |
| --- | ---: | ---: | ---: |
| Northern Midlands & Mountains | 82.2% | 171.7 h | 1,966 |
| Central Highlands | 81.8% | 170.7 h | 1,498 |
| North Central Coast | 51.0% | 113.7 h | 532 |

These locations require targeted route / geography diagnosis.

### Exposure hotspots

| Region | Late Orders | Share of all late |
| --- | ---: | ---: |
| Southeast | 6,140 | 31.0% |
| Red River Delta | 4,817 | 24.3% |

Together:

> **55.3% of all late deliveries**

### Management rule

Do not choose between rate and volume.

Use two workstreams:

1. **Severity workstream** — fix structurally poor service regions.
2. **Exposure workstream** — reduce the largest absolute number of late deliveries.

---

## 5. Category: severity vs exposure

### Severity

- Sports: 73.0%
- Automotive: 72.7%
- Garden: 71.9%
- Home: 60.8%
- Toys: 60.7%

### Exposure

- Fashion: 4,602 late orders
- Home: 4,264
- Beauty: 3,563

Fashion + Home + Beauty:

> **62.7% of all late deliveries**

### Strongest combined signal

**Home**

- 60.8% Late Rate
- 4,264 late orders
- 21.5% of all late deliveries

### Action

Cross-tab Home/Toys by:

- region
- seller
- shipper
- route / fulfillment source if available

Do not infer product-weight or handling root causes without additional evidence.

---

## 6. Shipper diagnostic must control for geography

A raw carrier leaderboard is confounded by region.

Example:

Central Highlands baseline Late Rate:

- **81.8%**

Shippers operating there show similarly high raw late rates, so poor raw performance is not sufficient evidence of carrier-specific underperformance.

The workbook benchmarks shipper-region pairs against their local regional baseline and screens only pairs with at least **100 SLA-eligible orders**.

Current descriptive flags:

| Shipper | Region | Late Rate | Regional Baseline | Gap |
| --- | --- | ---: | ---: | ---: |
| 164 | Southeast | 57.4% | 43.9% | +13.5 pp |
| 41 | Southeast | 54.1% | 43.9% | +10.2 pp |

The ±10 pp threshold is a screening rule, not statistical significance.

### Action

Audit:

- route mix
- workload
- handoff timing
- exception handling
- final-mile duration

before making carrier-allocation decisions.

---

## 7. Customer feedback

Review coverage:

- **36.0%**

Therefore complaint themes are diagnostic, not population-wide evidence.

Recommended follow-up:

> review theme × SLA outcome × late duration × region × category × shipper

---

## 8. Scenario planning

At current volume, a **5 pp absolute improvement in Late Rate** implies approximately:

| Scope | Potential late deliveries avoided |
| --- | ---: |
| Network | 2,004 |
| Southeast + Red River Delta | 1,248 |
| Home + Toys | 530 |

Use this to communicate scale, not to claim expected realized savings.

---

## 9. Recommendation standard

Every recommendation must specify:

1. **Evidence**
2. **Working hypothesis**
3. **Action / test**
4. **Success KPI**

Example:

Weak:

> Add more shippers in Central Highlands.

Stronger:

> Central Highlands shows an 81.8% Late Rate and ~171-hour average delivery time, while shipper-level performance is close to the local baseline. Diagnose route structure and local final-mile constraints first; only test capacity expansion if delays concentrate in capacity-limited lanes. Measure Late Rate, Avg Late Duration, and final-mile hours.
