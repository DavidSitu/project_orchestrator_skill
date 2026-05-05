# WF

`WF` is an explicit project-mode skill for Codex. It is designed for repository work that needs structured catch-up, retrofit, planning, architecture maintenance, implementation discipline, and lightweight tracking without making that workflow always-on.

The explicit trigger is `$wf`.

## Why It Exists

This skill keeps normal chat and writing unstructured by default, then adds a predictable project workflow only when you ask for it.

Use it when you want Codex to:

- bootstrap docs and tracking for a new project
- retrofit an existing repo into the standard WF structure
- catch up on an existing repo
- update architecture docs or plan the overall architecture
- plan lightweight V0/V1/optional V2+/final-product milestones during architecture work
- plan subsystem-first code organization, import boundaries, and test ownership
- plan tracked work
- implement scoped changes
- review or debug current behavior

## Install

Copy this folder to:

```text
~/.codex/skills/wf/
```

The internal skill name is lowercase `wf` for validator compatibility. The UI display name can still appear as `WF`.

## Usage

Examples:

```text
use $wf, I'm starting a new project for ...
use $wf retrofit
use $wf arche
use $wf arche and plan the V1 milestones
use $wf arche and split the final goal into V1/V2 milestones
use $wf and review this repo
use $wf and split this into sessions
use $wf and plan feature X
use $wf arche and plan the overall architecture
use $wf and update the architecture for subsystem Y
use $wf and debug the current check-in flow
```

## Common Use Cases

- New project bootstrap
  - `use $wf, I'm starting a new project for ...`
- Existing project retrofit
  - `use $wf retrofit`
  - `use $wf retrofit this repo`
- Existing project catch-up
  - `use $wf and review this repo`
  - `use $wf and catch me up on this project`
- Planning
  - `use $wf and plan feature X`
  - `use $wf and break this into tasks`
- Implementation
  - `use $wf and implement feature X`
  - `use $wf and fix bug Y`
- Architecture updates
  - `use $wf arche`
  - `use $wf arche and plan the overall architecture`
  - `use $wf arche and plan the V1 milestones`
  - `use $wf arche and split the final goal into V1/V2 milestones`
  - `use $wf and update the architecture for subsystem Y`
  - `use $wf and document this repo structure`
- Review and debugging
  - `use $wf and review this change`
  - `use $wf and debug the current check-in flow`

## What It Does

- treats `ARCHITECTURE/current/` as canonical
- avoids `ARCHITECTURE/archive/` by default
- reads only the relevant docs and code for the task
- can restore or normalize `TODO.md`, `LOG.md`, and `ARCHITECTURE/current/` in an existing repo when asked
- uses a standard architecture folder contract for project intent, system design, UI design, repo mapping, subsystem docs, and optional ADRs
- can plan compact V0/V1/V1.x/optional V2+/final-product milestones as architecture direction
- treats subsystems as bounded behavior areas that own code, state, public interfaces, dependencies, and tests
- avoids creating subsystem docs for every function, hook, widget, helper, or UI page by default
- supports subsystem-by-subsystem refactor planning with public APIs, import rules, and local verification
- uses `TODO.md` and `LOG.md` as the WF session tracking standard for current work, completed sessions, and handoff notes
- prefers subsystem-level architecture docs over overly fragmented micro-docs

## What It Does Not Do

- it is not a permanent always-on mode
- it does not read the full architecture tree by default
- it does not replace code inspection with documentation
- it does not turn `TODO.md` into a long backlog
- it does not store full roadmaps in `TODO.md`
- it does not create business, promotion, GTM, `PRODUCT/`, or `05-roadmap.md` docs in the current version
- it does not treat `TODO.md` or `LOG.md` as an industry standard; they are WF's lightweight repo-local tracking convention
- it does not encourage per-function architecture docs by default
- it does not make every UI page, component, hook, helper, or device button its own subsystem unless it owns meaningful workflow, lifecycle, state, data, dependencies, and tests

`$wf arche` is the shorthand for architecture planning, lightweight milestone planning, and architecture updates. It should be planning-first when architecture direction is unclear, and direct-edit when the requested architecture change is already clear. Use `$wf arche` to plan V1, optional V2+, and final-product milestones when product direction affects architecture. Use `$wf retrofit` to adopt the WF structure in an existing project by creating or normalizing `TODO.md`, `LOG.md`, and `ARCHITECTURE/current/` without treating the repo as a brand-new project.

