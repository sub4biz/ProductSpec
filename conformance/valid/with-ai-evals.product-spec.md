---
spec_format_version: "0.1"
title: "AI Quote Search"
artifact_type: "prd"
spec_revision: 1
author: "ProductSpec"
created_at: "2026-07-06T00:00:00Z"
updated_at: "2026-07-06T00:00:00Z"
---

## Problem

Researchers lose time finding exact quotes in long video transcripts.

## Hypothesis

If quote search returns cited transcript passages, researchers will trust the transcript as a source.

## Product Summary

This Product Spec describes the product behavior, user-facing shape, and implementation boundaries for the work.

## Scope

```productspec-scope
in:
  - Let a researcher search a transcript by phrase.
  - Let a researcher copy timestamped quote citations.
out:
  - Do not build multi-transcript projects in this version.
```

## Acceptance Criteria

```productspec-acceptance-criteria
- id: AC-1
  criterion: When a user searches a transcript by phrase, the page returns matching timestamped passages.
- id: AC-2
  criterion: When a user copies a timestamped quote, the copied text includes the quote, source URL, and timestamp.
```

```productspec-ai-evals
- id: EVAL-1
  type: llm_judge
  cases:
    - input: "Representative input for this eval."
      expected: "Expected behavior for this eval."
  evaluator: llm
  pass_threshold: 0.85
```

## Success Metrics

```productspec-success-metrics
- id: SM-1
  metric: weekly_active_researchers_copying_timestamped_quote
  target: ">= 40%"
  window: weekly
```
