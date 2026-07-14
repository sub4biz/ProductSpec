---
spec_format_version: "0.1"
title: "Calendar SMS Reminder Bet"
artifact_type: "hypothesis"
spec_revision: 1
author: "ProductSpec"
created_at: "2026-07-04T00:00:00Z"
updated_at: "2026-07-04T00:00:00Z"
---

## Problem

Sales managers miss customer calls when browser notifications are hidden during back-to-back meetings.

## Hypothesis

If calendar reminders can escalate to SMS for high-priority meetings, sales managers will miss fewer customer calls because the reminder reaches them on the device they are actually checking.

## Product Summary

A calendar reminder product sends high-priority SMS reminders for meetings a user is likely to miss.

## Scope

```productspec-scope
in:
  - Include Google Calendar connection in this version.
  - Include high-priority meeting rules in this version.
  - Include SMS reminder opt-in in this version.
  - Include delivery logs in this version.
out:
  - Do not build calendar creation in this version.
  - Do not build full scheduling assistant in this version.
  - Do not build team admin controls in this version.
cut:
  - Cut WhatsApp reminders from the first version if implementation time is tight.
  - Cut custom reminder templates from the first version if implementation time is tight.
```

## User Experience

https://example.com/calendar-reminder-prototype

## Acceptance Criteria

```productspec-acceptance-criteria
- id: AC-1
  criterion: When a user connects Google Calendar, the app stores the connection and shows it as active.
- id: AC-2
  criterion: When a user marks a meeting as high priority, the meeting is eligible for SMS reminders.
- id: AC-3
  criterion: When a high-priority meeting starts in 5 minutes, the app sends an SMS reminder to opted-in users.
- id: AC-4
  criterion: Users can disable SMS reminders at any time.
```

## Success Metrics

```productspec-success-metrics
- id: SM-1
  metric: activated_user_high_priority_reminder_setup_rate
  target: ">= 50%"
  window: within 7 days of activation
- id: SM-2
  metric: missed_call_self_report_reduction
  target: ">= 25%"
  window: monthly
```
