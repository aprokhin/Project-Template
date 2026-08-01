# Secrets Management

**Status:** Active standard
**Applies to:** Every file, report, log, and command produced by an AI assistant in
this repository or any project created from it.

## Purpose

This standard governs credentials and other secret material: what must never be
written down, how configuration is expressed without it, and what happens when a
secret is found where it should not be.

A secret is any value whose disclosure would grant access or cause harm — passwords,
API keys, tokens, private keys, connection strings containing credentials, session
cookies, signing keys, and personal data held under an obligation to protect it.

It inherits from
[`working-agreement.md`](../project/working-agreement.md). Secure design of code more
broadly is owned by [`secure-coding.md`](secure-coding.md); this standard covers secret
material specifically.

## Rules

### Rule 1 — Secrets Never Enter Tracked Files

No secret value is written into any file under version control. This includes source
code, configuration, documentation, test fixtures, scripts, notebooks, and commit
messages.

It applies to secrets that are expired, revoked, belong to a development environment,
or are "only for local testing". A tracked secret is published to everyone who clones
the repository and everyone who ever will, and revocation does not remove it from
history.

### Rule 2 — Configuration Is Shape, Not Content

Configuration that requires secrets is expressed in two files with different jobs:

| File | Contents | Tracked |
|---|---|---|
| `.env.example` | Variable names and obviously fake placeholders. | Yes |
| `.env` | Real values for the local environment. | No — gitignored |

`.env.example` documents the shape of the configuration: every variable the project
reads, in the order it reads them, with a placeholder that could not be mistaken for a
real value. `.env` is never committed, and the assistant confirms it is gitignored
before creating it.

### Rule 3 — Secret Values Are Never Reproduced in Reports

When a secret must be referred to, the assistant names the variable and its location.
It does not print, echo, quote, partially redact, or summarise the value.

Partial disclosure is disclosure: the first four characters of a key narrow an attack,
and a "redacted" value that keeps its structure reveals what kind of credential it is
and where it came from.

This applies to reports, explanations, error analysis, and any command whose output
would contain the value.

### Rule 4 — Discovered Exposure Is Reported, Not Quietly Cleaned Up

When the assistant finds a secret in a tracked file, it stops and reports: which file,
which line, and what kind of credential — without reproducing the value.

The assistant does not remove the secret, rotate it, rewrite history, or force-push a
correction on its own initiative. Those actions are destructive, they are the user's to
authorise, and performing them silently can destroy the user's only record of what was
exposed.

A secret that has been committed is treated as compromised regardless of whether the
repository is private. Whether to rotate it is the user's decision, and the assistant
says plainly that rotation is the only reliable remedy.

### Rule 5 — Examples and Fixtures Use Obvious Fakes

Sample values in documentation, tests, and fixtures are unmistakably synthetic:
`your-api-key-here`, `sk-example-not-a-real-key`, `password-goes-here`.

Values that look real invite two failures: someone tries to use them, and a scanner
cannot distinguish them from a genuine leak. Realistic-looking test credentials are
never used, even where they are genuinely fake.

### Rule 6 — Secrets Do Not Travel Through Logs, Errors, or Output

Code written by the assistant does not log, print, or include secret values in error
messages, stack traces, telemetry, or debugging output.

Configuration objects and request payloads are not logged wholesale on the assumption
that they contain nothing sensitive. Where a value must be referenced in a log, it is
referenced by name.

### Rule 7 — Local and Generated Files Stay Untracked

Files that hold environment-specific or generated material — `.env`, credential
caches, key files, local database dumps, editor and tool state — are added to
`.gitignore` before they can be staged.

The assistant checks the ignore rules before creating such a file, rather than
discovering the problem after it is committed.

### Rule 8 — Access Is Requested, Not Assumed

The assistant does not read, open, or list secret-bearing files as a matter of course.
It reads them only when the task genuinely requires it, and it says why.

Needing to know that a variable exists is not a reason to read its value. The variable
name is available from `.env.example`, which is what that file is for.

## Required Workflow

Before writing any file, and before reporting:

1. **Identify whether the work touches secret material** — configuration, credentials,
   authentication, or external service access.
2. **Check the ignore rules** for any file that will hold real values, before creating
   it.
3. **Write names and placeholders**, never values, into anything tracked.
4. **Scan what was written** for values that look like credentials before presenting
   or committing it.
5. **Report exposure immediately** if a secret is found in a tracked file — location
   and kind only, never the value.
6. **Leave remediation to the user.** State that rotation is the only reliable remedy
   and wait for a decision.

## Compliance Checklist

Work performed under this standard satisfies all of the following:

- [ ] No secret value was written into any tracked file, including commit messages.
- [ ] Configuration requiring secrets is expressed as names and placeholders in `.env.example`.
- [ ] Any file holding real values is gitignored, and that was confirmed before creation.
- [ ] No secret value appears in any report, output, or command shown to the user.
- [ ] Example and fixture values are unmistakably synthetic.
- [ ] No code written logs, prints, or embeds secret values in errors or telemetry.
- [ ] Any discovered exposure was reported by location and kind, with no value reproduced.
- [ ] No remediation — removal, rotation, or history rewriting — was performed without the user's decision.

Work that fails any item has exposed something, however small the exposure appears.
