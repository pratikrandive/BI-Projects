# Pharma Drug Sales Performance Dashboard

An enterprise-level Power BI reporting solution designed to analyze historical pharmaceutical drug sales across hourly, daily, weekly, monthly, quarterly, and yearly granularities. This project transforms raw transaction logs into interactive visual insights, helping stakeholders track sales contribution, top-performing ATC drug categories, and period-over-period trends.

---

## Executive Summary & Dashboard Preview

![Pharma Drug Sales Performance Dashboard](Dashboard Screenshot.jpg)

### Key Performance Highlights
* **Total Monthly Sales**: ₹126.58K across tracked categories.
* **Average Monthly Sales**: ₹15.8K.
* **Highest Hourly Volume**: 251 units sold for the top-performing drug category (`N02BE`).
* **Top Category Dominance**: `N02BE` accounts for **49.38%** of total daily sales volume.

---

## Technical Stack & Architecture

* **BI Platform**: Microsoft Power BI Desktop & Service
* **Data Sources**: CSV Files (Daily, Hourly, Weekly, Monthly transactional data)
* **Data Transformation**: Power Query / M
* **Data Modeling & Calculations**: DAX (Data Analysis Expressions)
* **Target Audience**: Sales Operations, Product Managers, Executive Leadership

---

## Data Pipeline & ETL Transformation Process

1. **Data Ingestion**: Imported four dedicated sales datasets (`salesdaily.csv`, `saleshourly.csv`, `salesweekly.csv`, `salesmonthly.csv`).
2. **Data Cleaning & Standardization**:
   * Resolved date formatting errors and standardized text cases.
   * Filtered out duplicate rows, null values, and rows containing calculation errors.
   * Renamed technical column headers into standardized ATC drug classification codes (`M01AB`, `M01AE`, `N02BA`, `N02BE`, `N05B`, `N05C`, `R03`, `R06`).
3. **Data Modeling**: Extracted calendar dimensions (Week Numbers, Months, Quarters, Years) to enable multi-period drill-down analytics.

---

## Key DAX Measures & Analytics Logic

```dax
// Total Monthly Sales
Total Monthly Sales = 
SUMX(
    'salesmonthly',
    'salesmonthly'[M01AB] + 'salesmonthly'[M01AE] + 'salesmonthly'[N02BA] + 
    'salesmonthly'[N02BE] + 'salesmonthly'[N05B] + 'salesmonthly'[N05C] + 
    'salesmonthly'[R03] + 'salesmonthly'[R06]
)

// Average Monthly Sales
AVG Monthly Sales = 
DIVIDE([Total Monthly Sales], 8, 0)

// Weekly Sales Contribution By N02BE
Weekly Sales Contribution By N02BE = 
DIVIDE('Sales Weekly'[Weekly Sales], SUM('Sales Weekly'[N02BE]), 0) * 100

// Total Daily Sales
Total Daily Sales = 
SUMX(
    'salesdaily',
    'salesdaily'[M01AB] + 'salesdaily'[M01AE] + 'salesdaily'[N02BA] + 
    'salesdaily'[N02BE] + 'salesdaily'[N05B] + 'salesdaily'[N05C] + 
    'salesdaily'[R03] + 'salesdaily'[R06]
)
```

---

## Key Dashboard Features

* **Executive KPI Cards**: Instant visibility into monthly revenue, averages, hourly peak counts, and N02BE contribution rates.
* **Weekly Category Breakdown**: Stacked Column Chart evaluating sales distributions across the initial 10-week period.
* **Hourly Demand Patterns**: Horizontal Stacked Bar Chart tracking sales distribution across 24-hour cycles.
* **Category Contribution**: Donut/Pie Chart highlighting the percentage revenue contribution of each drug category.
* **Quarterly Sales vs. Total Trend**: Combination Line & Clustered Column Chart contrasting quarterly category performance against total monthly trends.
* **Multi-Year Trend Analysis**: Stacked Area Chart monitoring category shifts from 2014 through 2019.
* **Dynamic Slicers**: Year-level interactive filtering to isolate specific reporting periods.

---

## Project Repository Structure

```plaintext
├── assets/
│   └── Dashboard Screenshot.jpg      # High-res screenshot of the Power BI dashboard
├── data/
│   ├── salesdaily.csv                # Daily sales transactions
│   ├── saleshourly.csv               # Hourly sales logs
│   ├── salesweekly.csv               # Aggregated weekly sales data
│   └── salesmonthly.csv              # Monthly category totals
├── Pharma_Drug_Sales_Performance.pbix # Power BI Dashboard File
└── README.md                         # Project documentation
```

---

## How to Replicate & View

1. Clone or download this repository to your local machine:

```bash
git clone https://github.com/your-username/pharma-drug-sales-dashboard.git
```

2. Open Power BI Desktop.
3. Open `Pharma_Drug_Sales_Performance.pbix`.
4. If prompted to update data source paths, go to **Transform Data > Data Source Settings** and point the path to the local `/data` directory.
5. Click **Refresh** to reload the dataset.
