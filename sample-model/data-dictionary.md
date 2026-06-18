cat > sample-model/data-dictionary.md <<'EOF'
# Sample Model Data Dictionary

This document defines the sample star schema used to demonstrate the Power BI Copilot framework.

## Tables

### FactSales
- **Grain**: One row per sales transaction line.
- **Primary key**: `SalesKey`
- **Foreign keys**: `DateKey`, `ProductKey`, `CustomerKey`, `RegionKey`

| Column | Type | Description |
|---|---|---|
| SalesKey | Whole number | Unique transaction line identifier |
| DateKey | Whole number (YYYYMMDD) | Links to DimDate |
| ProductKey | Whole number | Links to DimProduct |
| CustomerKey | Whole number | Links to DimCustomer |
| RegionKey | Whole number | Links to DimRegion |
| OrderQuantity | Whole number | Units sold |
| UnitPrice | Decimal | Unit selling price |
| DiscountAmount | Decimal | Discount applied to line |
| SalesAmount | Decimal | Net sales after discount |
| TotalCost | Decimal | Cost of goods sold |

### DimDate
| Column | Type | Description |
|---|---|---|
| DateKey | Whole number (YYYYMMDD) | Surrogate date key |
| Date | Date | Calendar date |
| Year | Whole number | Calendar year |
| Quarter | Text | Calendar quarter |
| MonthNumber | Whole number | Month number (1-12) |
| MonthName | Text | Month name |
| WeekOfYear | Whole number | ISO week number |
| IsWeekend | Boolean | Weekend flag |

### DimProduct
| Column | Type | Description |
|---|---|---|
| ProductKey | Whole number | Product surrogate key |
| ProductName | Text | Product display name |
| Category | Text | Product category |
| Subcategory | Text | Product subcategory |
| UnitCost | Decimal | Unit product cost |
| ListPrice | Decimal | Unit list price |
| IsActive | Boolean | Active product flag |

### DimCustomer
| Column | Type | Description |
|---|---|---|
| CustomerKey | Whole number | Customer surrogate key |
| CustomerName | Text | Customer name |
| Segment | Text | Customer segment |
| Industry | Text | Customer industry |
| RegionKey | Whole number | Home region (reference) |
| JoinDate | Date | First active date |
| IsActive | Boolean | Active customer flag |

### DimRegion
| Column | Type | Description |
|---|---|---|
| RegionKey | Whole number | Region surrogate key |
| RegionName | Text | Region name |
| Country | Text | Country |
| SalesTerritory | Text | Territory grouping |
