# DAX Measures

Create these under `Home → New Measure` (or right-click the table in the Fields pane → `New Measure`). Put them all in a dedicated measures table for a clean model — `Modeling → New Table`, name it `_Measures`, and move each measure into it via its properties.

## Core financial measures

**Total Revenue**
```
Total Revenue = SUM('Financial_KPI_Data'[Revenue])
```
Adds up every transaction's revenue. This is the base number almost every other measure builds on.

**Total Cost**
```
Total Cost = SUM('Financial_KPI_Data'[Cost of Goods Sold]) + SUM('Financial_KPI_Data'[Operating Expenses])
```
Combined direct (COGS) and indirect (operating) cost — the full cost picture, not just production cost.

**Gross Profit**
```
Gross Profit = [Total Revenue] - SUM('Financial_KPI_Data'[Cost of Goods Sold])
```
What's left after covering the direct cost of goods sold, before overhead.

**Net Profit**
```
Net Profit = [Gross Profit] - SUM('Financial_KPI_Data'[Operating Expenses])
```
What's actually left after every cost. This is the bottom-line profitability number.

**Profit Margin %**
```
Profit Margin % = DIVIDE([Net Profit], [Total Revenue], 0)
```
Net Profit as a share of revenue. `DIVIDE` is used instead of `/` so the measure returns 0 (not an error) when revenue is 0 for a filtered slice.

## Budget measures

**Budgeted Revenue**
```
Budgeted Revenue = SUM('Financial_KPI_Data'[Budgeted Revenue])
```

**Actual Revenue**
```
Actual Revenue = SUM('Financial_KPI_Data'[Actual Revenue])
```

**Budget Variance**
```
Budget Variance = [Actual Revenue] - [Budgeted Revenue]
```
Positive means the company beat budget; negative means it fell short.

**Budget Variance %**
```
Budget Variance % = DIVIDE([Budget Variance], [Budgeted Revenue], 0)
```
Same idea as Budget Variance, expressed as a percentage so a $50K miss on a $5M budget doesn't look as alarming as a $50K miss on a $200K budget.

## Growth and ratio measures

**Revenue Growth %**
```
Revenue Growth % =
VAR CurrentRevenue = [Total Revenue]
VAR PreviousRevenue = CALCULATE([Total Revenue], DATEADD('Financial_KPI_Data'[Date], -1, MONTH))
RETURN DIVIDE(CurrentRevenue - PreviousRevenue, PreviousRevenue, 0)
```
Compares the current filter context's revenue to the prior month. Needs a proper Date table marked as the model's date table for `DATEADD` to work correctly.

**Cost Ratio %**
```
Cost Ratio % = DIVIDE([Total Cost], [Total Revenue], 0)
```
What share of every revenue rupee/dollar gets eaten by cost. A rising Cost Ratio % alongside flat revenue is an early warning sign before Net Profit itself drops.

## Category and region measures

**Region-wise Revenue**
```
Region-wise Revenue = CALCULATE([Total Revenue], ALLEXCEPT('Financial_KPI_Data', 'Financial_KPI_Data'[Region]))
```
Forces the revenue total to always break down by Region regardless of what other slicers are active — useful in a matrix or a "Best Performing Region" card.

**Category-wise Profitability**
```
Category-wise Profitability = CALCULATE([Net Profit], ALLEXCEPT('Financial_KPI_Data', 'Financial_KPI_Data'[Product Category]))
```
Same pattern, applied to Net Profit by Product Category — this is what powers the "most profitable category" insight, which is often a different category than the highest-revenue one.

## Helper measures for KPI cards

**Best Performing Region**
```
Best Performing Region =
VAR RankedRegions =
    TOPN(1, VALUES('Financial_KPI_Data'[Region]), CALCULATE([Total Revenue]), DESC)
RETURN
    CONCATENATEX(RankedRegions, 'Financial_KPI_Data'[Region])
```
Returns the single highest-revenue region as text, for a callout card.

**Best Performing Product Category**
```
Best Performing Product Category =
VAR RankedCategories =
    TOPN(1, VALUES('Financial_KPI_Data'[Product Category]), CALCULATE([Net Profit]), DESC)
RETURN
    CONCATENATEX(RankedCategories, 'Financial_KPI_Data'[Product Category])
```
Same logic, ranked by Net Profit instead of Revenue — deliberately, since the highest-revenue category isn't always the most profitable one.

**Channel-wise Profitability**
```
Channel-wise Profitability = CALCULATE([Net Profit], ALLEXCEPT('Financial_KPI_Data', 'Financial_KPI_Data'[Sales Channel]))
```
Same ALLEXCEPT pattern applied to Sales Channel, for the donut chart / channel comparison table.
