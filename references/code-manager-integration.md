# Code Manager Integration

Use this reference when `$wf` implementation work needs detailed code organization or refactor execution.

`$wf` owns project workflow and memory:

- active session selection
- `TODO.md` and `LOG.md`
- `ARCHITECTURE/current/`
- subsystem docs as the canonical contract
- milestone direction
- ADR triggers

The future separate `code-manager` skill should own coding execution details:

- physical file layout
- file naming
- subsystem public APIs
- internal file boundaries
- import cleanup
- test placement
- TDD loops
- diagnosis loops
- safe file moves and large-file splits
- focused verification

## When WF Should Hand Off

Use or suggest `code-manager` when a `$wf` task involves:

- moving or splitting code files
- organizing code by subsystem
- fixing messy imports
- defining or tightening a public API
- deciding where tests should live
- applying TDD to a new behavior
- diagnosing a bug with reproduction and regression tests
- cleaning shallow modules or pass-through wrappers
- refactoring without changing behavior

## Shared Contract

WF subsystem docs define the contract.

Code layout implements the contract.

Tests prove the contract.

Milestones become code through verified TODO sessions, but TODO sessions do not define file boundaries. A session is one testable capability slice. A module or file is one coherent ownership boundary. Functions are implementation details inside that boundary.

Do not create one file per function or one file per checklist item. Split files by subsystem ownership, data ownership, dependency direction, lifecycle, independently testable behavior, or repeated reasons to change. Prefer compact deep modules over many shallow pass-through files.

The intended flow:

1. `$wf` identifies the active milestone when relevant.
2. `$wf` derives or selects the current TODO session.
3. `$wf` identifies the affected subsystem.
4. `code-manager` aligns files, imports, public APIs, and tests to that subsystem contract.
5. `code-manager` implements the session inside the correct module boundaries.
6. `code-manager` verifies the session outcome.
7. `$wf` records completed outcomes and updates docs only when project truth changes.

Do not duplicate the full code-manager rules inside WF. Keep WF focused on planning, architecture truth, and session tracking.
