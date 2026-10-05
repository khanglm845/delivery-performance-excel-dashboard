# Workbook Structure & QA Guide
## Delivery Operations & SLA Diagnostic — Excel

The rebuilt workbook is an analysis case study, not a dashboard-first workbook.

---

## Sheet structure

### 00_Executive_Story

One-page management narrative:

- What happened
- Why
- So what
- Now what
- analytical guardrails

This is the recommended first sheet for recruiters and stakeholders.

### 01_What_Happened

Contains:

- lifecycle baseline
- SLA baseline
- monthly trend
- data-driven peak-month definition
- trend chart

Primary question:

> How reliable is the order lifecycle and promised-date delivery performance?

### 02_Why_Delays

Contains:

- late vs on-time stage decomposition
- stage contribution to total gap
- peak vs normal stage decomposition
- supporting charts

Primary question:

> Where does delivery delay accumulate?

### 03_Region_Analysis

Contains:

- region orders
- SLA-eligible volume
- Late Orders
- Late Rate
- Avg Delivery Time
- Avg Late Duration
- Late Order Share
- Severity × Exposure priority classification

Primary question:

> Which regions are severe hotspots versus high-impact exposure markets?

### 04_Category_Analysis

Same framework as region, applied to category.

Primary question:

> Which categories combine operational severity with meaningful business exposure?

### 05_Shipper_Diagnostic

Compares shipper-region pairs against local regional Late Rate.

Screening rules:

- minimum 100 SLA-eligible orders
- descriptive ±10 percentage-point comparison band

Primary question:

> Is poor shipper performance still visible after geography is controlled?

### 06_Now_What

Contains:

- evidence-driven action matrix
- working hypotheses
- recommended tests
- success KPIs
- editable 5 pp sensitivity scenario

### 07_KPI_Dictionary

Canonical definitions and current KPI values.

### 08_Data_QA

Contains:

- grain checks
- duplicates
- date range
- distinct dimensions
- review coverage
- timestamp sequence QA
- lifecycle / SLA consistency checks

Critical finding:

- 13,233 source `success` rows are late by timestamp
- 530 source `late` rows are on time by timestamp

### 09_Data

Raw source data.

No analytical overwrite should occur here.

### 10_Helper

Hidden analytical layer containing derived flags and durations.

---

## Final workbook QA checklist

Before publishing:

- [ ] 49,996 rows = 49,996 distinct order IDs
- [ ] duplicate order IDs = 0
- [ ] lifecycle counts reconcile to Total Orders
- [ ] On-Time + Late = 40,077 SLA-eligible deliveries
- [ ] Late Rate = 49.43%
- [ ] Avg Late Duration = 57.3 h
- [ ] source status is not used as SLA outcome
- [ ] late-vs-on-time final-mile gap = ~54.4 h
- [ ] final mile contributes ~90% of total gap
- [ ] peak-month definition remains >1.5× median monthly volume
- [ ] region/category tables include both rate and late-order count
- [ ] shipper comparison is region-adjusted
- [ ] review coverage is visible where customer feedback is discussed
- [ ] impact scenario is labeled as sensitivity, not forecast
- [ ] no formula errors
- [ ] helper sheet remains hidden
- [ ] raw data remains unchanged

---

## Storytelling standard

Chart and section titles should state conclusions rather than field names.

Prefer:

> Final Mile Drives 90% of the Late-vs-On-Time Lead-Time Gap

over:

> Average Time by Stage

Prefer:

> Southeast + Red River Delta Generate 55% of Late Deliveries

over:

> Orders by Region

The workbook should help a stakeholder move from evidence to decision, not simply inspect metrics.
