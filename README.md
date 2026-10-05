# Delivery Operations & SLA Diagnostic — Excel

An Excel-only operations analytics case study built from **49,996 order-level records**.  
The project was rebuilt from raw data around a management storyline:

> **What happened → Why → So what → Now what**

Rather than treating the workbook as a dashboard-only project, the analysis validates KPI logic first, diagnoses where delivery failure accumulates, separates **severity** from **business exposure**, and converts findings into measurable operational actions.

> **Period:** May 2022–December 2023  
> **Orders:** 49,996 unique orders  
> **Geography:** 62 provinces / 7 economic regions  
> **Products:** 10 categories / 70 products  
> **Network:** 999 sellers / 155 shippers / 9,928 customers  
> **Reviews:** 18,022 (~36.0% coverage)  
> **Tool:** Microsoft Excel only

📊 [Excel workbook](Project.xlsx)  
📘 [KPI dictionary](docs/kpi-dictionary.md)  
🎯 [Operations priority framework](docs/operations-priority-framework.md)  
🧭 [Workbook structure & QA guide](docs/workbook-structure.md)

---

## Executive Story

### What happened?

The order lifecycle appears relatively healthy at first glance:

| KPI | Result |
| --- | ---: |
| Total Orders | 49,996 |
| Completed Orders | 40,077 |
| Completion Rate | 80.16% |
| Canceled Orders | 3,422 |
| Cancellation Rate | 6.84% |

But completion does not mean the promised date was met.

Among **40,077 SLA-eligible completed deliveries**:

- **20,265 were on time — 50.57%**
- **19,812 were late — 49.43%**
- Average end-to-end delivery time: **112.6 hours**
- Average lateness among late deliveries: **57.3 hours**

The core operating issue is therefore **delivery reliability**, not simply whether orders eventually complete.

---

## Why did deliveries miss the promised date?

The strongest diagnostic comes from comparing late versus on-time orders.

| Stage | On-Time Avg | Late Avg | Gap |
| --- | ---: | ---: | ---: |
| Confirmation | 6.4 h | 6.7 h | +0.3 h |
| Pickup | 11.9 h | 13.1 h | +1.3 h |
| Transit | 22.9 h | 27.3 h | +4.4 h |
| **Final Mile** | **41.6 h** | **96.0 h** | **+54.4 h** |
| **Total Delivery** | **82.8 h** | **143.1 h** | **+60.4 h** |

**Final mile contributes ~90% of the observed late-vs-on-time lead-time gap.**

This is stronger than simply noting that final mile is the largest stage. It shows that the stage is the main differentiator between successful and late SLA outcomes.

### Peak-period stress

Peak months are defined as monthly order volume above **1.5× the median month**:

- November 2022
- December 2022
- January 2023
- November 2023

During those periods:

- End-to-end delivery: **121.7 h vs 107.1 h** in normal months
- Final mile: **77.7 h vs 63.0 h**

Nearly all of the **+14.6 h** peak-period deterioration appears after carrier handoff.

This supports a **final-mile capacity / routing stress hypothesis**, but does not by itself prove the underlying cause.

---

## So what? Severity is not the same as business impact

### Regional view

The worst SLA-rate regions are not the largest sources of late deliveries.

| Region | SLA Eligible | Late Orders | Late Rate | Share of Late Orders |
| --- | ---: | ---: | ---: | ---: |
| Southeast | 13,981 | 6,140 | 43.9% | 31.0% |
| Red River Delta | 10,971 | 4,817 | 43.9% | 24.3% |
| South Central Coast | 4,940 | 2,471 | 50.0% | 12.5% |
| Mekong River Delta | 4,917 | 2,388 | 48.6% | 12.1% |
| Northern Midlands & Mountains | 2,393 | 1,966 | 82.2% | 9.9% |
| Central Highlands | 1,832 | 1,498 | 81.8% | 7.6% |
| North Central Coast | 1,043 | 532 | 51.0% | 2.7% |

Northern Midlands & Mountains and Central Highlands are clear **severity hotspots**, but together contribute only **17.5%** of late deliveries.

By contrast, Southeast + Red River Delta contribute **55.3% of all late deliveries** despite below-network late rates.

This creates two different workstreams:

- **Severity reduction:** difficult geographies with extreme SLA failure
- **Exposure reduction:** high-volume markets where small percentage improvements can remove many late orders

---

## Category prioritization

The same logic applies to product categories.

| Category | Late Orders | Late Rate | Share of Late Orders |
| --- | ---: | ---: | ---: |
| Fashion | 4,602 | 42.7% | 23.2% |
| Home | 4,264 | 60.8% | 21.5% |
| Beauty | 3,563 | 42.7% | 18.0% |
| Toys | 2,179 | 60.7% | 11.0% |
| Electronics | 1,315 | 41.2% | 6.6% |
| Food | 1,044 | 43.1% | 5.3% |
| Sports | 910 | 73.0% | 4.6% |
| Books | 813 | 41.4% | 4.1% |
| Automotive | 576 | 72.7% | 2.9% |
| Garden | 546 | 71.9% | 2.8% |

