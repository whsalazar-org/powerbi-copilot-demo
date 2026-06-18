# Power BI Bug Triage Playbook

## 1) Reproduce
- Capture filters, page, user role, timestamp, and expected vs actual output.

## 2) Classify
- Data issue
- DAX logic issue
- Relationship/model issue
- Visual interaction issue
- Security/RLS issue
- Performance issue

## 3) Diagnose
- Reconcile against source
- Inspect relationship/filter paths
- Test impacted measures in isolation
- Validate role context for RLS bugs

## 4) Fix
- Apply smallest safe change
- Add/adjust tests in validation checklist
- Document root cause and mitigation

## 5) Verify
- Confirm bug resolved
- Confirm no regression in related pages/measures
