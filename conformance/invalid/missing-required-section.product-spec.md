---
spec_format_version: "0.1"
title: "Missing Metrics"
artifact_type: "prd"
author: "ProductSpec"
created_at: "2026-07-04T00:00:00Z"
updated_at: "2026-07-04T00:00:00Z"
---

## Problem

This document intentionally omits Success Metrics.

## Hypothesis

If required sections are missing, validation should fail.

## Product Summary

This Product Spec describes the product behavior, user-facing shape, and implementation boundaries for the work.

## Scope

```productspec-scope
in:
  - Exercise missing-section conformance in this fixture.
out:
  - Do not include every required ProductSpec section.
```

## Acceptance Criteria

```productspec-acceptance-criteria
- id: AC-1
  criterion: When a required section is absent, the validator returns `missing_required_section`.
```
