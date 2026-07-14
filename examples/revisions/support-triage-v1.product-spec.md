---
spec_format_version: "0.1"
title: "AI Support Triage"
artifact_type: "prd"
spec_revision: 1
author: "ProductSpec"
created_at: "2026-07-06T00:00:00Z"
updated_at: "2026-07-06T00:00:00Z"
linked_github_repo: "productspec/example-support-triage"
---

## Problem

Support leads at B2B SaaS companies lose their morning planning window because urgent tickets are buried among routine product questions.

## Hypothesis

If incoming tickets are automatically labeled by urgency and likely owner, support leads will respond to urgent customer issues faster because the queue starts each day pre-sorted by consequence.

## Product Summary

A first support triage version labels ticket urgency, recommends owners, and exposes confidence before routing changes are automated.

## Scope

```productspec-scope
in:
  - Ingest tickets from the helpdesk API.
  - Include urgency labels in this version.
  - Include owner recommendation in this version.
  - Include confidence score in this version.
  - Include reviewer override in this version.
out:
  - Do not build auto-replies in this version.
  - Do not build direct ticket reassignment in this version.
  - Do not build customer-visible status changes in this version.
  - Do not build custom routing rules in this version.
cut:
  - Cut customer-tier lookup from the first version if implementation time is tight.
  - Cut audit-log export from the first version if implementation time is tight.
```

## Acceptance Criteria

```productspec-acceptance-criteria
- id: AC-1
  criterion: When a new ticket arrives, it receives urgency, suggested owner, confidence score, and model version within 60 seconds.
- id: AC-2
  criterion: Reviewers can override any urgency label before it changes downstream workflow state.
- id: AC-3
  criterion: When a label has confidence below 0.70, it is marked `needs_review` and does not trigger escalation.
```

```productspec-ai-evals
- id: EVAL-1
  type: llm_judge
  cases:
    - input: "Representative input for this eval."
      expected: "Expected behavior for this eval."
  evaluator: llm
  pass_threshold: 0.88
  checks:
    - urgency classification identifies urgent tickets
    - non-urgent tickets are not escalated
```

## Success Metrics

```productspec-success-metrics
- id: SM-1
  metric: median_time_to_first_human_response
  target: "< 30 minutes"
  window: business hours
- id: SM-2
  metric: suggested_owner_review_rate
  target: ">= 60%"
  window: weekly
- id: SM-3
  metric: false_urgent_escalation_rate
  target: "< 8%"
  window: weekly
```
