# Product Harness example

This folder shows the Product Harness loop:

1. `video-transcript.product-spec.md` is the canonical product intent.
2. `video-transcript.agent-handoff.md` is a generated build contract for an agent.
3. `video-transcript.agent-run.json` records what the agent checked.
4. `video-transcript.decision-trace.json` records what changed or stayed explicit when implementation pressure appeared.

Generate the handoff from the Product Spec:

```bash
npm exec --package @productspec/parser -- productspec handoff examples/product-harness/video-transcript.product-spec.md
```

Or write it to a file:

```bash
npm exec --package @productspec/parser -- productspec handoff examples/product-harness/video-transcript.product-spec.md examples/product-harness/video-transcript.agent-handoff.md
```
