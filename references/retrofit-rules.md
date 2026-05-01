# Retrofit Rules

Use these rules when `$WF` is asked to adopt or restore the workflow in an existing repository, especially via `$wf retrofit`.

## Goal

Bring an existing repository into the standard WF structure without treating it like a brand-new project and without overwriting useful existing material.

## First Pass Inspection

- Inspect the repo shape, entrypoints, and key folders first.
- Read the project README and any existing project docs that explain intent or structure.
- Inspect `TODO.md`, `LOG.md`, and `ARCHITECTURE/` if they already exist.
- Determine what already exists, what is missing, and what is nonstandard.

## Preservation Rules

- Preserve useful user content by default.
- Do not overwrite existing files unless the user clearly wants normalization or replacement.
- Prefer migrating or reshaping existing tracking and docs over deleting and recreating them.
- If old structure is unclear or mixed-quality, preserve it conservatively and summarize the tradeoffs.

## Standard WF Structure

Ensure these exist when needed:

- `TODO.md`
- `LOG.md`
- the standard `ARCHITECTURE/` skeleton from `references/architecture-structure.md`

Create the four standard current architecture docs when reconstructing architecture. Mark `03-overall-ui-design.md` as `N/A` with a short reason for backend-only, CLI-only, or library projects. Create `ARCHITECTURE/decisions/` only when recording actual ADRs.

## TODO Migration Rules

- Convert active work into the standard session-based structure.
- Use one date heading with session sections such as `S1`, `S2`, `S3`.
- Keep only the current and near-next sessions in `TODO.md`.
- Do not copy a long stale backlog into the new `TODO.md`.
- If an old `TODO.md` contains mixed backlog and active work, preserve the useful active items and summarize any dropped backlog in the handoff.

## LOG Migration Rules

- Preserve useful history.
- Normalize only enough to make future entries consistent.
- Do not rewrite a large historical log unless the user asks for a full cleanup.
- New entries should follow the same date and session IDs used in `TODO.md`.

## Architecture Recovery Rules

- Use `references/architecture-structure.md` as the folder and file contract.
- Create or normalize the top-level current docs first.
- Create subsystem docs only for clearly justified bounded areas.
- Prefer a thin but correct first-pass architecture set over speculative detail.
- Use actual code and project docs as the source of truth when reconstructing missing architecture.

## Completion Criteria

A successful retrofit should leave the repo with:

- standard WF tracking files or clearly normalized equivalents
- a usable current architecture skeleton
- a clean session-based `TODO.md`
- a `LOG.md` structure that can record future sessions consistently
- a brief summary of what was created, what was preserved, and what still needs follow-up
