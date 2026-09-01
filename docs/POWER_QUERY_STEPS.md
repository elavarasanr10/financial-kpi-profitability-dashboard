# Power Query Steps

Load `Raw_Dataset_Before_Cleaning.xlsx` into Power BI first if you want to practice the cleanup yourself. Otherwise load `Financial_KPI_Dataset.xlsx` directly, which is already clean.

## 1. Get Data

`Home → Get Data → Excel Workbook` → select the file → check the data table → `Transform Data` to open Power Query Editor.

## 2. Remove null values

The raw file has a few blank cells in **Region** and **Operating Expenses**.

- Select the **Region** column → `Home → Remove Rows → Remove Blank Rows` (or right-click the column header → `Remove Empty`).
- For **Operating Expenses**, replace nulls with 0 instead of deleting the row, since the rest of that transaction's data is still valid: right-click the column → `Replace Values` → replace `null` with `0`.

*Why the difference:* a missing Region breaks every region-based visual, so that row is dropped. A missing Operating Expenses figure just needs a safe default so downstream profit formulas don't error.

## 3. Fix inconsistent text casing

Some **Region** values came in lowercase (`west` instead of `West`). Select the column → `Transform → Format → Capitalize Each Word`.

## 4. Trim extra whitespace

Some **Department** values have leading/trailing spaces (`"  Sales "`), which makes Power BI treat `"Sales"` and `" Sales "` as two different categories. Select the column → `Transform → Format → Trim`.

## 5. Remove duplicate rows

Select all columns (`Ctrl+A` in the column headers) → `Home → Remove Rows → Remove Duplicates`. Power Query treats a row as a duplicate only if every column matches — that's intentional here, since two transactions with identical values across all 20 fields are almost certainly the same row loaded twice.

## 6. Change data types

Check each column's type icon in the header and correct any that Power Query guessed wrong:

- **Date** → Date
- **Revenue, Cost of Goods Sold, Operating Expenses, Gross Profit, Net Profit, Budgeted Revenue, Actual Revenue, Budget Variance** → Fixed Decimal Number (or Decimal Number)
- **Profit Margin %** → Percentage
- **Year, Sales Volume** → Whole Number
- **Everything else (Region, Department, Product Category, Product Name, Customer Segment, Sales Channel, Month, Quarter)** → Text

`Transform → Data Type` dropdown, or click the type icon in the column header.

## 7. Confirm/derive Month, Quarter, Year

The dataset already includes these as columns, but if you're working from a raw date-only source, derive them in Power Query instead of hardcoding:

- **Month:** `Add Column → Date → Month → Name of Month`
- **Quarter:** `Add Column → Date → Quarter → Quarter of Year`, then optionally prefix with "Q" via `Add Column → Custom Column` using `"Q" & Text.From([Quarter])`
- **Year:** `Add Column → Date → Year → Year`

## 8. Rename columns

Keep names business-friendly and consistent — this dataset already uses clean names (`Cost of Goods Sold`, not `COGS`), so if you're renaming anything, match that style: full words, title case, no abbreviations, so the fields read cleanly in visual tooltips and legends.

## 9. Format currency and percentage fields

Formatting in Power Query is cosmetic only (it doesn't change the underlying value), so the more important step is setting the correct **data type** in step 6. Visual-level currency/percentage formatting is applied later in Power BI's Report view via the **Format** pane on each visual, or globally by setting the column's **Format** property in Model view (`$ English (United States)` for currency fields, `Percentage` for Profit Margin %).

## 10. Add calculated columns where needed

`Gross Profit`, `Net Profit`, `Profit Margin %`, and `Budget Variance` are already present as formula-driven columns in the Excel source. If you're rebuilding from scratch or a different raw file, add them in Power Query as custom columns:

- `Add Column → Custom Column → Gross Profit = [Revenue] - [Cost of Goods Sold]`
- `Add Column → Custom Column → Net Profit = [Gross Profit] - [Operating Expenses]`
- `Add Column → Custom Column → Profit Margin % = [Net Profit] / [Revenue]`
- `Add Column → Custom Column → Budget Variance = [Actual Revenue] - [Budgeted Revenue]`

Prefer building these as **DAX measures** instead (see `DAX_MEASURES.md`) rather than static Power Query columns — measures recalculate dynamically as slicers filter the report, while Power Query columns are fixed at refresh time.

## 11. Close & Apply

`Home → Close & Apply` to load the cleaned table into the Power BI data model.
