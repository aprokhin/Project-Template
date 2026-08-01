# ADR Format

**Status:** Active standard
**Applies to:** Every Architecture Decision Record written in this repository or any
project created from it.

## Purpose

This standard defines the ADR as an artifact: where it lives, how it is named and
numbered, what it must contain, and how its status changes over time.

It supplies the mechanics that
[`architecture-decisions.md`](architecture-decisions.md) relies on. That standard
governs *whether* a decision may be recorded and *whose* decision it is; this one
governs what the resulting file looks like.

## Rules

### Rule 1 — One Decision Per Record

An ADR records exactly one decision. A record covering several decisions cannot be
superseded, cited, or reversed independently, which defeats the purpose of keeping it.

Where a single conversation produced several decisions, it produces several ADRs.
Related records reference each other rather than merging.

### Rule 2 — Location, Naming, and Numbering

ADRs live in `docs/decisions/` and nowhere else.

Each file is named `NNNN-short-title.md`, where `NNNN` is a four-digit zero-padded
sequence number and the title is kebab-case — for example,
`docs/decisions/0007-postgres-for-primary-storage.md`.

Numbers are assigned at creation, one higher than the highest existing number in the
directory. Numbers are never reused, never renumbered, and never reordered, including
when a record is superseded or deprecated. The number is the record's permanent
identifier.

### Rule 3 — Required Structure

Every ADR uses this structure:

```markdown
# NNNN. Decision Title

**Status:** Accepted
**Date:** YYYY-MM-DD
**Decided by:** The user

## Context

The situation that forced a decision: constraints, requirements, and what made the
existing state insufficient. Written so that a reader who was not present understands
why this came up.

## Decision

What was decided, stated in one or two sentences, in the active voice.

## Alternatives Considered

Each option that was genuinely weighed, and why it was not chosen.

## Consequences

What follows from this decision — what becomes possible, what becomes harder, what is
now committed to, and what will need revisiting.
```

Sections are not omitted. An ADR with no alternatives recorded asserts that no
alternatives existed, which is almost never true and cannot be checked later.

### Rule 4 — Status Values Are Fixed

The `Status` field holds exactly one of:

| Status | Meaning |
|---|---|
| `Accepted` | The decision is in force. |
| `Superseded by NNNN` | A later decision replaced this one. |
| `Deprecated` | The decision no longer applies and nothing replaced it. |

There is no `Proposed` status. An ADR records a decision that has already been made,
so a proposed ADR is a contradiction — proposals are handled under Rule 8.

### Rule 5 — Consequences Include the Costs

The Consequences section records what the decision costs, not only what it buys.

A record listing only benefits is a sales document. Its value in two years is that it
tells a reader what was knowingly traded away, so that a later reversal is made with
the same information the original decision had.

### Rule 6 — Alternatives Are Recorded Honestly

Alternatives are the options that were actually considered, described accurately
enough that a reader could evaluate them independently.

Straw men — options listed only to be dismissed — make the record worse than no record,
because they misrepresent the decision as more obvious than it was.

### Rule 7 — Records Are Immutable Except for Status

Once written, an ADR's Context, Decision, Alternatives, and Consequences are not
edited to reflect later understanding. The record states what was decided, when, on
what basis.

Two changes are permitted: correcting a factual error about what was decided, and
updating the `Status` field. Everything else that has changed is a new decision, and a
new decision is a new record.

Superseded records are never deleted. Deleting the losing half of a decision history
destroys the only thing the history was for.

### Rule 8 — Proposals Live Outside `docs/decisions/`

A document evaluating options the user has not yet chosen is a proposal, not an ADR.
Proposals live in `docs/architecture/`, with `Proposal` in the title and status, and
they never occupy an ADR number.

When the user decides, the proposal's analysis becomes the Context and Alternatives of
a new ADR. The proposal itself may then be archived or left in place, but it is not
promoted by renaming.

### Rule 9 — Superseding Is Linked in Both Directions

When a new ADR replaces an older one:

- the new record's Context states which record it replaces and why;
- the old record's Status becomes `Superseded by NNNN`, naming the new number.

A one-way link leaves a reader who arrives at the old record believing it is current.

## Required Workflow

Before writing an ADR:

1. **Confirm the decision was made by the user.** If it was not, this is a proposal —
   apply Rule 8 instead.
2. **Read `docs/decisions/`** to establish the highest existing number and to check
   whether an existing record already covers this decision.
3. **Assign the next number.** Never reuse or renumber.
4. **Write the record** using the structure in Rule 3, with every section filled.
5. **Link supersessions in both directions** where this record replaces another.
6. **Verify** that the file exists at the expected path and that any referenced record
   numbers resolve to real files.

## Compliance Checklist

An ADR produced under this standard satisfies all of the following:

- [ ] It records exactly one decision, already made by the user.
- [ ] It lives in `docs/decisions/` and is named `NNNN-short-title.md`.
- [ ] Its number is one higher than the previous highest, and is not reused.
- [ ] It contains Status, Date, Decided by, Context, Decision, Alternatives Considered, and Consequences.
- [ ] Its status is `Accepted`, `Superseded by NNNN`, or `Deprecated` — never `Proposed`.
- [ ] Consequences state the costs, not only the benefits.
- [ ] Alternatives are real options, described fairly.
- [ ] No prior record was edited beyond its status, and none was deleted.
- [ ] Any supersession is linked from both records.

An ADR that fails any item is incomplete, however finished it looks.
