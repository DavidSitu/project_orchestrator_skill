# Architecture Structure

Use this reference when creating, normalizing, or updating `ARCHITECTURE/`.

The WF architecture format is industry-aligned, not a full clone of any one framework. Use arc42-style coverage for goals and constraints, C4-style thinking for system views and boundaries, and optional ADRs for important decisions.

Reference anchors:

- arc42: https://arc42.org/
- C4 model: https://c4model.com/
- ADRs: https://adr.github.io/

## Planning-First Architecture

For `$wf arche`, first determine whether the user wants exploration, an architecture plan, or direct documentation edits.

- Ask only for missing intent that cannot be learned from existing docs or code.
- Use current code and current docs as runtime truth for what exists now.
- Treat product direction, scope, constraints, tradeoffs, and target users as user intent.
- When architecture intent is unclear, clarify project goal, target users, in-scope and out-of-scope areas, constraints, system type, desired documentation depth, and whether ADRs are needed before writing docs.
- When the user is in Codex Plan Mode, produce a decision-complete architecture plan before file changes.
- When the user has already specified the architecture change clearly, update the relevant docs directly.
- Do not update `TODO.md` for pure architecture discussion unless the architecture work becomes tracked project work.

## Folder Contract

Use this structure by default:

```text
ARCHITECTURE/
├── README.md
├── current/
│   ├── 01-project-intent.md
│   ├── 02-overall-system-design.md
│   ├── 03-overall-ui-design.md
│   ├── 04-repo-map.md
│   └── subsystems/
│       ├── README.md
│       └── <bounded-behavior>.md
├── decisions/
└── archive/
```

`decisions/` and `archive/` are optional. Create `decisions/` only when an architecturally significant decision exists. Create or read `archive/` only for historical context, migration history, or explicitly archived docs.

## Top-Level Files

- `ARCHITECTURE/README.md`: index for the architecture set, recommended reading order, folder meanings, and links to current docs, subsystem docs, decisions, and archive when present.
- `ARCHITECTURE/current/01-project-intent.md`: project goals, target users, scope, non-goals, key constraints, success direction, and current phase.
- `ARCHITECTURE/current/02-overall-system-design.md`: system boundaries, subsystem responsibilities, data flow, external dependencies, backend/frontend ownership, deployment/runtime shape, and shared terminology.
- `ARCHITECTURE/current/03-overall-ui-design.md`: UI surfaces, navigation, key user flows, state relationships, canonical UI patterns, and accessibility expectations. For backend-only, CLI-only, or library projects, keep the file and mark it `N/A` with a short reason.
- `ARCHITECTURE/current/04-repo-map.md`: folder responsibilities, entrypoints, major modules, ownership boundaries, generated or external code notes, and doc-to-code mapping.

## Subsystem Files

Use `ARCHITECTURE/current/subsystems/README.md` as the subsystem index and naming guide.

Create `ARCHITECTURE/current/subsystems/<bounded-behavior>.md` only when an area has meaningful behavior or complexity. Name subsystem docs by behavior boundary, not vague buckets. Use `references/subsystem-doc-template.md` for the content shape.

Prefer a few useful subsystem docs over many tiny files. A medium or large app often starts with 4-6 subsystem docs, then expands only when work repeatedly needs more detail.

## ADRs And Logs

Use `ARCHITECTURE/decisions/` for ADRs when a decision changes or constrains the architecture.

ADRs are not TODOs:

- `TODO.md` tracks current and near-next work sessions.
- `LOG.md` records completed session outcomes, handoffs, and short factual history.
- ADRs record why a significant architecture decision was made, what alternatives were considered, and what consequences future work must respect.

Create ADRs only for decisions future contributors would otherwise re-litigate or accidentally undo. Use simple numbered names such as `0001-use-managed-auth-provider.md`.

## Update Boundaries

- Update `01-project-intent.md` when product goals, users, scope, non-goals, constraints, or phase direction changes.
- Update `02-overall-system-design.md` when system boundaries, ownership, data flow, dependencies, runtime shape, or shared terminology changes.
- Update `03-overall-ui-design.md` when surfaces, navigation, key journeys, UI state rules, visual language, or accessibility expectations change.
- Update `04-repo-map.md` when entrypoints, folder responsibilities, module ownership, generated code, or doc-to-code mapping changes.
- Update a subsystem doc when one bounded behavior area's flows, states, dependencies, code map, known gaps, or extension points change.
- Add an ADR when the reason behind an architecture decision matters beyond the current session.

## Bootstrap And Retrofit Checklist

- Create `ARCHITECTURE/README.md` and `ARCHITECTURE/current/`.
- Create the four standard current docs. Mark `03-overall-ui-design.md` as `N/A` with a short reason when the project has no UI.
- Create `ARCHITECTURE/current/subsystems/README.md`.
- Create subsystem docs only for clearly justified bounded behavior areas.
- Create `ARCHITECTURE/decisions/` only when recording an actual ADR.
- Create or preserve `ARCHITECTURE/archive/` only when historical docs exist or the user asks for archival structure.
- Prefer thin, accurate first-pass docs over speculative detail.
