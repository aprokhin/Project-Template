# Architecture Documentation

**Status:** Active standard
**Applies to:** Every document describing system design in this repository or any
project created from it.

## Purpose

This standard defines what an architecture document contains and when it is updated.

It is the content counterpart to
[`architecture-decisions.md`](architecture-decisions.md), which governs authority —
whose decisions these are and what must be settled before writing. The record format
for individual decisions is owned by [`adr-format.md`](adr-format.md).

Architecture documents live in `docs/architecture/`.

## Rules

### Rule 1 — A System Has a Current Architecture Document

Any project with more than one component has a document describing how those
components fit together, and it describes the system as it exists today.

Its job is to let a reader who has never seen the code understand the shape of the
system before reading any of it: what the pieces are, what each is responsible for,
and how they communicate.

### Rule 2 — Required Content

An architecture document covers each of the following:

| Section | Contents |
|---|---|
| Purpose | What the system does, and for whom. |
| Components | Each part, and the one thing it is responsible for. |
| Boundaries | Where responsibility passes between components, and the interface at each. |
| Data flow | How data enters, moves through, and leaves the system. |
| External dependencies | Services, APIs, and systems this one relies on, and what happens when each is unavailable. |
| Non-goals | What the system deliberately does not do. |

A section with nothing to say is stated as such rather than omitted. An absent section
is ambiguous between "nothing to report" and "nobody considered it".

### Rule 3 — Diagrams Are Text in the Repository

Diagrams are written as Mermaid inside the Markdown document, so they are diffable,
reviewable, and editable by whoever next needs to change them.

````markdown
```mermaid
flowchart LR
    Client --> API --> Database
```
````

Image files and externally hosted diagrams are not used, because they cannot be
updated by the person who changes the system and drift away from it silently.

Every diagram is accompanied by prose. A diagram shows the arrangement; only prose can
say why it is arranged that way.

### Rule 4 — Decisions Are Referenced, Not Restated

Where the architecture reflects a recorded decision, the document links to the ADR by
number and states the outcome in one line.

It does not reproduce the context, alternatives, or reasoning. Duplicated rationale
drifts out of step with the record, and then the two disagree with no way to tell which
is current.

### Rule 5 — Documents Describe What Exists

Architecture documents are written in the present tense and describe the system that is
actually built.

Planned components, intended refactors, and future integrations are labelled as
planned, in a clearly separated section — or they live in a proposal under
[`adr-format.md`](adr-format.md) Rule 8. Undated intentions written as fact become
false the moment a reader believes them.

### Rule 6 — Nothing Is Assumed Into the Architecture

Technology, deployment targets, integrations, and standards appear in an architecture
document only where the user decided them or where they are explicitly marked as open
assumptions.

> This is [`architecture-decisions.md`](architecture-decisions.md) Rule 5, and it
> governs the content of every document produced under this standard.

### Rule 7 — Updated With the System It Describes

A change to components, boundaries, data flow, or external dependencies updates the
architecture document in the same piece of work.

The document is not a snapshot taken at the start of a project. Where a change makes
part of it wrong, that part is corrected before the work is reported complete.

### Rule 8 — Proposals Are Labelled and Kept Separate

A document evaluating an architecture the project does not have is a proposal. It
carries `Proposal` in its title and in a status line, and it is never mistaken for a
description of the system.

Proposals share `docs/architecture/` with current documentation, so the label is the
only thing distinguishing them. It is not optional.

## Required Workflow

Before writing or updating an architecture document:

1. **Read the existing document**, if there is one, and the ADRs it references.
2. **Establish what is decided and what is open**, per
   [`architecture-decisions.md`](architecture-decisions.md) Rules 2 and 3.
3. **Read the code** the document describes, so that it reflects what exists rather
   than what was intended.
4. **Write or update** the sections in Rule 2, referencing decisions rather than
   restating them.
5. **Update or add diagrams** as Mermaid, with prose alongside.
6. **Label anything provisional** as planned, proposed, or assumed.
7. **Verify** that every ADR reference resolves to a real record and every link works.

## Compliance Checklist

An architecture document produced under this standard satisfies all of the following:

- [ ] It lives in `docs/architecture/` and describes the system as it exists.
- [ ] It covers purpose, components, boundaries, data flow, external dependencies, and non-goals.
- [ ] Diagrams are Mermaid in the document, each with prose alongside.
- [ ] Recorded decisions are referenced by ADR number, not restated.
- [ ] Every ADR reference resolves to a real record.
- [ ] No technology, deployment target, integration, or standard appears unattributed.
- [ ] Planned and proposed material is labelled and separated from what exists.
- [ ] It was updated in the same work as the change it describes.

A document that fails any item describes a system nobody can rely on it to match.
