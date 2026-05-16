---
name: po
description: Explicit $po Project Orchestrator workflow for Codex. Use only when the user invokes $po or clearly asks for the Project Orchestrator workflow to convert accepted product direction, rough function scope, and UI/design input into ARCHITECTURE/current/, milestones, subsystem docs, TODO.md/LOG.md sessions, retrofit/catch-up/review coordination, and code-manager handoff.
---

# Project Orchestrator

Use this skill only when the user explicitly invokes `$po` or clearly asks for the project workflow. Keep normal chat, writing, and reasoning unstructured when this skill is not requested.

## Operating Principles

- Treat the Project Orchestrator workflow as per-turn project mode, not a permanent conversation mode.
- Classify the request first, then run only the relevant path.
- Default to read-only catch-up, planning, or explanation unless the user explicitly asks to create, update, implement, refactor, normalize, retrofit, or otherwise change files.
- Assume Project Orchestrator usually starts after the user has accepted the business direction, rough function scope, and UI/design direction. Convert that accepted input into repo-operational structure.
- Clarify missing product, function, UI, or technical intent only when needed to write useful architecture docs, milestones, subsystem boundaries, or session plans.
- Do not invent business strategy, go-to-market, PMF analysis, pricing, promotion plans, or raw product positioning unless the user explicitly asks for that outside normal Project Orchestrator.
- Use `ARCHITECTURE/current/` as the canonical documentation set.
- Do not read `ARCHITECTURE/archive/` unless the user explicitly asks for historical context, migration history, or past reasoning.
- Read only the relevant docs and code for the task. Do not load the whole architecture tree by default.
- Documentation guides understanding. Runtime code is still the final source of truth for actual behavior.
- Treat `TODO.md` as the active session queue, not a backlog.
- Treat `LOG.md` as the completed-session record, not a transcript or changelog.
- Treat session boundaries as the only time to roll tracking forward: when a session is complete or reaches a meaningful stopping point, write the matching `LOG.md` entry and close out or carry forward the matching `TODO.md` session.
- Keep tracking lightweight. Do not rewrite `TODO.md` after each small edit or partial check-in.
- Treat milestones as product and architecture direction, not execution sessions or a `TODO.md` backlog.
- Build milestones through detailed TODO sessions. A milestone is complete only when the implementation sessions derived from it are finished, verified, and recorded.
- Treat `$po arche` as shorthand for converting accepted product/UI/function direction into architecture docs, lightweight milestone direction, and subsystem boundaries.
- Treat `$po retrofit` as shorthand for restoring or normalizing the standard Project Orchestrator structure in an existing repository.
- Use the standard architecture folder contract in `references/architecture-structure.md` when bootstrapping, retrofitting, or updating architecture docs.
- Use `references/doc-update-rules.md` to decide which architecture doc changes.
- Use `references/session-tracking.md` when creating, normalizing, or updating `TODO.md` and `LOG.md`.
- Treat subsystems as bounded behavior areas. Use `references/subsystem-planning-rules.md` for detailed granularity, ownership, import, and test rules.
- Session size does not determine file size. Coordinate session work around the correct subsystem or module; do not create one file per function or one file per checklist item.
- Use `references/code-manager-integration.md` when code organization, implementation, refactor, test placement, diagnosis, or focused verification is involved.

## Responsibility Model

Project Orchestrator has three connected layers:

1. Project Memory: owns `ARCHITECTURE/current/`, `TODO.md`, `LOG.md`, ADR triggers, and doc drift handling.
2. Project Planning: owns milestone-to-session translation, active or near-next TODO sessions, and verification targets.
3. Project Coordination: owns catch-up, bootstrap/retrofit coordination, implementation handoff, review/debug routing, and `code-manager` handoff.

Keep these layers connected, but do not let one path do all three unless the user request requires it.

## Request Classification

Run only the path that matches the user's request:

Project Memory:

1. `bootstrap-new-project`
2. `retrofit-existing-project`
3. `architecture-update`

Project Planning:

4. `planning`

Project Coordination:

5. `catch-up-existing-project`
6. `implementation-coordination`
7. `review-debugging`

Treat `$po retrofit` as shorthand for `retrofit-existing-project`.
Treat `$po arche` as shorthand for `architecture-update`.

Do not edit files just because the skill was activated. Activation loads the operating procedure; the user request chooses the path.

## Routing Table

