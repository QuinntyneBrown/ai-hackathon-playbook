# One-Day Team Challenge with a Partner Organization

A workflow for delivering a working product in one hack day with a team of 8–10 participants building with AI-assisted development tools, on a challenge supplied by a partner organization.

## Context

| Attribute | Value |
| --- | --- |
| Team size | 8–10 participants |
| Duration | One hack day |
| Challenge source | Partner organization |
| Development mode | AI-assisted; each team builds with AI coding tools |
| Ideation input | Discover output from the [FaithTech 4D cycle](https://workbook.faithtech.com/) (Discover, Discern, Develop, Demonstrate) |

## Workflow at a glance

| Phase | Steps | Output |
| --- | --- | --- |
| 1. Foundation | 1 | Selected starter template |
| 2. Discovery and ideation | 2–3 | Consolidated idea set |
| 3. Definition | 4–5 | Low-fidelity PRD chunked into core capabilities |
| 4. Repository and team setup | 6–10 | Central repository with protected main and per-team feature branches |
| 5. Build and integration | 11–12 | Working product on main |

## Phase 1 — Foundation

### Step 1. Select a starter template

Select a starter template that matches the expected product shape — for example, a Clean Architecture solution or a Next.js starter. A template removes project setup from the critical path and gives AI coding tools an established structure to extend rather than a blank repository to invent.

## Phase 2 — Discovery and ideation

### Step 2. Brainstorm in pairs

Brainstorm all product details in pairs, grounded in the Discover output of the FaithTech 4D cycle — gathered directly with the partner organization when present, or taken from the notes the partner left.

Keep the medium low fidelity:

- Use a notepad.
- Jot ideas down as they surface.
- Defer structure and polish.

Low-fidelity capture keeps the pace high within the timebox and prevents premature convergence on a single pair's framing.

### Step 3. Consolidate as a group

Share each pair's notes with the full group and consolidate them into a single idea set.

## Phase 3 — Definition

### Step 4. Derive a low-fidelity PRD

Derive a very low-fidelity product requirements document (PRD) from the consolidated idea set. The PRD records what the product does; it defers visual and technical detail.

### Step 5. Chunk the PRD into core capabilities

Chunk the PRD into core capabilities that teams can build in parallel:

- Modules — slices of domain functionality
- Pages — distinct screens, such as login
- UI — the design system shared across pages
- Spec management — ownership of the PRD chunks and their evolution during the day

Each capability shall be independently buildable so that teams do not block one another.

## Phase 4 — Repository and team setup

### Step 6. Set up a central repository

Create a central git repository from the starter template and push it to the shared host.

### Step 7. Assign capabilities

Assign each core capability to a small team or an individual.

### Step 8. Create feature branches

Each team creates its own feature branch for its capability.

### Step 9. Add collaborators

Add participants as collaborators so that each participant can push to their team's feature branch.

### Step 10. Protect main

Protect the main branch so that changes land only through reviewed pull requests.

## Phase 5 — Build and integration

### Step 11. Review and merge pull requests

Teams build their capabilities with AI assistance and open pull requests against main. Reviewers review each pull request and merge it to main.

### Step 12. Iterate until complete

Repeat the build–review–merge loop until the product is complete or the day ends.

## Design notes

- Chunking the PRD by capability lets 8–10 participants work in parallel; AI assistance makes each small team productive enough to own a full capability within the day.
- A protected main branch with pull request review keeps integration quality constant while many branches land in quick succession.
- Low-fidelity artifacts — notepad brainstorms and a minimal PRD — match the one-day timebox; detail beyond what teams need to start building is deferred.
