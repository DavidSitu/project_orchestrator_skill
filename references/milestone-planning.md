# Milestone Planning

Use this reference when `$wf arche` needs lightweight roadmap or milestone planning.

Milestones are product and architecture direction. They are not execution sessions, TODO entries, ADRs, or business/promotion plans.

## When To Use

Use milestone planning when:

- product direction is unclear during `$wf arche`
- the user asks for V1, roadmap, milestones, phases, or final-product direction
- architecture choices depend on the intended product phase
- a large request needs a roadmap before it can be split into sessions

Do not use milestone planning for every small architecture edit.

## Storage Location

Store compact milestone summaries in `ARCHITECTURE/current/01-project-intent.md` under a `Milestones` or `Roadmap` section.

Do not create a separate `ARCHITECTURE/current/05-roadmap.md` in this version. Do not create `PRODUCT/`, business logic, promotion, go-to-market, or GTM docs as part of milestone planning.

## Milestone Format

Use these milestone labels by default:

- `V0`: the smallest useful proving version or internal prototype
- `V1`: the first coherent user-facing product version
- `V1.x`: near-term post-V1 improvements that should not block V1
- `Final Product Direction`: the long-term north star, not a committed backlog

For each milestone, capture only:

- Outcome: what becomes true for users or the system
- Included scope: what is intentionally part of the milestone
- Excluded scope: what is intentionally deferred
- Architecture implications: system boundaries, data, UI, integration, or subsystem consequences
- Acceptance signal: how the milestone can be recognized as complete enough

Keep milestone entries concise. Prefer 3-6 bullets per milestone over a long roadmap.

## Relationship To TODO.md

Milestones guide session planning but do not belong in `TODO.md`.

- `TODO.md` contains current and near-next executable sessions only.
- A milestone may produce one or more session entries, but only for active or near-next work.
- Do not copy the full roadmap into `TODO.md`.
- Do not use milestone labels as session IDs; keep session IDs as `S1`, `S2`, `S3`.

## Planning Flow

1. Confirm the product goal, target users, scope, non-goals, constraints, and current phase.
2. Draft `V0`, `V1`, `V1.x`, and `Final Product Direction` only as far as the user intent supports.
3. Identify architecture implications before proposing subsystem or repo changes.
4. Update `01-project-intent.md` when milestones become accepted project direction.
5. Create or update `TODO.md` only if the milestone plan turns into tracked implementation work.
