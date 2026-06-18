# Executive Sales Scorecard — Report Specification & Build Plan

## Phase 1 — Intake

### Business objective
Provide an executive-ready, single-page scorecard that enables leadership to evaluate revenue performance, profitability quality, and trend direction, then make an informed next-quarter **region focus** decision.

### Executive audience
- Primary: **CFO**
- Secondary: COO, Sales VP

### Decisions supported
- Which regions should receive incremental sales investment next quarter.
- Whether current growth is high-quality (revenue + healthy margin).
- Which product categories/subcategories are strengthening or diluting performance.

### KPI definitions in scope
From `sample-model/kpi-definitions.md`:
- Revenue
- Total Cost
- Gross Margin
- Gross Margin %
- Orders
- Units Sold
- Average Selling Price (ASP)

From `sample-model/starter-measures.dax.md`:
- Revenue
- Total Cost
- Gross Margin
- Gross Margin %
- Orders
- Units Sold
- Average Selling Price
- Revenue YTD
- Revenue YoY %

### Assumptions
- Reporting focus is **Current Month + YTD**.
- `DimDate[Date]` will be marked as the model Date table.
- Relationships follow the defined single-direction star schema.
- Executive benchmark: **Gross Margin % target = 35%**.
- No additional source systems beyond provided CSV/model assets.

### Open questions
1. Should default date context be “current month to date” or “last completed month”?
2. Is the primary executive trigger based on GM% target breach, YoY decline, or both?
3. Should region ranking prioritize Revenue, Gross Margin dollars, or Margin %?
4. Are there planned role-based views (e.g., CFO full access vs regional leadership filtered)?

### Acceptance criteria
- One-page executive scorecard is implementable directly in Power BI.
- KPI cards, trend, regional, and product views reconcile under filters.
- GM% target variance is visible and conditionally formatted.
- Slicer behavior is minimal and intuitive.
- Validation checklist is complete (reconciliation, context, performance, security, accessibility).

---

## Phase 2 — Semantic Model Plan

### Fact/dimension mapping
- **Fact table**: `FactSales`
  - Keys: `DateKey`, `ProductKey`, `CustomerKey`, `RegionKey`
  - Metrics: `SalesAmount`, `TotalCost`, `OrderQuantity`, `DiscountAmount`, `UnitPrice`
- **Dimension tables**:
  - `DimDate` (`DateKey`, `Date`, year/quarter/month attributes)
  - `DimProduct` (`ProductKey`, `Category`, `Subcategory`, `ProductName`)
  - `DimCustomer` (`CustomerKey`, `Segment`, `Industry`)
  - `DimRegion` (`RegionKey`, `RegionName`, `SalesTerritory`)

### Relationship validation against `relationship-map.md`
Required active relationships:
- `DimDate[DateKey]` (1) → `FactSales[DateKey]` (*)
- `DimProduct[ProductKey]` (1) → `FactSales[ProductKey]` (*)
- `DimCustomer[CustomerKey]` (1) → `FactSales[CustomerKey]` (*)
- `DimRegion[RegionKey]` (1) → `FactSales[RegionKey]` (*)

Filter direction:
- **Single direction** from dimensions to fact.

### Grain confirmation
- Fact grain: **one row per sales transaction line** (`SalesKey`).
- All executive KPIs aggregate from transaction-line grain via filter context.

### Risk flags
- Many-to-many: **No current risk** (monitor if additional bridge tables are added).
- Ambiguity: **Low risk** in current single-path star design.
- Cardinality:
  - Ensure dimension keys are unique.
  - Validate no orphan fact keys before productionizing.

---

## Phase 3 — DAX Plan

### Base measures (reuse starter measures)
```DAX
[Revenue] =
SUM ( FactSales[SalesAmount] )

[Total Cost] =
SUM ( FactSales[TotalCost] )

[Orders] =
COUNTROWS ( FactSales )

[Units Sold] =
SUM ( FactSales[OrderQuantity] )
```

