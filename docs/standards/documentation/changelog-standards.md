# Changelog Standards

**Status:** Active standard
**Applies to:** Every user-visible change made in this repository or any project
created from it.

## Purpose

This standard defines what belongs in the changelog, how entries are written, and when
they are added.

When a changelog entry is required is a lifecycle question owned by
[`documentation-lifecycle.md`](documentation-lifecycle.md) Rule 2; this standard
defines the artifact. Form follows
[`documentation-standards.md`](documentation-standards.md).

## Rules

### Rule 1 — The Changelog Records User-Visible Change

An entry is written for anything that changes what a user of the project experiences:
new capability, altered behaviour, fixed defect, removed feature, changed interface,
or a security issue addressed.

Refactoring, internal renaming, test additions, formatting, and dependency updates with
no observable effect do not get entries. The changelog is read by people deciding
whether to upgrade and what will break when they do — internal churn is noise to them.

"User" includes developers consuming a library or API. A breaking change to an
interface is user-visible even where no end user sees it.

### Rule 2 — Location and File

The changelog lives in `docs/changelog/`. A project maintains a single
`CHANGELOG.md` there unless its release process requires per-release files, in which
case the existing arrangement is followed.

The assistant reads what is already there before adding to it, and matches its format
even where that format differs from the default below.

### Rule 3 — Entries Are Grouped by Kind

Within each release, entries are grouped under these headings, in this order, omitting
any that are empty:

| Heading | Contents |
|---|---|
| `Added` | New capabilities. |
| `Changed` | Altered behaviour of existing capabilities. |
| `Deprecated` | Capabilities still present but scheduled for removal. |
| `Removed` | Capabilities no longer present. |
| `Fixed` | Defects corrected. |
| `Security` | Vulnerabilities addressed. |

### Rule 4 — Release Sections Are Ordered and Dated

Releases appear newest first. Each carries its version and release date:

```markdown
## [Unreleased]

### Added

- Export queue retries failed uploads up to three times.

## [1.4.0] — 2026-03-14

### Fixed

- Pagination no longer skips the final record on exact page boundaries.
```

Unreleased work accumulates under `[Unreleased]` and moves into a version section when
that version is released.

### Rule 5 — Entries Are Written for the Reader, Not the Author

Each entry states what changed from the outside, in one sentence, in the present tense,
without requiring knowledge of the codebase.

"Pagination no longer skips the final record on exact page boundaries" is an entry.
"Fixed off-by-one in `PageCursor.advance()`" is a commit subject. Function names,
file paths, and internal component names do not appear unless they are part of the
public interface.

Breaking changes say so explicitly, and say what the reader must do about it.

### Rule 6 — Entries Are Added With the Change

A changelog entry is written in the same piece of work as the change it describes, not
assembled from commit history at release time.

Reconstructing a changelog after the fact produces entries written by someone who has
forgotten why the change mattered, and silently drops everything nobody remembers.

### Rule 7 — Released Entries Are Not Rewritten

Once a version has been released, its section is a historical record and is not edited.

A mistake in a released entry is corrected by a note in the current unreleased section,
not by rewriting what was published. Readers compare changelogs across versions, and a
section that changes after release makes those comparisons unreliable.

Corrections to unreleased entries are unrestricted — they have not been published yet.

## Required Workflow

For any change that affects what a user experiences:

1. **Determine whether the change is user-visible.** Internal-only work gets no entry.
2. **Read the existing changelog** and match its format, headings, and version scheme.
3. **Write the entry** under the correct heading in `[Unreleased]`, in one sentence,
   from the reader's point of view.
4. **Mark breaking changes explicitly**, with what the reader must do.
5. **Leave released sections untouched.**
6. **Verify** the file on disk and that the entry sits under the right heading.

## Compliance Checklist

Work performed under this standard satisfies all of the following:

- [ ] Every user-visible change has an entry; internal-only work has none.
- [ ] The entry is in `docs/changelog/`, matching the project's existing format.
- [ ] It sits under the correct heading, in a correctly ordered and dated release section.
- [ ] Unreleased work is under `[Unreleased]`.
- [ ] The entry reads from the outside, without internal names or paths.
- [ ] Breaking changes are marked, with the required reader action stated.
- [ ] The entry was written with the change, not reconstructed later.
- [ ] No released section was edited.

Work that fails any item leaves users unable to tell what changed beneath them.
