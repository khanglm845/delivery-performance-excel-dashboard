# Operations Priority Framework
## Delivery Performance Excel Dashboard

This document converts dashboard findings into an evidence-driven operations
prioritization framework.

The goal is to avoid generic recommendations such as “add more shippers everywhere”
and instead separate **severity**, **volume exposure**, and **diagnostic confidence**.

---

## 1. Network baseline

Current full-period dashboard baseline:

| KPI | Result |
| --- | ---: |
| Total Orders | 49,996 |
| Completion Rate | 80.16% |
| Cancellation Rate | 6.84% |
| Delivering Rate | 9.03% |
| Processing Rate | 3.96% |
| On-Time Delivery Rate | 60.37% |
| Late Delivery Rate | 39.63% |
| Avg End-to-End Delivery Time | 112.61 h |
| Avg Late Duration | ~89.79 h |

This baseline should be used as the comparison point when evaluating regions,
categories, months, or shippers.

---

## 2. Bottleneck hierarchy

Average stage time:

| Stage | Avg time | Share |
| --- | ---: | ---: |
| Confirmation | 6.51 h | 5.8% |
| Pickup preparation | 12.49 h | 11.1% |
| Transit | 25.09 h | 22.3% |
| Shipper / final mile | 68.52 h | 60.8% |

The shipper/final-mile stage is the largest observed lead-time component.

### Operational implication

Prioritize diagnostics at the final-mile stage first because it offers the largest
time pool to investigate.

However:

> 60.8% of lead time is evidence of concentration, not proof that shipper capacity
> is the root cause.

A follow-up shipper scorecard should compare:

- completed volume
- late-delivery rate
- average late duration
- average final-mile time
- region
- peak vs normal months

---

## 3. Regional prioritization: severity vs volume

A high late rate and a high number of late orders are different operational problems.

### A. Severity hotspots

The strongest regional severity signals are:

| Region | Orders | Avg Delivery | Late Rate | Avg Late Duration |
| --- | ---: | ---: | ---: | ---: |
| Trung du & miền núi phía Bắc | 2,998 | ~171.7 h | 65.6% | ~140.7 h |
| Tây Nguyên | 2,301 | ~170.7 h | 65.1% | ~138.9 h |

Both regions are far above the network baseline of:

- 112.61 h average delivery
- 39.63% late rate
- ~89.79 h average late duration

### Recommended action

Treat these regions as **service-severity hotspots**.

Investigate:

1. final-mile route length / coverage,
2. shipper availability,
3. handoff waiting time,
4. province-level concentration,
5. whether performance deteriorates further in peak periods.

Do not immediately assume “insufficient shipper coverage” without shipper- or
route-level evidence.

---

### B. Volume-exposure hotspots

High-volume regions can generate more total late deliveries even when their late
rate is closer to the network average.

Examples:

| Region | Orders | Late Rate | Completion Rate |
| --- | ---: | ---: | ---: |
| Đông Nam Bộ | 17,389 | 35.3% | 80.4% |
| Đồng bằng sông Hồng | 13,724 | 35.1% | 79.9% |

Using the displayed rounded rates only as a rough prioritization estimate:

```text
Estimated late delivered orders
≈ Total Orders × Completion Rate × Late Rate
```

produces approximately:

- Đông Nam Bộ: ~4.9k late delivered orders
- Đồng bằng sông Hồng: ~3.8k

These are not raw late-order counts and should be recalculated directly from the
workbook for operational reporting, but they illustrate why volume exposure matters.

### Recommended action

For these regions, prioritize **absolute late-order reduction** rather than treating
them as the worst SLA-rate regions.

A small improvement in a high-volume region may remove more late deliveries than a
large percentage improvement in a small region.

---

## 4. Product-category prioritization

### Severity view

Highest displayed category late rates:

| Category | Orders | Avg Delivery | Late Rate | Avg Late Duration |
| --- | ---: | ---: | ---: | ---: |
| Sports | 1,516 | 157.6 h | 60.0% | 128.2 h |
| Automotive | 989 | 154.4 h | 58.2% | 131.7 h |
| Garden | 945 | 155.1 h | 57.8% | 126.9 h |
| Toys | 4,471 | 132.2 h | 48.7% | 105.2 h |
| Home | 8,818 | 131.7 h | 48.4% | 103.7 h |

These categories are materially worse than the 39.63% network late-rate baseline.

