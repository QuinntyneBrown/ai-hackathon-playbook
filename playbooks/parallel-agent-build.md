# Parallel Agent-Assisted Build Within One Capability

A workflow for a team of 3–4 developers, each driving one or more coding agents, building a single hackathon capability in parallel without blocking one another.

## Context

| Attribute | Value |
| --- | --- |
| Team size | 3–4 developers |
| Scope | One capability from a chunked PRD |
| Duration | One hack day |
| Development mode | AI-assisted; each developer drives one or more coding agents |
| Prerequisite | A capability assigned to the team under the [One-day team challenge](one-day-team-challenge.md) workflow (Step 7) |

This playbook zooms into a single capability. The parent workflow assigns each capability to a small team; this workflow governs how the developers inside that team divide the capability further, run their agents in parallel, and integrate the results.

## Terminology

| Term | Usage |
| --- | --- |
| slice | An independently buildable piece of a capability assigned to one developer and that developer's agents |
| interface contract | The agreed boundary between two slices — the types, function signatures, API routes, or events they exchange |
| integration owner | The team member responsible for keeping the capability's branch coherent as slices merge |

## What shall be predetermined

Parallel agent-assisted work fails at the seams, not in the middle of a slice. Agents generate plausible code quickly; when two agents each invent their own version of a shared boundary, the cost surfaces at integration, when the least time remains. The following shall be settled before any developer starts an agent on build work:

- **The slice boundaries.** Decompose the capability into slices that each developer can build without waiting on another. Prefer slices that follow existing seams in the starter template — a module, a page, a service, the design system.
- **The interface contracts.** For every boundary between slices, agree the exchanged types, function signatures, API routes, or events, and commit them as code before the slices diverge. A contract committed once is the single source of truth both agents read; a contract described only in conversation is not.
- **File and directory ownership.** Assign each file or directory to exactly one slice. Two agents editing the same file in parallel is the most common source of merge conflict; disjoint ownership removes it by construction.
- **The shared conventions.** Confirm the `CLAUDE.md` (or equivalent agent-guidance file), the lint rules, the test command, and the formatting rules in the repository before the build starts, so every agent generates code to the same standard without per-developer correction.
- **The stub strategy.** Decide how each slice stands in for its unbuilt neighbours — a mock, a fake, or a hardcoded fixture behind the interface contract — so no slice blocks on another slice being finished.
- **The definition of done per slice.** State the acceptance criteria for each slice so a developer, and that developer's agent, knows when the slice is complete and ready to merge.
- **The branching and integration cadence.** Confirm the branch each developer works on, the target branch they merge into, and how often slices integrate. Frequent small merges keep conflicts small; a single merge at the end concentrates every conflict into the moment with the least time to resolve it.

## Workflow at a glance

| Phase | Steps | Output |
| --- | --- | --- |
| 1. Decompose | 1–3 | Slices, contracts, and ownership recorded |
| 2. Scaffold | 4–5 | Shared contracts and stubs committed |
| 3. Build in parallel | 6–7 | Slices built on separate branches |
| 4. Integrate | 8–9 | Completed capability on the team branch |

## Phase 1 — Decompose

### Step 1. Split the capability into slices

Split the capability into 3–4 slices, one per developer, each independently buildable. Favour slices that follow the seams already present in the starter template so that ownership lines up with the existing structure.

### Step 2. Define the interface contracts

For each boundary between slices, define the interface contract: the exact types, signatures, routes, or events crossing it. Record each contract precisely enough that an agent on either side can build against it without consulting the developer on the other side.

### Step 3. Assign ownership

Assign each slice, and every file or directory within it, to exactly one developer. No file shall be owned by two slices.

## Phase 2 — Scaffold

### Step 4. Commit the contracts first

Commit the interface contracts to the team branch before any slice diverges — as type definitions, interface declarations, empty function signatures, or route stubs. Every agent then reads the same committed boundary rather than inventing its own.

### Step 5. Stub the neighbours

Behind each contract, commit a stub — a mock, a fake, or a fixture — so that each slice runs and tests against its neighbours before those neighbours are built. Stubbing decouples the slices in time: a developer whose slice depends on another can start immediately.

## Phase 3 — Build in parallel

### Step 6. Drive agents against the contracts

Each developer drives one or more agents to build the assigned slice against the committed contracts and stubs. Because ownership is disjoint and the boundaries are fixed, the agents do not compete for the same files and do not need to agree on interfaces mid-build.

### Step 7. Merge slices frequently

Each developer opens small pull requests as slice work reaches a mergeable state, rather than holding one large change to the end. Frequent small merges keep each integration cheap and surface contract mismatches while time remains to correct them.

## Phase 4 — Integrate

### Step 8. Replace stubs with real slices

As slices land, the integration owner replaces the corresponding stubs with the real implementations and confirms the capability holds together across the boundaries. A contract change discovered here shall be made once, in the committed contract, and pulled by every affected slice — not patched independently in each.

### Step 9. Hand the capability up

When the capability meets its definition of done, integrate it into the central repository through the parent workflow's review-and-merge loop (One-day team challenge, Step 11). Work still open at the end of the day moves into the follow-on development cycle recorded in the working agreement.

## How the developers communicate

Communication in a parallel agent-assisted build carries one dominant load: keeping the boundaries stable while the interiors change fast. It runs on three channels.

- **Committed artifacts are the primary channel.** The interface contracts, the stubs, the shared `CLAUDE.md`, and the pull requests are how a developer's intent reaches another developer's agent. An agent reads committed code, not conversation; a decision that lives only in chat does not reach the agents. Any decision that affects a boundary shall be committed, not merely spoken.
- **A contract-change announcement is mandatory and immediate.** A slice interior may change silently; an interface contract may not. When a developer must change a committed contract, that change shall be announced to every developer on the affected boundary before it merges, so their agents rebuild against the new boundary rather than the old one. This is the single message that, if skipped, produces the integration failures this workflow exists to prevent.
- **A short standing sync keeps the picture shared.** The team holds a brief synchronization at a set cadence — on the order of every 60–90 minutes — covering three points only: which slices have merged, which contracts changed, and which slices are now blocked. The sync is for surfacing boundary and blocking issues, not for reviewing slice interiors; interior review happens asynchronously in pull requests.

The integration owner holds the communication overview: watching the merges land, confirming announced contract changes propagate, and raising a sync early when a boundary is in dispute.

## Design notes

- The predetermined boundaries — slices, contracts, ownership — are what make agent speed compound rather than collide. Agents remove the interior as the bottleneck, which moves the bottleneck to the seams; fixing the seams first is what lets three or four agents run at once.
- Disjoint file ownership converts the merge-conflict problem into a decomposition problem solved once at the start, when time is cheap, rather than repeatedly at integration, when it is not.
- Committing contracts and stubs before the parallel build decouples the slices in time, so no developer waits on another's slice to be finished before starting.
- Routing boundary decisions through committed artifacts, and announcing every contract change, keeps every agent building against the same boundary — the failure mode that most often turns fast parallel work into slow serial integration.
