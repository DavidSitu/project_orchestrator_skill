# Planning Rules

Use these rules when `$WF` is handling planning, review, or scoped implementation work.

Use `references/session-tracking.md` for the canonical `TODO.md` and `LOG.md` formats.
Use `references/milestone-planning.md` when a plan depends on V0, V1, V1.x, roadmap, phase, or final-product direction.

## Task Slicing

- Prefer session-sized tasks that affect one subsystem or one clear behavior.
- Each session should be small enough to complete in one focused pass.
- Each session should have an obvious verification step.
- If a task spans multiple systems or sittings, split it into sequenced sessions whenever possible.
- Keep only the current and near-next sessions in `TODO.md`. Remove stale or merged items.
- Treat milestones as roadmap direction, not session-sized tasks.

## TODO Discipline

Use `TODO.md` as the active session queue, not a backlog.

- Follow `references/session-tracking.md` for the exact file format.
- Keep only the current session, the next few planned sessions, and blockers that affect active or near-next work.
- If a request is too large, split it into additional sessions instead of extending one session indefinitely.
- If a roadmap exists, derive `TODO.md` entries only from the active milestone and near-next work.

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
- split the work into the smallest useful session-sized slices
- define how each session will be verified
- keep the `TODO.md` output clean enough to execute session by session
