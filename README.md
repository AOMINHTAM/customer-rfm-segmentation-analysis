# 🎯 Customer 360 & RFM Segmentation Analysis

An end-to-end customer analytics project utilizing multi-dimensional transaction records (**51,290 sales orders across 17,415 customers**) for cosmetic retailer *CosmeticWorld*. The project builds an automated **Recency, Frequency, and Monetary (RFM)** model combined with demographic, geographic, and basket-affinity analysis to optimize corporate marketing budgets for the **New Year Rejuvenation Campaign**.

---

## 🎯 1. Business Context & Strategic Objectives

* **Business Scenario:** The marketing leadership aimed to restructure annual campaign spend by transitioning away from broad-spectrum discounting toward personalized, high-ROI customer lifecycle campaigns.
* **Analytical Objectives:**
  * Quantify behavioral engagement across **Recency** (days since last order), **Frequency** (distinct order counts), and **Monetary** (total net spend).
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
* **Geographics:** **Asia Pacific** and **Europe** serve as primary profit hubs, outpacing North America (USCA) and Latin America (LATAM).
* **VIP Basket Preferences:** Champions prioritize premium self-care lines: **Nail care products**, **hand creams**, and **body moisturizers**.

---

## 💡 5. Technical Review & Implementation Standards

* **Cross-Platform Portability:** All file path references decoupled into modular relative directory structures (`os.path.join("data", ...)`) to ensure containerized and multi-OS reproducibility.
* **Deterministic Dynamic Snapshot Date:** Replaced hardcoded date boundaries with algorithmic snapshotting (`OrderDate.max() + 1 day`), ensuring metrics calculate consistently across backtesting windows.
* **Object-Oriented Plotting Pipeline:** Refactored visualizations into explicit `fig, ax = plt.subplots()` structures, resolving Matplotlib label clipping and automating thousands-separator currency formatters (`ticker.StrMethodFormatter`).

---

## 🚀 6. Actionable Campaign Recommendations (New Year Rejuvenation)

1. **70/30 Budget Allocation:** Concentrate 70% of promotional budget strictly on **Champions** (Exclusive VIP gifting and concierge access) and **Cant Lose Them** (High-touch win-back email sequence offering tailored re-activation vouchers).
2. **Direct Mail Suppression:** Immediately suppress the **Lost** and **Hibernating** segments ($>5,100$ accounts) from costly outbound direct mail and SMS marketing to curb CAC waste.
3. **Category-Aligned Cross-Selling:** Bundle high-performing subcategories (`Nail Care` & `Hand Creams`) as promotional gift-with-purchase (GWP) items for the `New / Promising` tier to expedite their transition into `Loyal Customers`.