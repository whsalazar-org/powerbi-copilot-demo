
Demo Scenario: Product Performance Analysis
Objective
Help product managers identify top and low-performing categories and subcategories.

Suggested visuals
Bar chart:
Axis: DimProduct[Subcategory]
Values: Revenue
Scatter chart:
X: Units Sold
Y: Gross Margin %
Details: ProductName
Size: Revenue
Decomposition tree:
Analyze: Revenue
Explain by: Category -> Subcategory -> Region -> Segment
Table:
ProductName, Revenue, Total Cost, Gross Margin, Gross Margin %, Units Sold, ASP
Slicers
Date
Region
Segment
Category
Validation checks
Subcategory totals match product-level rollups.
ASP remains stable and explainable by pricing/discount patterns.
Outliers in scatter chart are explainable from raw rows. 
