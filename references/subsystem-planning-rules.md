# Subsystem Planning Rules

Use this reference when planning subsystem boundaries, repo layout, import rules, test ownership, or subsystem-by-subsystem refactors.

These rules combine C4-style component boundaries, DDD bounded-context thinking, vertical-slice architecture, and Feature-Sliced Design-style public APIs. They are guidance for repo-local code management, not a requirement to adopt any one framework.

Reference anchors:

- C4 components: https://c4model.com/abstractions/component
- C4 code diagrams: https://c4model.com/diagrams/code
- DDD bounded contexts: https://learn.microsoft.com/en-us/azure/architecture/microservices/model/tactical-domain-driven-design
- Feature-Sliced Design: https://feature-sliced.github.io/documentation/

## Definition

A subsystem is a bounded behavior area that owns meaningful code, state, interfaces, dependencies, and tests.

A subsystem is usually not:

- one function
- one hook
- one helper file
- one UI component
- one UI page by default

A page, device capability, or external integration becomes a subsystem only when it owns a real workflow, lifecycle, state machine, data contract, or test surface.

Example: `CameraButton` is not a subsystem. `camera-capture-and-upload` can be a subsystem if it owns permissions, preview lifecycle, capture, compression, upload, error states, and tests.

## Session-To-Code Mapping

Small implementation sessions do not imply tiny files.

Use this mapping:

```text
TODO session = one testable capability slice
Module or file = one coherent ownership boundary
Function = internal behavior inside that module
Test = proof
LOG = completion record
```

Do not split files by individual functions or checklist items. Split files by subsystem ownership, data ownership, dependency direction, lifecycle, independently testable behavior, or repeated reasons to change. Prefer compact deep modules over many shallow files.

## Starting Granularity

For a medium application, start with roughly 4-8 subsystem candidates. Expand only when repeated work proves that a boundary needs its own document, code ownership, and tests.

Prefer subsystem names that describe bounded behavior:

- `auth-session-and-timezone`
- `media-capture-and-upload`
- `checkout-and-payment`
- `offline-queue-and-sync`

Avoid names that are only implementation buckets:

- `utils`
- `components`
- `pages`
- `services`
- `camera-button`

## Split Criteria

Split a subsystem when the candidate area has at least one strong reason:

- it has its own lifecycle, state machine, or business rules
- it owns data models, storage keys, tables, API contracts, or jobs
- it can be tested independently with meaningful fixtures or mocks
- it is reused by multiple pages, workflows, or entrypoints
- it changes for different reasons than the surrounding code
- it has distinct failure modes, permissions, or operational risks
- future contributors repeatedly need a focused doc to work safely

## Merge Or Avoid-Split Criteria

Do not create a separate subsystem when:

- the area is just a function, hook, widget, page shell, or small helper
- the proposed boundary cannot be tested alone
- the files always change together with another subsystem
- the split would create circular dependencies or chatty internal APIs
- the doc would mostly repeat another subsystem doc
- the only reason is matching the current folder structure

## Code Ownership Contract

Each subsystem should document:

- owned files and folders
- public entrypoints that other subsystems may import
- internal files that other subsystems should not import
- owned data, storage, APIs, jobs, or device capabilities
- allowed dependencies
- forbidden dependencies
- local unit or contract tests
- cross-subsystem integration tests

Prefer imports through a subsystem public API such as `index.ts`, `mod.rs`, or package-level exports. Avoid cross-subsystem imports from internal files unless the current task is explicitly correcting or documenting a temporary exception.

## Test Strategy

Use the smallest test surface that proves the behavior:

- Unit tests live with or near subsystem code.
- Contract tests prove public API behavior when the subsystem is consumed by others.
- Integration tests belong in a shared integration test area when behavior crosses subsystem boundaries.
- End-to-end tests should cover critical user journeys, not every internal branch.

Every subsystem doc should answer: how can this subsystem be tested by itself?

## Planning Flow

When asked to plan or refactor subsystem-by-subsystem:

1. Inspect current repo folders, entrypoints, tests, and architecture docs.
2. Identify behavior-based subsystem candidates, not just existing directories.
3. Map existing files to proposed subsystem owners.
4. Mark mixed-ownership or unclear files as temporary compatibility areas.
5. Define each subsystem's public API and forbidden internal imports.
6. Define local tests and cross-subsystem tests.
7. Refactor one subsystem or one integration boundary per session.
8. Add an ADR only when a boundary decision materially constrains future architecture.

## ADR Triggers

Create or update an ADR when:

- splitting or merging subsystems changes future ownership
- dependency direction changes
- a shared/platform layer is introduced
- data ownership or storage ownership changes
- an important architecture pattern is chosen over realistic alternatives
- a temporary boundary exception is accepted for a reason future work must know
