# KPI Dictionary & Logic
## Delivery Operations & SLA Performance Analytics — Excel

This document standardizes the KPI logic used to interpret the workbook. The main
goal is to prevent denominator mixing between **order lifecycle status** metrics and
**delivery SLA** metrics.

---

## 1. Order population

### Total Orders

**Definition**

Distinct order records in the source dataset.

**Current result**

- 49,996 unique orders

**Denominator role**

Use Total Orders for lifecycle-status rates such as completion, cancellation,
delivering, and processing.

---

## 2. Lifecycle status KPIs

The four lifecycle statuses are treated as mutually exclusive in the current
dashboard.

| KPI | Numerator | Denominator | Current result |
| --- | --- | --- | ---: |
| Completion Rate | Completed orders | Total Orders | 80.16% |
| Cancellation Rate | Canceled orders | Total Orders | 6.84% |
| Delivering Rate | Delivering orders | Total Orders | 9.03% |
| Processing Rate | Processing orders | Total Orders | 3.96% |

The corresponding counts are:

- Completed: 40,077
- Canceled: 3,422
- Delivering: 4,515
- Processing: 1,982

These counts sum to 49,996, so the four status rates sum to approximately 100%.

### Important interpretation

A canceled or still-processing order should **not** automatically enter an
on-time/late-delivery denominator because it does not yet have a comparable final
delivery outcome.

---

## 3. Delivery SLA KPIs

### SLA-Eligible Delivered Orders

For on-time/late analysis, use only orders with the timestamps required to compare
actual delivery against the promised/estimated delivery date.

This population is conceptually different from Total Orders.

### On-Time Delivery Rate

**Definition**

Delivered orders meeting the promised/estimated delivery date divided by
SLA-eligible delivered orders.

**Current dashboard result**

- 60.37%

### Late Delivery Rate

**Definition**

Delivered orders exceeding the promised/estimated delivery date divided by
SLA-eligible delivered orders.

**Current dashboard result**

- 39.63%

### Reconciliation check

For the same filter context:

```text
On-Time Delivery Rate + Late Delivery Rate ≈ 100%
```

The current dashboard shows:

```text
60.37% + 39.63% = 100%
```

This is the main QA check separating SLA rates from lifecycle-status rates.

### Do not use

```text
Late orders / Total Orders
```

when the business question is delivery SLA compliance, because canceled,
processing, and undelivered orders would distort the denominator.

---

## 4. Time KPIs

### Average End-to-End Delivery Time

**Definition**

Average elapsed time from purchase to final delivery among orders with an actual
delivery timestamp.

**Current result**

- 112.61 hours
- 4.69 days

The Excel formula documented in the project returns blank when the final delivery
timestamp is missing, so incomplete lifecycle records should not be treated as
zero-hour deliveries.

### Average Late Duration

**Definition**

Average amount of time beyond the estimated/promised date among **late delivered
orders only**.

**Current dashboard result**

- approximately 89.79 hours

This should not be averaged across on-time orders as zeros because that answers a
different business question.

---

## 5. Delivery-stage KPIs

Current average stage times:

| Stage | Average time | Share of end-to-end time |
| --- | ---: | ---: |
| Confirmation | 6.51 h | 5.8% |
| Pickup preparation | 12.49 h | 11.1% |
| Transit | 25.09 h | 22.3% |
| Shipper / final mile | 68.52 h | 60.8% |
| End-to-end delivery | 112.61 h | 100% |

### Eligibility rule

A stage-duration average should include only rows with both timestamps required to
calculate that stage.

For a strict operational comparison, use a common completed-order population with
all required lifecycle timestamps whenever possible. Otherwise disclose that stage
averages may use different eligible row counts.

### Interpretation

The final-mile stage is the **largest observed component of lead time**.

This supports prioritizing final-mile diagnostics, but time share alone does not
prove the underlying root cause.

---

## 6. Customer rating KPIs

### Average Customer Rating

**Definition**

Average rating among orders with an observed customer review.

**Current result**

- 5.08 / 10

### Review Coverage

```text
18,022 reviewed orders / 49,996 total orders ≈ 36.0%
```

Therefore the rating KPI represents the reviewed subset, not the full order base.

When presenting customer-feedback insights, disclose the review coverage rather
than implying that review themes represent every customer.

---

## 7. Average Order Value

**Current result**

- 2,521.65

The repository does not document a currency label for this KPI, so do not add a
currency symbol unless it is verified from the source workbook/data.

The denominator should be orders with a valid order value. If canceled orders
carry order values in the source, state explicitly whether AOV is based on all
orders or completed orders.

---

## 8. KPI naming standard

Use management-readable labels on the dashboard:

| Current / technical label | Standard label |
| --- | --- |
| Orders | Total Orders |
| Delivery_time | Avg Delivery Time (h) |
| Late_ratio | Late Delivery Rate |
| On_time ratio | On-Time Delivery Rate |
| Canceled_ratio | Cancellation Rate |
| Delivering ratio | Delivering Rate |
| Processing ratio | Processing Rate |
| AVG_Score | Avg Rating (Reviewed Orders) |
| late_duration | Avg Late Duration (h) |

Avoid mixing snake_case / technical field names with presentation labels.

---

## 9. Recommended KPI QA checks

For every refresh/filter context:

1. Completed + Canceled + Delivering + Processing = Total Orders.
2. Lifecycle status rates sum to approximately 100%.
3. On-Time Rate + Late Rate = approximately 100% within the same SLA-eligible population.
4. Average Delivery Time excludes rows with missing final delivery timestamps.
5. Average Late Duration includes only late delivered orders.
6. Review count ≤ Total Orders and rating is calculated only on observed reviews.
7. Stage durations are non-negative and use documented timestamp boundaries.
8. Slicer changes update numerator and denominator together.

---

## 10. Why the denominator distinction matters

Two different questions require two different populations:

**Operations pipeline**

> What share of all orders are completed, canceled, delivering, or processing?

Use **Total Orders**.

**Delivery reliability**

> Of orders that reached a measurable delivery outcome, what share met the promised date?

Use **SLA-eligible delivered orders**.

Keeping these populations separate makes the dashboard more defensible for
Operations, Logistics, Supply Chain, and E-commerce interviews.
