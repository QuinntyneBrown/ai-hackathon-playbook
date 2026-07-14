# Cross-Capability Contract Drafting Prompt

A reusable prompt that turns clear per-capability specifications into the cross-capability contracts two independent developers — each driving many agents — build against, so their capabilities merge into a shared branch and rebase onto it along a predictable path.

## Context

| Attribute | Value |
| --- | --- |
| Actor | Facilitator, or the spec-management capability owner acting for the facilitator |
| Position in the parent workflow | Between [One-day team challenge](one-day-team-challenge.md) Step 5 (PRD chunked into capabilities with clear specs) and Step 8 (contract skeleton committed to main) |
| Input | A clear specification for each capability |
| Output | Cross-capability contracts drafted as committable code, an ownership map, and a change-and-rebase protocol |
| Development mode | AI-assisted; two or more developers each drive multiple coding agents on separate capabilities |

This prompt automates the drafting in [One-day team challenge](one-day-team-challenge.md) Step 6. The facilitator supplies the per-capability specs; the AI proposes the contracts, the file-ownership map, and the integration protocol; the facilitator reviews and commits the result as the contract skeleton (Step 8). The team-internal decomposition that follows is governed by the [Parallel agent-assisted build](parallel-agent-build.md) workflow.

## When to use this prompt

Use this prompt when all of the following hold:

- A specification exists for each capability, precise enough to name the data each capability owns and the surfaces it exposes to or consumes from other capabilities.
- Two or more capabilities will be built in parallel by developers who do not coordinate continuously.
- The capabilities will integrate on a shared branch through repeated merges, and an in-progress capability will need to rebase onto that branch after other capabilities have merged.

Do not use this prompt to define contracts internal to a single capability; those are the slice-level interface contracts the owning team defines under the [Parallel agent-assisted build](parallel-agent-build.md) workflow.

## Inputs the prompt requires

The facilitator fills the four fields marked with double braces before issuing the prompt:

| Field | Content |
| --- | --- |
| `{{PER_CAPABILITY_SPECS}}` | The clear specification for each capability |
| `{{CAPABILITY_LIST}}` | Each capability and its assigned owner |
| `{{STARTER_TEMPLATE}}` | The starter template and its repository layout |
| `{{REPO_CONVENTIONS}}` | The agent-guidance file, lint rules, format rules, and test command |
| `{{TARGET_BRANCH}}` | The branch capabilities merge into and rebase onto (typically `main`) |

## The prompt

