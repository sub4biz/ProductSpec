# Handoff Example

This example shows how ProductSpec fits into a normal software workflow. It does not replace Jira, Linear, Figma, Git, OpenSpec, Spec Kit, or coding agents. It gives them a shared intent layer.

## Scenario

A team wants to build searchable transcripts for YouTube videos.

The Product Spec answers:

- What problem are we solving?
- What behavior do we expect to change?
- What is in and out of scope?
- What must be true before the work is accepted?
- What outcome tells us the work mattered?

## Flow

```text
Product Spec
  -> Figma / prototype links
  -> Jira / Linear tickets
  -> OpenSpec or Spec Kit engineering spec
  -> Git branches and pull requests
  -> AI coding agent implementation loop
  -> shipped code and outcome measurement
```

## ProductSpec

ProductSpec is the durable statement of intent.

Example:

- `problem`: Researchers waste time hunting through long videos for exact quotes.
- `hypothesis`: If transcripts are searchable and copyable, researchers will move from source discovery to usable citation faster.
- `scope`: Search, timestamped results, transcript snippets, copy passage.
- `acceptance_criteria`: Given a YouTube URL with captions, the user can search transcript text and copy a passage with timestamp attribution.
- `success_metrics`: Median time to find and copy a usable quote falls below 3 minutes for first-time transcript sessions.

ProductSpec should remain stable enough that a teammate can ask, later, whether the implementation still matches the original intent.

## Figma

Figma stores the design artifact.

ProductSpec can reference it in `user_experience`:

```md
## User Experience

https://figma.com/proto/example-searchable-transcripts
```

The Product Spec does not replace Figma. It tells readers why that design exists and what it must accomplish.

## Jira Or Linear

Jira and Linear store work tracking.

The Product Spec can become epics, tickets, or tasks:

- Epic: Searchable transcript experience
- Ticket: Accept YouTube URL and fetch transcript
- Ticket: Build transcript search results
- Ticket: Add copy passage with timestamp
- Ticket: Add empty, loading, and failure states

Those tickets should link back to the Product Spec. Tickets can change as engineering learns. The Product Spec preserves the intent those tickets serve.

## OpenSpec Or Spec Kit

OpenSpec and Spec Kit operate at the engineering spec layer.

They can consume the Product Spec and produce:

- technical design
- implementation plan
- task breakdown
- migration plan
- test plan

ProductSpec answers what and why. OpenSpec and Spec Kit answer how.

## Git

Git stores implementation history.

The Product Spec can live in the repo, for example:

```text
specs/searchable-transcripts.product-spec.md
```

Pull requests can link back to it:

```md
Implements acceptance criteria from specs/searchable-transcripts.product-spec.md.
```

Commit history shows what changed. ProductSpec explains why the work exists and what success means.

## AI Coding Agents

AI coding agents can use the Product Spec as the upstream control document.

A goal loop might be:

1. Read the Product Spec.
2. Generate or update an engineering spec.
3. Create implementation tasks.
4. Build until acceptance criteria pass.
5. Report which acceptance criteria are satisfied.
6. Leave success metrics for product measurement after launch.

Acceptance criteria are the build contract. Success metrics are the market contract.

## Result

Each tool keeps its job:

- ProductSpec: durable software intent
- Figma: design artifact
- Jira / Linear: work tracking
- OpenSpec / Spec Kit: engineering plan
- Git: implementation history
- AI coding agents: execution

The benefit is not another place to write the same thing. The benefit is one portable source of intent that survives handoff.