### Diagnostic interpretation

The dashboard does **not** contain enough evidence to conclude that size, weight,
packaging complexity, or special handling causes the delay.

Those are follow-up hypotheses.

Recommended additional fields:

- product weight
- package dimensions
- fulfillment location
- carrier
- route distance
- service type

---

### Volume-impact view

Because category sizes differ greatly, moderate late rates can create high total
late volume.

Using displayed counts and rounded rates as a rough prioritization estimate:

- Fashion: roughly 3.7k late delivered orders
- Home: roughly 3.4k
- Beauty: roughly 2.9k

By comparison, Sports / Automotive / Garden have higher late rates but much lower
order volume.

### Recommended action

Use a two-axis category matrix:

```text
x-axis = completed / delivered volume
y-axis = late-delivery rate
```

Then classify categories into:

1. **High volume / high risk** → highest operations priority
2. **High volume / moderate risk** → scale-efficiency opportunity
3. **Low volume / high risk** → targeted root-cause investigation
4. **Low volume / low risk** → monitor

---

## 5. Peak-period evidence

High-volume periods identified in the current analysis include:

- November 2022
- December 2022
- January 2023
- November 2023

During peak periods, the project reports approximately:

- Completion Rate: 78–79%
- Cancellation Rate: close to 9%
- Avg Delivery Time: 120–124 h

Network baseline:

- Completion Rate: 80.16%
- Cancellation Rate: 6.84%
- Avg Delivery Time: 112.61 h

### Interpretation

Peak volume and weaker operational performance occur together.

This supports a **capacity-stress hypothesis**, but does not prove capacity is the
cause.

### Recommended action

Before the next peak period:

1. establish a peak baseline from historical high-volume months;
2. review shipper/route capacity in advance;
3. monitor cancellation and lead-time deviation from normal-month baselines;
4. create a weekly exception report during peak windows;
5. compare whether deterioration is concentrated by region, category, or shipper.

Success should be measured against the same peak-period baseline, not only against
annual averages.

---

## 6. Customer feedback

The workbook contains:

- 18,022 customer reviews
- average rating: 5.08 / 10
- review coverage: approximately 36.0% of total orders

Common negative themes include:

- poor service
- slow delivery
- packaging issues
- damaged/broken products
- customers saying they would not return

### Interpretation

These themes indicate areas for investigation.

They do not prove that operational delays directly caused all poor ratings because:

- reviews cover only ~36% of orders;
- the dashboard currently shows themes rather than causal analysis;
- product and service issues may overlap with logistics performance.

### Recommended action

Cross-tab review themes with:

- late vs on-time status
- late duration
- region
- category
- shipper

This would test whether negative feedback is disproportionately concentrated in
specific operational failure modes.

---

## 7. Operational action matrix

| Priority | Evidence | Action | KPI to monitor |
| --- | --- | --- | --- |
| Final-mile process | 68.52 h / 60.8% of lead time | Build shipper/final-mile scorecard | final-mile time, late rate, late duration |
| Severity regions | ~65% late; ~171 h delivery | route / carrier diagnostic | regional late rate, late duration |
| High-volume regions | largest estimated late-order exposure | reduce absolute late volume | late order count + rate |
| Sports / Auto / Garden | ~58–60% late | investigate product/route handling | category late rate, delivery time |
| Home / Fashion / Beauty | high volume exposure | prioritize scalable process fixes | late order count, volume |
| Peak months | delivery 120–124 h; cancel ~9% | pre-peak capacity planning | delivery time, cancel rate, backlog |
| Review themes | 36% review coverage | link feedback to operational failures | rating/review theme by SLA status |

---

## 8. Decision rule for recommendations

Every recommendation should answer four questions:

1. **What evidence triggered the action?**
2. **Is the problem high severity, high volume, or both?**
3. **What hypothesis are we testing?**
4. **Which KPI determines whether the action worked?**

Example:

Weak recommendation:

> Add more delivery staff in Tây Nguyên.

Stronger recommendation:

> Tây Nguyên shows a 65.1% late rate and ~170.7-hour average delivery time, both
> materially above the network baseline. Audit route- and shipper-level final-mile
> capacity first; if delays concentrate in under-covered routes, test targeted
> capacity expansion and measure late rate and average late duration before/after.

This wording separates **evidence**, **hypothesis**, **action**, and **measurement**.
