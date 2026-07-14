---
spec_format_version: "0.1"
title: "YouTube Transcription Search"
artifact_type: "prd"
spec_revision: 1
author: "ProductSpec"
created_at: "2026-07-04T00:00:00Z"
updated_at: "2026-07-04T00:00:00Z"
---

## Problem

Researchers using YouTube videos as source material spend too much time finding exact quotes they can cite.

## Hypothesis

If searchable transcripts expose timestamped passages, researchers will cite video sources more often because evidence becomes easier to find and verify.

## Product Summary

A YouTube transcription search product lets researchers create searchable, timestamped transcripts from video source material.

## Scope

```productspec-scope
in:
  - Let a researcher paste a YouTube URL and create a transcript page.
  - Let a researcher search the transcript and jump to matching timestamps.
  - Let a researcher copy timestamped citations from transcript results.
out:
  - Do not build multi-video projects in this version.
cut:
  - Cut speaker diarization from the first version.
```

## Acceptance Criteria

```productspec-acceptance-criteria
- id: AC-1
  criterion: Given a valid public YouTube URL, the user can create a transcript page.
- id: AC-2
  criterion: When the user searches the transcript, the page returns matching passages with timestamps.
- id: AC-3
  criterion: When the user submits a private or unsupported video, the page returns a clear error.
```

## Success Metrics

```productspec-success-metrics
- id: SM-1
  metric: first_transcript_search_rate
  target: ">= 60%"
  window: first transcript session
```
