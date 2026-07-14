---
spec_format_version: "0.1"
title: "Transcript Search"
artifact_type: "prd"
spec_revision: 1
author: "ProductSpec"
created_at: "2026-07-06T00:00:00Z"
updated_at: "2026-07-06T00:00:00Z"
---

## Problem

Researchers lose time finding exact quotes in long video transcripts.

## Hypothesis

If transcript search returns timestamped passages, researchers will cite video sources more often.

## Product Summary

This Product Spec describes the product behavior, user-facing shape, and implementation boundaries for the work.

## Scope

```productspec-scope
in:
  - Include transcript search in this version.
  - Include timestamped quote copy in this version.
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
  window: within 7 days of transcript creation
```
