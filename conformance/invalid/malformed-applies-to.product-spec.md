---
spec_format_version: "0.1"
title: "Malformed Applies To"
artifact_type: "prd"
spec_revision: 1
author: "ProductSpec"
created_at: "2026-07-09T00:00:00Z"
updated_at: "2026-07-09T00:00:00Z"
applies_to:
  - path: "apps/web/src/transcripts/"
    component: "transcript-search"
---

## Problem

Researchers lose time finding exact video quotes.

## Hypothesis

If transcript search returns timestamped passages, researchers will cite videos faster.

## Product Summary

This Product Spec describes the product behavior, user-facing shape, and implementation boundaries for the work.

## Scope

```productspec-scope
in:
  - Include transcript search in this version.
out:
  - Do not build team libraries in this version.
cut:
  - Cut speaker labels from the first version if implementation time is tight.
```

## Acceptance Criteria

```productspec-acceptance-criteria
- id: AC-1
  criterion: When a user searches one transcript by phrase, the page returns matching timestamped passages.
```

## Success Metrics

```productspec-success-metrics
- id: SM-1
  metric: copied_timestamped_quote_rate
  target: ">= 35%"
  window: within 7 days
```
