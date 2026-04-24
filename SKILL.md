---
name: wf
description: Explicit project-mode workflow for Codex. Use when bootstrapping a new project, retrofitting an existing repo into the workflow, catching up on an existing repo, updating architecture docs, planning tracked work, implementing scoped tasks, or reviewing/debugging within a repo while maintaining session-based TODO.md, LOG.md, and ARCHITECTURE/current/.
---

# WF

Use this skill only when the user explicitly invokes `$wf` or clearly asks for the project workflow. Keep normal chat, writing, and reasoning unstructured when this skill is not requested.

## Core Defaults

- Treat the `WF` workflow as per-turn project mode, not a permanent conversation mode.
- Use `ARCHITECTURE/current/` as the canonical documentation set.
- Do not read `ARCHITECTURE/archive/` unless the user explicitly asks for historical context, migration history, or past reasoning.
- Read only the relevant docs and code for the task. Do not load the whole architecture tree by default.
- Documentation guides understanding. Runtime code is still the final source of truth for actual behavior.
- Treat `TODO.md` as a clean session tracker, not a backlog.
- Organize `TODO.md` under a date heading using `YYYY-MM-DD`, then session sections such as `S1`, `S2`, `S3`.
- Keep each session section small enough for one focused work session, with a short title and a small checklist.
- Keep only the current session and the next few sessions in `TODO.md`.
- Use `LOG.md` as the matching dated record of completed or meaningfully concluded sessions, using the same session IDs.
- Treat `$wf arche` as shorthand for architecture planning and architecture updates.
- Treat `$wf retrofit` as shorthand for restoring or normalizing the standard WF structure in an existing repository.
- Use a two-layer architecture doc model by default: top-level docs for cross-cutting truth, subsystem docs for bounded behavior.
- Stop at subsystem-level by default. Do not split architecture into per-function docs unless a function is unusually critical or complex.

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
5. Only the additional top-level or subsystem docs relevant to the task
6. The actual code paths touched by the task

Skip files that do not exist or are not needed for the current path.

For a focused task, the ideal read set is usually:

- `ARCHITECTURE/current/01-project-intent.md` only if product intent matters
- one relevant top-level current doc
- one relevant subsystem doc
- `ARCHITECTURE/current/04-repo-map.md` only when code location is needed

If one task requires many scattered top-level docs, consolidate subsystem detail instead of multiplying cross-cutting files.

## Paths

### bootstrap-new-project

Use when the user is starting a new project or explicitly asks to set up the workflow.

- Create `ARCHITECTURE/`, `TODO.md`, and `LOG.md` if they do not already exist.
- Create the top-level docs in `ARCHITECTURE/current/`.
- Create `ARCHITECTURE/current/subsystems/README.md`.
- Create initial subsystem docs only for clearly known functional areas.
- Seed `TODO.md` with an initial date heading and a few session-sized checklist blocks.
- Add a short `LOG.md` entry only after meaningful setup work is complete.

### retrofit-existing-project

Use when the user wants to adopt the WF workflow in the middle of an existing repo, especially when `TODO.md`, `LOG.md`, or `ARCHITECTURE/` are missing, incomplete, or nonstandard.

- Inspect the existing repo shape, docs, and workflow files first.
- Preserve useful existing content by default instead of replacing it.
- Create missing standard WF files and folders only where needed.
- Normalize tracking and architecture structure conservatively when existing files are nonstandard.
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

Use when the user wants to update architecture docs, plan the overall architecture, or clarify subsystem boundaries.

- Read only the affected current docs.
- Inspect code if needed to confirm runtime truth.
- Clarify the architecture scope first: overall system, top-level docs, or one subsystem.
- Plan or revise subsystem boundaries and top-level architecture structure when needed.
- Update only the relevant architecture files.
- Prefer bounded subsystem docs over many small fragmented documents.
- Do not touch `archive/` unless the request is explicitly historical.

### planning

Use when the user asks for task planning, breakdown, or sequencing.

- Read the relevant docs and code.
- Break work into small verifiable session-sized slices.
- Refine `TODO.md` using dated session sections instead of a long undifferentiated task list.
- If a task spans multiple systems or would take multiple sittings, split it into sequenced sessions.
- Update architecture docs only if product or system truth changes.

See `references/planning-rules.md` for task slicing and review guidance.

### implementation

Use when the user asks to build or change a concrete behavior.

- Read the relevant docs and code first.
- Refine task tracking only if the task is real project work.
- If the task is too large for one focused session, split it into the next session entries in `TODO.md`.
- Implement only what the current session needs.
- Run the smallest useful verification.
- Update `LOG.md` using the same date and session ID when a session is completed or reaches a meaningful stopping point.

### review-debugging

Use when the user asks for review, diagnosis, or debugging.

- Read the relevant current docs first, then inspect code and tests.
- Compare intended behavior vs actual behavior.
- Return findings first for review tasks.
- Update docs or tracking only if the user asks or the current truth clearly changed.

## Reference Files

- Read `references/planning-rules.md` when planning or reviewing task slices.
- Read `references/retrofit-rules.md` when handling `$wf retrofit` or normalizing an existing repo into the WF structure.
- Read `references/doc-update-rules.md` when deciding which architecture doc to update.
- Read `references/subsystem-doc-template.md` when creating a new subsystem doc.
