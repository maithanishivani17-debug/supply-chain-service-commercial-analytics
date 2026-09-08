# Supply Chain Service & Commercial Performance Analytics

## SQL | Tableau | Supply Chain Analytics | Commercial Performance

![SQL](https://img.shields.io/badge/SQL-DuckDB-blue)
![Tableau](https://img.shields.io/badge/Tableau-Dashboard-orange)
![Supply Chain Analytics](https://img.shields.io/badge/Domain-Supply%20Chain-green)

---

## Project Overview

This project analyses supply chain delivery performance and commercial exposure using the **DataCo SMART Supply Chain dataset**.

The analysis focuses on a practical management question:

> **Where are the biggest supply chain performance gaps, what business dimensions are associated with them, and where should management prioritise improvement?**

SQL is used as the analytical and validation layer, while Tableau is used to communicate the results through management-focused dashboards.

The analysis moves from:

**Performance → Diagnosis → Commercial Exposure → Management Priorities**

---

# Business Problem

A high-level delivery KPI can show that a supply chain has a service-performance problem, but it does not explain where management should focus.

This project therefore investigates delivery performance across:

- Markets
- Regions
- Product categories
- Shipping modes
- Customer segments
- Time periods

The analysis also considers commercial exposure through:

- Realised sales
- Calculated profit proxy
- Profit margin
- Order volume
- Sales contribution

The objective is not simply to identify the highest late-delivery percentage, but to identify areas where service-performance gaps coincide with meaningful business exposure.

---

# Project Objectives

The analysis was designed to:

1. Establish reliable supply chain performance KPIs.
2. Measure order realisation and delivery reliability.
3. Identify whether delivery issues persist over time.
4. Compare delivery performance across markets and regions.
5. Analyse product-category performance.
6. Evaluate shipping-mode performance.
7. Assess customer-segment delivery and commercial exposure.
8. Connect operational performance with commercial significance.
9. Develop a management priority framework.
10. Translate the findings into practical management recommendations.

---

# Dataset

### DataCo SMART Supply Chain Dataset

The dataset contains:

- **180,519 order-item / transaction records**
- **53 raw columns**
- **65,752 distinct orders**
- **20,652 customers**

The transaction data covers approximately **January 2015 to January 2018**.

Key fields include:

- Order ID
- Order Item ID
- Customer Segment
- Product Category
- Sales
- Order Profit Per Order
- Order Status
- Delivery Status
- Shipping Mode
- Market
- Order Region
- Order State
- Order Date
- Shipping Date

---

# Data Quality & Preparation

A data audit was performed before the KPI analysis.

Key findings:

- `Product Description` was completely missing and was not required for the analysis.
- `Order Zipcode` had approximately 86% missing values and was excluded.
- Geography was analysed using available market, region, state and city fields.
- `Order Item Id` was treated as the transaction-level identifier.
- The dataset was confirmed to be at **order-item / transaction grain rather than one row per order**.
- Order-level aggregation was therefore applied where required.

Data preparation included:

- Cleaning categorical fields
- Standardising data types
- Creating a revenue-eligibility flag
- Creating date fields
- Separating realised and non-realised orders
- Aggregating transaction data to order level where appropriate
- Validating KPI calculations before Tableau visualisation

---

# Revenue / Sales Definition

The dataset contains sales values across multiple order statuses.

For this project, transactions with:

- `COMPLETE`
- `CLOSED`

were classified as **revenue-eligible**.

This is an analytical assumption for the project and should not be interpreted as an accounting revenue-recognition policy.

### Recorded Sales

**$36.78M**

### Realised Sales Proxy

**$16.12M**

This represents sales associated with COMPLETE and CLOSED transactions.

Approximately **43.82%** of recorded sales falls within this analytical realised-sales definition.

The remaining **56.18%** is associated with other order statuses.

Therefore, the project consistently uses the realised-sales definition when assessing commercial exposure.

---

# Key KPIs

| KPI | Result |
|---|---:|
| Total Orders | 65,752 |
| Realised Orders | 28,965 |
| Realisation Rate | 44.05% |
| Late Realised Orders | 16,633 |
| Late Delivery Rate | 57.42% |
| Realised Sales Proxy | $16.12M |
| Calculated Profit Proxy | $1.78M |
| Calculated Profit Margin | 11.04% |

### KPI Definitions

**Total Orders**  
Distinct orders in the dataset.

**Realised Orders**  
Distinct orders with `COMPLETE` or `CLOSED` status.

**Realisation Rate**

`Realised Orders / Total Orders × 100`

**Late Delivery Rate**

`Late Realised Orders / Realised Orders × 100`

**Realised Sales Proxy**  
Sales associated with COMPLETE and CLOSED transactions.

**Calculated Profit Proxy**  
Sum of `Order Profit Per Order` for COMPLETE and CLOSED transactions.

**Calculated Profit Margin**

`Calculated Profit Proxy / Realised Sales Proxy × 100`

---

# Profit Data Limitation

An important data-quality issue was identified during the analysis.

Although the dataset contains a field named:

`Order Profit Per Order`

the field does not consistently contain a single value for each Order ID.

Approximately **69.4% of realised orders contain multiple distinct values** in this field.

Therefore, directly summing the field should not be interpreted as an accounting-grade order profit measure.

For this portfolio project, the resulting figure is presented as a:

> **Calculated Profit Proxy**

It is used to support comparative commercial analysis across markets, categories and customer segments.

This limitation is explicitly documented rather than hidden.

---

# Analytical Approach

The project follows a structured analytics workflow:

```text
Raw Data
   ↓
Data Audit
   ↓
Data Cleaning & Preparation
   ↓
SQL Environment Setup
   ↓
Core KPI Analysis
   ↓
Delivery Performance Analysis
   ↓
Commercial Impact Analysis
   ↓
Management Priority Analysis
   ↓
Tableau Dashboards
   ↓
Business Recommendations
