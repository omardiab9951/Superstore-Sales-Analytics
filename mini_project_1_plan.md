# Mini-Project 1 — Advanced Python Data Exploration & Automated Reporting
### Dataset: Sample - Superstore 2019.xls

A step-by-step build plan from scratch, matching all grading requirements (100 marks).

---

## Phase 0 — Setup
1. Create project folder structure:
   ```
   mini_project_1/
   ├── data/
   │   └── Sample - Superstore 2019.xls
   ├── output/
   │   ├── cleaned_data.csv
   │   └── charts/
   ├── mini_project_1.ipynb
   └── report_summary.txt
   ```
2. Install/import libraries: `pandas`, `numpy`, `matplotlib`, `seaborn`, `os`, `logging`.
3. Set global plot style (e.g. `sns.set_theme()`).
4. Set up basic `logging` config (for exception handling + tracking pipeline steps).

---

## Phase 1 — Import & Inspect Data
1. Load the `.xls` file with `pd.read_excel()` inside a `try/except` block.
2. Inspect structure:
   - `.shape`, `.info()`, `.head()`, `.tail()`
   - `.dtypes`, `.columns`
   - `.describe()` for numeric summary
   - `.isnull().sum()` for missing values overview
   - `.duplicated().sum()` for duplicate count
3. Note down initial observations (data types that look wrong, missing values, obvious issues) — you'll need these for the cleaning phase and final report.

---

## Phase 2 — Design the OOP Structure
Since OOP is a hard requirement, plan your classes **before** writing cleaning code. Suggested structure:

- **`DataLoader`** — handles reading the file, basic validation, exception handling.
- **`DataCleaner`** — handles missing values, duplicates, outliers, format fixes. Reusable/modular methods.
- **`FeatureEngineer`** — adds new columns (Profit Margin, Shipping Duration, Sales Performance Category).
- **`EDAAnalyzer`** — statistical analysis (correlations, distributions, trends).
- **`Visualizer`** — generates and saves all charts.
- **`ReportGenerator`** — builds the automated KPI summary/report and exports files.

Each class should:
- Take the DataFrame in via `__init__` or a method.
- Use `try/except` around risky operations (parsing, type conversion, division).
- Return/modify the DataFrame so classes can be chained.

---

## Phase 3 — Advanced Data Cleaning (inside `DataCleaner`)
1. **Missing values**: 
   - Identify columns with missing data.
   - Decide strategy per column (drop vs. fill with mean/median/mode/"Unknown").
   - Implement as a reusable method, e.g. `handle_missing_values(strategy='auto')`.
2. **Duplicates**: 
   - Detect and drop exact duplicate rows, log how many were removed.
3. **Inconsistent formats**:
   - Standardize text columns (e.g. `.str.strip()`, `.str.title()`).
   - Fix date columns with `pd.to_datetime()` (wrap in try/except for bad formats).
   - Standardize categorical values with inconsistent casing/spelling.
4. **Outliers**:
   - Detect using IQR method or Z-score on numeric columns (Sales, Profit, Discount, Quantity).
   - Decide: cap, remove, or flag outliers (document your reasoning).
5. Wrap each step in a method so the whole cleaning process can run as one pipeline call, e.g.:
   ```python
   cleaner = DataCleaner(df)
   df_clean = cleaner.run_pipeline()
   ```

---

## Phase 4 — Feature Engineering (inside `FeatureEngineer`)
Create these new columns (all as reusable methods):
1. **Profit Margin** = `Profit / Sales` (handle division by zero with try/except or `np.where`).
2. **Shipping Duration** = `Ship Date - Order Date` (in days).
3. **Sales Performance Category** — bucket Sales or Profit into categories (e.g. Low/Medium/High) using `pd.cut()` or custom logic.
4. Optional extra features that strengthen the analysis: Order Year/Month (from Order Date), Discount Impact, Profit per Unit.

---

## Phase 5 — Exploratory Data Analysis (inside `EDAAnalyzer`)
1. **Univariate analysis**: distributions of Sales, Profit, Discount, Quantity.
2. **Categorical breakdowns**: sales/profit by Region, Category, Sub-Category, Segment.
3. **Time trends**: sales/profit over time (monthly/yearly).
4. **Correlation analysis**: correlation matrix between numeric variables (Sales, Profit, Discount, Quantity, Profit Margin, Shipping Duration).
5. Document key findings/insights as you go — you'll need them for the final report.

---

## Phase 6 — Visualizations (inside `Visualizer`, minimum 8 charts)
Plan at least 8, mixing Matplotlib and Seaborn. Suggestions:
1. Sales distribution (histogram/KDE)
2. Profit distribution (histogram/boxplot — good for showing outliers too)
3. Sales by Category (bar chart)
4. Profit by Sub-Category (bar chart, sorted)
5. Sales trend over time (line chart, monthly)
6. Correlation heatmap (Seaborn `heatmap`)
7. Sales vs Profit scatter plot (colored by Category or Region)
8. Sales Performance Category counts (bar/count plot)
9. (Optional) Regional performance comparison (grouped bar chart)
10. (Optional) Shipping Duration distribution by Ship Mode

Save each chart automatically to `output/charts/` with descriptive filenames.

---

## Phase 7 — Automated KPI Summary & Report (inside `ReportGenerator`)
1. Calculate key KPIs programmatically:
   - Total Sales, Total Profit, Overall Profit Margin
   - Average Shipping Duration
   - Top 5 products/sub-categories by Sales and by Profit
   - Best/worst performing Region or Segment
2. Format these into a readable text/markdown summary, generated automatically (not hardcoded — pull live from the DataFrame).
3. Save this as `report_summary.txt` (or `.md`).

---

## Phase 8 — Export & Performance Optimization
1. Export the cleaned dataset: `df_clean.to_csv('output/cleaned_data.csv', index=False)`.
2. Optimize memory usage:
   - Downcast numeric types (`pd.to_numeric(..., downcast=...)`).
   - Convert repetitive text columns to `category` dtype.
   - Compare `.memory_usage(deep=True)` before/after optimization and note the improvement.
3. Confirm all outputs (CSV + charts + report) exist in the `output/` folder.

---

## Phase 9 — Documentation (in the Notebook)
1. Add markdown cells explaining each phase (what you did and why) — this is graded.
2. Structure the notebook to mirror this plan: Setup → Load → Clean → Feature Engineer → EDA → Stats → Visuals → KPI Report → Export → Optimization → Conclusion.
3. End with a short written conclusion: 3–5 key business insights derived from the analysis.

---

## Quick Checklist Against Requirements
- [ ] Import + inspect dataset
- [ ] Advanced cleaning (missing, outliers, formats, duplicates)
- [ ] Reusable preprocessing pipeline
- [ ] Feature engineering (Profit Margin, Shipping Duration, Sales Performance Category)
- [ ] Modular functions/classes
- [ ] Advanced EDA
- [ ] Statistical analysis (correlation, distribution, trend)
- [ ] 8+ visualizations (Matplotlib + Seaborn)
- [ ] Automated KPI summary/report
- [ ] Exported cleaned dataset + visuals
- [ ] Memory/performance optimization
- [ ] OOP used throughout
- [ ] Exception handling used throughout
- [ ] Full documentation in notebook
