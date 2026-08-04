# Delivery Performance Analytics Dashboard in Excel

## Project Overview

This project analyzes the operational performance of a delivery company using Microsoft Excel. Starting from a raw order-level dataset, I performed data validation, handled missing values, created analytical features with Excel formulas, summarized the data using PivotTables, and built two interactive dashboards.

The project focuses on delivery efficiency, order status, regional performance, product-category performance, customer feedback, and operational bottlenecks.

## Business Objectives

The analysis was designed to answer the following questions:

- How many orders were completed, canceled, processing, or still being delivered?
- What is the average end-to-end delivery time?
- Which delivery stage contributes the most to total lead time?
- Which regions and product categories have the highest delivery delays?
- How does operational performance change across months and years?
- What customer complaints appear most frequently?
- Which areas should the company prioritize to improve delivery performance?

## Dataset

The dataset contains **49,996 unique delivery orders** from **May 2022 to December 2023**.

It includes information about order lifecycle timestamps, order status, customers, sellers, shippers, products, product categories, provinces, economic regions, estimated and actual delivery dates, and customer feedback.

### Dataset Summary

| Metric | Value |
|---|---:|
| Orders | 49,996 |
| Original columns | 24 |
| Final columns | 37 |
| Provinces | 62 |
| Economic regions | 7 |
| Product categories | 10 |
| Products | 70 |
| Sellers | 999 |
| Customers | 9,928 |
| Shippers | 155 |
| Analysis period | May 2022–December 2023 |

## Tools and Excel Features

- Microsoft Excel
- Excel Tables
- Structured-reference formulas
- IF and ISBLANK functions
- Data filtering and validation
- PivotTables and PivotCharts
- Slicers
- KPI cards
- Interactive dashboards

## Project Workflow

### 1. Data Validation and Cleaning

The raw dataset was reviewed for duplicate order IDs, missing timestamps, missing shipper information, missing customer reviews, inconsistent order statuses, and data-type issues.

All **49,996 order IDs were unique**.

Missing values were not automatically replaced with zero because many blanks represented valid stages in the order lifecycle. For example, canceled orders may not have delivery timestamps, while orders still being delivered do not yet have a final delivery time.

### 2. Feature Engineering

I created 13 analytical columns to convert raw operational data into measurable KPIs:

- `total_delivery_time`
- `Is_orders`
- `Is_canceled`
- `Is_late`
- `Is_on_time`
- `Is_delivering`
- `Is_processing`
- `Is_completed`
- `confirm_time`
- `pickup_time`
- `transit_time`
- `shipper_time`
- `late_duration`

Example formula for calculating total delivery time in hours:

```excel
=IF(
    ISBLANK(data[[#This Row],[delivery_time]]),
    "",
    (data[[#This Row],[delivery_time]]
    -data[[#This Row],[purchase_time]])*24
)
```

Binary indicator columns were created to make order statuses easier to aggregate in PivotTables.

### 3. Data Aggregation

The workbook contains approximately **30 PivotTables** that summarize performance by year, month, economic region, province, product category, product, order status, delivery stage, customer rating, and review description.

### 4. Dashboard Development

Two interactive Excel dashboards were created.

#### Overview Dashboard

The overview dashboard provides management-level KPIs such as total orders, completion rate, cancellation rate, processing rate, delivering rate, average delivery time, late-delivery ratio, average customer rating, monthly order volume, and regional performance.

#### Detail Dashboard

The detailed dashboard provides deeper analysis of delivery-stage lead times, product-category performance, regional performance, customer review categories, order-status distribution, and monthly operational trends.

The dashboards include slicers for year, month, and economic region.

## Key Performance Indicators

| KPI | Result |
|---|---:|
| Total orders | 49,996 |
| Completed orders | 40,077 |
| Completion rate | 80.16% |
| Canceled orders | 3,422 |
| Cancellation rate | 6.84% |
| Delivering orders | 4,515 |
| Delivering rate | 9.03% |
| Processing orders | 1,982 |
| Processing rate | 3.96% |
| Average total delivery time | 112.61 hours |
| Average total delivery time | 4.69 days |
| Average order value | 2,521.65 |
| Customer reviews | 18,022 |
| Average customer rating | 5.08/10 |

