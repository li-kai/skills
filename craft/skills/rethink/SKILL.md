---
name: rethink
description: Rethink a software system from first principles when local cleanup is insufficient. Use for structural changes to representation, ownership, lifecycle, boundaries, performance, or failure semantics.
---

# Rethink

Find a better whole-system design. Preserve behavior and compatibility unless the user approves a tradeoff. Prefer designs that removes, replaces, rather than adds.

## Form the problem model

Establish:

- hard and negotiable requirements, including compatibility
- representative workloads and cold, warm, and worst-case behavior
- state, ownership, lifecycle, concurrency, and failure recovery
- existing measurements and unresolved, decision-changing uncertainty

Separate requirements from implementation. An existing boundary, cache, format, or lifecycle is not automatically a requirement.

## Generate alternatives

Identify the general problem beneath the current implementation and seek structurally analogous problems and their solutions. Use those connections to reconsider the framing and derive alternative designs.

Form three to five internally consistent configurations. Each must be a structural move that could change the selection. Always include a clean-sheet candidate derived solely from the problem model, nudged in slightly different directions.

Launch independent candidate subagents concurrently, one per surviving configuration.

Each candidate brief must state:

- its structural move, ownership, flow, lifecycle, and failure behavior
- workload and compatibility consequences, likely fatal flaw, and cheapest falsifying check

## Decide

Gather evidence that can change the selection. Stop when the evidence separates the candidates or the remaining uncertainty is not worth the next check. Surface claims that remain predictions.

Correctness is a gate. Report the valid design decisions, tradeoffs, and risks.
