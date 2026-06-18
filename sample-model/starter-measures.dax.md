# Starter Measures (DAX)

Use these as baseline measures for demo reports.

```DAX
[Revenue] =
SUM ( FactSales[SalesAmount] )
DAX
[Total Cost] =
SUM ( FactSales[TotalCost] )
DAX
[Gross Margin] =
[Revenue] - [Total Cost]
DAX
[Gross Margin %] =
DIVIDE ( [Gross Margin], [Revenue] )
DAX
[Orders] =
COUNTROWS ( FactSales )
DAX
[Units Sold] =
SUM ( FactSales[OrderQuantity] )
DAX
[Average Selling Price] =
DIVIDE ( [Revenue], [Units Sold] )
DAX
[Revenue YTD] =
TOTALYTD ( [Revenue], DimDate[Date] )
DAX
[Revenue YoY %] =
VAR _Current = [Revenue]
VAR _Prior =
    CALCULATE ( [Revenue], DATEADD ( DimDate[Date], -1, YEAR ) )
RETURN
    DIVIDE ( _Current - _Prior, _Prior )
