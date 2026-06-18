# Copilot Instructions for Power BI Development

These instructions define **global standards** for this repository. Follow them for all Power BI changes unless a task explicitly says otherwise.

## 1) Project Goals

- Build clear, trustworthy, and maintainable Power BI solutions.
- Prioritize semantic model quality, performance, and usability over visual novelty.
- Keep changes small, reviewable, and documented.

## 2) Source Control and Branching

- Use feature branches for all work.
- Keep commits focused and atomic (one logical change per commit when practical).
- Write descriptive commit messages that explain *why* the change was made.
- Never commit secrets, credentials, API keys, or personal data.

## 3) File and Artifact Standards

- Prefer storing Power BI artifacts in source-control-friendly formats when possible:
  - `.pbip` project structure preferred over single binary `.pbix` for collaborative development.
  - Keep model metadata, report definitions, and supporting assets organized by feature area.
- Maintain consistent naming for reports, pages, visuals, measures, and columns.
- Remove obsolete/unused assets during refactors.

## 4) Data Modeling Rules

- Use a **star schema** whenever feasible:
  - Fact tables for events/transactions.
  - Dimension tables for descriptive attributes.
- Define clear relationships:
  - Prefer single-direction filtering unless a justified exception exists.
  - Avoid ambiguous many-to-many relationships when possible.
- Keep data types correct and explicit.
- Hide technical keys and helper columns from report view when not needed by authors.
- Use surrogate keys where appropriate and document business key assumptions.

## 5) DAX Standards

- Prefer **measures** over calculated columns for aggregations and business logic when feasible.
- Use variables (`VAR`) to improve readability and performance.
- Keep measures modular and composable (base measures + derived measures).
- Follow consistent naming conventions, e.g.:
  - Base measures: `[Sales Amount]`, `[Total Cost]`
  - Ratios/percentages: `[Gross Margin %]`
  - Time intelligence: `[Sales Amount YTD]`, `[Sales Amount YoY %]`
- Avoid unnecessarily complex DAX in a single measure; split into helper measures.
- Validate filter context explicitly for critical calculations.

## 6) Performance and Optimization

- Optimize at the model first, then DAX, then visuals.
- Minimize high-cardinality columns unless required.
- Reduce expensive iterators and row-by-row logic where possible.
- Prefer Import mode for interactive analytics unless scale/freshness requires DirectQuery or composite models.
- For DirectQuery/composite models:
  - Push transformations upstream when possible.
  - Avoid patterns that generate chatty SQL or excessive source round-trips.
- Keep report pages responsive (target fast slicer and visual interactions).

## 7) Power Query (M) and Data Preparation

- Keep transformations deterministic and readable.
- Name query steps clearly (no generic `Added Custom`, `Changed Type1` style names in finalized queries).
- Push heavy transformations to the source system or dataflows when practical.
- Ensure data type assignment is explicit and early.
- Avoid duplicating logic across multiple queries; centralize reusable transformations.

## 8) Report Design and UX

- Design for clarity first:
  - Clear titles, units, labels, and legends.
  - Consistent color and formatting conventions.
  - Avoid visual clutter and unnecessary decorative elements.
- Keep slicers and navigation predictable across pages.
- Ensure accessibility:
  - Sufficient color contrast.
  - Do not rely on color alone to convey meaning.
  - Provide meaningful alt text where appropriate.
- Prefer standard visuals unless a custom visual has a clear, documented benefit.

## 9) Security and Governance

- Implement Row-Level Security (RLS) where required by business rules.
- Follow least-privilege access principles for datasets and workspaces.
- Do not embed secrets in M code, parameters, or documentation.
- Document data sources, refresh expectations, and ownership.

## 10) Testing and Validation

For every meaningful change, validate:

- **Data correctness**: key metrics reconcile with trusted source(s).
- **DAX behavior**: measures return correct values across expected filter contexts.
- **Performance**: no significant regressions in report interaction.
- **UX consistency**: formatting and navigation stay coherent.
- **Security**: RLS and role behavior still work as intended.

## 11) Documentation Requirements

- Document major modeling and DAX decisions, especially trade-offs.
- Keep a changelog entry or PR description for user-visible/report-impacting changes.
- For new measures/tables, include short intent notes when not self-evident.

## 12) Definition of Done (Power BI)

A task is complete only when:

- Model changes are structurally sound and follow repository conventions.
- DAX is readable, reviewed, and validated.
- Report pages impacted by the change are tested for correctness and performance.
- Security implications are reviewed.
- Documentation is updated.

## 13) Copilot Behavior Rules

When generating or modifying Power BI assets, Copilot should:

- Prefer incremental, low-risk edits.
- Preserve existing naming and folder conventions.
- Explain assumptions when requirements are ambiguous.
- Propose alternatives when there are modeling or performance trade-offs.
- Flag potential governance/security concerns before implementation.

## 14) Out of Scope / Do Not Do

- Do not introduce breaking semantic model changes without explicit approval.
- Do not remove or rename widely used measures/columns without migration notes.
- Do not hardcode sensitive values or environment-specific secrets.
- Do not bypass validation steps for speed.

## 15) Framework Contract (Execution Phases)

When asked to develop or modify a Power BI report, execute these phases in order unless explicitly told otherwise:

1. **Intake**
   - Restate business objective, audience, grain, KPI definitions.
   - Document assumptions and open questions.
2. **Model Plan**
   - Propose/validate star schema and relationships.
   - Identify risks (many-to-many, ambiguous paths, high cardinality).
3. **DAX Plan**
   - Build base measures first, then derived, then time intelligence.
   - Define expected filter behavior.
4. **Report UX Plan**
   - Define page purpose, visuals, slicers, interactions, accessibility.
5. **Validation**
   - Reconciliation, filter-context tests, RLS checks, performance checks.
6. **Delivery**
   - Provide concise summary, test evidence, assumptions, and next steps.
