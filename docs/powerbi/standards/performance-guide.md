# Power BI Performance Guide

## Priority order
1. Semantic model design
2. DAX optimization
3. Visual/report tuning

## Model optimization
- Reduce cardinality where possible
- Remove unused columns
- Validate relationship design and directionality
- Push heavy transformations upstream

## DAX optimization
- Reuse base measures
- Avoid unnecessary iterators on large tables
- Cache repeated expressions with variables
- Test expensive measures under realistic filter context

## Report optimization
- Limit visuals per page
- Avoid excessive interactions
- Use simple visuals for high-density pages
- Verify slicer performance with large dimensions
