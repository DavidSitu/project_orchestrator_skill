# Milestone Planning

Use this reference when `$wf arche` needs lightweight roadmap or milestone planning.

Milestones are product and architecture direction. They are not execution sessions, TODO entries, ADRs, or business/promotion plans.

## When To Use

Use milestone planning when:

- product direction is unclear during `$wf arche`
- the user asks for V1, V2+, roadmap, milestones, phases, or final-product direction
- architecture choices depend on the intended product phase
- a large request needs a roadmap before it can be split into sessions

Do not use milestone planning for every small architecture edit.

## Storage Location

Store compact milestone summaries in `ARCHITECTURE/current/02-milestones.md`.

Keep `ARCHITECTURE/current/01-project-intent.md` limited to stable project target: goals, target users, scope, non-goals, constraints, current phase, and success direction.

Do not create a separate `ARCHITECTURE/current/05-roadmap.md`. Do not create `PRODUCT/`, business logic, promotion, go-to-market, or GTM docs as part of milestone planning.

## Milestone Format

Use the fewest milestone labels needed to make the roadmap clear. The default ladder is:

`V0 -> V1 -> optional V1.x -> optional V2/V3/V4+ -> Final Product Direction`

- `V0`: the smallest useful proving version or internal prototype
- `V1`: the first coherent user-facing product version
- `V1.x`: near-term post-V1 improvements that should not block V1
- `V2`, `V3`, `V4+`: larger product generations added only when each version represents a meaningful capability jump toward the final goal
- `Final Product Direction`: the long-term north star, not a committed backlog

Do not force `V2+`. Add major versions only when the final goal is too complex for `V1` plus `V1.x`. Use `V1.x` for incremental improvements and `V2+` for distinct product generations.

For each milestone, capture only:

- Outcome: what becomes true for users or the system
- Included scope: what is intentionally part of the milestone
- Excluded scope: what is intentionally deferred
- Architecture implications: system boundaries, data, UI, integration, or subsystem consequences
- Acceptance signal: how the milestone can be recognized as complete enough

Keep milestone entries concise. Prefer 3-6 bullets per milestone over a long roadmap. If `V2+` exists, each major version should have a distinct outcome and acceptance signal.

`02-milestones.md` may be very short for small projects. Do not fill it with speculative versions just because the file exists.

## Relationship To TODO.md

Milestones guide session planning but do not belong in `TODO.md`.

- `TODO.md` contains current and near-next executable sessions only.
- A milestone may produce one or more session entries, but only for active or near-next work.
- Do not copy the full roadmap into `TODO.md`.
- Do not use milestone labels as session IDs; keep session IDs as `S1`, `S2`, `S3`.
- A milestone is not complete because the milestone doc exists. It is complete only when all derived implementation sessions are finished, verified, and recorded in `LOG.md`.

Use this mapping:

```text
Milestone = product capability direction
TODO session = one testable slice of that capability
Test = proof the session works
LOG = completion record for the verified session
```

## Planning Flow

1. Confirm the product goal, target users, scope, non-goals, constraints, and current phase.
2. Draft `V0`, `V1`, optional `V1.x`, optional `V2+`, and `Final Product Direction` only as far as the user intent supports.
3. Use `V2+` only for major capability jumps; otherwise keep the roadmap to `V0`, `V1`, optional `V1.x`, and `Final Product Direction`.
4. Identify architecture implications before proposing subsystem or repo changes.
5. Update `02-milestones.md` when milestones become accepted project direction.
6. Create or update `TODO.md` only if the milestone plan turns into tracked implementation work.
7. Mark milestone progress based on completed, verified, logged sessions rather than on documentation being written.

## Existing Repo Migration

- If accepted milestone content already exists in `01-project-intent.md`, move it to `02-milestones.md` during retrofit or normalization.
- Keep stable project target content in `01-project-intent.md`.
- Do not move stale roadmap ideas into `02-milestones.md`; preserve or archive them only when they remain useful historical context.
- Do not renumber existing architecture files unless the user asked for retrofit or normalization and the links can be updated cleanly.
