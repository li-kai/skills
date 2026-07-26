---
name: simplify
description: Clean up changed code without changing behavior. Use after making code changes to improve reuse, simplicity, efficiency, and maintainability.
argument-hint: "[target]"
---

Improve the quality of the changed code, not correctness. Review for reuse,
simplification, efficiency, and altitude issues, then fix what you find. Do not
hunt for bugs; use code review for that.

## Phase 1: Review

Launch 5 independent review agents concurrently. Pass each agent the diff and
one of these angles:

- **Reuse:** duplicated logic, missed shared abstractions, or code that should use existing helpers or reliable dependencies.
- **Simplification:** unnecessary branches, indirection, state, configuration, or special cases.
- **Efficiency:** wasted work, avoidable allocations, repeated IO, redundant queries, or expensive loops.
- **Altitude:** code at the wrong layer, leaky responsibilities, misplaced policy, hard-to-maintain structure, or abstraction.
- **Prose:** unnecessary, misleading, or confusing comments, docstrings, or naming.

Each agent should return findings with:

- `file`
- `line`
- one-line `summary`
- `reason`: why this matters concretely

## Phase 2: Apply Fixes

Wait for all agents to complete. Deduplicate findings that point at the same
line or mechanism, then fix each remaining issue directly.

Skip any finding whose fix would change intended behavior, require changes well
outside the reviewed diff, or appears to be a false positive. Note skipped
findings briefly instead of debating them.

Finish with a concise summary of what was fixed and what was skipped, or confirm
the changed code was already clean.
