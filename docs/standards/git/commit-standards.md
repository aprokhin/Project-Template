# Commit Standards

**Status:** Active standard
**Applies to:** Every commit an AI assistant creates in this repository or any project
created from it.

## Purpose

This standard governs what a commit contains and what its message says. It applies
once a commit has been requested — whether the assistant may commit at all is owned by
[`git-workflow.md`](git-workflow.md) Rule 2.

A commit is the unit at which work is reviewed, reverted, and understood years later.
Its contents and its message are the whole of what survives.

## Rules

### Rule 1 — One Logical Change Per Commit

A commit contains one change, complete. Everything in it belongs to that change, and
nothing belonging to that change is left out.

A commit that both fixes a bug and reformats a file cannot be reverted without losing
one of them, and cannot be reviewed without separating them by hand. Where the work
produced several logical changes, it produces several commits.

### Rule 2 — Subject Lines Are Imperative and Specific

The subject line completes the sentence "Applying this commit will…". It is written in
the imperative mood, under 72 characters, capitalised, with no trailing full stop.

```text
Add retry handling to the export queue
Fix off-by-one in pagination offset
Remove unused migration helpers
```

Not `Added retry handling`, not `bugfix`, not `update code`. A subject line that does
not identify what changed forces every future reader to open the diff.

Where the project's existing history uses a convention — a type prefix, a ticket
reference — that convention is followed. The repository's own history takes precedence
over any default in this standard.

### Rule 3 — The Body Explains Why

Where the reason is not obvious from the subject, the message includes a body: a blank
line, then prose explaining what problem this solves and why it was solved this way.

The diff already records what changed. The body records what the diff cannot: the
constraint, the alternative rejected, the bug's actual cause. Wrapped at 72 characters.

Where a decision was recorded as an ADR, the body references it by number rather than
restating it.

### Rule 4 — Only Intended Files Are Staged

Files are staged by name. Blanket staging — `git add -A`, `git add .` — sweeps in
untracked files, editor state, build output, and local configuration that nobody
intended to commit.

Before committing, the assistant reviews what is staged and confirms every path in it
belongs to the change being made.

### Rule 5 — Nothing Secret, Generated, or Incidental Is Committed

A commit contains no credentials, no build output, no dependency directories, no local
tool state, and no unrelated files that happened to be dirty.

Secret material is governed by
[`secrets-management.md`](../security/secrets-management.md), and its Rule 1 applies
to commit messages as well as to files. Generated artifacts belong in `.gitignore`, and
the assistant adds them there rather than committing them once and removing them later.

### Rule 6 — Commit Messages Are Honest

A commit message describes what the commit does, not what the author hoped it would do.

It does not claim that tests pass unless they were run and passed. It does not describe
a change as complete when part of it was deferred. A message that overstates the work
is a false record in the one place that cannot easily be corrected.

### Rule 7 — Authorship Is Attributed

Where the assistant authored the change, the commit carries the trailer the project
uses for AI attribution, after a blank line at the end of the message.

Attribution is not decoration: it tells a future reader how the change was produced,
which is information they need when auditing it.

### Rule 8 — Published Commits Are Not Amended

Once a commit has been pushed, it is corrected by a new commit, never by amending or
rebasing.

Amending a published commit rewrites history that others may have, and is destructive
under [`git-workflow.md`](git-workflow.md) Rule 4. A follow-up commit is honest about
the sequence of events, which is what the history is for.

## Required Workflow

Once a commit has been requested:

1. **Review the working tree.** Run `git status` and `git diff` to establish what
   actually changed.
2. **Group the changes** into logical units. If there is more than one, make more than
   one commit.
3. **Stage by name**, then re-check what is staged.
4. **Scan the staged content** for secrets, generated files, and unrelated changes.
5. **Write the message**: imperative subject, body explaining why, attribution trailer.
6. **Commit non-interactively**, with the message supplied on the command line or via a
   file.
7. **Run `git status`** and report the resulting state, including what was not
   committed and what was not pushed.

## Compliance Checklist

Every commit produced under this standard satisfies all of the following:

- [ ] It contains exactly one logical change, complete.
- [ ] Its subject is imperative, specific, under 72 characters, with no trailing full stop.
- [ ] It follows the repository's existing message convention where one exists.
- [ ] Its body explains why, where the reason is not self-evident.
- [ ] Every staged path was staged deliberately and belongs to this change.
- [ ] It contains no secrets, generated output, or incidental files.
- [ ] Its message claims nothing that was not verified.
- [ ] It carries the project's attribution trailer.
- [ ] No published commit was amended or rebased.

A commit that fails any item misrepresents the work it records.
