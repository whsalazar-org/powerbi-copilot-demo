# Sample Star Schema (Reference)

## Fact tables
- FactSales (grain: one row per sales transaction line)

## Dimension tables
- DimDate
- DimCustomer
- DimProduct
- DimGeography
- DimChannel

## Relationship guidelines
- Dimension (1) -> Fact (*) single-direction filtering
- Active relationship from DimDate[Date] to FactSales[OrderDate]
- Avoid bi-directional filters unless explicitly justified

## Notes
- Hide surrogate keys and technical columns from report view
- Ensure date table is marked and complete for time intelligence
