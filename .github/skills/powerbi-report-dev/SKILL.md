# Skill: Power BI Report Development

## Purpose
Provide a structured process to design, build, validate, and document Power BI reports with strong semantic modeling, DAX quality, performance, and usability.

## When to use
- New report requests
- KPI pack implementation
- Semantic model refactors
- Report performance optimization
- UX/accessibility improvements

## Inputs required
- Business objective and decisions enabled by the report
- KPI definitions (business formula + desired grain)
- Data source inventory and refresh expectations
- User personas (exec, analyst, operations)
- Security requirements (RLS)
- Scope constraints and timeline

## Workflow

### Step 1: Requirement Intake
Use `templates/requirement-intake.md`.

Output:
- Objective and scope
- Out-of-scope
- KPI list and ownership
- Assumptions and open questions
- Acceptance criteria

### Step 2: Semantic Model Design
Use `templates/semantic-model-checklist.md`.

Output:
- Fact/dimension mapping
- Relationship matrix
- Grain and key strategy
- Data quality and conformance checks

### Step 3: DAX Authoring
Use `templates/dax-measure-template.md`.

Output:
- Base measures
- Derived/ratio measures
- Time intelligence measures
- Filter context notes and edge-case handling

### Step 4: Report UX/Page Design
Use `templates/report-page-spec.md`.

Output:
- Page-level purpose
- Visual inventory and mapping to measures
- Slicer/navigation behavior
- Accessibility notes

### Step 5: Validation and Performance
Use `templates/validation-checklist.md`.

Output:
- Reconciliation outcomes
- Filter context test results
- RLS verification
- Performance observations and remediations

### Step 6: Delivery/PR Packaging
Use `templates/pr-template.md`.

Output:
- Change summary
- Risks and mitigations
- Test evidence
- Follow-up recommendations

## Quality bar
- Star schema or documented exception
- No unexplained DAX logic
- KPI definitions traceable to source/business owner
- Validation evidence captured
- Security impact explicitly stated
