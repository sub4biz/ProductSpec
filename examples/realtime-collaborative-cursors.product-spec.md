---
spec_format_version: "0.1"
title: "Realtime Collaborative Cursors"
artifact_type: "prd"
spec_revision: 1
author: "ProductSpec"
created_at: "2026-07-13T00:00:00Z"
updated_at: "2026-07-13T00:00:00Z"
linked_github_repo: "acme/canvas"
applies_to:
  - path: "apps/canvas/src/collaboration/"
  - path: "services/realtime-presence/"
---

## Problem

Design reviewers working in the same canvas talk past each other because they cannot see where teammates are looking, selecting, or pointing during live review.

## Hypothesis

If collaborators can see lightweight realtime cursors and selections during a shared canvas session, review comments will resolve faster because people can point at the same object without narrating location.

## Scope

```productspec-scope
in:
  - realtime cursor position
  - selected object outline
  - participant display name and color
  - reconnect after transient network loss
  - per-document presence opt out
out:
  - voice chat
  - full screen-sharing
  - edit conflict resolution
cut:
  - animated cursor trails
  - custom participant avatars
```

## User Experience

https://example.com/prototypes/collaborative-cursors

## Acceptance Criteria

```productspec-acceptance-criteria
- id: AC-1
  criterion: A collaborator's cursor position appears to other active document viewers within 250 milliseconds at p95 while both clients are connected.
- id: AC-2
  criterion: Selecting a canvas object shows a lightweight outline and collaborator label to other active viewers.
- id: AC-3
  criterion: Presence disappears within 10 seconds after a collaborator closes the document or loses connection.
- id: AC-4
  criterion: Reconnecting after a transient network drop restores presence without requiring a page reload.
- id: AC-5
  criterion: Turning off presence for a document stops sending cursor and selection updates for that viewer.
```

## Success Metrics

```productspec-success-metrics
- id: SM-1
  metric: live_review_comment_resolution_time
  target: "<= 70% of baseline"
  window: first 30 days after launch
- id: SM-2
  metric: collaborative_session_presence_opt_out_rate
  target: "<= 8%"
  window: weekly
- id: SM-3
  metric: realtime_presence_p95_latency
  target: "<= 250ms"
  window: daily
```

## Related Artifacts

```productspec-related-artifacts
- type: figma
  url: "https://figma.example.com/file/collaborative-cursors"
  title: "Collaborative cursor interaction model"
  section_id: user_experience
- type: github_issue
  url: "https://github.com/acme/canvas/issues/88"
  title: "Add realtime presence protocol"
  section_id: acceptance_criteria
  item_id: AC-1
- type: dashboard
  url: "https://analytics.example.com/dashboards/realtime-presence"
  title: "Realtime presence latency and usage"
  section_id: success_metrics
  item_id: SM-3
```
