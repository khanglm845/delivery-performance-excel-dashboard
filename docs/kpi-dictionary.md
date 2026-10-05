# KPI Dictionary & Logic
## Delivery Operations & SLA Diagnostic — Excel

This document defines the canonical metrics used by the rebuilt workbook.

The most important design choice is to separate **order lifecycle** from **delivery SLA outcome**.

---

## 1. Analytical grain

- 49,996 source rows
- 49,996 distinct `order_id`
- duplicate order IDs: 0

Therefore the analytical grain is:

> **one row = one order**

---

## 2. Lifecycle KPIs

Lifecycle status comes from the raw `status` field.

| KPI | Definition | Current result |
| --- | --- | ---: |
| Total Orders | all order records | 49,996 |
| Completed Orders | status in `success` or `late` | 40,077 |
| Completion Rate | Completed / Total | 80.16% |
| Canceled Orders | status = `canceled` | 3,422 |
| Cancellation Rate | Canceled / Total | 6.84% |
| Delivering Orders | status = `delivering` | 4,515 |
| Delivering Rate | Delivering / Total | 9.03% |
| Processing Orders | status = `processing` | 1,982 |
| Processing Rate | Processing / Total | 3.96% |

Reconciliation:

```text
Completed + Canceled + Delivering + Processing = 49,996
```

---

## 3. SLA eligibility

An order is SLA-eligible when:

1. it has reached a completed lifecycle outcome,
2. actual delivery timestamp exists,
3. estimated/promised delivery timestamp exists.

In this dataset all 40,077 completed orders are SLA-eligible.

---

## 4. SLA outcome

### On-Time

```text
actual delivery <= estimated delivery
```

Result:

- 20,265 orders
- **50.57%**

### Late

```text
actual delivery > estimated delivery
```

Result:

- 19,812 orders
- **49.43%**

Reconciliation:

```text
On-Time + Late = SLA-Eligible Delivered Orders
20,265 + 19,812 = 40,077
```

### Why source status is not used for SLA

QA identified:

- 13,233 `success` orders that are late by timestamp
- 530 `late` orders that are on time by timestamp

Therefore source `status` is retained only as a lifecycle field.

---

## 5. Time KPIs

### Avg End-to-End Delivery Time

```text
delivery_time - purchase_time
```

Population:

> SLA-eligible completed orders

Current result:

- **112.6 hours**

### Avg Late Duration

```text
delivery_time - estimated_delivery_time
```

Population:

> late delivered orders only

Current result:

- **57.3 hours**

On-time orders are excluded rather than filled with zero.

---

## 6. Delivery-stage KPIs

Timestamp boundaries:

| Stage | Formula concept | Avg |
| --- | --- | ---: |
| Confirmation | seller confirmation − purchase | 6.5 h |
| Pickup | pickup − seller confirmation | 12.5 h |
| Transit | carrier handoff − pickup | 25.1 h |
| Final Mile | delivery − carrier handoff | 68.5 h |
| End-to-End | delivery − purchase | 112.6 h |

All stage averages use the common SLA-eligible completed-order population.

### Late-vs-on-time diagnostic

| Stage | On-Time | Late | Gap |
| --- | ---: | ---: | ---: |
| Confirmation | 6.4 h | 6.7 h | +0.3 h |
| Pickup | 11.9 h | 13.1 h | +1.3 h |
| Transit | 22.9 h | 27.3 h | +4.4 h |
| Final Mile | 41.6 h | 96.0 h | +54.4 h |
| Total | 82.8 h | 143.1 h | +60.4 h |

Final mile accounts for approximately **90% of the observed total lead-time gap**.

---

## 7. Peak-period definition

Monthly median order volume:

- **1,954 orders**

Peak threshold:

```text
monthly orders > 1.5 × median
= 2,931 orders
```

Peak months:

- 2022-11
- 2022-12
- 2023-01
- 2023-11

This rule is data-driven and avoids manually selecting months after seeing the KPI outcome.

---

## 8. Regional / category prioritization

### Severity

Primary severity metric:

> **Late Delivery Rate**

Supporting severity metrics:

- Avg Late Duration
- Avg Delivery Time

### Exposure

Primary exposure metric:

> **Late Orders**

Supporting exposure metric:

- SLA-eligible volume

Decision-making uses both dimensions rather than ranking by percentage alone.

---

## 9. Review KPIs

Observed reviews:

- 18,022

Review coverage:

```text
18,022 / 49,996 = 36.0%
```

Average rating:

- **5.1 / 10**

Rating insights apply only to reviewed orders.

---

## 10. Scenario metric

Illustrative avoided late deliveries:

```text
SLA-eligible volume × assumed absolute Late Rate improvement
```

The default workbook input is:

- **5.0 percentage points**

This is a sensitivity calculation, not a forecast.

---

## 11. QA rules

Before publishing refreshed analysis:

1. Total rows = distinct order IDs.
2. Duplicate order IDs = 0.
3. Lifecycle counts reconcile to Total Orders.
4. On-Time + Late = SLA Eligible.
5. SLA result is timestamp-derived, not source-status-derived.
6. Stage durations are non-negative.
7. Completed outcomes have delivery timestamps.
8. Non-completed outcomes do not have final delivery timestamps.
9. Review coverage is shown whenever ratings are interpreted.
10. Scenario outputs are labeled as sensitivity, not forecast.
