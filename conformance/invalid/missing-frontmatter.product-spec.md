## Problem

This document has no frontmatter.

## Hypothesis

If frontmatter is missing, validation should fail.

## Product Summary

This Product Spec describes the product behavior, user-facing shape, and implementation boundaries for the work.

## Scope

In: missing-frontmatter conformance.

## Acceptance Criteria

```productspec-acceptance-criteria
- id: AC-1
  criterion: Validator returns missing_frontmatter.
```

## Success Metrics

```productspec-success-metrics
- id: SM-1
  metric: invalid_fixture_validation_failure
  target: "100%"
  window: conformance run
```
