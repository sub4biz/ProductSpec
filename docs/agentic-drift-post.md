# Draft post: Agentic drift

AI agents introduce a new product failure mode: agentic drift.

The agent starts with a spec. It makes a plan. It edits code. Then something changes.

Maybe the Product Spec changes mid-session.

Maybe an engineer makes a workaround that changes behavior.

Maybe an acceptance criterion quietly stops matching what shipped.

This is where agent-written software gets messy. The failure is often not that the agent ignored the spec. The failure is that nobody can tell which version of intent the agent was following, what it checked, and what evidence supported the completion claim.

That is what we are building into ProductSpec.

ProductSpec now has:

- `spec_revision`: the exact version of intent an agent started from
- MCP session tools: `begin_spec_session` and `check_spec_session`
- Acceptance Criteria and AI Evals with durable IDs
- Related Artifacts for PRs, eval runs, dashboards, and analytics snapshots
- Agent Run receipts that record what the agent checked
- Decision Trace for the human judgment calls after reality disagrees with the spec

The model can write code.

The spec needs to tell the model what done means.

The run receipt needs to show what was actually checked.

The trace needs to record why intent changed.

This matters because more software work is becoming long-running agent work. The agent may run for minutes, hours, or eventually days. During that time, the product decision can move.

If the change is a typo, the agent should not restart the world.

If the change alters scope, acceptance criteria, evals, or success metrics, the agent should re-read the Product Spec and re-plan.

ProductSpec keeps that boundary explicit. Humans still make the judgment call on materiality. The standard gives them a place to record it.

This is the direction I am most excited about: specs that agents can execute, humans can review, and teams can audit later.

If you are building with Claude Code, Codex, Cursor, or another coding agent, try wiring ProductSpec into your repo this week.

The first step is simple:

```bash
npx --yes -p @productspec/parser@latest productspec mcp-config claude
```

ProductSpec is open source. Contributions welcome.