## Key Findings

### 1. Final-Mile Delivery Was the Main Bottleneck

| Delivery Stage | Average Time | Share of Total Time |
|---|---:|---:|
| Order confirmation | 6.51 hours | 5.8% |
| Pickup preparation | 12.49 hours | 11.1% |
| Transit to carrier | 25.09 hours | 22.3% |
| Shipper/final-mile delivery | 68.52 hours | 60.8% |
| Total delivery time | 112.61 hours | 100% |

The final-mile delivery stage accounted for approximately **61% of the total delivery cycle**, making it the largest operational bottleneck.

### 2. Delivery Performance Varied Significantly by Region

| Economic Region | Average Delivery Time | Late Rate Among Delivered Orders |
|---|---:|---:|
| Northern Midlands and Mountains | 171.7 hours | 82.2% |
| Central Highlands | 170.7 hours | 81.8% |
| North Central Coast | 113.7 hours | 51.0% |
| South Central Coast | 112.0 hours | 50.0% |
| Mekong River Delta | 112.0 hours | 48.6% |
| Southeast | 102.9 hours | 43.9% |
| Red River Delta | 102.8 hours | 43.9% |

Although completion rates were relatively similar across regions, delivery speed and lateness varied considerably. This suggests that regional logistics capacity was a more significant issue than order completion itself.

### 3. Some Product Categories Had Higher Delivery Risk

| Product Category | Orders | Average Delivery Time | Late Rate |
|---|---:|---:|---:|
| Sports | 1,516 | 157.6 hours | 73.0% |
| Automotive | 989 | 154.4 hours | 72.7% |
| Garden | 945 | 155.1 hours | 71.9% |
| Home | 8,818 | 131.7 hours | 60.8% |
| Toys | 4,471 | 132.2 hours | 60.7% |
| Fashion | 13,413 | 100.5 hours | 42.7% |
| Beauty | 10,384 | 100.3 hours | 42.7% |
| Electronics | 3,951 | 100.0 hours | 41.2% |

Sports, Automotive, and Garden products had the highest delivery times and late-delivery rates. A possible explanation is that these categories may contain larger or more difficult-to-handle products, but this hypothesis requires additional data such as product weight and dimensions.

### 4. Peak Months Were Associated With Lower Performance

High-volume periods included November 2022, December 2022, January 2023, and November 2023. During these periods, completion rates decreased to approximately 78–79%, cancellation rates increased to nearly 9%, and average delivery time increased to approximately 120–124 hours.

This pattern suggests that logistics capacity may not have scaled effectively during peak periods.

### 5. Customer Feedback Highlighted Service and Delivery Problems

Common negative review themes included poor service, slow delivery, poor packaging, damaged products, broken products, and customers stating that they would not return.

This indicates that delivery performance and product handling may have directly affected customer experience.

## Business Recommendations

1. Prioritize final-mile delivery improvements because this stage accounts for most of the total lead time.
2. Increase delivery capacity and shipper coverage in high-risk regions.
3. Review delivery processes for Sports, Automotive, Garden, Home, and Toys products.
4. Improve demand and workforce planning before peak sales months.
5. Monitor shipper-level performance using delivery time, late rate, and completed-order volume.
6. Investigate packaging and handling processes for damaged-product complaints.
7. Separate operational KPIs by order lifecycle stage to ensure fair performance comparisons.
8. Create alert thresholds for regions, categories, or shippers with unusually high late-delivery rates.

## Repository Structure

```text
delivery-performance-excel-dashboard/
│
├── README.md
├── Project.xlsx
├── dashboard_images/
│   ├── overview-dashboard.png
│   └── detail-dashboard.png

```

## Skills Demonstrated

- Data cleaning and validation
- Missing-value analysis
- Feature engineering
- Operational KPI development
- PivotTable analysis
- Dashboard design
- Data visualization
- Business insight generation
- Data-quality assessment
- Analytical storytelling

