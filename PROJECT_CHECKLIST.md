# Dashboard Layout Spec, GitHub Setup, and Final Checklist

## Target dashboard layout

- **Top section — KPI cards:** Total Revenue, Gross Profit, Net Profit, Profit Margin %, Budget Variance. One row, five cards, equal width.
- **Middle section — charts:** column chart (Revenue by Region) and bar chart (Profit by Product Category) side by side; line chart (Monthly Revenue & Profit Trend) full width below them; donut chart (Sales Channel Distribution) and waterfall chart (Revenue → Net Profit breakdown) side by side beneath that.
- **Bottom section:** matrix table (Region × Revenue × Cost × Profit Margin %) plus a short text box with 3–4 key insights written in plain language.
- **Side panel (left or right):** slicers for Region, Department, Product Category, Sales Channel, and Month, stacked vertically, plus a date range filter.
- **Theme:** corporate blue for structural/neutral elements, green for profit and positive budget variance, red/orange for cost and negative variance. One font family throughout (e.g. Segoe UI). Consistent card corner radius and spacing — don't mix tight and loose padding across visuals.

## Repository name and description

**Repository name:** `financial-kpi-profitability-dashboard`

**One-line description:** Power BI dashboard tracking revenue, cost, profit, and budget performance across regions, departments, and product categories — built for FP&A and business analyst-style financial monitoring.

## GitHub upload steps

1. Create a GitHub account at github.com if you don't have one.
2. Click **New repository**.
3. Name it `financial-kpi-profitability-dashboard`, paste the one-line description above.
4. Set visibility to **Public** (so recruiters can view it without a login).
5. Check **Add a README file** (or skip this if you're uploading the one already prepared here).
6. Click **Create repository**.
7. On the repo page, click **Add file → Upload files**.
8. Drag in: `README.md`, `Financial_KPI_Dataset.xlsx`, `Raw_Dataset_Before_Cleaning.xlsx`, the `docs/` folder, the `screenshots/` folder (once you have images), and your `.pbix` file once it's built.
9. Write a commit message, e.g. "Initial commit: Financial KPI Monitoring & Profitability Dashboard".
10. Click **Commit changes**.

## Files to upload to GitHub

- [ ] `Financial-KPI-Profitability-Dashboard.pbix` (export/save from Power BI Desktop after building)
- [ ] `Financial_KPI_Dataset.xlsx` (clean dataset — already included)
- [ ] `Raw_Dataset_Before_Cleaning.xlsx` (optional but shows you can clean data — already included)
- [ ] `README.md` (already included)
- [ ] `docs/` folder — Power Query steps, DAX measures, project overview, resume/LinkedIn content (already included)
- [ ] Dashboard screenshots (`screenshots/` folder — capture after building)
- [ ] Optional: PDF export of the dashboard (`File → Export → Export to PDF` in Power BI Desktop)
- [ ] Optional: one-page project summary PDF for recruiters who won't open the full README

## Adding screenshots to the README

1. In Power BI Desktop, arrange the finished dashboard, then use `File → Export → Export to Image` (or a screenshot tool) to save PNGs.
2. Create a `screenshots/` folder in the repo and upload the images there.
3. In `README.md`, reference them with standard Markdown image syntax:
   `![Dashboard Overview](screenshots/01-full-dashboard.png)`
4. Keep file names descriptive and numbered so they stay in a sensible order in the file browser.

## Final checklist before publishing

- [ ] Dataset loads cleanly into Power BI with no Power Query errors
- [ ] All DAX measures return correct, non-error values (spot-check a few against `KPI_Summary` sheet in the Excel file)
- [ ] Every visual has a title and correctly formatted currency/percentage values
- [ ] Slicers are tested — filtering by Region/Month/Category updates every visual correctly
- [ ] Dashboard is visually consistent (one font, one color theme, aligned visuals)
- [ ] README.md is complete and all internal links (to `docs/`) work
- [ ] Screenshots are uploaded and displayed correctly in the README
- [ ] Repository is set to Public
- [ ] LinkedIn post drafted and GitHub link ready to drop in the first comment
