# DAX Style Guide

## Core principles
- Use `VAR` for readability and repeat-use expressions
- Keep measures focused and composable
- Prefer `DIVIDE()` over `/` for safe division
- Prefer measures over calculated columns for aggregations

## Formatting
- One measure per block
- Include short purpose comments for non-obvious logic
- Use consistent indentation and spacing

## Filter context
- Be explicit when overriding filter context
- Document any use of `ALL`, `REMOVEFILTERS`, `ALLEXCEPT`, `KEEPFILTERS`

## Anti-patterns to avoid
- Monolithic measures with mixed concerns
- Unnecessary row-context iterators on large tables
- Hidden dependency chains without documentation
