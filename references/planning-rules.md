# Planning Rules

Use these rules when `$WF` is handling planning, review, or scoped implementation work.

Use `references/session-tracking.md` for the canonical `TODO.md` and `LOG.md` formats.
Use `references/milestone-planning.md` when a plan depends on V0, V1, V1.x, optional V2+, roadmap, phase, or final-product direction.
Use `references/subsystem-planning-rules.md` when a plan involves code ownership, subsystem boundaries, import direction, test ownership, or subsystem-by-subsystem refactoring.

## Task Slicing

- Prefer session-sized tasks that affect one subsystem or one clear behavior.
- Prefer one subsystem or one named cross-subsystem integration per implementation session.
- Each session should be small enough to complete in one focused pass.
- Each session should have an obvious verification step.
- If a task spans multiple systems or sittings, split it into sequenced sessions whenever possible.
- Keep only the current and near-next sessions in `TODO.md`. Remove stale or merged items.
- Treat milestones as roadmap direction, not session-sized tasks.
- When planning from a milestone, derive concrete current or near-next TODO sessions from the milestone instead of expanding the milestone doc into a backlog.
- A milestone is complete only when its derived sessions are implemented, verified, and recorded.

## Subsystem Planning Flow

When the user asks for subsystem planning or cleaner code management:

1. Inspect current folders, entrypoints, tests, and relevant architecture docs.
2. Identify behavior-based subsystem candidates before proposing file moves.
3. Map existing files to subsystem owners and mark unclear mixed-ownership areas.
4. Define public entrypoints, internal files, import rules, and test strategy for each candidate.
5. Split work into sessions that refactor one subsystem or one integration boundary at a time.
6. Add ADR work only for boundary decisions future contributors would otherwise re-litigate.

## TODO Discipline

Use `TODO.md` as the active session queue, not a backlog.

- Follow `references/session-tracking.md` for the exact file format.
- Keep only the current session, the next few planned sessions, and blockers that affect active or near-next work.
- If a request is too large, split it into additional sessions instead of extending one session indefinitely.
- If a roadmap exists, derive `TODO.md` entries only from the active milestone and near-next work.
- Make TODO sessions detailed enough to execute, but do not make them dictate file boundaries. Sessions are capability slices; modules are ownership boundaries.

## LOG Discipline

Use `LOG.md` as the completed-session record.

- Follow `references/session-tracking.md` for the exact file format.
- Record useful outcomes, verification, decisions, blockers, or handoff notes.
- Do not log every prompt, every edit, or in-progress work that has not reached a useful stopping point.

## Review Flow

For review requests:

1. Identify the intended behavior from current docs and code.
2. Inspect the changed or affected code paths.
3. Return findings first, ordered by severity.
4. Note open questions or assumptions.
5. Add summaries only after findings.

## Planning Output

A good plan should:

- state the goal clearly
- identify the touched subsystem or code area
- identify the active milestone when roadmap direction matters
- identify public APIs, import boundaries, and test ownership when code organization is involved
- split the work into the smallest useful session-sized slices
- define how each session will be verified
- keep the `TODO.md` output clean enough to execute session by session
