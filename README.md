# E-Commerce Customer Segmentation — RFM & KMeans Clustering

**Dataset:** Online Retail II — UCI Machine Learning Repository  
**Tool:** Python, SQL, Machine Learning  
**Period:** December 2010 – December 2011  

---

## Overview

This project applies RFM (Recency, Frequency, Monetary) analysis combined with KMeans clustering to segment 4,338 customers from 397,885 cleaned transactions into four actionable business groups: **Champions**, **Loyal**, **Churn Risk**, and **Lost**.

---

## Project Structure

```
rfm-segmentation/
│
├── data/
│   ├── online_retail_II.csv       # raw dataset (download from UCI)
│   └── ecommerce.db               # SQLite DB generated during analysis
│
├── notebooks/
│   └── analysis.ipynb             # full pipeline: cleaning → RFM → clustering → viz
│
├── outputs/
│   ├── rfm_3d_scatter.html        # interactive 3D scatter plot
│   ├── rfm_revenue_pie.html       # revenue donut chart
│   ├── rfm_radar.html             # segment radar chart
│   └── rfm_heatmap.html           # RFM heatmap
│
├── report/
│   ├── main.tex                   # LaTeX report
│   ├── references.bib             # bibliography
│   └── figures/                   # static plots (elbow, bar charts, etc.)
│
├── README.md
├── requirements.txt
└── .gitignore
```

---

## Pipeline

```
Raw CSV (541,910 rows)
    ↓  SQL Cleaning (remove cancellations, nulls, negatives)
Clean Data (397,885 rows, 4,338 customers)
    ↓  SQL Aggregation
RFM Features (Recency, Frequency, Monetary per customer)
    ↓  Quantile Scoring (1–5 per metric)
RFM Scores
    ↓  Log Transform + Standard Scaling
Preprocessed Features
    ↓  KMeans (k=4, Elbow Method)
4 Customer Segments
    ↓  Plotly Visualisations
Interactive HTML Charts
```

---

## Results

| Segment    | Customers | Avg Recency | Avg Frequency | Avg Monetary | Revenue Share |
|------------|-----------|-------------|---------------|--------------|---------------|
| Champions  | Small     | 10.7 days   | 13.8 orders   | £8,142       | Highest       |
| Loyal      | Medium    | 69.3 days   | 4.1 orders    | £1,808       | Second        |
| Churn Risk | Large     | 16.7 days   | 2.1 orders    | £545         | Third         |
| Lost       | Large     | 179.6 days  | 1.3 orders    | £341         | Lowest        |

---

## Interactive Visualisations

| Chart | Description |
|-------|-------------|
| `rfm_3d_scatter.html` | Every customer plotted in 3D RFM space, coloured by segment |
| `rfm_revenue_pie.html` | Revenue share donut chart by segment |
| `rfm_radar.html` | Normalised RFM radar profiles per segment |
| `rfm_heatmap.html` | Mean RFM heatmap across clusters |

> Open any `.html` file directly in your browser — no server needed.

---

## Requirements

```bash
pip install pandas numpy scikit-learn matplotlib seaborn plotly
```

All other dependencies (`sqlite3`) are part of the Python standard library.

---

## Dataset

- **Source:** [UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/502/online+retail+ii)
- **File:** `[online_retail_II_2010_2011.csv](https://drive.google.com/file/d/1AoWtGUSumBXfHTYjyB3mnVqmR-5SV2N0/view?usp=drive_link)`
- **Encoding:** `latin-1`

Download the dataset and place it in the project root before running the notebook.

---

## Key Findings

- **Champions** are the smallest segment but generate the highest revenue per customer (avg £8,142), confirming the Pareto Principle.
- **Lost** customers (179.6 days inactive) contribute the least revenue — re-engagement spend on this group yields poor returns.
- **Loyal** customers are an under-exploited opportunity — upsell strategies could migrate them to Champions.
- **Churn Risk** customers bought recently but show low engagement — targeted win-back campaigns may recover them.

---

## Author

**YMd. Ferdous Rahman** — Data Science Portfolio Project, April 2026