### Derived measures (reuse starter measures)
```DAX
[Gross Margin] =
[Revenue] - [Total Cost]

[Gross Margin %] =
DIVIDE ( [Gross Margin], [Revenue] )

[Average Selling Price] =
DIVIDE ( [Revenue], [Units Sold] )
```

### Time-intelligence measures (reuse starter measures + executive extension)
```DAX
[Revenue YTD] =
TOTALYTD ( [Revenue], DimDate[Date] )

[Revenue YoY %] =
VAR _Current = [Revenue]
VAR _Prior =
    CALCULATE ( [Revenue], DATEADD ( DimDate[Date], -1, YEAR ) )
RETURN
    DIVIDE ( _Current - _Prior, _Prior )

[Revenue YTD YoY %] =
VAR _CurrentYTD = [Revenue YTD]
VAR _PriorYTD =
    CALCULATE ( [Revenue YTD], DATEADD ( DimDate[Date], -1, YEAR ) )
RETURN
    DIVIDE ( _CurrentYTD - _PriorYTD, _PriorYTD )
```

### Target and executive signal measures (new)
```DAX
[Gross Margin % Target] =
0.35

[Gross Margin % Variance to Target] =
[Gross Margin %] - [Gross Margin % Target]

[Executive Region Rank by Revenue] =
RANKX ( ALL ( DimRegion[RegionName] ), [Revenue],, DESC )
```

### Filter-context notes
- Keep measures fully context-responsive to Date, Region, Segment, and Category slicers.
- Avoid hardcoded filters for core executive KPIs.
- Use `DIVIDE` for denominator safety and consistent blank behavior.

### Edge-case behavior
- If prior-year context is unavailable, YoY measures return blank.
- If Revenue = 0, GM% returns blank (not error).
- Low-volume categories may show volatile GM%; annotate in narrative.

### Tests for critical KPIs
- Revenue equals sum of `FactSales[SalesAmount]` at total and filtered levels.
- Gross Margin equals Revenue minus Total Cost in all contexts.
- Gross Margin % is ratio of totals (not average of row-level percentages).
- Revenue YTD resets at year boundary and respects Date slicer.
- Region rank recalculates correctly with slicers.

---

## Phase 4 — Executive Page Spec

### Single-page executive layout
**Page name**: Executive Sales Scorecard

#### Top band (KPI cards)
1. Revenue  
2. Revenue YTD  
3. Revenue YoY %  
4. Gross Margin  
5. Gross Margin %  
6. GM% Variance to Target

#### Middle section
- Left: Revenue trend (month over month + YTD overlay)
- Right: Regional comparison (Revenue and Gross Margin)

#### Bottom section
- Left: Product performance matrix (Category/Subcategory)
- Right: Executive narrative panel (dynamic text summary)

### Visual inventory

1. **KPI Cards**
   - Measures: `[Revenue]`, `[Revenue YTD]`, `[Revenue YoY %]`, `[Gross Margin]`, `[Gross Margin %]`, `[Gross Margin % Variance to Target]`
   - Executive question: “Are we performing to plan right now?”

2. **Line Chart — Trend**
   - Axis: `DimDate[Date]` (monthly display)
   - Values: `[Revenue]`, `[Revenue YTD]`
   - Executive question: “Is current trajectory improving or weakening?”

3. **Clustered Bar — Region Performance**
   - Axis: `DimRegion[RegionName]`
   - Values: `[Revenue]`, `[Gross Margin]`
   - Tooltip: `[Gross Margin %]`, `[Executive Region Rank by Revenue]`
   - Executive question: “Where should next-quarter focus go?”

4. **Matrix — Product Summary**
   - Rows: `DimProduct[Category]`, `DimProduct[Subcategory]`
   - Values: `[Revenue]`, `[Gross Margin %]`, `[Units Sold]`, `[Average Selling Price]`
   - Executive question: “Which product areas drive profitable growth?”

### Measure mapping by visual
- KPI cards: headline metrics and target variance.
- Trend: period movement and cumulative momentum.
- Region chart: investment prioritization.
- Matrix: product mix and profitability quality.

