# Power BI Copilot Demo

This repository demonstrates a practical framework for developing, documenting, and scaling **Power BI report development with GitHub Copilot**.

It includes reusable standards, templates, and prompt assets that help teams build high-quality Power BI solutions with consistent modeling, DAX, performance, UX, validation, and governance practices.

## Repository Purpose

The goal of this repo is to show how to:

- Define global development rules for Power BI projects.
- Standardize report implementation workflows.
- Improve collaboration through source-control-friendly documentation and templates.
- Accelerate delivery of report enhancements and KPI packs using structured Copilot guidance.
- Raise quality by enforcing validation and review checklists.

## What’s Included

### 1) Global Copilot Instructions
Path: `.github/copilot-instructions.md`

Repository-wide guidance for:

- Modeling and DAX standards
- Performance optimization
- Report UX and accessibility
- Security and governance (including RLS)
- Definition of done and delivery expectations

### 2) Power BI Skill Pack
Path: `.github/skills/powerbi-report-dev/`

A reusable framework containing:

- `SKILL.md` — end-to-end delivery workflow
- `templates/` — intake, model checklist, DAX spec, page spec, validation, PR template
- `prompts/` — reusable prompt patterns for report build, optimization, and KPI packs
- `examples/` — reference DAX measures and star-schema patterns

### 3) Standards and Playbooks
Path: `docs/powerbi/`

- `standards/` — naming conventions, DAX style guide, performance guidance
- `playbooks/` — bug triage and enhancement workflow

## Quick Start Prompts

Use these reusable prompts to apply the Power BI framework quickly:

- [Generate Executive Report](.github/skills/powerbi-report-dev/prompts/generate-executive-report.prompt.md)  
  Create an executive-ready scorecard plan using the sample model and repository standards.

- [Build Report](.github/skills/powerbi-report-dev/prompts/build-report.prompt.md)  
  Run the full report development lifecycle (intake → model → DAX → UX → validation → PR packaging).

- [Optimize Model](.github/skills/powerbi-report-dev/prompts/optimize-model.prompt.md)  
  Identify model/DAX/report performance bottlenecks and propose prioritized improvements.

- [Create KPI Pack](.github/skills/powerbi-report-dev/prompts/create-kpi-pack.prompt.md)  
  Generate modular KPI measures with business definitions, assumptions, and validation tests.

## Recommended Workflow

1. Capture requirements using the intake template.
2. Design/validate the semantic model (prefer star schema).
3. Build measures in layers (base → derived → time intelligence).
4. Specify report pages, interactions, and accessibility behavior.
5. Run reconciliation, context, RLS, and performance checks.
6. Package and review changes with the PR template.

## Intended Audience

- Power BI developers
- Analytics engineers
- BI leads/architects
- Teams using GitHub + Copilot for BI delivery

## Contributing

Contributions should follow repository standards in `.github/copilot-instructions.md` and the templates under `.github/skills/powerbi-report-dev/templates/`.

When submitting changes:

- Keep commits focused and descriptive.
- Include validation evidence for model/DAX/report changes.
- Document assumptions and trade-offs.

## Notes

This repository is demonstration-oriented and intended to be adapted to your organization’s data platform, governance controls, and reporting requirements.
