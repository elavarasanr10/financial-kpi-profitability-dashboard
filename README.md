# Financial KPI Monitoring & Profitability Dashboard

A Power BI dashboard that tracks revenue, cost, profit, and budget performance across regions, departments, and product categories — built to mirror how a Finance Analyst, Business Analyst, or FP&A team monitors company profitability in the real world.

## Objective

To design a financial monitoring system that helps management answer four questions at a glance:
1. Are we making money, and how much?
2. Are we hitting our budget targets?
3. Which regions, categories, and channels drive profit — and which drag it down?
4. Is profitability improving or declining over time?

## Tools Used

- **Power BI Desktop** — data modeling, DAX, dashboard build
- **Power Query** — data cleaning and transformation
- **Microsoft Excel** — source dataset
- **DAX (Data Analysis Expressions)** — KPI and measure logic
- **GitHub** — version control and portfolio hosting

## Dataset Description

`Financial_KPI_Dataset.xlsx` contains 150 transaction-level rows (Jan 2024 – Dec 2025) with 20 columns:

| Column | Description |
|---|---|
| Date | Transaction date |
| Month | Month name, derived from Date |
| Quarter | Q1–Q4, derived from Date |
| Year | Calendar year |
| Region | North / South / East / West / Central |
| Department | Sales, Marketing, Operations, Finance, Retail |
| Product Category | Electronics, Home Appliances, Furniture, Apparel, FMCG |
| Product Name | Specific product sold |
| Revenue | Total sales revenue for the row |
| Cost of Goods Sold | Direct cost of producing/sourcing the product |
| Operating Expenses | Indirect costs (marketing, admin, overhead) |
| Gross Profit | Revenue − Cost of Goods Sold |
| Net Profit | Gross Profit − Operating Expenses |
| Profit Margin % | Net Profit ÷ Revenue |
| Sales Volume | Units sold |
| Budgeted Revenue | Planned/target revenue for the row |
| Actual Revenue | Revenue actually achieved (equals Revenue) |
| Budget Variance | Actual Revenue − Budgeted Revenue |
| Customer Segment | Corporate, Retail, SME, Government, Individual |
| Sales Channel | Online, Retail Store, Distributor, Direct Sales, Marketplace |

A second file, `Raw_Dataset_Before_Cleaning.xlsx`, is the same data before cleanup — it deliberately contains null values, inconsistent text casing, extra whitespace, and duplicate rows so the Power Query cleaning steps below have something real to fix. Use this file for the "before," and load `Financial_KPI_Dataset.xlsx` (or your own cleaned export) into Power BI as the "after."

## Power Query Steps

See [`docs/POWER_QUERY_STEPS.md`](docs/POWER_QUERY_STEPS.md) for the full click-by-click walkthrough. Summary:

1. Remove/handle null values (Region, Operating Expenses)
2. Fix inconsistent text casing (Region) and trim whitespace (Department)
3. Remove duplicate rows
4. Change data types (Date, currency fields as decimal, Year as whole number)
5. Confirm/derive Month, Quarter, Year columns
6. Rename columns to business-friendly labels
7. Format currency and percentage fields
8. Add any calculated columns not already present

## DAX Measures

See [`docs/DAX_MEASURES.md`](docs/DAX_MEASURES.md) for every measure with its formula and a plain-language explanation. Includes: Total Revenue, Total Cost, Gross Profit, Net Profit, Profit Margin %, Budgeted Revenue, Actual Revenue, Budget Variance, Revenue Growth %, Cost Ratio %, Region-wise Revenue, Category-wise Profitability.

## Dashboard Features

- **KPI cards:** Total Revenue, Gross Profit, Net Profit, Profit Margin %, Budget Variance
- **Column chart:** Revenue by Region
- **Bar chart:** Profit by Product Category
- **Line chart:** Monthly Revenue and Profit trend
- **Donut chart:** Sales Channel distribution
- **Waterfall chart:** Revenue → Net Profit breakdown
- **Matrix table:** Region × Revenue, Cost, Profit Margin %
- **Slicers:** Region, Department, Product Category, Sales Channel, Month
- **Corporate color theme:** blue for neutral metrics, green for profit/positive variance, red/orange for cost or negative variance

## Key Insights

*(Fill in with your actual numbers once you build the dashboard — sample structure below)*

- The highest-revenue region and the margin gap between best and worst region
- The most profitable product category vs. the highest-revenue category (often not the same)
- Whether the company is over or under budget for the period, and by how much
- The direction of the profit margin trend over the two-year window
- Which sales channel delivers the best margin, not just the most volume

## Screenshots

Add dashboard screenshots here after building in Power BI Desktop:

```
screenshots/
  01-full-dashboard.png
  02-kpi-cards.png
  03-revenue-by-region.png
  04-monthly-trend.png
  05-waterfall-breakdown.png
```

![Dashboard Overview](screenshots01_full_dashboard.png)

## Repository Structure

```
financial-kpi-profitability-dashboard/
├── README.md
├── Financial_KPI_Dataset.xlsx
├── Raw_Dataset_Before_Cleaning.xlsx
├── Financial-KPI-Profitability-Dashboard.pbix   (add after building in Power BI Desktop)
├── docs/
│   ├── POWER_QUERY_STEPS.md
│   ├── DAX_MEASURES.md
│   ├── PROJECT_OVERVIEW.md
│   ├── RESUME_DESCRIPTIONS.md
│   ├── LINKEDIN_CONTENT.md
│   └── PROJECT_CHECKLIST.md
└── screenshots/
    └── (dashboard images go here)
```

## Conclusion

This project demonstrates an end-to-end BI workflow: messy raw data → cleaned and modeled data → DAX-driven KPIs → a decision-ready dashboard. It reflects the kind of financial monitoring tool used in FP&A, business analysis, and management consulting roles to track profitability and support budget decisions.

**Author:** Elavarasan R  
**Role:** Business / Data Analyst
