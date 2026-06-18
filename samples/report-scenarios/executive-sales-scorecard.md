
Demo Scenario: Executive Sales Scorecard
Objective
Provide leadership with a one-page view of revenue performance, margin health, and trend direction.

Suggested visuals
KPI cards:
Revenue
Gross Margin
Gross Margin %
Revenue YoY %
Line chart:
Axis: DimDate[Date]
Values: Revenue, Revenue YTD
Clustered bar chart:
Axis: DimRegion[RegionName]
Values: Revenue, Gross Margin
Matrix:
Rows: DimProduct[Category], DimProduct[Subcategory]
Values: Revenue, Gross Margin %, Units Sold
Slicers
Date (Month/Date)
Region
Customer Segment
Product Category
Validation checks
Revenue card equals sum of visible revenue rows in matrix.
Margin % remains mathematically consistent under all slicers.
Region totals reconcile with fact table aggregates. 
