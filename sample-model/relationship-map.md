# Sample Model Relationship Map

## Relationship design (star schema)

- `DimDate[DateKey]` (1) -> `FactSales[DateKey]` (*)
- `DimProduct[ProductKey]` (1) -> `FactSales[ProductKey]` (*)
- `DimCustomer[CustomerKey]` (1) -> `FactSales[CustomerKey]` (*)
- `DimRegion[RegionKey]` (1) -> `FactSales[RegionKey]` (*)

## Filter direction
- Single direction from dimensions to fact table.

## Notes
- Keep all relationships active and single-direction for clarity.
- Avoid introducing many-to-many relationships in this demo model.
- Mark `DimDate[Date]` as date table when building the semantic model.
