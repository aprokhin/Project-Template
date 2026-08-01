# Verification

**Status:** Active standard
**Applies to:** Every claim an AI assistant makes about the state of this repository,
any project created from it, or the outcome of work performed in it.

## Purpose

This standard defines what counts as evidence and how outcomes are reported. It
supplies the mechanics that
[`working-agreement.md`](working-agreement.md) Rule 7 states as a principle: claims
require evidence.

It governs the relationship between what happened and what is said to have happened.
Test design, coverage, and what makes a good test are owned by
[`testing-standards.md`](../testing/testing-standards.md); this standard governs the
act of checking and the honesty of the resulting report.

## Rules

### Rule 1 — Every Claim Traces to an Observation

A statement about the state of the repository is made only where the assistant has
observed that state in the current session.

Memory of having written a file is not observation. A prior session's report is not
observation. The plausibility of a command having worked is not observation. The tool
output, read after the fact, is.

Where the assistant has not observed something, it does not describe it — it either
observes it or says it has not.

### Rule 2 — Writes Are Confirmed on Disk

A file is not created until the filesystem says it is. After creating or modifying
files, the assistant confirms that each path exists and holds what it should.

For a new file, existence and size or line count are sufficient. For an edit, the
confirmation covers the region that changed — an edit that silently matched nothing,
or matched in the wrong place, produces a file that exists and is wrong.

### Rule 3 — The Project's Own Checks Are the Standard

Validation uses the commands the project already defines — its test runner, linter,
type checker, formatter, or build. These are discovered by reading the project's
configuration, not assumed from its language.

The assistant does not invent a validation command, substitute a weaker check for a
stronger one that is failing, or narrow a test run to the subset that passes.

Where a project defines no checks, that fact is stated in the report. "No tests were
run because this project has none" is a complete and honest statement; silence is not.

### Rule 4 — Failures Are Reported With Their Output

A failing check is reported as failing, in the same response in which it was run, with
the relevant output included.

Failures are not summarised into vagueness, deferred to a later message, or described
as "a minor issue" without the user seeing what it was. Where a failure is genuinely
pre-existing and unrelated to the work, the assistant says so and shows it anyway.

### Rule 5 — Verified, Unverified, and Skipped Are Distinct

Every claim in a report falls into one of three states, and the report makes clear
which:

| State | Meaning |
|---|---|
| Verified | The assistant ran or read something that establishes this, in this session. |
| Unverified | The assistant believes this but did not check it. |
| Skipped | A step that would normally be performed was not performed. |

An unverified claim written in the language of certainty is a false claim, regardless
of whether it later turns out to be true. Skipped steps are named, with the reason.

### Rule 6 — Output Is Never Simulated

The assistant never presents output it did not receive. It does not write what a
command would print, illustrate a result with a plausible example, or reconstruct
output from memory and present it as a transcript.

If a command was not run, no output for it appears in the report.

### Rule 7 — Evidence Is Proportional to the Claim

The strength of the evidence matches the strength of the claim.

"The file was created" needs the file to exist. "The tests pass" needs the suite to
have been run to completion. "This fixes the bug" needs the failing behaviour to have
been reproduced before and shown absent after. "This is ready to ship" needs every
check the project defines to have run and passed.

Where the assistant cannot gather evidence proportional to a claim, it makes a weaker
claim rather than a stronger one it cannot support.

### Rule 8 — Reports Name Paths and Commands

A report states exactly which paths were created, modified, or deleted, by
repository-relative path, and which commands were run.

"Updated the documentation" is not a report. "Updated `docs/setup/install.md`" is.
The user must be able to review the work from the report without first having to
discover what it touched.

### Rule 9 — Passing Checks Are Not a Completion Claim

A green test suite establishes that the tests passed. It does not establish that the
work is correct, complete, or what the user asked for.

Completion is claimed against the request, not against the tooling. Before reporting
work as complete, the assistant re-reads the request and confirms each part of it was
delivered — and names any part that was not.

## Required Workflow

After making changes and before reporting on them:

1. **Confirm existence.** Verify that every file claimed to be created or modified
   exists at the stated path.
2. **Confirm content.** Check the regions that changed, not merely that the file is
   present.
3. **Discover the project's checks** by reading its configuration, and run them.
4. **Capture results as received.** Keep the actual output; do not paraphrase failures.
5. **Classify every claim** as verified, unverified, or skipped.
6. **Re-read the request** and confirm each part of it was delivered.
7. **Report** paths, commands, results, failures, skips, and anything left open.

## Compliance Checklist

A report produced under this standard satisfies all of the following:

- [ ] Every claim about repository state was observed in this session, not assumed.
- [ ] Every file claimed created or modified was confirmed to exist, with its changed region checked.
- [ ] The project's own checks were discovered and run, or their absence was stated.
- [ ] Every failure is reported, with output, in the response where it occurred.
- [ ] Verified, unverified, and skipped items are distinguishable in the report.
- [ ] No output appears that was not actually produced.
- [ ] The evidence gathered is proportional to the strongest claim made.
- [ ] Exact repository-relative paths and commands are named.
- [ ] Completion is claimed against the request, not against a passing check.

A report that fails any item is a defect in the work, not a matter of phrasing.
