# Olist E-Commerce: End-to-End LTV & Marketing Analytics Pipeline

## Project Objective
To transform raw marketplace data into an actionable strategic growth engine. This project processes **97,006 delivered orders** to calculate true Customer Lifetime Value (LTV), segment users via RFM modeling, isolate high-performing acquisition channels, and map revenue concentration via an interactive Tableau Dashboard.

---

## Core Performance KPIs (Verified Platform Metrics)
* **True Average Customer LTV:** $232.28  
* **True Total Attributed Revenue:** $15,489,522.09  
* **Total Global Marketing Spend:** $634,503.28  
* **True Global ROAS:** 24.41x (2,441.20%)  

---

## Technical Architecture & Workflow

### Phase 1: Python Data Engineering & Simulation
* **Data Cleansing:** Consolidated an 8-table relational marketplace dataset, resolved schema missing values, converted localized time dimensions, and mapped Portuguese product profiles to English.
* **RFM Segmentation:** Engineered an algorithmic scoring matrix (1–5) tracking Recency, Frequency, and Monetary parameters for 93,357 unique profiles across 7 distinct operational tiers (Champions, At Risk, Lost, etc.).
* **Marketing & Attribution Engine:** Synthesized multi-touch customer clickstreams and multi-channel acquisition cost records (`fact_marketing_spend`) utilizing linear fractional-credit distribution matrices to compute exact Customer Acquisition Cost (CAC) and ROAS.

### Phase 2: PostgreSQL Data Warehousing
Engineered low-latency analytical database views within a local PostgreSQL environment to automate backend KPI business logic:
* `v_channel_performance`: Calculates monthly ROAS, dynamic CAC, and Click-Through-Rates (CTR).
* `v_cohort_retention`: Tracks monthly cohort-based customer decay profiles.
* `v_customer_segments`: Measures total transaction shares per engineered RFM profile.

### Phase 3: Tableau Strategic BI Dashboard
Developed a consolidated corporate-level visualization dashboard focusing on actionable business variables:
* **The Whale Curve (Revenue Concentration):** Implemented decile ranking analysis showing that the top ~20% of customers generate nearly 80% of Olist's gross revenue stream.
* **High-Value Channel Performance:** Built an insulated channel-yield visualizer leveraging Level of Detail (LOD) expressions. By evaluating only top-10% decile high-value spenders and stabilizing the axis variance, it exposes substantial value discrepancies previously masked by flat population means.

---

## Executive Insights & Analytical Conclusions

### 1. High Concentration Risk (The Whale Curve)
Our concentration analysis demonstrates that the business is hyper-dependent on a minimal cohort of power shoppers. The initial steep climb of the Whale Curve proves that retaining an existing top-decile customer offers a drastically higher ROI than acquiring cold, unsegmented traffic.

### 2. Hidden Quality Gaps in Acquisition Channels
While the overall standard population mean LTV hovers uniformly around **$232.28** across all marketing mediums, isolating our high-value whales reveals a critical gap: **Direct Traffic** and **Email** significantly outperform Paid Social platforms at surfacing high-tier spenders. Standard channel averages were entirely masking this high-value yield.

### 3. The Retention Cliff
Longitudinal cohort grids reveal a steep retention decline, dropping near 99% immediately following Month 0 (Acquisition Month). Olist functions fundamentally as a high-velocity, single-purchase acquisition engine; structural lifetime value is heavily restricted by a lack of back-end customer activation.

---

## Operational Validation & Verification Guide
To ensure the integrity of the dashboard and confirm that the executive insights are structurally sound, the data logic was cross-verified using explicit mathematical and visual checkpoints:

### KPI & Metric Validation Ledger
* **LTV Core Aggregation Check:** Verified that the global LTV card utilizes an `AVG` aggregation layer targeting the `ltv_estimate` column rather than a `SUM`. A row-level straight average across transaction items mistakenly yields a fragmented order value (~$12.99), whereas the true unique customer lifetime anchor resolves to **$232.28**, confirmed via Python Pandas programmatic auditing (`df_customers['ltv_estimate'].mean()`).
* **Attributed Revenue Boundary Test:** Confirmed that the platform revenue metrics evaluate to exactly **$15,489,522.09**. This is validated by assigning a global `SUM` aggregation on fractional row attribution weights ($\sum (\text{Total Revenue} \times \text{Attribution Weight})$), guaranteeing that no split multi-touch revenue credits are double-counted or dropped at the interface boundaries.
* **ROAS Formula Enforcement:** Verified that the global return ratio evaluates to **24.41x**. This was protected against native Tableau row-level grouping traps by forcing database-level execution order via calculated expressions: `SUM([Total Revenue] * [Attribution Weight]) / SUM([Spend])`. The resulting dashboard element registers properly as an aggregated field (`AGG`), eliminating row-inflation errors.

### Visual & Strategic Alignment Checkpoints
* **Whale Curve Verification:** Validated by tracking the 20th percentile customer marker along the X-axis of the concentration profile. The corresponding Y-axis metric successfully maps to the ~80% cumulative revenue mark, mathematically confirming the Pareto concentration thesis.
* **Insulated Channel Verification:** Validated by stripping dashboard level filters to observe identical, flat population baseline means across channels (~$232). Applying the Top-10% LOD Decile Filter isolates the visual variation, causing the Email and Direct bars to disproportionately scale higher than Paid Social, proving the "Hidden Quality Gap" conclusion.
* **Cohort Decay Integrity Check:** Validated by inspecting the transition column between Month 0 and Month 1 on the retention heatmap matrix. The immediate, uniform color drop-off confirms the ~99% operational churn rate, validating the "Retention Cliff" diagnostic.

---

## Strategic Action Plan (Betterment Strategies)

* **Launch a Dedicated VIP Tier:** Deploy tailored loyalty initiatives (exclusive shipping terms, tiered reward structures) targeted specifically at the top 10% LTV decile to insulate the core revenue stream from churn.
* **Capital Realignment:** Divert 15% of underperforming Paid Social budgets directly into high-yield search intent optimization (SEO) and automated Email CRM funnels where whale-generation capacity is fundamentally proven.
* **Automated Win-Back Triggers:** Set up automated event listeners targeting customers entering the "At Risk" and "Can't Lose Them" RFM groups, prompting dynamic re-engagement offers exactly at 1.5x their historical average buying intervals to fix the "leaky bucket" cohort retention.