## Milestone Planning

WF keeps stable project target content in `ARCHITECTURE/current/01-project-intent.md` and compact milestone direction in `ARCHITECTURE/current/02-milestones.md`:

- `V0`: smallest useful proving version or internal prototype
- `V1`: first coherent user-facing product version
- `V1.x`: near-term post-V1 improvements that should not block V1
- `V2`, `V3`, `V4+`: larger product generations used only for meaningful capability jumps
- `Final Product Direction`: long-term north star, not a committed backlog

Use the fewest milestone versions needed to make the roadmap clear. Milestones guide architecture and session planning. `TODO.md` should still contain only current and near-next executable sessions.

`02-milestones.md` may stay very short for small projects. Its role is product and architecture phase direction, not backlog, GTM, business planning, or a second TODO file.

A milestone is not complete because the milestone doc exists. It is complete when the TODO sessions derived from it are implemented, verified, and recorded in `LOG.md`.

Use this mapping:

```text
Milestone = product capability direction
TODO session = one testable slice of that capability
Module/file = one coherent ownership boundary
Function = internal behavior inside that module
Test = proof
LOG = completion record
```

Build milestones through detailed TODO sessions, but organize code by ownership boundaries, not by checklist items. Do not create one file per function or one file per TODO checkbox.

## Session Tracking

WF uses a session tracking convention for agent work:

- `TODO.md` is the active session queue, organized by `YYYY-MM-DD` and `S1`, `S2`, `S3` session headings.
- `LOG.md` is the completed-session record, using the same dates and session IDs with concise outcome summaries.
- `TODO.md` should stay short and focused on current or near-next sessions.
- `LOG.md` should record useful completed outcomes, verification, decisions, blockers, and handoff notes.
- ADRs in `ARCHITECTURE/decisions/` record architecture decisions, not session history.

## Recommended Architecture Doc Model

Use a two-layer architecture model:

- top-level docs for cross-cutting truth
- subsystem docs for bounded behavior areas

A subsystem should be large enough to test and reason about independently, but not so large that unrelated behavior is grouped together. For a medium app, start with roughly 4-8 subsystem candidates and expand only when repeated work proves the boundary needs its own doc and ownership contract.

The standard current architecture set is:

- `ARCHITECTURE/README.md`: thin index, reading order, and folder meanings
- `ARCHITECTURE/current/01-project-intent.md`: stable project target, goals, users, scope, non-goals, constraints, phase, and success direction
- `ARCHITECTURE/current/02-milestones.md`: compact V0/V1/V1.x/V2+ and final-product direction when needed
- `ARCHITECTURE/current/03-overall-system-design.md`: system boundaries, responsibilities, data flow, dependencies, and terminology
- `ARCHITECTURE/current/04-overall-ui-design.md`: UI surfaces, navigation, key user flows, state relationships, and accessibility; may be marked `N/A`
- `ARCHITECTURE/current/05-repo-map.md`: folder ownership, entrypoints, module responsibilities, and doc-to-code mapping
- `ARCHITECTURE/current/subsystems/*.md`: bounded behavior docs using the subsystem template
- `ARCHITECTURE/decisions/`: optional ADRs for important architecture decisions

Subsystem docs should capture ownership, public entrypoints, internal files, import rules, data ownership, test strategy, known gaps, and safe extension points.

`ARCHITECTURE/README.md` should remain navigation only. It should not duplicate project goals, milestone details, system design, subsystem behavior, or implementation TODOs.

For a focused task, the ideal read set is usually:

- `01-project-intent.md` only if product intent matters
- `02-milestones.md` only if roadmap, phase, milestone, or session planning depends on it
- one relevant top-level doc
- one relevant subsystem doc
- `05-repo-map.md` only when code location is needed

If one task repeatedly needs many scattered top-level docs, consolidate the detailed behavior into a subsystem doc instead.

## Example Subsystem Taxonomy

These are examples of good subsystem slicing, not required filenames:

- `auth-session-and-timezone`
- `wake-flow-and-checkin`
- `room-risk-and-atonement`
- `companion-lifecycle-and-reveal`
- `offline-queue-and-lifecycle`
- `room-membership-and-joins`

The naming principle is to describe the bounded behavior a contributor actually needs to understand, not to create vague buckets or one doc per tiny unit.
