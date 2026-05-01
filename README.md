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
- uses `TODO.md` and `LOG.md` as the WF session tracking standard for current work, completed sessions, and handoff notes
- prefers subsystem-level architecture docs over overly fragmented micro-docs

## What It Does Not Do

- it is not a permanent always-on mode
- it does not read the full architecture tree by default
- it does not replace code inspection with documentation
- it does not turn `TODO.md` into a long backlog
- it does not treat `TODO.md` or `LOG.md` as an industry standard; they are WF's lightweight repo-local tracking convention
- it does not encourage per-function architecture docs by default

`$wf arche` is the shorthand for architecture planning and architecture updates. It should be planning-first when architecture direction is unclear, and direct-edit when the requested architecture change is already clear. Use `$wf retrofit` to adopt the WF structure in an existing project by creating or normalizing `TODO.md`, `LOG.md`, and `ARCHITECTURE/current/` without treating the repo as a brand-new project.

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

The standard current architecture set is:

- `ARCHITECTURE/README.md`: index, reading order, and folder meanings
- `ARCHITECTURE/current/01-project-intent.md`: goals, users, scope, non-goals, constraints, and phase
- `ARCHITECTURE/current/02-overall-system-design.md`: system boundaries, responsibilities, data flow, dependencies, and terminology
- `ARCHITECTURE/current/03-overall-ui-design.md`: UI surfaces, navigation, key user flows, state relationships, and accessibility; may be marked `N/A`
- `ARCHITECTURE/current/04-repo-map.md`: folder ownership, entrypoints, module responsibilities, and doc-to-code mapping
- `ARCHITECTURE/current/subsystems/*.md`: bounded behavior docs using the subsystem template
- `ARCHITECTURE/decisions/`: optional ADRs for important architecture decisions

For a focused task, the ideal read set is usually:

- `01-project-intent.md` only if product intent matters
- one relevant top-level doc
- one relevant subsystem doc
- `04-repo-map.md` only when code location is needed

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
