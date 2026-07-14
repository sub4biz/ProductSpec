---
spec_format_version: "0.1"
title: "Human Handoff for an AI Front Desk"
artifact_type: "prd"
spec_revision: 2
author: "ProductSpec"
created_at: "2026-07-01T00:00:00Z"
updated_at: "2026-07-10T00:00:00Z"
linked_github_repo: "acme/front-desk"
applies_to:
  - path: "apps/inbox/src/handoff/"
  - component: "conversation-handoff"
tool_metadata:
  source_doc: "internal-prd-handoff-v3"
  converted_by: "spec-conversion-pipeline"
---

## Problem

A business owner running an AI agent on their customer conversations has no reliable way to get a human into a conversation the AI cannot finish. When a customer asks for a person, or an action needs approval, the conversation stalls or the owner has to watch every thread all day, which defeats the reason they bought an AI.

## Hypothesis

If the AI can hand a conversation to a named human with SLA tracking and full context, owners will let the AI run autonomously, because exceptions reliably reach a person. The owner's daily check becomes "47 handled by AI, 3 need attention" instead of reading every thread.

## Product Summary

A customer handoff workflow keeps CRM ownership and handoff context synchronized when accounts move between teams.

## Scope

```productspec-scope
in:
  - Let the AI request a human handoff through a `request_human_handoff` tool.
  - Create handoff records with SLA columns.
  - Let each handoff be assigned to a team or person and appear in the inbox.
out:
  - Do not build signal-triggered handoff until the risk-signals work exists.
  - Do not build CRM owner sync in this version.
cut:
  - Cut a separate copilot product with its own billing in favor of one agent with a mode setting.
```

## Acceptance Criteria

```productspec-acceptance-criteria
- id: AC-1
  criterion: When the AI calls `request_human_handoff`, the system creates a pending handoff record and shows the conversation in the inbox.
- id: AC-2
  criterion: When an operator assigns a handoff, the system sets the assignee and starts the SLA clock.
- id: AC-3
  criterion: When a conversation is routed, the router uses the conversation assignee and never the CRM contact owner.
```

```productspec-ai-evals
- id: EVAL-1
  type: llm_judge
  cases:
    - input: "Customer writes: this is useless, let me talk to a real person."
      expected: "Agent calls request_human_handoff instead of continuing to answer."
  evaluator: llm
  pass_threshold: 0.9
```

## Success Metrics

```productspec-success-metrics
- id: SM-1
  metric: median_time_to_first_human_response
  target: tbd
  target_status: provisional
  target_owner: Ops lead
  window: 30 days after launch
- id: SM-2
  metric: ai_containment_rate
  target: tbd
  target_status: provisional
  target_owner: Ops lead
  window: 30 days after launch
```

## Related Artifacts

```productspec-related-artifacts
- type: github_issue
  url: "https://github.com/acme/front-desk/issues/210"
  title: "Build the handoff record and SLA columns"
  section_id: acceptance_criteria
  item_id: AC-1
- type: dashboard
  url: "https://analytics.example.com/handoff-response-times"
  section_id: success_metrics
  item_id: SM-1
```

## Open Questions

- The SM-1 and SM-2 targets are provisional because no baseline exists before launch. The Ops lead sets both from the first 30 days of real traffic.
