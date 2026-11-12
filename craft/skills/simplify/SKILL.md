---
name: simplify
description: Clean up changed code without changing behavior. Use after making code changes to improve reuse, simplicity, efficiency, and maintainability.
argument-hint: "[target]"
---

Improve the quality of the changed code. This is not an exhaustive correctness audit. But examine invariants and failure paths where they explain structural complexity, and flag suspected correctness issues separately.

## Phase 1: Review

Use the diff as the entry point, not the review boundary. Preserve required behavior, but let reviewers challenge the implementation's representations and boundaries.

Give reviewers requirements and compatibility constraints separately from the implementation rationale.

Launch 5 independent review agents concurrently. Pass each agent the diff and
one of these angles:

- Reuse: duplicated logic, missed shared abstractions, or code that should use existing helpers or reliable dependencies.
- Simplification: unnecessary branches, indirection, state, configuration, or special cases
- Efficiency: wasted work, avoidable allocations, repeated IO, redundant queries, or expensive loops.
- Altitude: code at the wrong layer, leaky responsibilities, misplaced policy, hard-to-maintain structure, or abstraction. Does each layer express intent at a coherent level? Look for missing concepts, unnecessary concepts, implementation details leaking upward, and unhelpful abstractions.
- Prose: unnecessary, misleading, or confusing comments, docstrings, or naming.

Each agent should return findings with:

- `file`
- `line`
- one-line `summary`
- `reason`: why this matters concretely

## Phase 2: Synthesize

Wait for all agents to complete. The main agent must assess whether findings
share a structural cause. Five independent local reviews do not substitute
for this synthesis. Deduplicate findings that point at the same mechanism.

Report significant findings outside the editable scope rather than silently
excluding them. Discovery does not authorize a broader rewrite.

## Phase 3: Apply Fixes

Fix each remaining issue within the authorized scope. Defer findings whose fixes would change intended behavior or require a broader rewrite. Skip false positives, and briefly explain deferred or skipped findings.

Summarize fixes and deferred structural findings. If there are no findings, say the scoped review found none.
