# Session Tracking

Use this reference when creating, normalizing, or updating `TODO.md` and `LOG.md`.

This is the WF session tracking standard. It is a lightweight repo-local convention optimized for agent work, not a universal industry standard.

## File Roles

- `TODO.md` is the active session queue.
- `LOG.md` is the completed-session record.
- ADRs under `ARCHITECTURE/decisions/` record architecture decisions, not session history.
- Milestones are roadmap direction in `ARCHITECTURE/current/01-project-intent.md`, not TODO sessions.

## TODO.md Format

Use this shape:

```md
# TODO

## YYYY-MM-DD

### S1: Short Session Title
- [ ] Do one scoped task
- [ ] Do the next scoped task
- [ ] Verify the session outcome
```

Rules:

- Use one date heading for the active work block.
- Use session headings such as `S1`, `S2`, `S3`.
- Keep each session small enough for one focused work pass.
- Use a short checkbox list for the session only.
- Make the final checkbox a verification step when useful.
- Keep only the current session and the next few sessions.
- Do not keep a long backlog, speculative ideas, or stale work in `TODO.md`.
- Do not copy a full milestone roadmap into `TODO.md`; include only executable sessions for active or near-next work.

## LOG.md Format

Use this shape:

```md
# LOG

## YYYY-MM-DD

### S1: Short Session Title
- Completed the scoped work that matters for handoff.
- Verified the useful outcome.
- Recorded any decision, blocker, or next-session handoff that still matters.
```

Rules:

- Use the same date and session IDs as `TODO.md`.
- Record outcomes, not checkboxes.
- Keep entries brief and factual.
- Include completed work, verification, key decisions, blockers, or handoff notes only when useful.
- Do not log every prompt, every tiny edit, or in-progress work that has not reached a useful stopping point.
- Do not use `LOG.md` as a changelog; use it as session history for future work.

## Session Lifecycle

- Plan active work in `TODO.md`.
- Execute one session at a time.
- When work comes from a milestone plan, derive only the current or near-next sessions from the active milestone.
- If work grows too large, split it into another session instead of extending one session indefinitely.
- When a session is completed or reaches a meaningful stopping point, write a matching `LOG.md` entry.
- Mark the completed TODO session done or remove it when rolling the session queue forward.
- Carry unfinished work into a new or continuing session with a clear title.

## Migration Rules

- Preserve useful active work from existing tracking files.
- Normalize existing active work into dated session sections.
- Preserve useful history from existing logs, but do not rewrite large historical logs unless the user asks.
- Do not copy stale backlog items into the new `TODO.md`.
- If old tracking content is unclear, preserve it conservatively and summarize what was kept or left out.

## Bootstrap Checklist

- Create `TODO.md` with `# TODO`, today's `YYYY-MM-DD` heading, and one or more session sections.
- Create `LOG.md` with `# LOG`; add entries only after meaningful work is complete.
- Keep both files short enough to support fast handoff and resume.
