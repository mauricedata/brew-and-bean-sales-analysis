# Brew & Bean Co. — Commercial Sales & Profitability Analysis

An end-to-end commercial analytics project modeling multi-channel transactional data for an omni-channel specialty coffee retailer.

---

## Executive Summary & Dashboard
![Dashboard Preview](images/dashboard_overview.png)

### Key Commercial Insights
* **Channel Mix:** Wholesale drives 55.3% of total revenue ($1,030.63) and the largest gross profit pool ($622.63), maintaining a healthy 56.98% margin despite volume pricing.
* **Direct Retail Margin Power:** In-store transactions produce the highest margin efficiency at **65.47%**, operating completely free of discount erosion.
* **Promotion Elasticity:** The `WELCOME20` acquisition campaign creates significant margin compression down to **48.42%** (~17 percentage points below baseline non-discounted transactions of 65.65%).
* **Strategic Recommendation:** Implement a minimum cart threshold of $40 on promotional code `WELCOME20` to protect unit margins against small basket sizes.

---

## Technical Methodology

### 1. Ingestion & Data Hygiene
* Normalized multi-channel logs across inconsistent string casing.
* Eliminated trailing and leading whitespace anomalies using dynamic text formulas (`TRIM`).
* Converted raw ranges into structured Excel objects (`Fact_Transactions` and `Dim_Products`) for dynamic array expansion and schema stability.

### 2. Relational Modeling & Schema Design
* Built relational links between transactional facts and product dimension tables using vector lookup arrays:
  ```excel
  =XLOOKUP([@[Product_SKU]], Dim_Products[Product_SKU], Dim_Products[Category])