```text
You are drafting the cross-capability contracts for a product built in parallel by
independent capability teams, each driving several coding agents. A clear specification
exists for every capability. Derive, from those specifications, the set of contracts that
fixes every boundary between capabilities, so that two developers who never speak can each
build a capability, merge it into a shared branch alongside other capabilities, and rebase
an in-progress capability onto that branch after others have merged — without their agents
inventing conflicting versions of any shared surface.

Inputs:
- Per-capability specifications: {{PER_CAPABILITY_SPECS}}
- Capabilities and their owners: {{CAPABILITY_LIST}}
- Starter template and repository layout: {{STARTER_TEMPLATE}}
- Repository conventions (agent-guidance file, lint, format, test command): {{REPO_CONVENTIONS}}
- Target integration branch: {{TARGET_BRANCH}}

Produce the following, in order.

1. Boundary inventory. From the specifications, list every boundary where one capability
   consumes another. For each boundary, name the providing capability, the consuming
   capability or capabilities, and the kind of surface exchanged — shared data, module API,
   transport, design system, navigation, identity, spec, or convention.

2. Contract per boundary. For each boundary, draft the contract as code, not prose: the
   exact entity shapes, type and function signatures, routes and request/response schemas,
   events, component props, or design tokens crossing it. State the single owning capability
   that may change the contract and the consuming capabilities. Mark each contract's
   stability — the surfaces expected to change least (typically the shared data model and the
   design system) shall be identified so they stabilize first.

3. Committable contract skeleton. Emit the contracts as files that can be committed to
   {{TARGET_BRANCH}} before any capability diverges — type and entity definitions, interface
   declarations, route and schema stubs, design tokens, and component signatures. Behind each
   contract, emit a stub (a mock, a fake, or a fixture) so a consuming capability builds and
   tests before the providing capability is finished. Place every file at a concrete path in
   the repository layout.

4. Ownership map. Assign every file and directory to exactly one owner: either a single
   capability, or the contract skeleton owned by spec management. No file may be owned by two
   capabilities. This map is what makes parallel merges and rebases conflict-free by
   construction: capabilities edit disjoint files, and the only shared files are the
   contracts, which change rarely and through one owner.

5. Change-and-rebase protocol. Define, as numbered steps:
   a. How a contract change is made — once, in the committed contract, by its owner — and
      announced to every consuming capability before it merges.
   b. How a completed capability merges into {{TARGET_BRANCH}} alongside others.
   c. How an in-progress capability rebases onto {{TARGET_BRANCH}} after other capabilities
      have merged. Make explicit which files a rebase can touch — the contract skeleton only —
      so a clean rebase is the default and any conflict signals an unannounced contract change
      to resolve against the committed contract rather than patch locally.

Constraints:
- Define only cross-capability surfaces. Contracts internal to a single capability are out of
  scope and are defined by the team that owns the capability.
- Every contract shall be precise enough that an agent on either side builds against it
  without consulting the other team.
- Prefer boundaries that follow seams already present in {{STARTER_TEMPLATE}}.
- Do not invent capabilities, entities, or routes absent from the specifications. Where a
  specification is silent on a surface two capabilities must exchange, flag it as an open
  contract to resolve rather than filling it in.

Output format:
- The boundary inventory as a table.
- Each contract as a fenced code block preceded by its path, owner, consumers, and stability.
- The ownership map as a table of path to owner.
- The change-and-rebase protocol as numbered steps.
```

## What the prompt returns

The prompt yields five artifacts the facilitator reviews before committing:

- A **boundary inventory** naming every place one capability consumes another.
- A **contract per boundary**, drafted as code, with a named owner, its consumers, and a stability marking.
- A **committable contract skeleton** — the contract code and its stubs, placed at concrete repository paths, ready to commit to the target branch under Step 8.
- An **ownership map** assigning every file to exactly one owner, with no file co-owned.
- A **change-and-rebase protocol** stating how contracts change and how capabilities merge and rebase.

The facilitator reviews the draft against the specifications, resolves any surface the AI flagged as an open contract, and commits the skeleton to the target branch before the capabilities diverge.

## How the output supports parallel development, merge, and rebase

- **Parallel development** holds because the ownership map gives each developer a disjoint set of files. Two developers, each driving many agents, build against the same committed contracts and never edit the same file, so their agents do not compete for a shared surface.
- **Merge into a shared branch** stays cheap because capabilities touch disjoint files; two capabilities merging in sequence conflict only where they touch a shared file, and the only shared files are the contracts.
- **Rebase onto the branch** follows a predictable path because a rebase can touch only the contract skeleton. A capability that pulls the branch after others have merged replays its own commits over unchanged files, unless a contract changed. A conflict is therefore a precise signal — a contract changed — resolved once against the committed contract rather than patched independently in each capability.

## Design notes

- The prompt draws its contract kinds from [One-day team challenge](one-day-team-challenge.md) Step 6 so that its output slots directly into the Step 8 contract skeleton without re-derivation.
- Requiring the AI to emit contracts as code at concrete paths, rather than as prose, is what makes the output committable and therefore readable by every agent; a contract described only in prose does not reach the agents that build against it.
- The ownership map converts the merge-conflict problem into a decomposition decision made once, at drafting time, when time is cheap — the same principle the [Parallel agent-assisted build](parallel-agent-build.md) workflow applies at the slice level.
- Instructing the AI to flag silent surfaces as open contracts, rather than invent them, keeps fabricated boundaries out of the committed skeleton and puts each unresolved surface in front of the facilitator to decide.
