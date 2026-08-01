# Documentation Lifecycle

**Status:** Active standard
**Applies to:** Every change made by an AI assistant in this repository or any project
created from it that affects what the documentation describes.

## Purpose

This standard governs *when* documentation must be written or updated, and *which*
document receives which kind of knowledge.

The form documentation takes is owned by
[`documentation-standards.md`](documentation-standards.md). This standard supplies the
mechanics that [`working-agreement.md`](../project/working-agreement.md) Rule 8 states
as a principle: knowledge belongs in the repository.

## Rules

### Rule 1 — Documentation Changes With the Work

Documentation updates are part of the change that made them necessary, not a follow-up
task. They are written before the work is reported complete and, where the work is
committed, in the same commit.

A structural change with stale documentation is incomplete work, not finished work
with an outstanding chore. Deferred documentation is documentation that does not get
written.

### Rule 2 — The Change Determines the Document

Each kind of change has a location that owns it:

| Location | Updated when |
|---|---|
| `README.md` | The project's purpose, structure, or setup changed. |
| `CLAUDE.md` | The working rules or conventions for the repository changed. |
| `docs/standards/` | A rule governing how work is performed changed. |
| `docs/architecture/` | System design, components, boundaries, or data flow changed. |
| `docs/decisions/` | A significant technical decision was made. |
| `docs/api/` | A published interface changed. |
| `docs/setup/` | Installation, environment, or configuration steps changed. |
| `docs/developer/` | How to build, operate, deploy, or troubleshoot the project changed. |
| `docs/user/` | End-user behaviour or workflows changed. |
| `docs/changelog/` | A user-visible or release-relevant change was made. |
| `docs/references/` | External material the project depends on was added or changed. |

Where a change touches several of these, each is updated. Where it appears to touch
none, that is worth a second look before concluding the change needs no documentation.

### Rule 3 — Dependent Documents Are Found Before They Go Stale

Before making a change, the assistant identifies what documents describe the thing
being changed, and updates them as part of the same work.

That means searching the repository for references to the renamed function, the moved
directory, the removed option — not relying on memory of where they are mentioned.
A document that is wrong is worse than a document that is missing, because it is
trusted.

### Rule 4 — Documents Are Superseded or Archived, Never Silently Deleted

Documentation that no longer applies is either updated in place, or moved to
`docs/archive/` with a note saying what replaced it and when.

Deleting a document is destructive under
[`change-authorisation.md`](../project/change-authorisation.md) Rule 1 and requires
explicit approval. Obsolete documentation still records what the project once did,
which is frequently the only surviving explanation of why it does what it does now.

### Rule 5 — `README.md` Is the Entry Point

Every repository has a `README.md`, and it states what the project is, how to set it
up, how to run it, and where the rest of the documentation lives.

It is the first document read and the first to go stale. Any change to structure,
setup, or purpose reaches it in the same piece of work.

### Rule 6 — Indexes Are Updated With Their Contents

Where a directory has an index — a `README.md` listing what it contains — adding to
that directory includes adding to the index.

An index that omits half its directory is worse than no index, because a reader stops
looking once they have read it.

### Rule 7 — Knowledge Is Recorded Where It Is Explained

If the assistant explains something substantial in conversation — how a component
works, why an approach was taken, how to run something, what a failure meant — and it
is not already written down, writing it down is part of the task.

The explanation is placed in the location Rule 2 identifies, not appended wherever is
convenient. Conversation is not a record: it is not searchable by the next person and
does not survive the session.

### Rule 8 — Documents State What Is True Now

Documentation describes the current state of the project in the present tense. Planned
work, proposals, and intentions are labelled as such, in documents that say so.

An aspiration written in the present tense becomes a false statement the moment
someone relies on it.

## Required Workflow

For any change that affects what the documentation describes:

1. **Identify affected documents** before making the change — search the repository for
   references to what is being changed.
2. **Make the change.**
3. **Update every affected document** in the same piece of work, using the mapping in
   Rule 2.
4. **Update indexes** for any directory whose contents changed.
5. **Archive rather than delete** anything superseded, and request approval first.
6. **Record anything substantial that was explained** but not yet written down.
7. **Verify** that every updated document is accurate and that its links resolve.

## Compliance Checklist

Work performed under this standard satisfies all of the following:

- [ ] Documentation was updated as part of the change, not deferred.
- [ ] Every location the change touched, per Rule 2, was updated.
- [ ] The repository was searched for dependent documents rather than relying on memory.
- [ ] No document was deleted without explicit approval; superseded material was archived.
- [ ] `README.md` reflects the current structure, setup, and purpose.
- [ ] Directory indexes list everything their directories now contain.
- [ ] Substantial explanations given in conversation were written to the repository.
- [ ] Every updated document describes the present state, with future work labelled as such.

Work that fails any item leaves the repository describing a project that no longer
exists.
