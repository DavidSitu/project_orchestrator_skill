---
name: wf
description: Explicit project-mode workflow for Codex. Use when bootstrapping a new project, retrofitting an existing repo into the workflow, catching up on an existing repo, updating architecture docs or milestones, planning tracked work, implementing scoped tasks, or reviewing/debugging within a repo while maintaining session-based TODO.md, LOG.md, and ARCHITECTURE/current/.
---

# WF

Use this skill only when the user explicitly invokes `$wf` or clearly asks for the project workflow. Keep normal chat, writing, and reasoning unstructured when this skill is not requested.

## Core Defaults

- Treat the `WF` workflow as per-turn project mode, not a permanent conversation mode.
- Default to read-only catch-up, planning, or explanation unless the user explicitly asks to create, update, implement, refactor, normalize, retrofit, or otherwise change files.
- Use `ARCHITECTURE/current/` as the canonical documentation set.
- Do not read `ARCHITECTURE/archive/` unless the user explicitly asks for historical context, migration history, or past reasoning.
- Read only the relevant docs and code for the task. Do not load the whole architecture tree by default.
- Documentation guides understanding. Runtime code is still the final source of truth for actual behavior.
- Treat `TODO.md` as the active session queue, not a backlog.
- Treat `LOG.md` as the completed-session record, not a transcript or changelog.
- Use the WF session tracking standard in `references/session-tracking.md` when creating, normalizing, or updating `TODO.md` and `LOG.md`.
- Treat milestones as product and architecture direction, not execution sessions or a `TODO.md` backlog.
- Build milestones through detailed TODO sessions. A milestone is complete only when the implementation sessions derived from it are finished, verified, and recorded.
- Treat `$wf arche` as shorthand for architecture planning, lightweight milestone planning, and architecture updates.
- Treat `$wf retrofit` as shorthand for restoring or normalizing the standard WF structure in an existing repository.
- Use the standard architecture folder contract in `references/architecture-structure.md` when bootstrapping, retrofitting, or updating architecture docs.
- Use a two-layer architecture doc model by default: top-level docs for cross-cutting truth, subsystem docs for bounded behavior.
- Stop at subsystem-level by default. Do not split architecture into per-function docs unless a function is unusually critical or complex.
- Treat a subsystem as a bounded behavior area that owns meaningful code, state, interfaces, dependencies, and tests.
- Do not create subsystem docs per function, hook, widget, or UI page by default; a page or device capability becomes a subsystem only when it owns a real workflow or lifecycle.
- Session size does not determine file size. Implement session work inside the correct subsystem or module; do not create one file per function or one file per checklist item.
- Use `references/subsystem-planning-rules.md` when planning subsystem boundaries, repo layout, import rules, test ownership, or subsystem-by-subsystem refactors.

## Request Classification

Classify the request first, then run only the relevant path:

1. `bootstrap-new-project`
2. `retrofit-existing-project`
3. `catch-up-existing-project`
4. `architecture-update`
5. `planning`
6. `implementation`
7. `review-debugging`

Treat `$wf retrofit` as shorthand for `retrofit-existing-project`.
Treat `$wf arche` as shorthand for `architecture-update`.

Do not edit files just because the skill was activated. Activation loads the operating procedure; the user request chooses the path.

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

For a focused task, the ideal read set is usually:

- `ARCHITECTURE/current/01-project-intent.md` only if product intent matters
- `ARCHITECTURE/current/02-milestones.md` only if roadmap, phase, milestone, or session planning depends on it
- one relevant top-level current doc
- one relevant subsystem doc
- `ARCHITECTURE/current/05-repo-map.md` only when code location is needed

If one task requires many scattered top-level docs, consolidate subsystem detail instead of multiplying cross-cutting files.

## Paths

### bootstrap-new-project

Use when the user is starting a new project or explicitly asks to set up the workflow.

- Create `ARCHITECTURE/`, `TODO.md`, and `LOG.md` if they do not already exist.
- Create the standard architecture skeleton from `references/architecture-structure.md`.
- Create initial subsystem docs only for clearly known functional areas.
- Seed `TODO.md` and `LOG.md` from `references/session-tracking.md`.
- Add a short `LOG.md` entry only after meaningful setup work is complete.

### retrofit-existing-project

Use when the user wants to adopt the WF workflow in the middle of an existing repo, especially when `TODO.md`, `LOG.md`, or `ARCHITECTURE/` are missing, incomplete, or nonstandard.

- Inspect the existing repo shape, docs, and workflow files first.
- Preserve useful existing content by default instead of replacing it.
- Create missing standard WF files and folders only where needed.
- Normalize tracking and architecture structure conservatively when existing files are nonstandard.
- Normalize tracking files against `references/session-tracking.md`.
- Normalize architecture docs against `references/architecture-structure.md`.
- Seed `TODO.md` in the current session-based format.
- Add a short `LOG.md` entry only after the retrofit work is meaningfully complete.
- See `references/retrofit-rules.md` for detailed retrofit and migration guidance.

