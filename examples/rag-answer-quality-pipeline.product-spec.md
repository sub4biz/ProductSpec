---
spec_format_version: "0.1"
title: "RAG Answer Quality Pipeline"
artifact_type: "prd"
spec_revision: 1
author: "ProductSpec"
created_at: "2026-07-13T00:00:00Z"
updated_at: "2026-07-13T00:00:00Z"
linked_github_repo: "acme/knowledge"
applies_to:
  - path: "services/answering/"
  - path: "evals/rag/"
---

## Problem

Customer-success teams cannot trust the internal answer bot because it sometimes gives plausible answers without citing the source paragraph that supports the answer.

## Hypothesis

If answers are blocked unless they cite retrieved source passages that actually support the claim, customer-success teams will use the bot for account questions because every answer is auditable.

## Product Summary

A RAG answer quality pipeline generates source-grounded internal answers and evaluates whether responses stay faithful to retrieved material.

## Scope

```productspec-scope
in:
  - Include source-grounded answer generation in this version.
  - Require a citation for every factual claim in generated answers.
  - Refuse to answer when retrieved context is insufficient.
  - Run nightly evals on the golden support-question set.
  - Link the eval result from release notes.
out:
  - Do not build retraining the embedding model in this version.
  - Do not build external customer-facing answers in this version.
  - Do not build Slack bot redesign in this version.
cut:
  - Cut automatic knowledge-base article creation from the first version if implementation time is tight.
  - Cut multi-hop account analytics questions from the first version if implementation time is tight.
```

## Acceptance Criteria

```productspec-acceptance-criteria
- id: AC-1
  criterion: When the bot answers a question about account policy, pricing, or feature behavior, every factual claim includes at least one source citation.
- id: AC-2
  criterion: The bot refuses to answer when retrieved passages do not contain enough evidence.
- id: AC-3
  criterion: When the nightly eval run completes, the system writes a durable eval-run artifact and links it from the release checklist.
- id: AC-4
  criterion: A release is blocked when launch-blocking eval cases fall below the pass threshold.
```

```productspec-ai-evals
- id: EVAL-1
  type: llm_judge
  cases:
    - input: "Can enterprise accounts export audit logs for the last 365 days?"
      expected: "Answer only if the retrieved policy text supports the retention window, and cite that policy."
    - input: "Does the basic plan include SSO?"
      expected: "Say no and cite the plan-comparison source."
  evaluator: llm
  pass_threshold: 0.9
  checks:
    - answer claims are supported by cited passages
    - unsupported claims are refused instead of guessed
- id: EVAL-2
  type: regex
  cases:
    - input: "What is the SLA for priority support?"
      expected: "Each factual SLA statement includes a source citation."
    - input: "Can admins remove a user immediately?"
      expected: "Answer cites the user-management source paragraph."
  evaluator: deterministic
  pass_threshold: 1
  checks:
    - every answer contains source identifiers
    - citation identifiers exist in retrieved context
```

## Success Metrics

```productspec-success-metrics
- id: SM-1
  metric: support_answer_bot_trusted_use_rate
  target: ">= 45%"
  window: weekly among customer-success teammates
- id: SM-2
  metric: unsupported_answer_escape_rate
  target: "<= 2%"
  window: weekly reviewed sample
- id: SM-3
  metric: median_time_to_answer_account_policy_question
  target: "<= 90 seconds"
  window: weekly
```

## Related Artifacts

```productspec-related-artifacts
- type: eval_run
  url: "./evidence/rag-answer-quality-nightly.json"
  title: "Nightly RAG answer quality eval"
  section_id: acceptance_criteria
  item_id: EVAL-1
- type: github_pr
  url: "https://github.com/acme/knowledge/pull/241"
  title: "Enforce grounded answer citations"
  section_id: acceptance_criteria
  item_id: AC-1
- type: dashboard
  url: "https://analytics.example.com/dashboards/support-answer-bot"
  title: "Support answer bot adoption and escape rate"
  section_id: success_metrics
  item_id: SM-2
```
