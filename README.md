

# Influencer Marketing ROI & Performance Analysis

A data analysis project exploring **150,000 influencer marketing campaigns** across Instagram, YouTube, TikTok, and Twitter — quantifying ROI, benchmarking campaign performance, tracking trends over time, and identifying which influencer categories and campaign types deserve future investment.

**[Open the notebook in Google Colab →](#getting-started)**

---

## 📋 Overview

This project answers four core business questions using a real-world-style influencer marketing dataset:

| Question | Approach |
|---|---|
| **ROI Analysis** | Quantify return on investment across platforms and influencer categories |
| **Campaign Benchmarking** | Compare performance by campaign type, influencer niche, and platform |
| **Trend Analysis** | Track engagement, reach, and sales over time |
| **Influencer Selection** | Score and rank categories/campaign types for future partnerships |

The full analysis, code, and visualizations live in [`influencer_marketing_roi_analysis.ipynb`](./influencer_marketing_roi_analysis.ipynb), with findings written up in [`Influencer_Marketing_ROI_Project_Report.docx`](./Influencer_Marketing_ROI_Project_Report.docx).

## 🗂️ Dataset

`influencer_marketing_roi_dataset.csv` — 150,000 campaign records, 10 columns, no missing values or duplicates.

| Field | Description |
|---|---|
| `campaign_id` | Unique campaign identifier |
| `platform` | Instagram, YouTube, TikTok, or Twitter |
| `influencer_category` | Fashion, Food, Travel, Beauty, Tech, Gaming, or Fitness |
| `campaign_type` | Giveaway, Product Launch, Brand Awareness, Seasonal Sale, or Event Promotion |
| `start_date` / `end_date` | Campaign start and end timestamps |
| `engagements` | Total user engagements recorded |
| `estimated_reach` | Estimated audience reach |
| `product_sales` | Units sold attributed to the campaign |
| `campaign_duration_days` | Campaign length in days |

> **Data quality note:** `start_date` increases sequentially by one day per row (2022‑01‑01 → 2432‑09‑07) rather than reflecting real scheduling, and `engagements`/`estimated_reach` appear generated independently of each other. Trend results should be read as *"how metrics evolve across the campaign sequence"* rather than genuine seasonality — see the notebook and report for details.

## ⚙️ Methodology

The raw dataset has **no cost/spend or revenue column**, so ROI isn't directly computable. To make ROI calculable, the notebook applies a transparent, editable cost model instead of silently guessing:

```
Cost    = engagements × assumed cost-per-engagement (CPE, varies by platform)
Revenue = product_sales × assumed average order value (AOV)
ROI %   = (Revenue − Cost) / Cost × 100
```

These constants (`CPE_BY_PLATFORM`, `AVERAGE_ORDER_VALUE`) sit in one editable cell — swap in real spend and pricing data and every table/chart downstream recalculates automatically. Three additional efficiency metrics that **don't** depend on any assumption are also computed: engagement rate, sales per 1,000 reach, and sales per engagement.

Influencer categories and campaign types are further ranked using a **composite 0–100 score** that min-max normalizes and averages ROI, sales-per-1,000-reach, and engagement rate, so no single metric dominates the ranking.

## 📊 Key Findings

- **Twitter** shows the strongest assumed ROI (~3,620% overall) — driven mainly by its lower assumed cost-per-engagement, not materially higher sales. Treat with caution until real spend data is available.
- ROI across **influencer categories** is tightly clustered (~1,987%–2,015%) — category choice alone is a weak ROI lever once cost is factored in.
- **Fashion** (score 77/100) and **Tech** (71/100) rank highest among influencer categories on the combined composite score.
- **Seasonal Sale** (75/100) is the strongest-scoring campaign type; **Product Launch** scores lowest (17/100) despite comparable average sales.
- All ten of the highest-ROI reliable platform × category × campaign-type combinations involve Twitter, led by **Twitter × Food × Product Launch** (~20,945% ROI, n=421).

Full breakdown, tables, and charts are in the [project report](./Influencer_Marketing_ROI_Project_Report.docx).

## 🚀 Getting Started

### Run in Google Colab (recommended)

1. Open [`influencer_marketing_roi_analysis.ipynb`](./influencer_marketing_roi_analysis.ipynb) in Colab.
2. Run all cells (`Runtime → Run all`) — you'll be prompted to upload `influencer_marketing_roi_dataset.csv` if it isn't already in the working directory.
3. (Optional) Edit `CPE_BY_PLATFORM` and `AVERAGE_ORDER_VALUE` in the ROI section with real spend/pricing data.

### Run locally

```bash
git clone https://github.com/shahanansari-creator/<repo-name>.git
cd <repo-name>
pip install pandas numpy matplotlib seaborn jupyter
jupyter notebook influencer_marketing_roi_analysis.ipynb
```

## 🧰 Tech Stack

- **Python** — pandas, NumPy
- **Visualization** — matplotlib, seaborn
- **Environment** — Google Colab / Jupyter Notebook

## 📁 Repository Structure

```
.
├── influencer_marketing_roi_analysis.ipynb   # Full analysis notebook
├── influencer_marketing_roi_dataset.csv      # Source dataset
├── Influencer_Marketing_ROI_Project_Report.docx  # Written report with findings
└── README.md
```

## ⚠️ Limitations

- No actual cost/spend or revenue data was available; ROI figures rely on assumed CPE and AOV constants and should be treated as directional, not decision-grade.
- The date field is sequential rather than reflecting real campaign scheduling, limiting the reliability of seasonal trend conclusions.
- The analysis is descriptive/correlational — it does not establish that a given platform, category, or campaign type *causes* higher sales.

## 👤 Author

**Mohd Shahan Ansari**
[GitHub](https://github.com/shahanansari-creator) · [LinkedIn](https://www.linkedin.com/in/mohd-shahan-ansari-100479259/)
