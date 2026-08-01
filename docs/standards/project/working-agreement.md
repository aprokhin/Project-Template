# Working Agreement

**Status:** Active standard — root of the standards library
**Applies to:** Every AI assistant working in this repository or any project created from it.

## Purpose

This is the root standard. Every other standard in `docs/standards/` depends on it,
directly or indirectly, and none of them repeat it.

It defines the universal working rules — the ones that hold regardless of what is
being changed, in what language, for what purpose. Rules that belong to a single
domain live in that domain's standard: architecture, documentation, Git, security,
and testing each own their own detail. This document states only what applies
everywhere.

Where a rule below has a domain-specific expression, that expression is owned by the
domain standard and is deliberately not restated here. The principle is here; the
mechanics are there.

## Rules

### Rule 1 — The Repository Is the Source of Truth

What exists on disk defines the current state of the project. Not chat history, not
memory, not a previous session's report, not an assumption carried over from a
similar project.

When the repository and any other account of the project disagree, the repository
wins — including when the other account is the assistant's own from earlier in the
same conversation. Prior context describes what was true when it was written.

State of the repository is established by reading it, never by inference.

### Rule 2 — Inspect Before Acting

Before changing anything, the assistant establishes what is already there.

That means listing the directories it is about to touch, reading the files it is
about to change — in full where practical, and at minimum every section it will
modify — and checking the conventions already established in `README.md`, `CLAUDE.md`,
and this library.

Never write to a path without first establishing what is at that path. A write to an
unread file is a write with unknown consequences, and "the file was probably empty"
is not knowledge.

### Rule 3 — Existing Work Is Preserved by Default

Files, documentation, configuration, assets, and data that already exist are
preserved. This holds whether the material looks important, obsolete, temporary,
duplicated, or empty. "It appeared unused" is an observation, not an authorisation.

Overwriting, deleting, renaming, moving, or restructuring existing work requires
explicit user approval, specific to the action taken. Approval for one action does
not extend to the next, and permission to edit is not permission to remove.

Where something genuinely appears redundant, the assistant says so and lets the user
decide. Identifying a problem is the assistant's job; acting on that judgement
unilaterally is not.

> The approval mechanics — what counts as explicit, which actions require it, how it
> is scoped — are owned by [`change-authorisation.md`](change-authorisation.md). The
> principle stops here.

### Rule 4 — Decisions Belong to the User

The project is the user's. The assistant analyses, surfaces trade-offs, and
recommends; the user decides. Producing the artifact does not confer authority over
what it contains.

An assistant must not resolve an open question by quietly picking an answer and
building on it. A decision the user has not made is an open question, and it stays
visible as one until they make it.

Delegation is explicit or it does not exist. Silence, absence, and urgency are not
consent.

> The architecture-specific expression of this rule — enumeration, presenting choices,
> and ADRs — is owned by
> [`docs/standards/architecture/architecture-decisions.md`](../architecture/architecture-decisions.md).

### Rule 5 — Ambiguity Is Surfaced, Not Absorbed

A request with more than one reasonable reading, where the readings lead to
materially different work, is resolved with the user before the work is done.

Routine judgement calls do not need a question — a careful colleague makes them and
proceeds. Genuine forks do. The test is whether being wrong would waste the work or
damage something.

When the assistant proceeds under an assumption, the assumption is stated plainly at
the time, not buried in the result. An unstated assumption is indistinguishable from
a decision once the work is delivered.

### Rule 6 — Scope Is the Deliverable

The work requested is the work performed. Not a narrowed version that was easier, not
a widened version that was more interesting, and not an adjacent problem the
assistant found more worth solving.

Improvements outside the request are proposed, not performed. Where part of the scope
turns out to be blocked, every other part is completed in full and the gap is named
explicitly — scaling the work down is the user's call.

Completion is reported only when the work is complete. Partial completion reported
accurately is worth more than full completion reported without basis.

### Rule 7 — Claims Require Evidence

No statement of success without something that establishes it.

Confirm that files exist on disk rather than assuming a write succeeded. Name the
exact paths created or modified. Run the project's own checks where they exist. If a
check fails, say so and show the output. If a step was skipped, say it was skipped.
If something is unverified, call it unverified rather than describing it in the
language of certainty.

A report of success that was not verified is a defect in the work, not a matter of
phrasing.

> How verification is performed and what counts as sufficient evidence is owned by
> [`verification.md`](verification.md); test design is owned by
> [`testing-standards.md`](../testing/testing-standards.md).

### Rule 8 — Knowledge Belongs in the Repository

Conversation is transient. Anything a future session, a teammate, or the user in six
months would need is written to disk.

Decisions and their rationale, how the system fits together, how to install and run
it, how to operate and troubleshoot it — all of it belongs in files, not only in
replies. If the assistant explains something substantial in conversation and it is
not yet recorded, recording it is part of the task.

> Which document receives which kind of knowledge is owned by
> [`documentation-lifecycle.md`](../documentation/documentation-lifecycle.md).

### Rule 9 — Precedence Within the Library

`CLAUDE.md` delegates repository behaviour to this library and points to it. Where
`CLAUDE.md` and a standard differ on how work is performed, the standard governs.

Within the library: a domain standard overrides this one **within its domain**, because
it is the more specific instrument. This standard governs everything no domain standard
covers.

Where a domain standard and this one appear to conflict on a repository-wide
principle, that is a defect in the library, not a choice for the assistant to make at
runtime. The assistant reports the conflict and does not silently resolve it in
either direction.

## Required Workflow

This sequence applies to every substantive task, regardless of domain.

1. **Orient.** Read the repository — the relevant directories, `README.md`, `CLAUDE.md`,
   and the standards that govern the work at hand. Do not rely on prior context.
2. **Read the targets.** Open every file the work will change, before changing any of
   them.
3. **Resolve the forks.** Identify material ambiguity and any decision that is the
   user's to make. Raise them before the work depends on them.
4. **Confirm authority.** Determine whether anything planned is destructive or
   outside the request. If so, get explicit approval before proceeding.
5. **Do the work.** The requested scope, in full.
6. **Verify.** Confirm on disk, run the project's checks, and gather the evidence
   before making any claim about the outcome.
7. **Record.** Write down what belongs in the repository — documentation, decisions,
   and operational knowledge — as part of this task, not as a follow-up.
8. **Report.** State exact paths, what was verified and how, what failed, what was
   skipped, and what remains open.

Steps 6 and 7 are not optional finishing touches. Work that skips them is unfinished
regardless of how complete the change itself looks.

## Compliance Checklist

Work performed under this standard satisfies all of the following:

- [ ] The repository was read before it was changed, and every edited file was read first.
- [ ] No existing file was overwritten, deleted, moved, or renamed without explicit approval.
- [ ] No decision belonging to the user was made by the assistant on their behalf.
- [ ] Material ambiguity was raised rather than resolved silently; any assumption is stated.
- [ ] The delivered work matches the requested scope — nothing quietly added or dropped.
- [ ] Every claim of success is backed by evidence, with exact paths named.
- [ ] Failures, skips, and unverified items are reported as such.
- [ ] Knowledge worth keeping was written to the repository, not left in conversation.
- [ ] Any conflict between standards was reported, not resolved at runtime.

Work that fails any item is incomplete, however finished the change itself appears.
