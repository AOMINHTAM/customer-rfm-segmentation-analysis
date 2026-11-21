# 🎯 Customer 360 & RFM Segmentation Analysis

> 🌐 **Portfolio Case Study:** [View full Case Study & Methodological Notes →](https://aominhtam-portfolio.vercel.app/projects/rfm-segmentation.html)

A personal e-commerce analytics case study analyzing multi-dimensional transaction records (**51,290 transaction line-items across 25,728 unique `OrderID`s and 17,415 customers**) for a simulated business scenario (*CosmeticWorld*, Jan 2020 – Dec 2023, USD). The project builds a reproducible **Recency, Frequency, and Monetary (RFM)** model paired with demographic, geographic, and basket-affinity profiling.

---

## 📦 Dataset & Methodological Scope

* **Project Type:** Personal Project / Simulated Business Case (*CosmeticWorld*)
* **Dataset Source:** Simulated E-Commerce CSVs (`EcomSales`, `Customer`, `Product`, `Region`)
* **Granularity & Scale:** `51,290` line-items &bull; `25,728` unique orders &bull; `17,415` customer accounts (Jan 2020 – Dec 2023, simulated USD)
* **RFM Formulas (Verified in Notebook):**
  * **Snapshot Date:** `2024-01-01` (`max(OrderDate) + 1 day`)
  * **Recency:** Days elapsed from each customer's latest order to `2024-01-01`
  * **Frequency:** Distinct `OrderID` count (`nunique`, preventing line-item inflation)
  * **Monetary:** Gross `Sales` sum in simulated USD (the dataset has no return/refund or ad-spend/CAC tables)
  * **Scoring:** Quintile `pd.qcut(q=5)` with `.rank(method="first")` tie-breaking on Frequency, mapped via deterministic R/F/M rules into 8 segments.

---

## 🎯 1. Business Context & Strategic Objectives

* **Business Scenario:** The marketing leadership aimed to restructure annual campaign spend by transitioning away from broad-spectrum discounting toward personalized, high-ROI customer lifecycle campaigns.
* **Analytical Objectives:**
  * Quantify behavioral engagement across **Recency** (days since last order), **Frequency** (distinct `OrderID` count), and **Monetary** (gross `Sales` spend).
  * Segment platform customers into operational tiers (`Champions`, `Loyal Customers`, `Cant Lose Them`, `Hibernating`, `Lost`, etc.).
  * Build a comprehensive **Customer 360 View** analyzing Demographics (Age, Gender, Education), Geographics (Global Markets), and Product Subcategory preferences.
  * Audit marketing spend allocation to eliminate budget waste on churned accounts while maximizing VIP retention.

---

## 🛠️ 2. Tech Stack & Methodology

* **Language:** Python 3.x
* **Data Processing & Feature Engineering:**
  * `pandas` / `numpy`: Multi-table relational joins, quantile-based scoring (`pd.qcut`), dynamic snapshot timestamping.
* **Data Visualization:**
  * `squarify`: Hierarchical Treemap visualization of customer volume vs. revenue concentration.
  * `seaborn` / `matplotlib`: Object-Oriented multi-plot dashboards for demographic pyramids, market rankings, and AOV correlations.

---

## 📊 3. Key Findings & Segment Breakdown

### RFM Segment Performance Matrix

| RFM Segment | Customer Count | Customer Share (%) | Total Revenue ($) | Revenue Share (%) | Strategic Lifecycle Classification |
| :--- | :---: | :---: | :---: | :---: | :--- |
| **Champions** | **2,361** | **13.56%** | **$2,138,211** | **32.8%** | Core Brand Advocates (High R, F, M) |
| **Loyal Customers** | 2,616 | 15.02% | $1,319,383 | 20.2% | Consistent Multi-Repurchasers |
| **Big Spenders** | 1,979 | 11.36% | $1,354,794 | 20.8% | High Basket Value / Low Frequency |
| **Cant Lose Them** | **833** | **4.78%** | **$653,354** | **10.0%** | Critical Churn Risk (High Historical Value) |
| **Hibernating** | 4,701 | 26.99% | $715,415 | 11.0% | Inactive / Low Engagement |
| **Need Attention** | 3,274 | 18.80% | $263,137 | 4.0% | Borderline Engagement |
| **New / Promising** | 1,171 | 6.72% | $61,198 | 0.9% | Recent First-Time Buyers |
| **Lost** | 480 | 2.76% | $12,182 | 0.2% | Dormant Accounts |

> **Concentration Insight:** The top 2 tiers (**Champions & Loyal Customers**) account for **under 29% of the customer base but drive over 53% of total company revenue**.

---

## 🔍 4. Customer 360 Profile Highlights

* **Demographics (Age & Education):**
  * Peak buying demographic resides between **ages 25 and 49**, driving $>60\%$ of total gross sales.
  * Strong positive correlation between academic credentials and order values: customers with **Bachelor's and Graduate degrees** average $\$60,000 - \$80,000$ in annual income and generate top-tier Average Order Value (AOV).
* **Geographics:** **Asia Pacific** and **Europe** serve as the primary **revenue drivers** in the simulated dataset, outpacing North America (USCA) and Latin America (LATAM).
* **VIP Basket Preferences:** Champions prioritize premium self-care lines: **Nail care products**, **hand creams**, and **body moisturizers**.

---

## 💡 5. Technical Review & Implementation Standards

* **Cross-Platform Portability:** All file path references decoupled into modular relative directory structures (`os.path.join("data", ...)`) to ensure containerized and multi-OS reproducibility.
* **Deterministic Dynamic Snapshot Date:** Replaced hardcoded date boundaries with algorithmic snapshotting (`OrderDate.max() + 1 day`), ensuring metrics calculate consistently across backtesting windows.
* **Object-Oriented Plotting Pipeline:** Refactored visualizations into explicit `fig, ax = plt.subplots()` structures, resolving Matplotlib label clipping and automating thousands-separator currency formatters (`ticker.StrMethodFormatter`).

---

## 🚀 6. Proposed Campaign Experiments & Evaluation Plan

> **Note:** Segment revenue concentration (`>53%` from top 2 tiers) is measured from the dataset; the budget splits below are testable campaign hypotheses evaluated via randomized holdout/A/B tests tracking **90-Day Repeat Purchase Rate**, **Win-back Conversion Rate**, **Retention Rate**, and **Incremental Net Revenue vs. Campaign Cost**.

1. **Hypothesis — Weighted Budget Pilot (70/30):** Test allocating ~70% of promotional spend toward **Champions** (loyalty perks) and **Cant Lose Them** (win-back vouchers, $653k historical pool), keeping 30% for nurturing *Big Spenders* and *New / Promising* tiers.
2. **Hypothesis — Dormant Outreach Suppression:** Pause higher-cost SMS/direct mail to **Lost** and **Hibernating** segments (`5,181` combined accounts) to reduce low-yield promotional outreach spend, testing low-cost email-only reactivation instead.
3. **Hypothesis — Category-Aligned Cross-Selling:** Test offering `Nail Care` and `Hand Creams` as Gift-With-Purchase incentives for `New / Promising` buyers to evaluate graduation into `Loyal Customers`.