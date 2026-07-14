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

Researchers using YouTube videos as source material spend too much time scrubbing through long videos to find exact quotes they can cite.

## Hypothesis

If we provide searchable transcripts with timestamped passages, researchers will treat YouTube videos as usable source material because they can find, verify, and cite the right moment quickly.

## Product Summary

A YouTube transcription search product lets researchers create searchable, timestamped transcripts from video source material.

## Scope

```productspec-scope
in:
  - Let a researcher paste a YouTube URL and create a transcript page.
  - Let a researcher search within the generated transcript.
  - Let a researcher jump to matching timestamps.
  - Let a researcher copy passages with citations.
out:
  - Do not build multi-video projects in this version.
  - Do not build team workspaces in this version.
  - Do not build non-YouTube video imports in this version.
  - Do not build automated citation-format switching in this version.
cut:
  - Cut speaker diarization from the first version.
  - Cut transcript editing from the first version.
```

## User Experience

https://example.com/transcript-search-prototype

## Acceptance Criteria

```productspec-acceptance-criteria
- id: AC-1
  criterion: Given a valid public YouTube URL, the user can create a transcript page.
- id: AC-2
  criterion: When the user searches the transcript, the page returns matching passages with timestamps.
- id: AC-3
  criterion: When the user clicks a search result, the video jumps to the matching timestamp.
- id: AC-4
  criterion: When the user copies a passage, the copied text includes transcript text, video URL, and timestamp.
- id: AC-5
  criterion: When the user submits an empty, private, or unsupported video, the page returns a clear error.
```

## Success Metrics

```productspec-success-metrics
- id: SM-1
  metric: first_transcript_search_rate
  target: ">= 60%"
  window: first session after transcript creation
- id: SM-2
  metric: timestamped_passage_copy_rate
  target: ">= 35%"
  window: within 7 days of transcript creation
- id: SM-3
  metric: median_time_to_first_copied_passage
  target: "< 3 minutes"
  window: first transcript session
```
