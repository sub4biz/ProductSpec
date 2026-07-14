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

## Product Summary

A collaborative cursor feature shows each editor where teammates are working inside a shared document.

## Scope

```productspec-scope
in:
  - Include realtime cursor position in this version.
  - Include selected object outline in this version.
  - Show each participant's display name and color.
  - Restore presence after transient network loss.
  - Include per-document presence opt out in this version.
out:
  - Do not build voice chat in this version.
  - Do not build full screen-sharing in this version.
  - Do not build edit conflict resolution in this version.
cut:
  - Cut animated cursor trails from the first version if implementation time is tight.
  - Cut custom participant avatars from the first version if implementation time is tight.
```

## User Experience

https://example.com/prototypes/collaborative-cursors

## Acceptance Criteria

```productspec-acceptance-criteria
- id: AC-1
  criterion: When two collaborators are connected to the same document, each cursor position appears to other active viewers within 250 milliseconds at p95.
- id: AC-2
  criterion: When a collaborator selects a canvas object, other active viewers see a lightweight outline and collaborator label.
- id: AC-3
  criterion: When a collaborator closes the document or loses connection, presence disappears within 10 seconds.
- id: AC-4
  criterion: When a collaborator reconnects after a transient network drop, presence restores without requiring a page reload.
- id: AC-5
  criterion: When a viewer turns off presence for a document, the system stops sending cursor and selection updates for that viewer.
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
