## Problem

This document has no frontmatter.

## Hypothesis

If frontmatter is missing, validation should fail.

## Product Summary

This Product Spec describes the product behavior, user-facing shape, and implementation boundaries for the work.

## Scope

```productspec-scope
in:
  - Exercise missing-frontmatter conformance in this fixture.
out:
  - Do not validate successfully when frontmatter is absent.
```

## Acceptance Criteria

```productspec-acceptance-criteria
- id: AC-1
  criterion: When frontmatter is absent, the validator returns `missing_frontmatter`.
```

## Success Metrics

```productspec-success-metrics
- id: SM-1
  metric: invalid_fixture_validation_failure
  target: "100%"
  window: conformance run
```
