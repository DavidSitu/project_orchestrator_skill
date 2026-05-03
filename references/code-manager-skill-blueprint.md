# Code Manager Skill Blueprint

This is a design blueprint for a future separate Codex skill, not active WF procedure.

The future skill should live beside `wf` as its own installed skill:

```text
agent_skill/
├── work_flow/
└── code_manager/

~/.codex/skills/
├── wf/
└── code-manager/
```

## Purpose

`code-manager` should execute a planned coding session with professional codebase discipline.

It should manage:

- physical file layout
- file naming
- subsystem public APIs
- import boundaries
- test placement
- safe file moves
- large-file splits
- TDD loops when practical
- bug diagnosis loops
- code architecture cleanup
- post-refactor verification

It should not own:

- project intent
- milestone planning
- TODO/LOG session tracking
- architecture source of truth
- subsystem documentation as the canonical contract
- product roadmap decisions

Those stay in `$wf`.

## Relationship To WF

`$wf` is the project brain.

`code-manager` is the coding execution discipline.

Use this split:

```text
WF decides:
- what the active session is
- which subsystem owns the behavior
- which docs are canonical
- what architecture changed
- what should be logged

code-manager decides:
- where files should live
- what imports are allowed
- what public API should expose the behavior
- where tests should be placed
- how to move/split/refactor code safely
- what focused verification proves the change
```

When both are active, the flow should be:

1. `$wf` reads `TODO.md`, `LOG.md`, and relevant `ARCHITECTURE/current/` docs.
2. `$wf` identifies the active session and affected subsystem.
3. `code-manager` reads the relevant subsystem doc and code paths.
4. `code-manager` executes the smallest professional coding slice.
5. `code-manager` runs focused verification.
6. `$wf` updates `TODO.md`, `LOG.md`, and subsystem docs only if project truth changed.

## Relationship To Andrej Karpathy Perspective

The Karpathy-style guardrail is taste, not process:

- simple first
- do not be a hero
- avoid speculative abstraction
- build one verifiable slice
- inspect data/code before guessing
- test edge cases, not only happy paths
- report verification honestly

`code-manager` should embody that taste without requiring the persona skill.

Practical translation:

- Prefer a boring module over a clever framework.
- Prefer one green vertical slice over many half-finished layers.
- Prefer a small public API with meaningful internals over many shallow pass-through files.
- Prefer reproduction and regression tests over bug-fix guessing.

## Matt Pocock Ideas To Borrow

Use Matt Pocock's skills as reference material, not as a replacement for WF.

Borrow these ideas:

- `grill-with-docs`: clarify vague requirements and shared language before coding.
- `tdd`: use red-green-refactor for new behavior when practical.
- `diagnose`: reproduce, minimize, hypothesize, instrument, fix, regression-test.
- `improve-codebase-architecture`: identify shallow modules, unclear boundaries, and architecture entropy.
- `to-issues`: split large plans into vertical slices.

Do not copy the whole system directly because WF already owns project memory, architecture docs, ADRs, and session tracking.

## Core Workflow

Classify the coding request first:

1. `new-behavior`
2. `bug-fix`
3. `refactor-file-layout`
4. `split-large-file`
5. `import-boundary-cleanup`
6. `test-placement`
7. `architecture-cleanup`

Then run the narrowest matching path.

### Common Start

For non-trivial work:

1. Identify the affected subsystem.
2. Read the matching WF subsystem doc when it exists.
3. Inspect current files, imports, tests, and entrypoints.
4. Identify the public API and internal files.
5. Define the smallest behavior or structure change that can be verified.

If no matching subsystem doc exists:

- infer the likely subsystem from code and behavior
- proceed only if the change is local and safe
- suggest a WF subsystem-doc update when the boundary matters

## New Behavior Flow

Use vertical-slice execution:

1. Clarify observable behavior.
2. Identify the subsystem public API or user-facing entrypoint.
3. Add or update a focused failing test when practical.
4. Implement the smallest code path.
5. Refactor only after the test passes.
6. Run subsystem-local verification first.
7. Add integration or E2E coverage only when the behavior crosses boundaries or is critical.

## Bug Fix Flow

Use a diagnosis loop:

1. Reproduce the bug.
2. Minimize the failing case.
3. Form a specific hypothesis.
4. Instrument only if needed.
5. Fix the narrowest cause.
6. Add a regression test.
7. Verify the affected subsystem and any touched integration boundary.

Do not guess from symptoms when reproduction is possible.

## Refactor And File Move Flow

Use safe movement:

1. Inspect current imports and exports.
2. Identify ownership: subsystem, shared, platform, app wiring, or mixed.
3. Move one subsystem or one integration boundary at a time.
4. Preserve the public API where possible.
5. Update imports.
6. Remove dead exports and duplicate old files.
7. Run formatter/typecheck/tests.
8. Update WF docs or propose an ADR only if ownership or dependency direction changed.

Do not combine large file moves with unrelated behavior changes unless the user explicitly asks.

## Module Boundary Rules

Good modules are deep:

- small public API
- meaningful internal behavior
- few reasons to change
- testable through the public contract

Weak modules are shallow:

- many pass-through wrappers
- public exports for every internal helper
- names like `utils`, `helpers`, `manager`, or `service` without clear behavior
- code that merely forwards calls without owning a rule or state

Prefer behavior names over implementation bucket names.

## Import Boundary Rules

Default rules:

- Other subsystems import only from a subsystem public entrypoint.
- Internal files stay internal.
- Avoid cross-subsystem deep imports.
- Avoid circular dependencies.
- UI should not own domain rules.
- Shared code should be generic and boring.
- Platform code should own framework/device/database adapters.
- Business rules belong in the subsystem that owns the behavior.

Temporary exceptions should be documented in the subsystem doc or raised as follow-up work.

## Test Placement Rules

Use tests as the proof of ownership:

- Unit tests live near subsystem code.
- Contract tests exercise public APIs.
- Integration tests cover cross-subsystem behavior.
- E2E tests cover critical user journeys only.
- Regression tests should be added for fixed bugs.

Every meaningful subsystem should answer: how can this be tested by itself?

## Recommended Skill Folder

```text
code_manager/
├── SKILL.md
├── agents/
│   └── openai.yaml
└── references/
    ├── wf-integration-rules.md
    ├── vertical-slice-rules.md
    ├── tdd-rules.md
    ├── diagnose-rules.md
    ├── module-boundary-rules.md
    ├── import-boundary-rules.md
    ├── test-placement-rules.md
    └── refactor-safety-checklist.md
```

Keep `SKILL.md` short. Put the detailed flows in references.

## Suggested Skill Metadata

```yaml
---
name: code-manager
description: Professional codebase execution skill for Codex. Use when implementing a WF-planned session, organizing code by subsystem, moving or splitting files, defining public APIs, enforcing import boundaries, placing tests, applying TDD, diagnosing bugs, or refactoring code structure with focused verification.
---
```

## Completion Checklist

Before finishing a code-manager task:

- affected subsystem identified
- public API preserved or intentionally changed
- internal imports not leaked
- moved files have updated imports
- dead exports and duplicate files removed
- tests placed at the right level
- focused verification run or clearly reported as not run
- WF docs/TODO/LOG update suggested when project truth changed
