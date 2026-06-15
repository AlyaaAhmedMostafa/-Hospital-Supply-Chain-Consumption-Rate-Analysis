# 🏥 Hospital Supply Chain Consumption Rate Analysis — Waste, Utilisation & Demand Efficiency Report

> **Period Covered:** January 2021 – December 2023
> **Datasets:** Procurement & Inventory (12,000 records) · Consumption & Waste Tracking (10,500 records)
> **Tools: Microsoft Excel  · OLS Linear Regression

---

## 📋 Table of Contents

1. [Executive Summary](#-executive-summary)
2. [Dataset Overview](#-dataset-overview)
3. [Key Performance Indicators](#-key-performance-indicators)
4. [Consumption & Waste Analysis](#-consumption--waste-analysis)
   - [Ward-Level Performance](#ward-level-performance)
   - [Item-Type Waste Cost Ranking](#item-type-waste-cost-ranking)
   - [Shift Performance](#shift-performance)
   - [Disposal Reason Breakdown](#disposal-reason-breakdown)
5. [Procurement & Inventory Analysis](#-procurement--inventory-analysis)
   - [Supplier Performance](#supplier-performance)
   - [Stockout Risk](#stockout-risk)
6. [Forecasting Model — 2024 Outlook](#-forecasting-model--2024-outlook)
7. [Critical Findings](#-critical-findings)
8. [Recommendations & Action Plan](#-recommendations--action-plan)
9. [Analysis File Guide](#-analysis-file-guide)

---

## 📌 Executive Summary

This report presents a comprehensive supply chain analytics study conducted across a multi-ward hospital network covering a 36-month operational period (2021–2023). The analysis spans two core supply chain dimensions: **downstream consumption and waste** at the ward level, and **upstream procurement and inventory management** across 10 supplier relationships.

The hospital issued **786,459 supply items** at a total cost of **\$7.15 million** over the period. Of those, **118,467 items were wasted** — a systemic waste rate of **15.1%** — resulting in **\$1.08 million in avoidable waste cost**, equivalent to **15.1% of the total supply budget**.

On the procurement side, **14.7% of purchase orders experienced supplier shortfalls**, and **20.4% of inventory positions fell below reorder point** at time of recording — exposing the hospital to recurrent stockout risk. Average supplier lead time stands at **15.7 days**, with Stryker Corp averaging **29.7 days**, nearly three times the baseline.

The findings reveal that waste and supply failure are not random — they are concentrated in specific wards, item categories, suppliers, and operational conditions that are actionable and correctable.

---

## 📂 Dataset Overview

| Dataset | Records | Period | Scope |
|---|---|---|---|
| **Procurement & Inventory** | 12,000 PO lines | Jan 2021 – Jan 2024 | 10 suppliers, 10 categories, 10 departments |
| **Consumption & Waste** | 10,500 ward records | Jan 2021 – Jan 2024 | 10 wards, 3 shifts, 15 item types |

Both datasets were engineered with **realistic asymmetry** — supplier concentration, ward-level demand skew, night-shift staffing differentials, and price heterogeneity across item categories — to reflect real-world hospital supply chain conditions.

---

## 📊 Key Performance Indicators

| KPI | Value | Benchmark Signal |
|---|---|---|
| Total Items Issued | 786,459 | Baseline |
| Total Items Wasted | 118,467 | 🔴 15.1% waste rate |
| Total Supply Cost (3 yr) | \$7,148,438 | ~\$197K/month avg |
| Total Waste Cost (3 yr) | \$1,080,611 | 🔴 15.1% of budget lost |
| Supply-Related Incidents | 518 | 🟡 4.9% of all records |
| POs with Supplier Shortfall | 1,760 / 12,000 | 🔴 14.7% fill-rate failure |
| Inventory Below Reorder Point | 2,444 / 12,000 | 🔴 20.4% stockout exposure |
| Average Supplier Lead Time | 15.7 days | 🟡 Range: 11–30 days |
| Total Procurement PO Value | \$189.2M | 3-year aggregate |

---

## 🔬 Consumption & Waste Analysis

### Ward-Level Performance

Ward performance varies significantly, indicating that waste is driven by **operational protocols and staffing discipline**, not patient volume alone.

| Ward | Waste Rate | Waste Cost | Share of Total Waste |
|---|---|---|---|
| **ER** | **21.8%** 🔴 | \$268,084 | 24.8% |
| Surgery | 14.9% | \$169,641 | 15.7% |
| ICU | **10.4%** 🟢 | \$150,504 | 13.9% |
| Cardiology | 15.2% | \$111,775 | 10.3% |
| Oncology | 14.5% | \$90,620 | 8.4% |
| Pediatrics | 15.0% | \$71,905 | 6.7% |
| Neurology | 14.7% | \$67,014 | 6.2% |
| Maternity | 14.2% | \$50,948 | 4.7% |
| General Ward | 14.5% | \$50,717 | 4.7% |
| Orthopedics | 14.3% | \$49,402 | 4.6% |

**Key Insight — The ICU Paradox:** The ICU handles the highest patient acuity and the highest item volume, yet achieves the **lowest waste rate in the hospital at 10.4%**. This is a strong signal that structured consumption protocols and tighter clinical oversight directly reduce waste — and that this model is replicable across other wards.

**Key Insight — ER Critical Overrun:** The ER's waste rate of **21.8% is 2.1× the ICU rate** and 1.5× the hospital average. With 133,424 items issued, this 11.4 percentage-point excess translates to approximately **15,200 unnecessarily wasted items** and **\$268K in recoverable cost** — the single largest waste cost centre in the hospital.

---

### Item-Type Waste Cost Ranking

| Rank | Item Type | Waste Cost | Avg Unit Cost | Waste Rate |
|---|---|---|---|---|
| 1 | **Blood Bags** | \$350,215 | \$41.01 | 15.2% |
| 2 | **Sutures** | \$207,228 | \$26.00 | 15.4% |
| 3 | **Medication Vials** | \$141,831 | \$18.98 | 14.5% |
| 4 | **Catheters** | \$99,070 | \$12.97 | 15.4% |
| 5 | **Surgical Drapes** | \$68,813 | \$9.01 | 14.8% |

Blood Bags alone account for **32.4% of all waste cost** (\$350K of \$1.08M), driven purely by their high unit cost rather than an above-average waste rate. This means even marginal improvements in Blood Bag management have outsized financial impact. Sutures follow a similar pattern. These two items together represent **\$557K** — over half of all waste cost — from just 2 of 15 item types.

---

### Shift Performance

| Shift | Waste Rate | Avg Staff Count | Incidents | Incident Rate |
|---|---|---|---|---|
| Morning | 15.1% | 10.4 | 198 | 4.6% |
| Afternoon | 15.2% | 10.5 | 193 | 5.4% |
| **Night** | **14.9%** | **6.8** | 127 | 4.9% |

The night shift operates with **35% fewer staff** (6.8 vs 10.4 average) yet maintains a waste rate and incident rate comparable to fully staffed shifts. While this appears positive on the surface, it is analytically concerning: **reduced staffing compresses reporting capacity**, meaning incidents and waste events on night shift are likely **under-captured**, not genuinely lower. This represents a hidden risk that warrants deeper qualitative investigation.

---

### Disposal Reason Breakdown

| Disposal Reason | Waste Cost | Share |
|---|---|---|
| **Over-issued** | \$228,650 | 21.2% |
| **Returned** | \$223,048 | 20.6% |
| Expired | \$215,153 | 19.9% |
| Used (standard) | \$211,535 | 19.6% |
| Damaged | \$202,225 | 18.7% |

**Over-issued** and **Returned** together account for **\$451,698 (41.8%)** of all waste cost. These two categories represent waste that is **entirely preventable** — they stem from inaccurate ward-level par levels and over-ordering rather than clinical necessity. This is a systemic procurement/issuance process failure, not a clinical one.

Critically, "Expired" waste (\$215K) indicates inadequate **FEFO (First-Expiry-First-Out)** discipline in inventory rotation, particularly relevant for Blood Bags and Medication Vials which have short shelf lives and high unit costs.

---

## 🏭 Procurement & Inventory Analysis

### Supplier Performance

| Supplier | Avg Lead Time | Shortfall Rate | PO Volume | PO Value |
|---|---|---|---|---|
| **Stryker Corp** | **29.7 days** 🔴 | 14.7% | 794 | \$11.8M |
| **Medtronic** | **22.2 days** 🔴 | 15.6% | 958 | \$13.6M |
| Abbott Labs | 18.4 days 🟡 | 13.1% | 834 | \$13.1M |
| Baxter Int | 17.5 days 🟡 | 15.9% | 565 | \$9.2M |
| BD Medical | 16.1 days 🟡 | 15.0% | 854 | \$12.8M |
| Owens & Minor | 15.7 days | 13.4% | 1,205 | \$16.7M |
| Henry Schein | 14.1 days | 14.6% | 1,078 | \$16.7M |
| McKesson Corp | 13.4 days | 15.1% | 1,714 | \$28.8M |
| Cardinal Health | 12.6 days | 16.3% | 1,801 | \$34.0M |
| **MedLine Industries** | **11.4 days** 🟢 | 13.6% | 2,197 | \$32.3M |

**Stryker Corp** is the most problematic supplier — average lead time of **29.7 days**, nearly 3× the best-performing supplier. Combined with a 14.7% shortfall rate, Stryker supply uncertainty creates significant planning risk for Orthopedic departments. **Medtronic** (22.2 days) presents similar concerns.

**Cardinal Health** has the highest shortfall rate at **16.3%** despite being the second-largest supplier by value (\$34M). This level of fill-rate failure from a high-value partner warrants formal contract review and dual-sourcing consideration.

**MedLine Industries** — the highest-volume supplier — demonstrates the best lead time at 11.4 days, establishing an achievable benchmark for supplier SLA negotiation.

---

### Stockout Risk

- **2,444 of 12,000 inventory records (20.4%)** showed stock on hand below reorder point
- This exposes the hospital to recurrent **clinical supply interruptions** across all departments
- The gap is most pronounced in categories with longer lead times (Orthopedic Implants, Diagnostic Equipment), where Stryker and Medtronic delays compound the stockout risk
- A reorder point recalibration incorporating actual lead time distributions (not theoretical averages) is recommended

---

## 🔮 Forecasting Model — 2024 Outlook

### Methodology

A **12-month demand and cost forecast for 2024** was produced using **Ordinary Least Squares (OLS) linear regression** fitted on 36 months of historical monthly actuals (Jan 2021 – Dec 2023).

Three separate models were estimated:

| Model | Slope (monthly Δ) | Interpretation |
|---|---|---|
| Items Issued | **−68 units/month** | Slight demand plateau / marginal decline |
| Total Supply Cost | **−\$378/month** | Cost broadly flat with mild downward pressure |
| Waste Cost | Tracked proportionally | Tied to issuance volume |

### 2024 Forecast Summary

| Period | Forecast Items Issued | Forecast Cost | Low (−10%) | High (+10%) |
|---|---|---|---|---|
| Jan 2024 | ~21,900 | ~\$196,300 | \$176,700 | \$215,900 |
| Jun 2024 | ~21,500 | ~\$194,000 | \$174,600 | \$213,400 |
| Dec 2024 | ~21,000 | ~\$191,700 | \$172,500 | \$210,900 |

### Forecast Interpretation

The **trend line is essentially flat**, indicating the hospital is operating in a **demand-stable environment** with no significant volume growth expected in 2024 under current operations. Monthly supply cost is expected to remain in the **\$191K–\$196K range**.

**Budget Recommendation:** Plan 2024 procurement budget at **\$205K/month** (\$2.46M annually), incorporating a **±10% buffer** to absorb the historical cost volatility observed (monthly range: \$136K–\$250K). This buffer corresponds directly to the ±10% confidence band in the forecast model.

> ⚠️ **Model Limitations:** OLS linear regression assumes trend continuity. Forecast accuracy degrades if significant changes occur in patient census, item pricing, new clinical programs, or supplier contract renegotiation. The model should be re-estimated quarterly with updated actuals.

---

## 🚨 Critical Findings

### Finding 1 — Waste is Structurally Concentrated, Not Random
The **ER generates 24.8% of all waste cost** from 17% of records. ICU demonstrates that low waste rates are achievable even under high-volume, high-acuity conditions. Waste is a **management and protocol problem**, not an inherent clinical necessity.

### Finding 2 — Two Items Drive Half the Waste Budget
Blood Bags (\$350K) and Sutures (\$207K) together account for **52% of total waste cost** (\$557K of \$1.08M). Neither has an abnormally high waste rate — their impact is driven entirely by unit cost. **Targeted inventory management for these two items alone could recover the majority of waste losses.**

### Finding 3 — "Preventable" Waste Dominates Disposal Reasons
Over-issued and Returned waste (\$451K, 42%) is systemic and preventable. This points directly to **inaccurate ward par levels** and **poor demand signaling** — both addressable through data-driven reorder point recalibration.

### Finding 4 — Two Suppliers Are Structural Risks
Stryker Corp (29.7-day lead time) and Cardinal Health (16.3% shortfall rate) represent a **dual-axis supply risk** — one for delivery speed, one for order fulfillment. Both are high-value partners, making their underperformance disproportionately impactful.

### Finding 5 — Night Shift Is a Blind Spot
With 35% less staff on night shifts maintaining near-identical reported waste and incident rates, the data suggests **reporting suppression rather than genuine performance parity**. Clinical and operational leaders should audit night-shift supply documentation practices.

---

##  Recommendations & Action Plan

| Priority | Category | Recommendation | Expected Impact |
|---|---|---|---|
| 🔴 **Critical** | Waste Reduction | Implement ER-specific real-time issuance controls and consumption tracking against patient census | Recover ~\$90K–\$130K/year |
| 🔴 **Critical** | Inventory Management | Deploy FEFO policy for Blood Bags and Medication Vials; add expiry-date alerts at 30 and 7 days | Recover ~\$85K/year in expiry waste |
| 🔴 **Critical** | Process Reform | Audit and recalibrate ward-level par levels to eliminate Over-issued and Returned waste | Recover ~\$90K–\$100K/year |
| 🟡 **High** | Supplier Management | Place Stryker Corp and Cardinal Health on formal SLA review; initiate dual-sourcing for Orthopedic Implants | Reduce stockout risk, lead time −30% |
| 🟡 **High** | Procurement Planning | Recalibrate reorder points using actual lead time distributions (not averages); address 20.4% stockout exposure | Eliminate ~2,400 stockout risk events |
| 🟡 **High** | Staffing | Commission audit of night-shift supply documentation; assess whether 6.8 avg staff is clinically safe | Risk mitigation |
| 🟢 **Opportunity** | Benchmarking | Standardise ICU consumption protocols (10.4% waste rate) across Cardiology, Pediatrics, and Surgery | Up to \$120K/year if all wards reach ICU rate |
| 🟢 **Opportunity** | Forecasting | Implement rolling 12-month demand forecast updated quarterly; use ±10% band for budget planning | Improves procurement accuracy |
| 🟢 **Opportunity** | KPI Monitoring | Launch monthly supply chain scorecard: waste rate, cost per patient, fill rate, and incident rate by ward | Enables early-warning intervention |

### Estimated Combined Recoverable Value

| Initiative | Annual Savings Estimate |
|---|---|
| ER waste protocol reform | \$90K – \$130K |
| FEFO / expiry management | \$85K |
| Par level recalibration | \$90K – \$100K |
| ICU protocol replication | Up to \$120K |
| **Total Recoverable** | **\$365K – \$435K / year** |

This represents a **34%–40% reduction in annual waste cost** from the current \$1.08M baseline, achievable without capital expenditure — purely through process, protocol, and data discipline.

---

## 📁 Analysis File Guide

```
hospital-supply-chain-analytics/
│
├── README.md                                    ← This executive report
│
├── data/
│   ├── hospital_procurement_inventory.xlsx      ← Raw dataset 1 (12,000 rows)
│   └── hospital_consumption_waste.xlsx          ← Raw dataset 2 (10,500 rows)
│
└── analysis/
    └── hospital_supply_chain_full_analysis.xlsx ← Full Excel analysis workbook
        ├──   Insights          → Executive KPIs, findings, and summary
        ├──   Data           → Full 10,500-row dataset with filters
        ├──   Ward Analysis      → Ward cost, waste rate, incident tables + charts
        ├──   Item Analysis      → 15 item types ranked by waste cost + pie/bar charts
        ├──   Shift & Disposal   → Shift performance + disposal reason + cross-tab heatmap
        ├──   Monthly Trends     → 36-month actuals with MoM change formulas + line charts
        ├──   Forecasting        → OLS 12-month forecast with ±10% confidence band + charts
        └──   Recommendations    → 8 prioritized actions with evidence and impact estimates
```

---

##  Methodology Notes

- **Waste Rate** = Items Wasted ÷ Items Issued × 100
- **Waste Cost** = Items Wasted × Unit Cost (USD)
- **Shortfall** = Qty Ordered − Qty Received (positive values only)
- **Stockout Risk** = Stock On Hand < Reorder Point
- **Forecasting Model** = OLS Linear Regression on monthly aggregates; 36-month training window; 12-month horizon
- **Confidence Band** = ±10% of point forecast (based on historical monthly cost range)
- All monetary values in **USD**; all analysis at **monthly granularity** for trend work

---

##  Data Caveats

- The Jan 2024 partial month was excluded from trend and forecast model training
- Disposal reason is only populated for records where Items Wasted > 0 (~75% of records)
- Lead time data includes random variation simulating real-world supplier inconsistency
- Supplier shortfall rates are uniform across categories; real analysis should segment by category

---

