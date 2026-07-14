---
spec_format_version: "0.1"
title: "Agent-Coded Saved Search Alerts"
artifact_type: "prd"
spec_revision: 1
author: "ProductSpec"
created_at: "2026-07-08T00:00:00Z"
updated_at: "2026-07-08T00:00:00Z"
linked_github_repo: "acme/transcripts"
applies_to:
  - path: "apps/web/src/search/"
  - component: "saved-search-alerts"
---

## Problem

Researchers who repeatedly search the same transcript library miss newly uploaded videos that match their topic because the product requires them to remember and rerun searches manually.

## Hypothesis

If researchers can save a transcript search and receive a weekly alert when new matching passages appear, they will return to the library more often because the product remembers their research thread for them.

## Product Summary

A saved-search alert feature emails account teams when new matching records appear and gives agents a precise Product Spec to implement against.

## Scope

```productspec-scope
in:
  - Let a user create a saved search from the search results page.
  - Include weekly email alert in this version.
  - Include alert unsubscribe link in this version.
  - Include account-level saved search list in this version.
  - Include agent-generated implementation plan in this version.
out:
  - Do not build real-time alerts in this version.
  - Do not build team-shared saved searches in this version.
  - Do not build Slack notifications in this version.
cut:
  - Cut custom alert schedules from the first version if implementation time is tight.
```

## User Experience

https://example.com/saved-search-alerts-prototype

## Acceptance Criteria

```productspec-acceptance-criteria
- id: AC-1
  criterion: Users can save the current query from the transcript search results page.
- id: AC-2
  criterion: When a user saves a search, account settings show its created date, last run date, and unsubscribe control.
- id: AC-3
  criterion: The weekly alert includes matching video title, passage excerpt, timestamp link, and query text.
- id: AC-4
  criterion: When a user unsubscribes from a saved search, that search stops sending alerts within one hour.
- id: AC-5
  criterion: The implementation pull request links back to this Product Spec revision.
```

```productspec-ai-evals
- id: EVAL-1
  type: llm_judge
  cases:
    - input: "Representative input for this eval."
      expected: "Expected behavior for this eval."
  evaluator: llm
  pass_threshold: 0.86
  checks:
    - returned passage is relevant to the saved query
    - passage excerpt is grounded in transcript content
    - timestamp link points to the cited passage
```

## Success Metrics

```productspec-success-metrics
- id: SM-1
  metric: weekly_alert_clickthrough_rate
  target: ">= 18%"
  window: first 4 weeks after saved search creation
- id: SM-2
  metric: repeated_manual_search_rate
  target: "<= 60% of baseline"
  window: 30 days after launch
```

## Related Artifacts

```productspec-related-artifacts
- type: github_issue
  url: "https://github.com/acme/transcripts/issues/42"
  title: "Create saved search alerts"
  section_id: acceptance_criteria
  item_id: AC-1
- type: github_pr
  url: "https://github.com/acme/transcripts/pull/77"
  title: "Implement saved search alerts"
  section_id: acceptance_criteria
  item_id: AC-5
- type: eval_run
  url: "https://evals.example.com/saved-search-alerts/run-12"
  title: "Saved search relevance eval"
  section_id: acceptance_criteria
  item_id: EVAL-1
```
