# Pull Request Standards

**Status:** Active standard
**Applies to:** Every pull request an AI assistant creates or updates for this
repository or any project created from it.

## Purpose

This standard defines when a pull request may be opened, what it must contain, and what
the assistant may do with it afterwards.

A pull request is outward-facing under
[`change-authorisation.md`](../project/change-authorisation.md) Rule 6: it publishes
work, notifies people, and cannot be un-seen. Branching and pushing are owned by
[`git-workflow.md`](git-workflow.md); commit contents by
[`commit-standards.md`](commit-standards.md).

## Rules

### Rule 1 — Pull Requests Are Opened Only on Explicit Request

The assistant does not open a pull request unless asked to open one.

Being asked to make a change, commit it, or push a branch is not a request to open a
pull request. Each is a separate action requiring its own authorisation, and opening a
pull request is the point at which work becomes visible to other people.

### Rule 2 — One Pull Request, One Purpose

A pull request carries one coherent piece of work. A reviewer should be able to state
its purpose in a sentence after reading the title.

Where the branch has accumulated unrelated changes, they are separated before the pull
request is opened, or the pull request says plainly what else is in it. Unrelated
changes bundled into a review are the changes that get approved without being read.

### Rule 3 — Required Description Content

Every pull request description covers:

| Section | Contents |
|---|---|
| What | What this changes, from the outside. |
| Why | The problem it solves, and why this approach. |
| How verified | The checks that were run and their results. |
| Not covered | What was deliberately left out, and anything known to be incomplete. |

A description that only restates the diff adds nothing. The reviewer can read the diff;
what they cannot recover from it is the reasoning and the limits.

### Rule 4 — Evidence Travels With the Pull Request

The `How verified` section reports actual results under
[`verification.md`](../project/verification.md): which commands were run, what passed,
what failed, and what was not run.

Claims of verification that did not happen are worse in a pull request than anywhere
else, because a reviewer relies on them to decide how closely to look.

Known failures and pre-existing breakage are stated in the description rather than left
for the reviewer to discover.

### Rule 5 — Decisions and Documents Are Linked

Where the work implements a recorded decision, the description links the ADR by number.
Where it changes architecture, setup, or user-visible behaviour, it links the
documentation updated alongside it.

Where such documentation was not updated, the description says so and why. Silence
implies it was not needed.

### Rule 6 — Scope Creep Is Split, Not Smuggled

Problems found while working are reported, not fixed inside an unrelated pull request,
per [`change-authorisation.md`](../project/change-authorisation.md) Rule 8.

Where an incidental fix genuinely could not be separated, it is called out explicitly
in the description, with the reason it could not stand alone.

### Rule 7 — The Assistant Does Not Merge, Approve, or Close

Merging, approving, requesting changes, closing, and re-opening are decisions belonging
to the people reviewing the work.

The assistant opens the pull request, responds to feedback by pushing further commits
when asked, and stops there. It does not merge its own work, dismiss a review, or close
a pull request because it believes the work is finished or no longer needed.

### Rule 8 — Updates Are Additive and Announced

Where a pull request is updated after review has begun, changes arrive as new commits
rather than a force-pushed rewrite, so reviewers can see what changed since they last
looked.

The assistant says what it changed in response to which feedback. A silently updated
pull request forces a full re-review.

## Required Workflow

Once a pull request has been requested:

1. **Confirm the request** names opening a pull request, not merely committing or
   pushing.
2. **Review the branch contents** — every commit that will be included — and separate
   unrelated work.
3. **Run the project's checks** and capture the actual results.
4. **Confirm documentation** required by
   [`documentation-lifecycle.md`](../documentation/documentation-lifecycle.md) is
   included, or state its absence.
5. **Write the description** covering what, why, how verified, and not covered.
6. **Open the pull request**, then report its URL and contents.
7. **Stop.** Do not merge, approve, or close.

## Compliance Checklist

A pull request produced under this standard satisfies all of the following:

- [ ] It was opened only after an explicit request to open one.
- [ ] It carries one coherent piece of work, with any exceptions stated.
- [ ] Its description covers what, why, how verified, and what is not covered.
- [ ] Its verification claims reflect checks actually run, including failures.
- [ ] Related ADRs and updated documentation are linked; omissions are explained.
- [ ] Incidental fixes are either split out or explicitly called out.
- [ ] The assistant did not merge, approve, close, or re-open it.
- [ ] Post-review updates are additive commits, with the changes announced.

A pull request that fails any item asks a reviewer to trust what it has not shown.
