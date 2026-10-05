# Excel Dashboard Alignment Checklist
## Delivery Operations & SLA Performance Analytics

Use this checklist when updating `Project.xlsx` so the workbook and GitHub narrative
tell the same Operations Analytics story.

---

## 1. KPI card naming

### Overview / Detail cards

Replace technical labels with management-facing labels:

| Current label | Recommended label |
| --- | --- |
| Orders | **Total Orders** |
| Delivery_time | **Avg Delivery Time (h)** |
| Late_ratio | **Late Delivery Rate** |
| On_time ratio | **On-Time Delivery Rate** |
| Canceled_ratio | **Cancellation Rate** |
| Delivering ratio | **Delivering Rate** |
| Processing ratio | **Processing Rate** |
| AVG_Score | **Avg Rating (Reviewed Orders)** |

Use consistent title case and avoid mixing field-name syntax with business labels.

---

## 2. Keep lifecycle and SLA metrics visually separate

### Lifecycle group

Use:

- Completion Rate
- Cancellation Rate
- Delivering Rate
- Processing Rate

Subtitle / tooltip:

> denominator = all orders

### SLA group

Use:

- On-Time Delivery Rate
- Late Delivery Rate
- Avg Delivery Time
- Avg Late Duration

Subtitle / tooltip:

> denominator = delivered orders eligible for SLA comparison

This prevents a stakeholder from interpreting 39.63% Late Rate as 39.63% of all
49,996 orders.

---

## 3. Add two missing operational KPIs

### A. Late Order Count

A rate shows severity, but Operations also needs exposure.

Add a KPI:

> **Late Delivered Orders**

This should be a direct count from the underlying late flag, not an estimate from
rounded rates.

### B. Review Coverage

Add:

```text
Reviewed Orders / Total Orders
```

Current dataset:

```text
18,022 / 49,996 ≈ 36.0%
```

This provides context for the 5.08/10 rating KPI.

---

## 4. Reframe the stage-time visual

Current message:

> Final mile is the bottleneck.

Recommended title:

> **Average Lead Time by Delivery Stage**

Recommended insight callout:

> Shipper / final-mile time = 68.52 h, or ~60.8% of observed end-to-end lead time.

Add a footnote:

> Largest time component; root cause requires shipper/route-level diagnosis.

This is analytically stronger than calling the stage a confirmed root cause.

---

## 5. Region visual: add Severity × Volume logic

The current region table already contains:

- order volume
- avg delivery time
- late rate
- completion rate
- average late duration

Add a derived column / Pivot measure:

> Late Delivered Orders

Then sort or conditionally format using both:

- Late Delivery Rate
- Late Delivered Orders

### Priority interpretation

**Severity hotspots**
- Trung du & miền núi phía Bắc
- Tây Nguyên

**Volume exposure**
- Đông Nam Bộ
- Đồng bằng sông Hồng

The strongest management view is a scatter or four-quadrant chart:

```text
X = delivered volume
Y = late-delivery rate
Bubble size = late delivered orders (optional)
```

If the current Excel version cannot support a clean bubble chart with pivots,
retain the table and use conditional formatting for both rate and count.

---

## 6. Category visual: avoid ranking only by late rate

The current table shows strong severity in:

- Sports
- Automotive
- Garden

But high-volume categories such as:

- Fashion
- Home
- Beauty

can generate greater absolute late volume.

Add:

> Late Delivered Orders

and use a priority matrix or conditional-format table.

Do not label Sports/Automotive/Garden as difficult-to-handle products unless product
weight/dimension data is actually analyzed.

---

## 7. Peak-period monitoring

Current evidence:

- Nov 2022
- Dec 2022
- Jan 2023
- Nov 2023

show high volume together with weaker KPIs.

Add a simple monthly exception table:

| Month | Orders | Completion | Cancellation | Late Rate | Avg Delivery |
| --- | ---: | ---: | ---: | ---: | ---: |

Recommended conditional rules:

- highlight Cancellation > network baseline 6.84%
- highlight Avg Delivery > network baseline 112.61 h
- highlight Late Rate > network baseline 39.63%

These are baseline comparisons, not formal SLA targets.

---

## 8. Customer-feedback visual

Rename:

> Top 10 Customer's Feedback

to:

> **Top Customer Feedback Themes**

Add visible context:

> 18,022 reviews / ~36% order coverage

Avoid implying that feedback themes represent all customers.

Future diagnostic:

> Review theme × Late/On-Time × Region × Category × Shipper

---

## 9. Number formatting

Standardize:

- rates: `0.0%`
- hours: `0.0 h`
- days: `0.00 d`
- order counts: `#,##0`
- ratings: `0.00 / 10`
- AOV: `#,##0.00` until currency is verified

Avoid displaying long decimals such as:

```text
171.6790059
89.79130567
```

on management-facing tables.

---

## 10. Dashboard hierarchy

### Overview page

Recommended top row:

1. Total Orders
2. Completion Rate
3. Cancellation Rate
4. On-Time Delivery Rate
5. Late Delivery Rate
6. Avg Delivery Time

Recommended supporting visuals:

- monthly volume + completion trend
- region severity / exposure
- category volume
- review themes

### Detail page

Recommended sections:

**Process**
- stage lead times
- avg late duration

**SLA**
- late / on-time trend
- monthly exceptions

**Operational drivers**
- region table
- category table
- shipper scorecard if added

---

## 11. Excel QA checklist

Before publishing an updated workbook:

- [ ] Status counts reconcile to Total Orders
- [ ] Status rates sum to ~100%
- [ ] On-Time + Late = ~100% for SLA-eligible delivered orders
- [ ] Late-order count is direct from row-level flags
- [ ] Avg Delivery excludes blank delivery timestamps
- [ ] Avg Late Duration includes late orders only
- [ ] Review Coverage is shown beside Avg Rating
- [ ] Region/category tables show both late rate and late count
- [ ] Hours/percentages use consistent number formats
- [ ] No technical snake_case labels remain on dashboard cards
- [ ] Peak-period statements are presented as associations, not causal conclusions
- [ ] Dashboard screenshots are refreshed after edits