| User intent | Layer | Path | Primary references |
| --- | --- | --- | --- |
| Start the workflow in a new repo | Memory | `bootstrap-new-project` | `architecture-structure.md`, `session-tracking.md` |
| Adopt or restore workflow in an existing repo | Memory + Coordination | `retrofit-existing-project` | `retrofit-rules.md`, `architecture-structure.md`, `session-tracking.md` |
| Understand current repo state | Coordination | `catch-up-existing-project` | Relevant current docs, code, tests |
| Update architecture, milestones, repo map, or subsystem docs | Memory | `architecture-update` | `architecture-structure.md`, `doc-update-rules.md`, plus milestone or subsystem refs when relevant |
| Break work into sessions | Planning | `planning` | `planning-rules.md`, `session-tracking.md` |
| Coordinate a concrete build/change | Coordination + Planning | `implementation-coordination` | `code-manager-integration.md`, relevant docs/code/tests |
| Review, diagnose, or debug | Coordination | `review-debugging` | Relevant current docs, code, tests; `planning-rules.md` for review shape |

## Path Boundary Rules

- `architecture-update` may update docs, but should not create TODO sessions unless architecture work turns into tracked implementation.
- `planning` may update `TODO.md`, but should not update architecture docs unless product or system truth changes.
- `implementation-coordination` may refine the current session and verification target, but should not expand backlog scope.
- `catch-up-existing-project` should report state, gaps, and next steps without creating files unless asked.
- `review-debugging` should return findings first and update docs or tracking only when asked or current truth clearly changed.
- `retrofit-existing-project` may touch all Project Memory files, but should preserve useful existing content and avoid speculative architecture detail.

## Default Read Order

For real project work, read in this order when relevant:

1. `TODO.md`
2. The latest relevant entries in `LOG.md`
3. `ARCHITECTURE/README.md`
4. `ARCHITECTURE/current/01-project-intent.md`
5. `ARCHITECTURE/current/02-milestones.md` only when roadmap, phase, milestone, or session planning depends on it
6. Only the additional top-level or subsystem docs relevant to the task
7. The actual code paths touched by the task

Skip files that do not exist or are not needed for the current path.

Use progressive read discipline: focused tasks stay narrow, but broad architecture requests must read broadly enough to preserve project-level judgment.

For a Global Arche Read, read enough current architecture context to reason about the whole project:

- `ARCHITECTURE/current/01-project-intent.md`
- `ARCHITECTURE/current/02-milestones.md`
- `ARCHITECTURE/current/03-overall-system-design.md`
- `ARCHITECTURE/current/04-overall-ui-design.md` when the project has UI or UX implications
- `ARCHITECTURE/current/05-repo-map.md` when code organization or implementation planning matters
- relevant subsystem docs when broad boundaries, lifecycle, state, or data ownership matter

Use this broad read for global view, overall architecture, whole project, MVP plan, final product direction, repo structure, or broad subsystem-boundary requests. Do not use it for a small bug, one page tweak, or one subsystem implementation session.

For a focused task, the ideal read set is usually:

- `ARCHITECTURE/current/01-project-intent.md` only if product intent matters
- `ARCHITECTURE/current/02-milestones.md` only if roadmap, phase, milestone, or session planning depends on it
- one relevant top-level current doc
- one relevant subsystem doc
- `ARCHITECTURE/current/05-repo-map.md` only when code location is needed

If one task requires many scattered top-level docs, consolidate subsystem detail instead of multiplying cross-cutting files.

## Path Contracts

### bootstrap-new-project

Use when the user is starting a new project or explicitly asks to set up the workflow.

- Create `ARCHITECTURE/`, `TODO.md`, and `LOG.md` if they do not already exist.
- Create the standard architecture skeleton from `references/architecture-structure.md`.
- Create initial subsystem docs only for clearly known functional areas.
- Seed `TODO.md` and `LOG.md` from `references/session-tracking.md`.
- Add a short `LOG.md` entry only after meaningful setup work is complete.

### retrofit-existing-project

Use when the user wants to adopt the Project Orchestrator workflow in the middle of an existing repo, especially when `TODO.md`, `LOG.md`, or `ARCHITECTURE/` are missing, incomplete, or nonstandard.

- Inspect the existing repo shape, docs, and workflow files first.
- Preserve useful existing content by default instead of replacing it.
- Create missing standard Project Orchestrator files and folders only where needed.
- Normalize tracking and architecture structure conservatively against the relevant references when existing files are nonstandard.
- Add a short `LOG.md` entry only after the retrofit work is meaningfully complete.
- See `references/retrofit-rules.md` for detailed retrofit and migration guidance.

### catch-up-existing-project

Use when the user asks to review the current state, catch up on a repo, or understand what exists now.

- Read the relevant tracking files and current docs.
- Inspect the actual code paths tied to the request.
- Summarize current state, gaps, risks, and likely next steps.
- Do not create missing workflow files unless the request implies they should exist.

### architecture-update