### Slicer strategy (low cognitive load)
Include only:
- Date
- Region
- Customer Segment
- Product Category

Default behavior:
- Date defaults to Current Month context; YTD measures remain visible.
- Others default to All.
- Sync slicers only on this page (single-page report).

### Interaction and drill behavior
- Cross-filtering ON for all visuals.
- Matrix drill-down Category → Subcategory enabled.
- No drillthrough required for initial executive release (keep simple).

### Accessibility notes
- Use color-safe conditional formatting (not red/green only).
- Ensure tab order follows top-to-bottom reading flow.
- Provide concise alt text on each visual.
- Use dynamic titles reflecting active filters.

---

## Phase 5 — Validation & Performance

### Reconciliation checks
- Validate `[Revenue]` against raw aggregate of `FactSales[SalesAmount]`.
- Validate `[Total Cost]` against raw aggregate of `FactSales[TotalCost]`.
- Confirm regional totals roll up to grand total under identical filters.
- Confirm matrix subtotals align with chart totals.

### Context behavior checks
- Test each slicer independently, then in combinations.
- Verify YoY/YTD behavior across month/year boundaries.
- Verify no unexpected context leakage between visuals.

### RLS/security checks
- Demo baseline: executive unrestricted view.
- If RLS is introduced:
  - Test by role for data visibility correctness.
  - Re-run reconciliation for each role.
  - Confirm no sensitive leakage in tooltips/narratives.

### Performance checks and mitigations
- Use Performance Analyzer for all visuals and interactions.
- Keep visuals to essential executive set (avoid dense tables).
- Reuse measures; avoid expensive repeated logic.
- Avoid unnecessary bi-directional filters or high-cardinality slicers.

---

## Phase 6 — PR-Ready Delivery

### Summary
Created an implementation-ready executive scorecard specification aligned with repository framework, sample model assets, and CFO decision needs (region focus for next quarter).

### Scope
- Executive page design blueprint.
- KPI/DAX measurement plan (including 35% GM target logic).
- Validation, performance, accessibility, and governance checklist.
- Delivery packaging guidance for PR.

### Model changes
- No mandatory schema changes.
- Confirm Date table marking and relationship integrity before report build.

### DAX changes
- Reuse starter measures.
- Add executive extension measures:
  - `[Gross Margin % Target]`
  - `[Gross Margin % Variance to Target]`
  - `[Revenue YTD YoY %]`
  - `[Executive Region Rank by Revenue]` (optional but recommended)

### UX changes
- KPI-first layout for leadership consumption.
- Minimal slicers and intuitive interactions.
- Conditional formatting tied to margin target variance.

### Validation evidence (attach in PR)
- Reconciliation table/screenshots.
- Slicer-context test cases.
- Performance Analyzer capture.
- Accessibility checklist completion notes.

### Risks and follow-ups
- Limited date history may constrain robustness of YoY interpretation.
- Follow-up recommended: define enterprise KPI threshold catalog and alerting bands.
- Optional extension: add plan/forecast dataset for target-vs-actual reporting.

---

## Build Sequence (Power BI Desktop)

1. Load `sample-data/*.csv`.
2. Create/validate relationships per `sample-model/relationship-map.md`.
3. Mark `DimDate[Date]` as Date table.
4. Implement starter measures from `sample-model/starter-measures.dax.md`.
5. Add executive extension measures from this spec.
6. Build visuals in prescribed layout order (top → middle → bottom).
7. Configure slicers, interactions, dynamic titles, conditional formatting.
8. Execute validation/performance/security/accessibility checks.
9. Package changes with PR template structure.

---

## Executive Narrative Layer (initial publish guidance)

- Revenue and YTD momentum indicate current commercial trajectory.
- Margin quality is evaluated against the **35% GM% target**.
- Regional performance highlights where next-quarter resources can generate strongest return.
- Product mix reveals where growth is profitable vs margin-dilutive.
- Scorecard emphasizes speed-to-insight for executive decision cycles.
