# Secure Coding

**Status:** Active standard
**Applies to:** Every change to executable code made by an AI assistant in this
repository or any project created from it.

## Purpose

This standard defines the security baseline that applies to code regardless of
language, framework, or domain.

Credentials and secret material are owned by
[`secrets-management.md`](secrets-management.md). This standard covers everything
else: trust boundaries, privilege, dependencies, and the defaults a change ships with.

It is a floor, not a security review. A project handling payments, health data, or
authentication for other systems needs more than this, and the assistant says so rather
than treating compliance here as sufficient.

## Rules

### Rule 1 — Input From Outside the Program Is Untrusted

Anything the program did not compute itself is untrusted: request bodies, query
parameters, headers, environment variables, file contents, command-line arguments,
message payloads, and responses from other services.

Untrusted input is validated at the boundary where it enters — checked for type,
range, length, and shape before it reaches logic that assumes it is well formed.
Validation happens on the trusted side; a check performed by a client is a usability
feature, not a control.

### Rule 2 — Data Is Kept Out of Command Position

Values from outside the program are never concatenated into anything that will be
interpreted: SQL, shell commands, file paths, HTML, templates, serialised objects, or
generated code.

The mechanism that separates data from instruction is used instead — parameterised
queries, argument arrays rather than shell strings, path resolution checked against a
permitted root, context-aware escaping for markup. Escaping by hand is the fallback of
last resort and is stated as such where it is unavoidable.

### Rule 3 — Least Privilege by Default

Code runs with the narrowest permissions that let it work: the minimum database rights,
the minimum file access, the minimum API scopes, the minimum network reach.

New credentials, roles, and permissions are scoped to the task rather than copied from
whatever already exists. Convenience-level privilege granted "for now" is never
narrowed later.

### Rule 4 — Security Controls Are Not Disabled to Make Something Work

Certificate verification, authentication checks, CSRF protection, sandboxing, content
security policies, and permission checks are not switched off, bypassed, or stubbed to
get a change working.

Where a control blocks legitimate work, the assistant reports what is blocking it and
why, and fixes the underlying cause. A disabled control added to make a test pass
survives into production far more often than anyone intends.

### Rule 5 — Dependencies Are Deliberate

Adding a dependency is an architectural decision belonging to the user, under
[`architecture-decisions.md`](../architecture/architecture-decisions.md) Rule 1. The
assistant proposes; it does not add libraries on its own initiative.

Where dependencies are added with the user's decision, versions are pinned and the
lockfile is committed. The assistant does not upgrade unrelated dependencies while
doing other work, and does not remove a lockfile to resolve a conflict.

### Rule 6 — Errors Do Not Leak Internals

Messages returned to a caller say what went wrong in terms the caller needs. They do
not carry stack traces, file paths, SQL, internal hostnames, configuration values, or
library versions.

Detail belongs in logs, which are subject to
[`secrets-management.md`](secrets-management.md) Rule 6. Authentication and lookup
failures are reported uniformly, so that error text cannot be used to enumerate what
exists.

### Rule 7 — Cryptography Is Used, Not Invented

Established, maintained libraries are used for hashing, encryption, signing, and random
value generation. The assistant does not implement a cryptographic primitive, design a
protocol, or improvise a token scheme.

Passwords are stored using a current password-hashing function, never a general-purpose
hash. Values that must be unguessable — tokens, session identifiers, nonces — come from
a cryptographically secure random source, never a general-purpose random generator.

### Rule 8 — Defaults Are Safe

A change ships in its secure configuration. Authentication on, encryption in transit
on, debug output off, permissive origins closed, verbose errors disabled, sample
credentials absent.

The safe configuration is the default and the insecure one is the deliberate override,
never the reverse. A default that must be hardened before deployment will reach
deployment unhardened.

### Rule 9 — Security-Relevant Changes Are Called Out

Where a change touches authentication, authorisation, session handling, cryptography,
input validation, file or network access, or dependency versions, the assistant says so
explicitly in its report.

These changes need human attention regardless of how routine they look. Burying them in
a list of edits denies the user the chance to look closely at the part that warranted
it.

## Required Workflow

Before making any change to executable code:

1. **Identify the trust boundaries** the change touches — where untrusted input enters
   and where privileged operations occur.
2. **Follow the project's existing security patterns** rather than introducing a second
   approach alongside them.
3. **Validate at the boundary** and keep external data out of command position.
4. **Scope privileges and credentials** to what the change actually needs.
5. **Propose, do not add, dependencies**; pin and commit the lockfile where they are
   approved.
6. **Check the defaults** the change ships with.
7. **Report security-relevant changes explicitly**, and state where this baseline is
   insufficient for the domain.

## Compliance Checklist

Work performed under this standard satisfies all of the following:

- [ ] Untrusted input is validated at the boundary, on the trusted side.
- [ ] No external value is concatenated into SQL, shell, paths, markup, or generated code.
- [ ] Privileges, scopes, and permissions are the minimum the change requires.
- [ ] No security control was disabled, bypassed, or stubbed.
- [ ] No dependency was added without the user's decision; lockfiles are committed and unrelated packages untouched.
- [ ] Errors returned to callers carry no internal detail, and failures are reported uniformly.
- [ ] Cryptography and randomness come from established libraries and secure sources.
- [ ] The change ships in its secure configuration by default.
- [ ] Security-relevant changes are named explicitly in the report.

Work that fails any item ships an exposure, whether or not anyone finds it.
