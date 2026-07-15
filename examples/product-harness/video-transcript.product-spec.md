---
spec_format_version: "0.1"
title: "Video Transcript Search"
artifact_type: "prd"
spec_revision: 1
author: "ProductSpec"
created_at: "2026-07-15T00:00:00Z"
updated_at: "2026-07-15T00:00:00Z"
linked_github_repo: "example/video-transcript"
applies_to:
  - path: "apps/web/src/transcripts/"
  - path: "apps/worker/src/transcription/"
---

## Problem

Researchers lose time scrubbing through long videos because the quotes they need are buried inside spoken content that cannot be searched like text.

## Hypothesis

If researchers can submit a video URL, receive a transcript, and search that transcript by keyword, they will find usable quotes faster because the video becomes a text-searchable source.

## Product Summary

A video transcript search product lets a researcher submit one video URL, generate a transcript, and search within that transcript for matching passages with timestamps.

## Scope

```productspec-scope
in:
  - Accept one public video URL and create a transcript job.
  - Show transcript generation status until the transcript is ready.
  - Let the researcher search the generated transcript by keyword.
  - Return matching transcript passages with timestamps and source links.
out:
  - Do not build team transcript libraries in this version.
  - Do not build semantic search or summarization in this version.
  - Do not build private video authentication in this version.
cut:
  - Cut transcript export from the first version if transcript search is not complete.
```

## Acceptance Criteria

```productspec-acceptance-criteria
- id: AC-1
  criterion: When a researcher submits a supported public video URL, the system creates one transcript job and shows a pending status.
- id: AC-2
  criterion: When transcript generation completes, the transcript page shows searchable transcript text.
- id: AC-3
  criterion: When the researcher searches for a keyword that appears in the transcript, the page returns matching passages with timestamps.
- id: AC-4
  criterion: When the researcher searches for a keyword that does not appear in the transcript, the page shows an empty state instead of an error.
```

```productspec-ai-evals
- id: EVAL-1
  type: contains
  cases:
    - input: "Search transcript for renewal pricing"
      expected: "Results include transcript passages containing renewal pricing and timestamps."
    - input: "Search transcript for a phrase that is absent"
      expected: "Results show no matches without a system error."
  evaluator: deterministic
  pass_threshold: 1
```

## Success Metrics

```productspec-success-metrics
- id: SM-1
  metric: transcript_search_success_rate
  target: ">= 70% of first transcript searches return at least one clicked result"
  target_status: provisional
  target_owner: "Transcript product lead"
  window: 14 days after first transcript creation
- id: SM-2
  metric: transcript_job_failure_rate
  target: "<= 5% of supported public video URLs fail transcript generation"
  target_status: committed
  window: weekly
```

## Related Artifacts

```productspec-related-artifacts
- type: github_issue
  url: "https://github.com/example/video-transcript/issues/12"
  title: "Build video transcript search"
  section_id: acceptance_criteria
  item_id: AC-1
- type: github_pr
  url: "https://github.com/example/video-transcript/pull/34"
  title: "Implement transcript jobs and search"
  section_id: acceptance_criteria
  item_id: AC-3
- type: eval_run
  url: "./video-transcript.eval-run.json"
  title: "Transcript search deterministic eval"
  section_id: acceptance_criteria
  item_id: EVAL-1
- type: dashboard
  url: "https://analytics.example.com/transcripts/search-success"
  title: "Transcript search success dashboard"
  section_id: success_metrics
  item_id: SM-1
```
