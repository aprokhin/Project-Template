# Changelog

All notable changes to this repository are recorded here, newest first.

Entries follow
[`docs/standards/documentation/changelog-standards.md`](../standards/documentation/changelog-standards.md).

## [Unreleased]

Nothing yet.

## [1.0.0] — 2026-08-01

The initial complete standards-library baseline. Every project created from this
template now inherits a full set of working standards rather than the directory
skeleton alone.

### Added

- **Standards library** at `docs/standards/` — sixteen standards across six domains,
  indexed in [`docs/standards/README.md`](../standards/README.md). Every standard uses
  the same structure: Status, Applies to, Purpose, Rules, Required Workflow, and
  Compliance Checklist.
- **Foundation** — `project/working-agreement.md` as the root standard, with
  `project/change-authorisation.md`, `project/verification.md`, and
  `project/repository-structure.md`.
- **Architecture** — `architecture/architecture-decisions.md`,
  `architecture/adr-format.md`, and `architecture/architecture-documentation.md`.
- **Documentation** — `documentation/documentation-standards.md`,
  `documentation/documentation-lifecycle.md`, and
  `documentation/changelog-standards.md`.
- **Git** — `git/git-workflow.md`, `git/commit-standards.md`, and
  `git/pull-request-standards.md`.
- **Security** — `security/secrets-management.md` and `security/secure-coding.md`.
- **Testing** — `testing/testing-standards.md`.
- **This changelog**, required by the standards library and absent until now.

### Changed

- `CLAUDE.md` now names the standards library as authoritative for repository
  behavior, links the library index, and states the precedence order: a standard
  governs over `CLAUDE.md` where the two differ, the more specific standard governs
  within its domain, and a genuine conflict between standards is reported rather than
  resolved at runtime.
- `README.md` now documents `docs/standards/` and describes the template as shipping
  standards alongside structure.
