# Project Template

## Purpose

This is the **master template** used to create all new projects.

It defines a single, consistent directory structure so that every project — regardless of language, framework, or scope — starts from the same known layout. Anyone (or any tool) moving between projects can rely on finding the same things in the same places.

The template ships no application code, no configuration, and no dependencies. It provides three things: the directory skeleton, the `.gitkeep` markers that allow Git to preserve otherwise-empty directories, and the standards library in [`docs/standards/`](docs/standards/README.md) that defines how work is performed in every project created from it. Structure and standards are the deliverable; application content belongs to the projects.

This directory is a **reference copy**. It is never used as a working project itself. See [Rules](#rules).

## Project Structure

### Top-level directories

| Directory | Purpose |
|---|---|
| `apps` | Deployable applications and user-facing entry points. Each app lives in its own subdirectory and is independently runnable. |
| `assets` | Static, non-code resources: images, fonts, icons, sample data, and design files. Contains `repo-template/` for boilerplate files used when scaffolding new repositories. |
| `docs` | All project documentation, organized by audience and purpose. See the breakdown below. |
| `packages` | Shared internal libraries consumed by `apps` and `services`. Code here is imported, never deployed on its own. |
| `prompts` | Prompt templates, system prompts, and AI agent instructions maintained as versioned artifacts rather than scattered inline strings. |
| `scripts` | Automation and operational tooling: build, deployment, migration, setup, and maintenance scripts. |
| `services` | Long-running backend services, APIs, and workers. Distinguished from `apps` by having no direct end-user interface. |
| `templates` | Reusable file and code templates used within the project — scaffolds, boilerplate, and generators. |
| `tests` | Cross-cutting tests: integration, end-to-end, and system-level suites that span more than one app, package, or service. Unit tests typically live beside the code they cover. |

### The `docs` directory

| Subdirectory | Contents |
|---|---|
| `api` | API reference material: endpoint documentation, schemas, request and response contracts. |
| `architecture` | System design: component diagrams, data flows, and how the pieces fit together. |
| `archive` | Superseded documentation retained for historical reference. Nothing here is current — it is kept so past decisions remain traceable. |
| `changelog` | Release notes and the record of what changed between versions. |
| `decisions` | Architecture Decision Records (ADRs). Each entry captures a decision, its context, the alternatives weighed, and the consequences accepted. |
| `developer` | Internal engineering documentation: conventions, workflows, debugging guides, and contributor-facing notes. |
| `references` | External material worth preserving: specifications, standards, vendor documentation, and research. |
| `setup` | Installation, environment configuration, and getting-started instructions. |
| `standards` | The standards library: the rules governing how work is performed in this repository and in every project created from it. Indexed in [`docs/standards/README.md`](docs/standards/README.md). |
| `user` | End-user documentation: guides, tutorials, and manuals for people using the software. |

## How to Create a New Project

> The absolute paths in the examples below are local examples from one machine. Substitute your own template and project locations.

### 1. Copy the template

Copy the entire template to your new project location. Do not move it — the master must remain in place.

```powershell
$src = "C:\Users\Alex\AI-Standards\Project-Template"
$dst = "C:\Users\Alex\Projects\My-New-Project"

Copy-Item $src $dst -Recurse
```

### 2. Rename the project

The directory name is the project name. Use the same convention across all projects — hyphenated, no spaces:

```
My-New-Project
```

Then update any project-specific references inside the copy, including replacing this `README.md` with one describing the new project.

### 3. Initialize Git

Initialize the repository with `main` as the initial branch:

```powershell
cd "C:\Users\Alex\Projects\My-New-Project"
git init -b main
```

The `-b main` flag is required if your global `init.defaultBranch` is still set to `master`. To change that default permanently:

```powershell
git config --global init.defaultBranch main
```

### 4. Verify the structure

Confirm the copy is a faithful replica before starting work. Compare directories and files against the template:

```powershell
$src = "C:\Users\Alex\AI-Standards\Project-Template"
$dst = "C:\Users\Alex\Projects\My-New-Project"

Compare-Object `
    (Get-ChildItem $src -Recurse -Force | ForEach-Object { $_.FullName.Substring($src.Length) }) `
    (Get-ChildItem $dst -Recurse -Force | Where-Object { $_ -notlike "*\.git\*" } | ForEach-Object { $_.FullName.Substring($dst.Length) }) `
    -IncludeEqual |
    Sort-Object InputObject |
    Format-Table SideIndicator, InputObject -AutoSize
```

Every row should show `==`. A `<=` means a file is missing from the new project; a `=>` means something extra is present.

Then confirm Git can see every directory:

```powershell
git status --porcelain -uall
```

Each `.gitkeep` should appear as untracked. A directory that produces no entry is invisible to Git and will not survive a clone.

### 5. Start development

Stage and commit the skeleton as your first commit, then begin work:

```powershell
git add .
git commit -m "Initial commit: project structure from Project-Template"
```

## Rules

- **Never modify the master template directly for project-specific work.** Changes here propagate to every future project. Project-specific work belongs in the copy, not the original.
- **Every new project starts from this template.** No ad-hoc directory layouts — consistency is the point.
- **Keep directory structure consistent across all projects.** Do not rename or remove standard directories. Unused directories stay in place, held open by their `.gitkeep`.
- **Structural improvements are welcome — deliberately.** If the template itself needs to change, change it here, intentionally, and understand that it affects all projects created afterward.
- **Every empty directory needs a `.gitkeep`.** Git tracks files, not directories. An empty directory without one will not survive a clone.

## Future Additions

The following files are planned for this template but not yet present:

- [ ] **`CONTRIBUTING.md`** — Contribution guidelines, branch naming, and pull request conventions.
- [ ] **`LICENSE`** — License terms. To be determined per project.
