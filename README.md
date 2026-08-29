# 📊 Superstore Analytics Pipeline

**Advanced Python Data Exploration & Automated Reporting** — an end-to-end, object-oriented data analytics pipeline built on the Sample Superstore 2019 dataset.

![Python](https://img.shields.io/badge/Python-3.10%2B-blue?logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Wrangling-150458?logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-Numerical%20Computing-013243?logo=numpy&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-Visualization-11557C)
![Seaborn](https://img.shields.io/badge/Seaborn-Statistical%20Viz-4C72B0)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen)
![License](https://img.shields.io/badge/License-MIT-yellow)

---

## 📑 Table of Contents

- [Overview](#-overview)
- [Business Scenario](#-business-scenario)
- [Project Structure](#-project-structure)
- [Pipeline Architecture](#-pipeline-architecture)
- [Key Features](#-key-features)
- [Visualizations](#-visualizations)
- [Key Insights & KPIs](#-key-insights--kpis)
- [Tech Stack](#-tech-stack)
- [How to Run](#-how-to-run)
- [Requirements Checklist](#-requirements-checklist)
- [Author](#-author)

---

## 🧭 Overview

This project is a full **OOP-based analytics pipeline** that takes raw retail transaction data and turns it into a cleaned dataset, engineered features, exploratory analysis, statistical insights, visual reports, and an automated KPI summary — all built with modular, reusable Python classes and proper exception handling.

Built as **Mini-Project 1** for a Data Analysis course, structured to reflect a real-world analytics engineering workflow rather than a single throwaway script.

## 💼 Business Scenario

A multinational retail company wants an automated analytical solution to monitor **sales, profitability, customer behavior, and operational performance** — this pipeline delivers exactly that, from raw `.xls` file to a ready-to-read KPI report.

## 📁 Project Structure

```
Mini-Project-1/
├── data/
│   └── Sample - Superstore 2019.xls
├── output/
│   ├── charts/                      # 9 saved visualizations
│   ├── cleaned_data.csv
│   ├── cleaned_data_optimized.csv
│   └── report_summary.txt
├── mini_project_1.ipynb             # Full documented workflow
├── mini_project_1_plan.md           # Original project plan
└── README.md
```

## 🏗️ Pipeline Architecture

The pipeline is built as six chainable, single-responsibility classes:

| Class | Responsibility |
|---|---|
| `DataLoader` | Loads the raw `.xls` file with exception-handled I/O |
| `DataCleaner` | Handles missing values, duplicates, format standardization, and outlier flagging |
| `FeatureEngineer` | Adds Profit Margin, Shipping Duration, Sales Performance Category, and date features |
| `EDAAnalyzer` | Runs numeric/categorical summaries, trend analysis, and correlation analysis |
| `Visualizer` | Generates and saves all charts |
| `ReportGenerator` | Produces the automated KPI summary report |

Each class exposes a `run_pipeline()` method, so the full workflow reads as:

```python
df = DataLoader(RAW_DATA_PATH).load()
df = DataCleaner(df).run_pipeline()
df = FeatureEngineer(df).run_pipeline()
EDAAnalyzer(df).run_pipeline()
Visualizer(df).run_pipeline()
ReportGenerator(df).run_pipeline()
```

## ✨ Key Features

- **Advanced data cleaning** — missing value imputation, duplicate removal, format standardization, IQR-based outlier flagging (preserved, not dropped, for full traceability)
- **Feature engineering** — Profit Margin (zero-division safe via `np.where`), Shipping Duration, Sales Performance Category, Order Year/Month
- **Statistical analysis** — correlation matrix, distribution analysis, monthly trend analysis
- **9 visualizations** across distribution, comparison, trend, and correlation chart types
- **Automated KPI reporting** — pulled live from the data, not hardcoded
- **Memory optimization** — numeric downcasting + categorical dtype conversion, with before/after comparison
- **Robust exception handling** across file I/O, date parsing, and division-safe calculations

## 📈 Visualizations

| # | Chart |
|---|---|
| 1 | Sales Distribution |
| 2 | Profit Boxplot |
| 3 | Sales by Category |
| 4 | Profit by Sub-Category |
| 5 | Monthly Sales Trend |
| 6 | Correlation Heatmap |
| 7 | Sales vs. Profit Scatter |
| 8 | Sales Performance Category Counts |
| 9 | Shipping Duration by Ship Mode |

*(All saved in `output/charts/`)*

## 🔑 Key Insights & KPIs

| Metric | Value |
|---|---|
| Total Sales | $2,297,200.86 |
| Total Profit | $286,397.02 |
| Overall Profit Margin | 12.47% |
| Average Shipping Duration | 3.96 days |
| Total Orders | 5,009 |
| Total Customers | 793 |
| Best Region (Profit) | West |
| Worst Region (Profit) | Central |

**Business takeaways:**
- **Technology** is the strongest-performing category overall.
- **Furniture** drives high sales but comparatively weak profit.
- **West** is the top-performing region; **Central** underperforms on profit.
- **Tables, Bookcases, and Supplies** need margin review — consistently low/negative profit.
- **Discounts show a strong negative correlation with Profit Margin** — heavier discounting erodes profitability.
- Average shipping takes ~4 days across orders.

## 🛠️ Tech Stack

- **Python 3.10+**
- **Pandas** & **NumPy** — data wrangling and numerical operations
- **Matplotlib** & **Seaborn** — visualization
- **xlrd** — legacy `.xls` file support
- **logging** — pipeline-level tracking and exception logging
- **Jupyter Notebook** — documented, reproducible workflow

## ▶️ How to Run

```bash
# Clone the repo
git clone https://github.com/<your-username>/superstore-analytics-pipeline.git
cd superstore-analytics-pipeline

# Install dependencies
pip install pandas numpy matplotlib seaborn xlrd jupyter

# Launch the notebook
jupyter notebook mini_project_1.ipynb
```

Run all cells top-to-bottom — the pipeline will regenerate the cleaned datasets, charts, and KPI report automatically in `output/`.

## ✅ Requirements Checklist

- [x] Import & inspect dataset
- [x] Advanced cleaning (missing values, outliers, formats, duplicates)
- [x] Reusable preprocessing pipeline
- [x] Feature engineering (Profit Margin, Shipping Duration, Sales Performance Category)
- [x] Modular OOP-based functions
- [x] Advanced EDA
- [x] Statistical analysis (correlation, distribution, trend)
- [x] 9 visualizations (exceeds minimum of 8)
- [x] Automated KPI summary/report
- [x] Exported cleaned dataset + visuals
- [x] Memory/performance optimization
- [x] Exception handling throughout
- [x] Full workflow documentation in notebook

## 👤 Author

**Omar** — B.Tech. Data Science & AI Student, ElSewedy University of Technology (Polytechnic of Egypt)

---

*Built as part of a Data Analysis course project (Mini-Project 1, 100 marks).*