Fashion + Home + Beauty generate **62.7% of all late deliveries**.

**Home** is the strongest Severity × Exposure signal: **60.8% late rate** while also contributing **21.5% of all late deliveries**.

The data does not support claiming that product size, weight, or handling complexity causes these differences. Those remain hypotheses for follow-up analysis.

---

## Region-adjusted shipper diagnostic

A raw carrier leaderboard can be misleading because some shippers operate in structurally difficult regions.

Example:

- Shippers in Central Highlands show ~81–84% late rates, but the **regional baseline itself is 81.8%**.
- Their poor raw performance therefore appears largely consistent with local operating conditions.

After benchmarking shipper performance within region and requiring at least **100 SLA-eligible orders**, two Southeast shipper-region combinations stand out:

| Shipper | SLA Eligible | Late Rate | Region Baseline | Gap |
| --- | ---: | ---: | ---: | ---: |
| 164 | 242 | 57.4% | 43.9% | **+13.5 pp** |
| 41 | 231 | 54.1% | 43.9% | **+10.2 pp** |

The ±10 pp rule is a **descriptive screening threshold**, not a statistical significance test.

---

## Now what?

Recommendations are structured as:

> **Evidence → Working hypothesis → Action / test → Success KPI**

| Priority | Evidence | Action / Test | Success KPI |
| --- | --- | --- | --- |
| Final-mile reliability | 90% of late-vs-on-time time gap occurs in final mile | Build route/shipper/region final-mile scorecard; test peak capacity/routing intervention | Final-mile hours, Late Rate, Late Orders |
| Regional severity | Northern / Central Highlands >81% late | Diagnose province, route, handoff and capacity constraints before changing service promise | Regional Late Rate, Avg Late Duration |
| High-volume markets | Southeast + Red River Delta = 55.3% of late deliveries | Focus scalable process improvement on highest-volume lanes | Absolute Late Orders + Late Rate |
| Category priority | Home = 60.8% late and 21.5% of late deliveries | Cross-tab seller/region/shipper mix before product-handling hypotheses | Category Late Orders + Late Rate |
| Carrier screening | Shipper 164 +13.5 pp; Shipper 41 +10.2 pp vs regional baseline | Audit route mix, workload, handoff timing and exception handling | Gap vs Region, Final-Mile Time |
| Customer feedback | Reviews cover only 36.0% of orders | Link feedback themes to SLA status and operational dimensions | Rating/theme by SLA outcome |

---

## Illustrative impact scenario

The workbook includes an editable sensitivity input—not a forecast.

At current volume, a **5 percentage-point absolute Late Rate improvement** would correspond to approximately:

- **2,004 fewer late deliveries** across the full network
- **1,248 fewer late deliveries** in Southeast + Red River Delta
- **530 fewer late deliveries** across Home + Toys

This scenario excludes intervention cost, mix changes, and behavioral effects.

---

## Critical KPI correction

The raw source contains lifecycle labels `success` and `late`, but these do **not** reliably encode SLA outcome.

Data QA found:

- **13,233 `success` orders were actually late by timestamp**
- **530 `late` orders were actually on time by timestamp**

Therefore:

- source `status` is used for **lifecycle outcome**
- SLA outcome is derived from **actual delivery timestamp vs estimated delivery timestamp**

This distinction materially changes the headline result from the legacy workbook.

---

## Workbook Structure

```text
00_Executive_Story
01_What_Happened
02_Why_Delays
03_Region_Analysis
04_Category_Analysis
05_Shipper_Diagnostic
06_Now_What
07_KPI_Dictionary
08_Data_QA
09_Data
10_Helper (hidden)
```

The workbook is intentionally structured as an analysis case study rather than a traditional two-page dashboard.

---

## Excel Skills Demonstrated

- Excel Tables / structured analytical layout
- formula-driven KPI logic
- timestamp arithmetic
- `IF`, `AND`, `COUNTIF(S)`, `FILTER`, lookup logic
- dynamic summary tables
- reconciliation / QA checks
- trend analysis
- process-stage decomposition
- Severity × Exposure prioritization
- conditional operational screening
- scenario analysis
- in-sheet charts
- management-facing analytical storytelling

---

## Analytical Guardrails

- Clustering or causal modeling is not used.
- Final-mile concentration is a diagnostic association, not proof of root cause.
- Peak-period deterioration is observational.
- Shipper comparisons should control for operating geography.
- Review findings apply only to the ~36% reviewed subset.
- Product-handling explanations require additional product-dimension data.
- The 5 pp impact scenario is a sensitivity calculation, not a forecast.

---

## Project Positioning

This project is designed for **Supply Chain, Logistics, Operations, E-commerce Operations, Merchandise, and Data Analyst** roles.

Its main value is not the dashboard itself. It demonstrates the ability to:

> validate metric logic → diagnose process performance → prioritize by business impact → translate analysis into measurable operational action.
