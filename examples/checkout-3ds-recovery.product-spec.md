---
spec_format_version: "0.1"
title: "Checkout 3DS Recovery"
artifact_type: "prd"
spec_revision: 1
author: "ProductSpec"
created_at: "2026-07-13T00:00:00Z"
updated_at: "2026-07-13T00:00:00Z"
linked_github_repo: "acme/checkout"
applies_to:
  - path: "apps/web/src/checkout/"
  - path: "services/payments/3ds/"
---

## Problem

Merchants using hosted checkout lose otherwise valid orders when 3DS authentication fails silently, returns users to an empty cart, or gives support teams no payment-attempt evidence to diagnose.

## Hypothesis

If 3DS failures return buyers to a recoverable checkout state with clear next steps and durable attempt evidence, more buyers will complete payment because authentication errors no longer feel like a dead end.

## Scope

```productspec-scope
in:
  - recoverable 3DS failure state
  - retry payment with the same cart
  - alternate card entry after failed challenge
  - payment-attempt audit record
  - support-visible failure reason
out:
  - new payment processor
  - merchant-defined recovery copy
  - wallet-specific recovery flows
cut:
  - SMS recovery link
  - automatic support ticket creation
```

## User Experience

https://example.com/prototypes/checkout-3ds-recovery

## Acceptance Criteria

```productspec-acceptance-criteria
- id: AC-1
  criterion: When a 3DS challenge fails, the buyer returns to checkout with cart contents, shipping details, and selected payment method preserved.
- id: AC-2
  criterion: The failure state explains that bank authentication failed and offers retry card, use another card, and cancel checkout actions.
- id: AC-3
  criterion: Each failed 3DS attempt records payment intent ID, merchant ID, failure code, browser family, processor response, and timestamp.
- id: AC-4
  criterion: Support users can find the failed attempt from order lookup without exposing full card data.
- id: AC-5
  criterion: Retrying a failed 3DS payment does not duplicate the order or charge the buyer twice.
```

## Success Metrics

```productspec-success-metrics
- id: SM-1
  metric: recovered_3ds_checkout_completion_rate
  target: ">= 18%"
  window: 30 days after launch
- id: SM-2
  metric: duplicate_charge_incidents_from_3ds_retry
  target: "0"
  window: weekly
- id: SM-3
  metric: merchant_support_contacts_with_missing_3ds_context
  target: "<= 5%"
  window: weekly
```

## Related Artifacts

```productspec-related-artifacts
- type: github_issue
  url: "https://github.com/acme/checkout/issues/183"
  title: "Recover buyers after failed 3DS challenge"
  section_id: acceptance_criteria
  item_id: AC-1
- type: dashboard
  url: "https://analytics.example.com/dashboards/3ds-recovery"
  title: "3DS recovery metrics"
  section_id: success_metrics
  item_id: SM-1
```