### catch-up-existing-project

Use when the user asks to review the current state, catch up on a repo, or understand what exists now.

- Read the relevant tracking files and current docs.
- Inspect the actual code paths tied to the request.
- Summarize current state, gaps, risks, and likely next steps.
- Do not create missing workflow files unless the request implies they should exist.

### architecture-update

Use when the user wants to update architecture docs, plan the overall architecture, plan V1, optional V2+, and final-product milestones, or clarify subsystem boundaries.

- Read only the affected current docs.
- Read `references/architecture-structure.md` for the standard file roles and folder contract.
- Read `references/subsystem-planning-rules.md` when the request involves subsystem granularity, code ownership, test boundaries, import direction, or repo layout.
- Read `references/milestone-planning.md` when product direction is unclear or the user asks for a V1, optional V2+, roadmap, milestone, or final-product plan.
- Inspect code if needed to confirm runtime truth.
- Use a planning-first workflow when architecture intent is unclear or the request involves major tradeoffs.
- Clarify the architecture scope first: overall system, top-level docs, or one subsystem.
- Confirm project goal, target users, scope, constraints, system type, current milestone, desired documentation depth, and whether ADRs are needed before creating or rewriting architecture docs.
- Keep stable project target content in `ARCHITECTURE/current/01-project-intent.md`.
- Keep milestone summaries compact in `ARCHITECTURE/current/02-milestones.md`.
- Plan or revise subsystem boundaries and top-level architecture structure when needed.
- For subsystem planning, define bounded behavior, owned code, public API, internal files, dependency direction, data ownership, and test strategy.
- Update only the relevant architecture files.
- Prefer bounded subsystem docs over many small fragmented documents.
- Do not touch `archive/` unless the request is explicitly historical.

### planning

Use when the user asks for task planning, breakdown, or sequencing.

- Read the relevant docs and code.
- Break work into small verifiable session-sized slices.
- Read `references/subsystem-planning-rules.md` when planning code organization, subsystem splits/merges, isolated testing, or cross-subsystem work.
- Read `references/session-tracking.md` before creating or rewriting session entries in `TODO.md`.
- Refine `TODO.md` using dated session sections instead of a long undifferentiated task list.
- If planning from milestones, derive only current and near-next executable sessions from the active milestone.
- If a task spans multiple systems or would take multiple sittings, split it into sequenced sessions.
- Prefer session slices that touch one subsystem or one clearly named cross-subsystem integration.
- Update architecture docs only if product or system truth changes.

See `references/planning-rules.md` for task slicing and review guidance.

### implementation

Use when the user asks to build or change a concrete behavior.

- Read the relevant docs and code first.
- Identify the affected subsystem and its public/internal entrypoints before editing when the change is more than a trivial local fix.
- Refine task tracking only if the task is real project work.
- If the task is too large for one focused session, split it into the next session entries in `TODO.md`.
- Implement only what the current session needs.
- Keep imports, tests, and data access aligned with documented subsystem ownership unless the current task is explicitly changing those boundaries.
- Run the smallest useful verification, preferring subsystem-local tests before broader integration tests.
- Read `references/session-tracking.md` before moving session outcomes from `TODO.md` to `LOG.md`.
- Update `LOG.md` using the same date and session ID when a session is completed or reaches a meaningful stopping point.

### review-debugging

Use when the user asks for review, diagnosis, or debugging.

- Read the relevant current docs first, then inspect code and tests.
- Compare intended behavior vs actual behavior.
- Return findings first for review tasks.
- Update docs or tracking only if the user asks or the current truth clearly changed.

## Reference Files

- Read `references/planning-rules.md` when planning or reviewing task slices.
- Read `references/session-tracking.md` when creating, normalizing, or updating `TODO.md` and `LOG.md`.
- Read `references/milestone-planning.md` when planning V0, V1, V1.x, optional V2+, final-product direction, or roadmap-like architecture direction.
- Read `references/retrofit-rules.md` when handling `$wf retrofit` or normalizing an existing repo into the WF structure.
- Read `references/architecture-structure.md` when creating, normalizing, or updating `ARCHITECTURE/`.
- Read `references/doc-update-rules.md` when deciding which architecture doc to update.
- Read `references/subsystem-doc-template.md` when creating a new subsystem doc.
- Read `references/subsystem-planning-rules.md` when defining subsystem granularity, code ownership, import rules, test strategy, or refactor sequencing.
- Read `references/code-manager-integration.md` when implementation work needs physical file organization, file moves, import cleanup, test placement, TDD, diagnosis loops, or structured refactor execution.
- Read `references/code-manager-skill-blueprint.md` only when designing or creating the separate `code-manager` skill.
