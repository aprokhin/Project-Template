# CLAUDE.md

Instructions for Claude Code when working in this repository and in any project created from it.

## Source of Truth

**The repository is the source of truth.**

What exists on disk in this repository defines the current state of the project — not chat history, not memory, not assumptions carried over from an earlier session, and not what a previous conversation reported having done. When the repository and any other account of the project disagree, the repository wins.

Read the repository to learn its state. Do not infer structure, contents, or conventions from context alone.

## Before Making Changes

**Inspect the existing repository structure before making any changes.**

At the start of substantive work, and before acting on any assumption about layout or contents:

1. List the relevant directories and confirm what actually exists.
2. Read the files you intend to change — in full where practical, and at minimum the sections you will touch.
3. Check `README.md` and this file for conventions already established.
4. Identify what is standard structure from the template and what is project-specific work added since.

Never write to a path without first establishing what is already there.

## Preserving Existing Work

**Existing files, documentation, and user work are preserved by default.**

Never overwrite, delete, rename, move, stage, commit, push, or restructure existing work without explicit user approval. This applies to source code, documentation, configuration, assets, and data alike — and it applies whether the file appears important, obsolete, temporary, or empty. "It looked unused" is not authorization.

Approval must be explicit and specific to the action taken. Approval for one destructive action does not extend to the next one, and permission to edit a file is not permission to delete or move it.

When something genuinely appears redundant or obsolete, say so and let the user decide. Do not act on that judgment yourself.

### Standard directories vs. project-specific structure

Missing standard directories from the template baseline **may be created automatically** — creating an absent `docs/decisions/` is additive and destroys nothing.

Existing project-specific structure **must not be replaced.** If a project has organized itself differently from the baseline, that difference is deliberate until the user says otherwise. Do not "normalize" a project back to the template. Report the divergence and ask.

## Before Editing

Before editing any file:

- **Inspect the relevant files.** Read what you are about to change.
- **Identify dependencies and affected documentation.** Determine what imports, references, or documents the thing being changed, and what will break or become stale as a result.
- **Explain any material ambiguity before proceeding.** If the request has more than one reasonable reading and the readings lead to materially different work, state the ambiguity and resolve it with the user first. Routine judgment calls do not need a question — genuine forks do.

## Documentation After Changes

After structural or architectural changes, update the appropriate documentation, as applicable:

| Location | Update when |
|---|---|
| `README.md` | Structure, setup, or the project's purpose changed. |
| `CLAUDE.md` | Working rules or conventions for this repository changed. |
| `docs/architecture/` | System design, components, or data flow changed. |
| `docs/decisions/` | A significant technical decision was made — record it as an ADR with context, alternatives, and consequences. |
| `docs/changelog/` | A user-visible or release-relevant change was made. |
| `docs/setup/` | Installation, environment, or configuration steps changed. |
| `docs/user/` | End-user behavior or workflows changed. |

Documentation updates are part of the change, not a follow-up task. A structural change with stale documentation is incomplete work.

## Knowledge Belongs in the Repository

**Important decisions, architecture, setup instructions, and operational knowledge must be saved in repository files — not only in chat.**

Chat is transient. Anything a future session, a teammate, or the user in six months would need must be written to disk in the appropriate location:

- Decisions and their rationale → `docs/decisions/`
- How the system fits together → `docs/architecture/`
- How to install, configure, or run it → `docs/setup/`
- How to operate, deploy, or troubleshoot it → `docs/developer/` or `scripts/`

If you explain something substantial in conversation and it is not yet written down, write it down.

## Verification

**Never claim success without evidence.**

After making changes:

1. **Confirm files exist on disk.** Do not assume a write succeeded — verify it.
2. **Show relevant file paths.** State exactly what was created or modified, by full or repository-relative path.
3. **Run appropriate tests or validation.** Use the project's own test or lint commands where they exist.
4. **Report failures honestly.** If a test fails, say so and show the output. If a step was skipped, say it was skipped. If something is unverified, say it is unverified.

A report of success that was not verified is a defect. Partial completion reported accurately is better than full completion reported without evidence.

## Git

- **Initialize Git only when requested,** or when creating a new repository from this template.
- **Use `main` as the initial branch** — `git init -b main`.
- **Never stage, commit, push, create a pull request, or modify remotes unless explicitly requested.** Making a change is not authorization to commit it. Committing is not authorization to push.
- **Always show `git status` after Git-related changes**, so the resulting state is visible rather than assumed.

## Documentation Standards

- **Use clear GitHub Markdown** — headings, tables, fenced code blocks with language hints, and lists where they aid comprehension.
- **Keep `README.md` current.** It is the entry point; a stale README misleads every future reader.
- **Do not leave outdated documentation after structural changes.** Update or remove it — do not let it rot in place.
- **Use relative repository paths in documentation when practical** (`docs/architecture/`, not an absolute machine-specific path). Relative paths survive being cloned, moved, and used by someone else.

## Security

- **Never write secrets, passwords, API keys, tokens, or credentials into tracked files.** This includes source code, configuration, documentation, commit messages, and test fixtures.
- **Use `.env.example` for variable names and placeholders only** — names and dummy values that show the shape of the configuration, never real values. Real values belong in `.env`, which must be gitignored.
- **Never expose secret values in reports.** When a secret must be referenced, name the variable, never its value. If a secret is discovered in a tracked file, report the location and the fact of the exposure without reproducing the value.

## Project Creation Behavior

- **Treat this repository layout as the standard baseline** for new projects.
- **Create missing standard folders** when scaffolding.
- **Preserve empty folders with `.gitkeep`.** Git tracks files, not directories — an empty directory without a marker will not survive a clone.
- **Do not search external drives, Google Drive, Documents, or unrelated directories for another template.** No such search is needed and no other template should be used.
- **This repository is the project template.** There is no other.

## Completion Checklist

Before reporting work as complete, confirm each item:

- [ ] Requested work completed
- [ ] Files verified on disk
- [ ] Tests or validation completed
- [ ] Documentation updated
- [ ] `git status` reviewed
- [ ] No unauthorized commit or push performed
