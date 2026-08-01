# Testing Standards

**Status:** Active standard
**Applies to:** Every test written or modified by an AI assistant in this repository or
any project created from it.

## Purpose

This standard governs test design: what is tested, how tests are structured, and what
must not be done to a test to make a suite pass.

Running checks and reporting their results is owned by
[`verification.md`](../project/verification.md). This standard covers the tests
themselves; that one covers the honesty of what is claimed about them.

## Rules

### Rule 1 — Tests Live in the Repository and Run From One Command

A project's tests are committed alongside its code and run by a single documented
command, recorded in `README.md` or `docs/developer/`.

A test that only runs on one machine, or requires a sequence of undocumented steps, is
not part of the project's safety net. The assistant discovers the existing command by
reading the project's configuration rather than assuming one.

### Rule 2 — Structure Mirrors the Code

Test files are placed and named so that the test for a given piece of code is
findable without searching: the project's existing convention, whether colocated with
the source or held under `tests/`, is followed exactly.

Test names state the behaviour under test and the condition — what is being verified
and when. A failure message should identify the problem before anyone opens the file.

### Rule 3 — Tests Assert Intended Behaviour, Not Observed Behaviour

A test encodes what the code is supposed to do. It is written from the requirement, not
from the current output.

Running the code and asserting whatever it produced creates a test that passes and
proves nothing — it will keep passing while the bug it was meant to catch stays in
place, and it converts a defect into a specification.

### Rule 4 — A Failing Test Is Never Weakened to Pass

A test that fails is reporting something. It is not deleted, skipped, commented out,
marked as expected-to-fail, or loosened until it passes.

Where a test appears to be wrong rather than the code, the assistant says so, explains
why, and lets the user decide. Changing a test to accommodate failing code is
destructive under
[`change-authorisation.md`](../project/change-authorisation.md) Rule 1 and requires
explicit approval naming that test.

### Rule 5 — What Must Be Covered

Tests cover, at minimum:

| Target | Why |
|---|---|
| Public behaviour | The contract other code and users depend on. |
| Boundaries | Empty, maximum, zero, negative, and the values either side of a limit. |
| Error paths | What happens when input is invalid or a dependency fails. |
| Regressions | Every fixed bug gets a test that fails without the fix. |

Internal implementation detail is not tested directly. Tests bound to internals break
on every refactor and discourage the refactoring they should be enabling.

### Rule 6 — Tests Are Deterministic and Independent

A test produces the same result on every run, in any order, on any machine.

That means no dependence on wall-clock time, random values, network availability,
execution order, or state left behind by another test. Where a test needs time,
randomness, or an external service, that dependency is injected or stubbed.

An intermittently failing test is treated as a defect, not as noise to be re-run.

### Rule 7 — New Behaviour Arrives With Tests

A change to behaviour includes the tests for that behaviour, in the same piece of work.

A bug fix includes a test that fails before the fix and passes after it — and the
assistant confirms it fails first. A test written after the fix, never seen to fail,
has not been shown to test anything.

### Rule 8 — Introducing Test Infrastructure Is the User's Decision

Where a project has no tests and no test framework, choosing one is an architectural
decision belonging to the user, under
[`architecture-decisions.md`](../architecture/architecture-decisions.md) Rule 1.

The assistant reports the absence, presents realistic options with trade-offs, and
waits. It does not install a framework, add a dependency, or establish a test layout on
its own initiative.

Where a framework already exists, it is used. The assistant does not introduce a second
one alongside it.

### Rule 9 — Coverage Is Evidence, Not a Target

Coverage figures indicate where tests are absent. They do not indicate that the tests
present are good.

Tests are not written to raise a number, and code is not restructured to make a
coverage tool report better results. A suite that executes every line while asserting
almost nothing is worse than a smaller suite that checks what matters, because it looks
like protection.

## Required Workflow

Before writing or changing tests:

1. **Discover the existing setup** — framework, layout, naming, and the command that
   runs the suite — by reading the project's configuration.
2. **Run the suite first**, to establish what passes before the work begins.
3. **Write the test from the requirement**, not from current output.
4. **For a bug fix, confirm the new test fails** before applying the fix.
5. **Apply the change**, then run the full suite, not only the new test.
6. **Report** results per [`verification.md`](../project/verification.md), including
   any pre-existing failures.
7. **Stop and ask** if no test infrastructure exists, rather than choosing one.

## Compliance Checklist

Work performed under this standard satisfies all of the following:

- [ ] Tests are committed and run from the project's documented command.
- [ ] Test placement and naming follow the project's existing convention.
- [ ] Every assertion encodes intended behaviour, not observed output.
- [ ] No test was deleted, skipped, or loosened to make a suite pass.
- [ ] Public behaviour, boundaries, error paths, and fixed bugs are covered.
- [ ] Every test is deterministic and independent of order and environment.
- [ ] Behaviour changes arrived with tests; bug-fix tests were seen to fail first.
- [ ] The full suite was run, and pre-existing failures were reported.
- [ ] No test framework or layout was introduced without the user's decision.

Work that fails any item leaves a suite that reports confidence it has not earned.
