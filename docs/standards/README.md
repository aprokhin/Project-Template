# Standards

This directory contains reusable project standards referenced by `CLAUDE.md`.

Each subdirectory holds the standards for one area of the project. They are written
to be reused across projects created from this template, so `CLAUDE.md` can point to
them rather than restating their contents.

Every standard follows the same structure — Status, Applies to, Purpose, Rules,
Required Workflow, Compliance Checklist — and each rule is owned by exactly one
standard. Where a rule has a domain-specific expression elsewhere, the standards
cross-reference rather than repeat it.

## Foundation

[`project/working-agreement.md`](project/working-agreement.md) is the root standard.
Every other standard in this library depends on it, directly or indirectly, and none
of them repeat it.

[`documentation/documentation-standards.md`](documentation/documentation-standards.md)
is listed twice by design: here, because every standard in this library is written
under it, and again under **Documentation**, its owning domain. Every other standard
appears exactly once, in its own domain.

| Standard | Governs |
|---|---|
| [`project/working-agreement.md`](project/working-agreement.md) | The universal working rules: source of truth, inspection before action, preservation of existing work, decision ownership, scope, evidence, and precedence within this library. |
| [`project/change-authorisation.md`](project/change-authorisation.md) | When the assistant may act alone and when it needs explicit approval; what approval is and how far it extends. |
| [`project/verification.md`](project/verification.md) | What counts as evidence, and how outcomes, failures, and unverified claims are reported. |
| [`project/repository-structure.md`](project/repository-structure.md) | The baseline directory layout, what may be created freely, and how project-specific structure is treated. |
| [`documentation/documentation-standards.md`](documentation/documentation-standards.md) | The form every document takes: structure, formatting, terminology, and register. |

## Architecture

| Standard | Governs |
|---|---|
| [`architecture/architecture-decisions.md`](architecture/architecture-decisions.md) | Ownership of architectural decisions, and the mandatory workflow before writing an architecture document or ADR. |
| [`architecture/adr-format.md`](architecture/adr-format.md) | The ADR as an artifact: location, numbering, required sections, status lifecycle, and supersession. |
| [`architecture/architecture-documentation.md`](architecture/architecture-documentation.md) | What an architecture document contains and when it is updated. |

## Documentation

| Standard | Governs |
|---|---|
| [`documentation/documentation-standards.md`](documentation/documentation-standards.md) | Structure, formatting, terminology, and register for every document. |
| [`documentation/documentation-lifecycle.md`](documentation/documentation-lifecycle.md) | When documentation must be written or updated, and which document receives which knowledge. |
| [`documentation/changelog-standards.md`](documentation/changelog-standards.md) | What belongs in the changelog, how entries are written, and when they are added. |

## Git

| Standard | Governs |
|---|---|
| [`git/git-workflow.md`](git/git-workflow.md) | Operations that change repository state: initialising, branching, staging, committing, pushing, history, and remotes. |
| [`git/commit-standards.md`](git/commit-standards.md) | What a commit contains and what its message says. |
| [`git/pull-request-standards.md`](git/pull-request-standards.md) | When a pull request may be opened, what it must contain, and what the assistant may not do with it. |

## Security

| Standard | Governs |
|---|---|
| [`security/secrets-management.md`](security/secrets-management.md) | Credentials and secret material: what is never written down, how configuration is expressed, and what happens on exposure. |
| [`security/secure-coding.md`](security/secure-coding.md) | The language-agnostic security baseline: trust boundaries, privilege, dependencies, and safe defaults. |

## Testing

| Standard | Governs |
|---|---|
| [`testing/testing-standards.md`](testing/testing-standards.md) | Test design: what is tested, how tests are structured, and what must never be done to make a suite pass. |
