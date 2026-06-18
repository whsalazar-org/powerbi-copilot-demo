# Sample KPI Measures (Reference)

## Revenue
```DAX
[Revenue] =
SUM ( 'FactSales'[SalesAmount] )
```

## Total Cost
```DAX
[Total Cost] =
SUM ( 'FactSales'[TotalCost] )
```

## Gross Margin
```DAX
[Gross Margin] =
[Revenue] - [Total Cost]
```

## Gross Margin %
```DAX
[Gross Margin %] =
DIVIDE ( [Gross Margin], [Revenue] )
```

## Revenue YTD
```DAX
[Revenue YTD] =
TOTALYTD ( [Revenue], 'DimDate'[Date] )
```

## Revenue YoY %
```DAX
[Revenue YoY %] =
VAR _Current = [Revenue]
VAR _Prior =
    CALCULATE ( [Revenue], DATEADD ( 'DimDate'[Date], -1, YEAR ) )
RETURN
    DIVIDE ( _Current - _Prior, _Prior )
```
