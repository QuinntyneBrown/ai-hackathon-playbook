# CLAUDE.md

Guidance for Claude Code when working in this repository.

## Purpose

This repository collects field-tested learnings on running large hackathons with AI-assisted development. Each learning is captured as a playbook: a repeatable workflow that a facilitator can apply at a future event and share with other organizers.

## Repository structure

| Path | Content |
| --- | --- |
| `README.md` | Repository overview and playbook index |
| `playbooks/` | Playbooks, one workflow per file |
| `CLAUDE.md` | This file — conventions for working in the repository |

## Voice and style

All prose follows the register defined in the [Architecture Description Style Guide](https://github.com/QuinntyneBrown/architecture-description-style-guide). The rules that apply to this repository:

- Write in a single impersonal, precise, declarative register addressed to one audience: event facilitators.
- Do not write in the first person ("we built") and do not address the reader directly ("as you can see").
- Do not use hype or intensifiers ("robust", "world-class", "really", "very").
- Carry normative force only with "shall", "should", and "may". Use the imperative mood for procedural steps.
- Use parallel structure and consistent punctuation in lists.
- Do not fabricate values. Flag missing facts with `<TO SUPPLY>`.
- Use terminology consistently: introduce a term once, then reuse it unchanged across all documents.

## Conventions for playbooks

- Place each playbook in `playbooks/` with a kebab-case filename.
- Open each playbook with a context section stating team size, duration, and setting.
- Group steps into named phases and number steps sequentially across the whole workflow.
- Record rationale only where it reflects an observed learning, not speculation.
- Add each new playbook to the index table in `README.md`.

## Terminology

| Term | Usage |
| --- | --- |
| playbook | A repeatable, field-tested workflow captured in this repository |
| partner organization | The external organization that supplies the challenge and domain context |
| capability | A slice of the product assigned to one team: a module, a page, the design system, or spec management |
| FaithTech 4D cycle | Discover, Discern, Develop, Demonstrate — the framework whose Discover output feeds ideation |
| FaithTech co-creation cycle | Request, Receive, Review, Render, Rejoice — the five R's iteration loop each team runs during the build phase |
| PRD | Product requirements document |
| working agreement | The agreement, understood by all parties before the build starts, that records the role mapping (partner organization as customer, facilitator as product owner, participants as development team), the facilitator's decision authority, the expected scope, and the disposition of work after the event |
| follow-on development cycle | The development cycle that receives work leaving the hack day and iterates with the partner organization after the event |
