Build or modify a Power BI report using the repository Power BI framework.

Follow this sequence:
1) Requirement intake
2) Semantic model plan
3) DAX plan and implementation
4) Report page/UX specification
5) Validation execution
6) PR packaging

Use these templates:
- templates/requirement-intake.md
- templates/semantic-model-checklist.md
- templates/dax-measure-template.md
- templates/report-page-spec.md
- templates/validation-checklist.md
- templates/pr-template.md

Constraints:
- Prefer star schema (document any exception)
- Build base measures first, then derived/time-intelligence
- Use clear naming and variables in DAX
- Include assumptions and open questions
- Include reconciliation + performance + RLS checks
- Produce concise deliverable notes for PR
