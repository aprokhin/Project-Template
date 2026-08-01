# Git Workflow

**Status:** Active standard
**Applies to:** Every Git operation an AI assistant performs in this repository or any
project created from it.

## Purpose

This standard governs the operations that change repository state: initialising,
branching, staging, committing, pushing, and anything that alters history or remotes.

It is the Git-specific application of
[`change-authorisation.md`](../project/change-authorisation.md). Message content and
commit composition are owned by [`commit-standards.md`](commit-standards.md); pull
requests are owned by [`pull-request-standards.md`](pull-request-standards.md).

## Rules

### Rule 1 — Git Is Initialised Only on Request

The assistant does not run `git init` in a directory that is not already a repository,
except when creating a new project from this template or when the user asks.

Initialising a repository in an unexpected place — a parent directory, a home
directory, a directory already inside another repository — creates problems that are
tedious to unpick. The assistant confirms where it is before initialising.

New repositories are created with `main` as the initial branch:

```bash
git init -b main
```

### Rule 2 — Repository State Changes Only on Explicit Request

Staging, committing, pushing, tagging, and changing remotes are separate actions, each
requiring its own explicit request.

Making a change is not authorisation to commit it. Committing is not authorisation to
push. Being asked to "fix the bug" is a request to change files, not a request to
record or publish that change.

The assistant makes the change, reports it, and stops. If the user wants it committed,
they will say so.

### Rule 3 — Work Is Not Committed Directly to the Default Branch

Where a commit has been requested and the repository is on `main`, the assistant
creates a branch first and says that it did.

The branch is named for the work it carries, in kebab-case, with a conventional prefix
where the project already uses one. Existing branch naming in the repository takes
precedence over any default.

### Rule 4 — History Is Not Rewritten

Amending, rebasing, resetting, squashing, and force-pushing rewrite history and are
destructive under
[`change-authorisation.md`](../project/change-authorisation.md) Rule 1. Each requires
explicit approval for that specific operation.

On a branch that has been pushed or shared, rewriting is refused rather than approved
casually — it breaks every clone that has the old history. The assistant states this
rather than performing it and mentioning the consequence afterwards.

Prefer a new commit over amending an existing one.

### Rule 5 — Uncommitted Work Is Never Discarded

`git reset --hard`, `git checkout --`, `git restore`, `git clean`, and stash drops
destroy work that exists nowhere else. None is run without explicit approval naming
that operation.

Before any such command, the assistant reports what would be lost. Uncommitted changes
have no undo, and the user may not know they are there.

### Rule 6 — Hooks and Signing Are Not Bypassed

`--no-verify`, `--no-gpg-sign`, and equivalent flags are not used unless the user asks
for them explicitly.

A failing hook is a signal, not an obstacle. The assistant reports what the hook
rejected and why, and fixes the underlying problem. Bypassing a project's own checks
to get a commit through defeats the reason the project installed them.

### Rule 7 — Remotes Are Not Added, Changed, or Removed

Remote configuration determines where the repository's contents can travel. The
assistant does not add, rename, retarget, or delete a remote without an explicit
request naming the change.

Pushing to a remote is outward-facing under
[`change-authorisation.md`](../project/change-authorisation.md) Rule 6: once content
has left, it cannot be recalled.

### Rule 8 — Interactive Commands Are Not Used

Commands that open an editor or expect terminal input — `git rebase -i`, `git add -i`,
`git commit` without a message — cannot be completed in this environment and leave the
session blocked.

Every Git command is run in a non-interactive form, with messages supplied on the
command line or via a file.

### Rule 9 — Git Work Ends With `git status`

After any operation that changes repository state, the assistant runs `git status` and
shows the result.

The resulting state is then visible rather than assumed: what is staged, what is
modified, what is untracked, and which branch the work is on. This is the evidence
required by [`verification.md`](../project/verification.md) for Git operations.

## Required Workflow

For any Git operation:

1. **Establish the current state.** Run `git status` and check the branch before acting.
2. **Confirm the request covers this operation.** Staging, committing, and pushing are
   authorised separately.
3. **Branch first** if a commit was requested and the repository is on `main`.
4. **Check for destructive effect.** History rewriting and work discarding require
   approval naming the operation; report what would be lost before asking.
5. **Run the operation non-interactively.**
6. **Run `git status`** and show it.
7. **Report** the branch, what changed, and what was not done.

## Compliance Checklist

Work performed under this standard satisfies all of the following:

- [ ] No repository was initialised without a request, and any new one uses `main`.
- [ ] Nothing was staged, committed, pushed, or tagged without an explicit request for that action.
- [ ] No commit was made directly to `main` without the user asking for exactly that.
- [ ] No history was rewritten and no uncommitted work was discarded without specific approval.
- [ ] No hook or signing requirement was bypassed.
- [ ] No remote was added, changed, or removed without an explicit request.
- [ ] No interactive Git command was run.
- [ ] `git status` was run and shown after the work.

Work that fails any item has changed repository state without authority.
