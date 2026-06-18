# Semantic Model Checklist

## Model strategy
- [ ] Star schema proposed
- [ ] Grain defined for each fact table
- [ ] Conformed dimensions identified

## Fact tables
| Fact table | Grain | Key columns | Additive measures | Notes |
|---|---|---|---|---|
| | | | | |

## Dimension tables
| Dimension | Business keys | Surrogate key | SCD type | Notes |
|---|---|---|---|---|
| | | | | |

## Relationships
| From | To | Cardinality | Filter direction | Active? | Justification |
|---|---|---|---|---|---|
| | | | | | |

## Data quality checks
- [ ] Null key handling defined
- [ ] Duplicate key strategy defined
- [ ] Type conversions explicitly defined
- [ ] Unknown member handling documented

## Anti-pattern checks
- [ ] No unnecessary many-to-many
- [ ] No ambiguous relationship paths
- [ ] No high-cardinality text in slicers unless justified