Use when the user wants to convert accepted product direction, rough function scope, UI/design input, or current repo truth into architecture docs, milestone direction, or subsystem boundaries.

- Read only the affected current docs.
- Use Global Arche Read when the request is broad: global view, overall architecture, whole project direction, MVP plan, final product direction, repo structure, or broad subsystem boundaries.
- Read `references/architecture-structure.md` for the standard folder contract.
- Read `references/doc-update-rules.md` when deciding which architecture doc to update.
- Read `references/subsystem-planning-rules.md` when the request involves subsystem granularity, ownership, import direction, test strategy, or repo layout.
- Read `references/milestone-planning.md` when accepted direction includes MVP / V1, Post-MVP / V1.x, optional Future / V2+, roadmap, milestone, phase, or final-product direction.
- Inspect code if needed to confirm runtime truth.
- Use a planning-first workflow when architecture intent is unclear or the request involves major tradeoffs.
- Clarify only missing project goal, target users, scope, constraints, system type, current milestone, desired documentation depth, or ADR needs that cannot be learned from the provided plan, current docs, or code.
- Update only the relevant architecture files.
- Do not touch `archive/` unless the request is explicitly historical.

### planning

Use when the user asks for task planning, breakdown, or sequencing.

- Read the relevant docs and code.
- Break work into small verifiable session-sized slices.
- Read `references/subsystem-planning-rules.md` when planning code organization, subsystem splits/merges, isolated testing, or cross-subsystem work.
- Read `references/session-tracking.md` before creating or rewriting session entries in `TODO.md`.
- Refine `TODO.md` using dated session sections instead of a long undifferentiated task list.
- If planning from milestones, derive only current and near-next executable sessions from the active milestone.
- Update architecture docs only if product or system truth changes.
- See `references/planning-rules.md` for task slicing and review guidance.

### implementation-coordination

Use when the user asks `$po` to build or change a concrete behavior. Project Orchestrator coordinates the tracked session; detailed code execution discipline belongs to code-manager guidance.

- Read the relevant docs and code first.
- Identify the affected subsystem, session scope, relevant public/internal entrypoints, and verification target before coding work starts when the change is more than a trivial local fix.
- Refine task tracking only if the task is real project work.
- If the task is too large for one focused session, split it into the next session entries in `TODO.md`.
- Coordinate only what the current session needs; avoid expanding the work into a backlog or unrelated refactor.
- Read `references/code-manager-integration.md` when the task needs file organization, import cleanup, public API design, test placement, TDD, diagnosis, refactoring, or focused code verification.
- Define the smallest useful verification, preferring subsystem-local tests before broader integration tests.
- Read `references/session-tracking.md` before moving session outcomes from `TODO.md` to `LOG.md`.
- Update `LOG.md` using the same date and session ID when a session is completed or reaches a meaningful stopping point.

### review-debugging

Use when the user asks for review, diagnosis, or debugging.

- Read the relevant current docs first, then inspect code and tests.
- Compare intended behavior vs actual behavior.
- Return findings first for review tasks.
- Update docs or tracking only if the user asks or the current truth clearly changed.

## Output Contracts

Project Memory outputs:

- files created or normalized
- source of truth changed
- decisions made
- unresolved questions or ADR needs

Project Planning outputs:

- active milestone when relevant
- affected subsystem or behavior area
- session-sized TODO entries
- verification target per session

Project Coordination outputs:

- current state, findings, or handoff scope
- affected subsystem
- code-manager handoff points
- `LOG.md` update only after completion or meaningful stop
- concrete evidence from docs, code, tests, or runtime behavior
- verification gaps

## Reference Files

- Read `references/planning-rules.md` when planning or reviewing task slices.
- Read `references/session-tracking.md` when creating, normalizing, or updating `TODO.md` and `LOG.md`.
- Read `references/milestone-planning.md` when translating accepted MVP / V1, Post-MVP / V1.x, optional Future / V2+, final-product direction, or roadmap-like architecture direction.
- Read `references/retrofit-rules.md` when handling `$po retrofit` or normalizing an existing repo into the Project Orchestrator structure.
- Read `references/architecture-structure.md` when creating, normalizing, or updating `ARCHITECTURE/`.
- Read `references/doc-update-rules.md` when deciding which architecture doc to update.
- Read `references/subsystem-doc-template.md` when creating a new subsystem doc.
- Read `references/subsystem-planning-rules.md` when defining subsystem granularity, code ownership, import rules, test strategy, or refactor sequencing.
- Read `references/code-manager-integration.md` when implementation coordination needs physical file organization, file moves, import cleanup, public API design, test placement, TDD, diagnosis loops, focused verification, or structured refactor execution.
