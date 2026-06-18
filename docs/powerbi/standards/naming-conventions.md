# Power BI Naming Conventions

## Tables
- Fact tables: `Fact<Subject>` (e.g., `FactSales`)
- Dimension tables: `Dim<Subject>` (e.g., `DimCustomer`)

## Columns
- Business-friendly names with spaces where helpful
- Avoid cryptic abbreviations unless domain-standard

## Measures
- Base: `[Revenue]`, `[Total Cost]`
- Derived: `[Gross Margin]`, `[Average Order Value]`
- Ratios: `[Gross Margin %]`
- Time intelligence suffixes: `YTD`, `QTD`, `MTD`, `YoY %`

## Display folders
- Organize measures by business domain and type:
  - `Sales\Base`
  - `Sales\Derived`
  - `Sales\Time Intelligence`
