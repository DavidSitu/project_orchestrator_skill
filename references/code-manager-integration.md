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

The intended flow:

1. `$wf` identifies the active session and affected subsystem.
2. `code-manager` aligns files, imports, public APIs, and tests to that subsystem contract.
3. `$wf` records completed outcomes and updates docs only when project truth changes.

Do not duplicate the full code-manager rules inside WF. Keep WF focused on planning, architecture truth, and session tracking.
