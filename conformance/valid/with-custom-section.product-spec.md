---
spec_format_version: "0.1"
title: "Import Error Reports"
artifact_type: "prd"
spec_revision: 1
author: "ProductSpec"
created_at: "2026-07-04T00:00:00Z"
updated_at: "2026-07-04T00:00:00Z"
custom_sections:
  - id: "custom-research-notes"
    label: "Research Notes"
    after: "problem"
---

## Problem

Operations teams cannot fix failed imports because row-level errors are hidden in raw logs.

## Research Notes

Support tickets repeatedly ask which rows failed and why.

## Hypothesis

If failed imports produce row-level error reports, operations teams will retry imports successfully because they can correct the source file.

## Product Summary

This Product Spec describes the product behavior, user-facing shape, and implementation boundaries for the work.

## Scope

```productspec-scope
in:
  - Show a row-level error report for failed imports.
  - Let operations teams download the error report as a CSV.
  - Show retry guidance for failed imports.
out:
  - Do not build automatic source-file correction in this version.
```

## Acceptance Criteria

```productspec-acceptance-criteria
- id: AC-1
  criterion: When an import fails, the report shows row number, field, and actionable error reason for each failed row.
```

## Success Metrics

```productspec-success-metrics
- id: SM-1
  metric: failed_import_support_ticket_reduction
  target: ">= 30%"
  window: within 30 days of launch
```
