# Repository Structure

**Status:** Active standard
**Applies to:** The layout of this template repository and of every project created
from it.

## Purpose

This standard defines the baseline directory layout, what may be created without
asking, and how to treat a project that has organised itself differently.

It inherits from [`working-agreement.md`](working-agreement.md) and applies
[`change-authorisation.md`](change-authorisation.md) to structural change: adding a
missing standard directory destroys nothing, while rearranging an existing one does.

## Rules

### Rule 1 — The Baseline Layout

Projects created from this template start with the following structure:

| Path | Holds |
|---|---|
| `apps/` | Deployable applications. |
| `services/` | Long-running services. |
| `packages/` | Shared libraries consumed by apps and services. |
| `scripts/` | Operational and development scripts. |
| `tests/` | Tests not colocated with the code they cover. |
| `templates/` | Reusable file and project templates. |
| `prompts/` | Prompt material used by the project. |
| `assets/` | Static assets. |
| `docs/` | All documentation, in the subdirectories below. |
| `docs/standards/` | The standards library governing how work is performed. |
| `docs/architecture/` | System design, components, data flow, and proposals. |
| `docs/decisions/` | Architecture Decision Records. |
| `docs/api/` | Published interface documentation. |
| `docs/setup/` | Installation, environment, and configuration. |
| `docs/developer/` | Building, operating, deploying, and troubleshooting. |
| `docs/user/` | End-user behaviour and workflows. |
| `docs/changelog/` | User-visible and release-relevant changes. |
| `docs/references/` | External material the project depends on. |
| `docs/archive/` | Superseded documentation, retained. |

A project does not need to populate every directory to comply. The baseline defines
where things go when they exist, not what must exist.

### Rule 2 — Missing Standard Directories May Be Created

A directory from Rule 1 that is absent may be created without asking. It is additive
under [`change-authorisation.md`](change-authorisation.md) Rule 2 and destroys nothing.

Creating a standard directory is not permission to move existing files into it.

### Rule 3 — Project-Specific Structure Is Not Normalised

Where a project has organised itself differently from the baseline, that difference is
deliberate until the user says otherwise.

The assistant does not restructure a project to match this template, relocate files
into baseline directories, or rename existing directories to baseline names. It reports
the divergence and lets the user decide.

Consistency with the template is worth less than the working arrangement a project
already has.

### Rule 4 — New Top-Level Directories Require Approval

Adding a top-level directory that is not in Rule 1 changes the shape of the project and
is requested before it is done.

Within existing directories, the assistant creates subdirectories as the work requires,
following whatever organisation is already present.

### Rule 5 — Empty Directories Carry `.gitkeep`

Git tracks files, not directories. A directory that must exist but has no content yet
holds a `.gitkeep` file, or it will not survive a clone.

When a directory gains real content, its `.gitkeep` may be removed in the same change.
Removing it at any other time is a deletion and requires approval.

### Rule 6 — Files Live in the Directory That Owns Their Kind

A file belongs in the directory Rule 1 assigns to its kind, not wherever it was
convenient to create it.

The repository root holds only what must be there: `README.md`, `CLAUDE.md`, and
project-level configuration that tooling expects to find at the root. Working notes,
scratch files, and one-off scripts do not accumulate at the top level.

### Rule 7 — Structure Is Read, Not Assumed

Before creating, moving, or referring to a path, the assistant lists the relevant
directories and confirms what is actually there.

This template's baseline is a starting point, not a description of any particular
project. A project three months old has a structure of its own, and the only reliable
account of it is the repository.

## Required Workflow

Before making any structural change:

1. **List the affected directories** and establish the current layout.
2. **Distinguish baseline structure from project-specific structure**, and identify
   which one the change touches.
3. **Create missing standard directories** freely, with `.gitkeep` where they are empty.
4. **Request approval** for a new top-level directory, or for any move, rename, or
   restructure of what exists.
5. **Report divergence** from the baseline rather than correcting it.
6. **Verify** the resulting layout on disk and update any documentation that describes
   the structure.

## Compliance Checklist

Work performed under this standard satisfies all of the following:

- [ ] The existing layout was listed and read before anything was created or moved.
- [ ] Files were placed in the directory that owns their kind.
- [ ] Missing standard directories were created additively; empty ones carry `.gitkeep`.
- [ ] No existing directory was moved, renamed, or restructured without explicit approval.
- [ ] No new top-level directory was added without a request.
- [ ] Divergence from the baseline was reported, not normalised away.
- [ ] The resulting structure was verified on disk and documented where it is described.

Work that fails any item has changed the shape of a project without being asked to.
