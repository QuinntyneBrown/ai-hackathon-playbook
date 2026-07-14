# Three-by-Three Model for a One-Day Hackathon

A nine-goal workflow that divides one hack day into three three-hour blocks, each with three concrete targets, adapted from the Thoughtworks 3×3×3 structure for AI-assisted hackathon delivery.

## Context

| Attribute | Value |
| --- | --- |
| Team size | 4–12 participants |
| Duration | One hack day (nine hours) |
| Block structure | Three blocks of three hours; three goals per block |
| Development mode | AI-assisted; participants drive coding agents |
| Prerequisite | A challenge supplied by a partner organization and a selected starter template |

## Design intent

The three-by-three model imposes a forcing function at each three-hour boundary: a team that cannot report the block's three goals as met has a visible signal that pace or scope must adjust before the next block starts. The nine goals are calibrated so that meeting all three goals in Block 1 makes Block 2 achievable, and meeting all three goals in Block 2 makes Block 3 achievable. Missing a goal in an earlier block cascades into the subsequent block; the facilitator's primary role during the day is to detect that drift early and adjust.

## Workflow at a glance

| Block | Hours | Three goals | Exit condition |
| --- | --- | --- | --- |
| 1. Foundation | 1–3 | Problem defined · Architecture decided · Agents running | Every team has an agent producing output against a committed scaffold |
| 2. Build | 4–6 | All capabilities under active build · Happy path integrated · All capabilities merged | A working product exists on main and runs end-to-end |
| 3. Demonstrate | 7–9 | Product stable · Product polished · Demonstration ready | The partner organization can walk through a live demonstration |

## Block 1 — Foundation (Hours 1–3)

### Goal 1. Problem defined

Derive a low-fidelity PRD from the partner organization's challenge. The PRD records what the product does; it defers visual and technical detail. Chunk the PRD into capabilities that teams can build in parallel and define the cross-capability contracts — shared types, module interfaces, transport routes, design tokens, and the navigation map — at a level of precision that an agent can build against without further clarification.

The facilitator shall confirm the scope is achievable in the remaining six hours before moving to Goal 2. Reduce scope here; expanding it later is not possible.

### Goal 2. Architecture decided

Select the starter template, initialize the central repository, and commit the cross-capability contract skeleton — shared type and entity definitions, interface declarations, route and schema stubs, design tokens, component signatures, and the repository-wide agent-guidance file. Protect the main branch, configure the CI pipeline, create per-team feature branches, and add participants as collaborators.

Every agent on every team shall read the same committed boundaries before any build work starts. A boundary that exists only in conversation does not reach the agents.

### Goal 3. Agents running

Each team decomposes its capability into slices, assigns ownership so that no file is owned by two developers, commits interface contracts and stubs for each slice, and starts at least one agent building against the committed scaffold. At the end of Hour 3, every team has an agent producing output.

Block 1 is complete when all three goals are met. If Hour 3 ends with a team still setting up, the facilitator adjusts scope or reallocates participants before Block 2 starts.

## Block 2 — Build (Hours 4–6)

### Goal 4. All capabilities under active build

Every team has its agents running against committed contracts and is producing mergeable pull requests. No team is waiting on a boundary that has not yet been committed. The facilitator confirms this at the start of Hour 4 and resolves any blocked team immediately.

### Goal 5. Happy path integrated

The capability teams that own the critical path — the core user flow from entry to the product's primary output — have merged their work to main, and that flow runs end-to-end. Secondary capabilities may still be in progress. CI is green on main.

Integrating the happy path at Hour 5 rather than Hour 9 surfaces contract mismatches while time remains to correct them.

### Goal 6. All capabilities merged

All capability teams have merged to main. The product runs end-to-end including secondary flows. CI is green. Work that cannot merge by the end of Hour 6 moves into the follow-on development cycle recorded in the working agreement; it shall not delay Block 3.

Block 2 is complete when the product runs end-to-end on main and CI is green.

## Block 3 — Demonstrate (Hours 7–9)

### Goal 7. Product stable

No regressions have been introduced since the end of Block 2. CI is green. The facilitator calls a feature freeze: no new capability work merges after this point unless it fixes a defect on the critical demo path.

### Goal 8. Product polished

Teams address edge cases, error states, and visual finish within the scope of the committed capabilities. Polish targets the demonstration path — the sequence of screens and interactions the partner organization will walk through — rather than the full product surface. Work outside the demonstration path is deferred to the follow-on development cycle.

### Goal 9. Demonstration ready

The product is deployed to the demonstration environment. The facilitator and at least one participant rehearse the demonstration end-to-end, confirm it succeeds, and brief the partner organization on what was built and what remains in the follow-on development cycle. The working agreement governs the disposition of all artifacts.

Block 3 is complete when the rehearsed demonstration succeeds and the partner organization has been briefed.

## Pacing guidance

| Hour | Facilitator focus |
| --- | --- |
| 1 | Drive PRD consolidation; prevent over-specification |
| 2 | Confirm contracts are committed; unblock teams that are still in setup |
| 3 | Verify every team has an agent running; adjust scope if needed |
| 4 | Confirm no team is blocked; surface and resolve boundary disputes |
| 5 | Check that the happy-path integration is on track; escalate if not |
| 6 | Call feature freeze on out-of-scope work; confirm all capabilities are merging |
| 7 | Enforce feature freeze; confirm CI is green |
| 8 | Direct polish effort to the demonstration path only |
| 9 | Confirm deployment; run rehearsal; brief the partner organization |

## Design notes

- Three three-hour blocks with explicit exit conditions make drift visible at each boundary rather than only at the end of the day; the facilitator can adjust scope or pace at Hour 3 and Hour 6, when adjustment is still possible.
- Integrating the happy path at Goal 5 rather than Goal 6 reserves one hour of the build block as a buffer for contract mismatches and merge conflicts; in practice that buffer is almost always used.
- Feature freeze at Goal 7 protects the demonstration from destabilization in the final block; the quality of a demonstration depends more on stability than on completeness.
- The nine goals are sequenced so that each goal's output is the direct input to the next goal; a team that skips a goal does not save time — it transfers the cost of that goal to the next goal, when less time remains.
