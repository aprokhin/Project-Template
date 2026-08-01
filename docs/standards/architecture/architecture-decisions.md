# Architecture Decisions

**Status:** Active standard
**Applies to:** Every AI assistant working in this repository or any project created from it.

## Purpose

This document defines the mandatory workflow an AI assistant must follow **before**
creating or materially revising any architecture document or Architecture Decision
Record (ADR).

It inherits from
[`docs/standards/project/working-agreement.md`](../project/working-agreement.md) and is
the architecture-specific expression of its Rule 4 — decisions belong to the user.

## Core Principle

**Architecture decisions belong to the user.**

The user owns the architecture of their project. An AI assistant may analyse
options, surface trade-offs, and recommend a direction — but it does not decide.
Authorship of a document is not authority over its contents.

A decision is only a decision once the user has made it. Until then it is an open
question, and it must be visible as one.

**Delegation is explicit or it does not exist.** If the user expressly asks the
assistant to choose, the assistant may choose — and the record must state that the
choice was delegated, name exactly what was delegated, and remain open to reversal.
Silence, absence, urgency, and "you know best" inferred from tone are not delegation.

## Rules

### Rule 1 — Never Invent a Missing Decision

An AI assistant must never fill an architectural gap by inventing an answer.

This includes, but is not limited to:

- choosing a language, framework, runtime, or library;
- choosing a database, storage model, or schema approach;
- choosing a hosting target, deployment model, or environment topology;
- choosing an authentication or authorisation approach;
- choosing third-party services, APIs, or integrations;
- choosing message formats, protocols, or interface boundaries;
- choosing coding standards, testing standards, or tooling.

"A placeholder for now", "a sensible default", "an example to illustrate the
structure", and "we can change it later" are **not** exemptions. A written
assumption is indistinguishable from a written decision once it is on disk, and
every later document, task, and reader inherits it.

If the decision has not been made, it is not written down as if it had been.

### Rule 2 — Enumerate Every Required Decision

Before writing any architecture document or ADR, the assistant must enumerate the
decisions that document depends on — both the ones already made and the ones still
open.

The enumeration must be explicit and complete for the scope in question. It is
produced **first**, before any drafting, and it is shown to the user.

For each item, state:

| Field | Meaning |
|---|---|
| Decision | What must be decided, in one line. |
| Status | Decided / Open. |
| Source | For decided items: where the decision is recorded, or when the user stated it. |
| Impact | What in the architecture depends on this. |

An assistant that cannot enumerate the decisions a document rests on does not yet
understand the document well enough to write it.

### Rule 3 — Present Open Items as Explicit Choices

Every item marked **Open** is brought to the user as a concrete choice, not as an
open-ended question and not as a silent gap.

Each open item is presented with:

- the decision to be made, stated plainly;
- realistic options — normally two to four, each named specifically;
- the trade-offs of each option in terms that matter to this project;
- a recommendation, where the assistant has a defensible one, marked clearly as a
  recommendation;
- what becomes blocked or has to be revisited if the decision is deferred.

Vague prompting ("what stack do you want?") shifts the work back to the user
without helping them. Present the analysis; let the user choose.

If the user declines to decide, the item stays open. It is recorded as open — in
the document, in an issue, or in a clearly marked "Open Decisions" section — and
the work that depends on it is either deferred or completed under an assumption
that is **stated in the document as an assumption, not attributed to the user, and
marked as pending confirmation.**

This is the only route by which an undecided item may appear in a document, and it
does not soften Rule 1. Rule 1 forbids an assumption that reads as a decision; a
marked, unattributed, pending-confirmation assumption does not read as one.

### Rule 4 — ADRs Record Decisions, Not Proposals

An ADR is a historical record. It documents a decision **that has already been
made**, the context it was made in, the alternatives that were weighed, and the
consequences accepted.

An ADR must not be used to:

- propose a direction the user has not agreed to;
- ratify an assistant's own preference by writing it up formally;
- capture a shortlist, a design sketch, or an idea under evaluation.

Proposals, options, and evaluations are legitimate work — they belong in a
proposal document, clearly labelled as such, not in `docs/decisions/`.

> Where proposals live and how they are labelled is owned by
> [`adr-format.md`](adr-format.md) Rule 8.

An ADR is written **after** the user decides, and it names the decision as the
user's.

#### Changing a Decision

A decision that is later reversed is recorded as a **new** ADR that supersedes the
old one. The superseded ADR stays in place, marked as superseded, with a pointer to
its replacement. An ADR is never edited to reflect a different decision and is never
deleted — rewriting the record destroys the context the record exists to preserve.

Reversing a recorded decision is itself a decision. Rules 1 through 3 apply to it in
full.

> The numbering, status values, and two-way linking that implement supersession are
> owned by [`adr-format.md`](adr-format.md) Rules 2, 4, and 9.

### Rule 5 — No Silent Assumptions in Architecture Documents

An architecture document must not silently assume:

- **Technology** — languages, frameworks, libraries, runtimes, versions.
- **Deployment** — hosting, environments, regions, scaling model, CI/CD.
- **Integrations** — external services, APIs, vendors, data sources.
- **Standards** — coding conventions, testing requirements, security baselines,
  documentation formats.

Where any of these appear in a document, one of the following must be true:

1. The user decided it, and the document says where that decision is recorded; or
2. It is explicitly marked as an open assumption pending user confirmation.

There is no third case. Unmarked technology in an architecture document is a claim
that the user chose it.

## Required Workflow

Before creating or materially revising any architecture document or ADR:

1. **Read the repository.** Establish what has already been decided and recorded.
   The repository is the source of truth — not chat history and not memory.
2. **Enumerate the decisions** the document depends on (Rule 2).
3. **Separate decided from open.** Cite the source for each decided item.
4. **Present open items to the user as explicit choices** (Rule 3).
5. **Wait for the user's decisions** on items that block the document. If the user
   declines to decide, the item stays open and is handled under Rule 3 — it is not
   resolved by proceeding.
6. **Write the document**, marking any remaining open item as an explicit,
   unresolved assumption.
7. **Record newly made decisions as ADRs** in `docs/decisions/`, attributed to the
   user (Rule 4).

## Compliance Checklist

A document produced under this standard satisfies all of the following:

- [ ] Every architectural choice in it traces to a user decision or is marked open.
- [ ] The decisions it depends on were enumerated before drafting began.
- [ ] Open items were presented to the user as concrete options with trade-offs.
- [ ] No ADR in `docs/decisions/` describes anything other than a decision already made.
- [ ] No technology, deployment target, integration, or standard appears unattributed.
- [ ] Every assumption in it is marked as an assumption and as pending confirmation.
- [ ] Any reversed decision is a new ADR; the superseded ADR is intact and marked.

A document that fails any item is incomplete, regardless of how finished it looks.
