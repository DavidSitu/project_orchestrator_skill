# Architecture Structure

Use this reference when creating, normalizing, or updating `ARCHITECTURE/`.

The WF architecture format is industry-aligned, not a full clone of any one framework. Use arc42-style coverage for goals and constraints, C4-style thinking for system views and boundaries, DDD/vertical-slice thinking for subsystem boundaries, and optional ADRs for important decisions.

Reference anchors:

- arc42: https://arc42.org/
- C4 model: https://c4model.com/
- ADRs: https://adr.github.io/
- Feature-Sliced Design: https://feature-sliced.github.io/documentation/

## Planning-First Architecture

For `$wf arche`, first determine whether the user wants exploration, an architecture plan, or direct documentation edits.

- Ask only for missing intent that cannot be learned from existing docs or code.
- Use current code and current docs as runtime truth for what exists now.
- Treat product direction, scope, constraints, tradeoffs, and target users as user intent.
- When architecture intent is unclear, clarify project goal, target users, in-scope and out-of-scope areas, constraints, system type, desired documentation depth, and whether ADRs are needed before writing docs.
- When the user asks for global view, overall architecture, whole project direction, MVP planning, final product direction, repo structure, or broad subsystem boundaries, read broadly across the relevant `ARCHITECTURE/current/` docs. Do not use a hard file cap for broad architecture work.
- When the user asks for MVP/V1, Post-MVP/V1.x, Future/V2+, roadmap, milestones, phases, or final-product direction, use `references/milestone-planning.md`.
- When the user provides a whole idea document at WF startup, distill accepted product truth into `01-05`. Keep a rich cleaned version of the idea in `01-project-intent.md`; do not store the raw full brief by default.
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
│   ├── 02-milestones.md
│   ├── 03-overall-system-design.md
│   ├── 04-overall-ui-design.md
│   ├── 05-repo-map.md
│   └── subsystems/
│       ├── README.md
│       └── <bounded-behavior>.md
├── decisions/
└── archive/
```

`decisions/` and `archive/` are optional. Create `decisions/` only when an architecturally significant decision exists. Create or read `archive/` only for historical context, migration history, or explicitly archived docs.

## Top-Level Files

- `ARCHITECTURE/README.md`: thin index for the architecture set, recommended reading order, folder meanings, and links to current docs, subsystem docs, decisions, and archive when present.
- `ARCHITECTURE/current/01-project-intent.md`: rich stable product intent: cleaned idea summary, goals, target users or customers, core problem, value proposition, product principles, scope, non-goals, key constraints, success direction, and current phase.
- `ARCHITECTURE/current/02-milestones.md`: compact product and architecture phase direction such as MVP/V1, Post-MVP/V1.x, optional Future/V2+, and final-product direction. MVP scope may include user journey flow, required pages, page-level capabilities, required buttons/controls, required states, and acceptance signal. It is not a backlog, TODO file, ADR, business plan, GTM plan, promotion plan, or file-by-file implementation checklist.
- `ARCHITECTURE/current/03-overall-system-design.md`: system boundaries, subsystem responsibilities, data flow, external dependencies, backend/frontend ownership, deployment/runtime shape, and shared terminology.
- `ARCHITECTURE/current/04-overall-ui-design.md`: UI design direction, visual language, navigation model, layout patterns, interaction conventions, responsive/accessibility expectations, and screenshot/prompt-derived UI decisions. It may start high-level before external UI design and become more concrete after the user provides screenshots, Figma-like prompts, images, or improved UI prompts. For backend-only, CLI-only, or library projects, keep the file and mark it `N/A` with a short reason.
- `ARCHITECTURE/current/05-repo-map.md`: folder responsibilities, entrypoints, major modules, ownership boundaries, generated or external code notes, and doc-to-code mapping.

## Subsystem Files

Use `ARCHITECTURE/current/subsystems/README.md` as the subsystem index and naming guide.

Create `ARCHITECTURE/current/subsystems/<bounded-behavior>.md` only when an area has meaningful behavior or complexity. Name subsystem docs by behavior boundary, not vague buckets. Use `references/subsystem-doc-template.md` for the content shape.

Prefer a few useful subsystem docs over many tiny files. A medium app often starts with roughly 4-8 subsystem docs, then expands only when work repeatedly needs more detail.

Use `references/subsystem-planning-rules.md` when deciding subsystem granularity, code ownership, public APIs, import rules, test strategy, or subsystem-by-subsystem refactor order.

Do not create subsystem docs per function, hook, widget, or UI page by default. A page or device capability becomes a subsystem only when it owns a real workflow, lifecycle, state, data contract, dependencies, or test surface.

## ADRs And Logs

Use `ARCHITECTURE/decisions/` for ADRs when a decision changes or constrains the architecture.

ADRs are not TODOs:

- `TODO.md` tracks current and near-next work sessions.
- `LOG.md` records completed session outcomes, handoffs, and short factual history.
- ADRs record why a significant architecture decision was made, what alternatives were considered, and what consequences future work must respect.

Create ADRs only for decisions future contributors would otherwise re-litigate or accidentally undo. Use simple numbered names such as `0001-use-managed-auth-provider.md`.

## Milestones And Roadmap

Use `references/milestone-planning.md` when `$wf arche` needs MVP/V1, Post-MVP/V1.x, optional Future/V2+, roadmap, phase, or final-product direction.

Keep milestone summaries compact inside `ARCHITECTURE/current/02-milestones.md`. Milestones guide architecture and session planning, but they are not TODO sessions or ADRs.

Detailed business logic, promotion, go-to-market, GTM, separate `PRODUCT/` docs, or a separate `05-roadmap.md` are out of scope for this architecture standard version.

## Product-To-Code SOP

WF supports this sequence without adding new commands:

1. The user does manual product planning: product-market-fit hypothesis, target customer, and user journey flow.
2. The user or another reasoning pass validates business logic and accepted direction.
3. WF initializes or updates architecture docs, keeping rich accepted intent in `01` and MVP/Post-MVP function scope in `02`.
4. UI design may happen outside the codebase or through a stronger prompt; when the user returns with screenshots, images, or UI prompts, update `04`.
5. Implementation planning turns accepted MVP scope into session-sized `TODO.md` entries, then code work follows subsystem/module ownership.

## Update Boundaries

- Update `01-project-intent.md` when product goals, target customer, core problem, value proposition, product principles, users, scope, non-goals, constraints, stable success direction, or current phase changes.
- Update `02-milestones.md` when MVP/V1, Post-MVP/V1.x, Future/V2+, roadmap direction, milestone direction, phase direction, final-product direction, MVP user journey, page capability scope, required controls, required states, or acceptance signal changes.
- Update `03-overall-system-design.md` when system boundaries, ownership, data flow, dependencies, runtime shape, or shared terminology changes.
- Update `04-overall-ui-design.md` when UI design direction, visual language, navigation, layout patterns, interaction conventions, responsive/accessibility expectations, or screenshot/prompt-derived UI decisions change.
- Update `05-repo-map.md` when entrypoints, folder responsibilities, module ownership, generated code, or doc-to-code mapping changes.
- Update a subsystem doc when one bounded behavior area's flows, states, dependencies, code map, known gaps, or extension points change.
- Add an ADR when the reason behind an architecture decision matters beyond the current session.

## Bootstrap And Retrofit Checklist

- Create `ARCHITECTURE/README.md` and `ARCHITECTURE/current/`.
- Create the standard current docs using the current numbering. Keep `02-milestones.md` thin when milestone direction is not yet known, and use it when the project has active phase planning.
- Mark `04-overall-ui-design.md` as `N/A` with a short reason when the project has no UI.
- Create `ARCHITECTURE/current/subsystems/README.md`.
- Create subsystem docs only for clearly justified bounded behavior areas.
- Create `ARCHITECTURE/decisions/` only when recording an actual ADR.
- Create or preserve `ARCHITECTURE/archive/` only when historical docs exist or the user asks for archival structure.
- Prefer thin, accurate first-pass docs over speculative detail.

## Existing Repo Migration

- For new WF bootstraps, use the current numbering.
- For existing repos, do not blindly rename architecture files unless the user asks for retrofit or normalization.
- If old milestone content exists in `01-project-intent.md`, move only accepted milestone direction into `02-milestones.md`; keep stable project target content in `01-project-intent.md`.
- If existing `02-overall-system-design.md`, `03-overall-ui-design.md`, or `04-repo-map.md` exist, plan a safe rename to `03`, `04`, and `05` only when links and references can be updated cleanly.
- If renaming would create churn, preserve existing filenames and document the local structure in `ARCHITECTURE/README.md`.
