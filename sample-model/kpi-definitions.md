# KPI Definitions (Demo)

## Revenue
- **Definition**: Total net sales amount after discounts.
- **Business formula**: Sum of `FactSales[SalesAmount]`.

## Total Cost
- **Definition**: Total cost of goods sold.
- **Business formula**: Sum of `FactSales[TotalCost]`.

## Gross Margin
- **Definition**: Profit before overhead.
- **Business formula**: Revenue - Total Cost.

## Gross Margin %
- **Definition**: Share of revenue retained as gross margin.
- **Business formula**: Gross Margin / Revenue.

## Orders
- **Definition**: Number of transaction lines.
- **Business formula**: Count of `FactSales[SalesKey]`.

## Units Sold
- **Definition**: Total quantity sold.
- **Business formula**: Sum of `FactSales[OrderQuantity]`.

## Average Selling Price (ASP)
- **Definition**: Revenue per unit sold.
- **Business formula**: Revenue / Units Sold.
