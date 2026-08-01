# Documentation Standards

**Status:** Active standard
**Applies to:** Every document written or edited by an AI assistant in this repository
or any project created from it — including the standards in this library.

## Purpose

This standard defines the **form** documentation takes: structure, formatting,
terminology, and register. It governs every Markdown file in the repository, and it
governs this library's own documents.

It deliberately does not cover *when* a document must be written or updated, or which
document receives which kind of knowledge. Those are lifecycle questions, owned by
[`documentation-lifecycle.md`](documentation-lifecycle.md). This standard answers only:
given that a document is being written, what must it look like.

It inherits from
[`docs/standards/project/working-agreement.md`](../project/working-agreement.md) and
adds nothing that contradicts it.

## Rules

### Rule 1 — GitHub-Flavoured Markdown, Nothing Else

Documentation is plain-text Markdown, rendered by GitHub-flavoured conventions, and
committed to the repository alongside the work it describes.

Word processor formats, PDFs, screenshots of text, and externally hosted documents are
not documentation for these purposes. They cannot be diffed, reviewed, searched, or
merged, and they rot invisibly.

Where a binary artifact is genuinely required — an exported diagram, a screenshot of a
user interface — it lives in the repository beside a Markdown document that explains
it and states what it depicts.

### Rule 2 — Every Document Declares What It Is

A reader arriving at a document with no context must learn, from the top of the file,
what the document is and whether it applies to them.

Every document opens with a single H1 title, followed immediately by its identifying
material. Standards in this library use a fixed skeleton:

```markdown
# Title

**Status:** Active standard
**Applies to:** Who or what this governs.

## Purpose

What this standard is for, what it deliberately excludes, and what it inherits from.

## Rules

### Rule 1 — Short Imperative Title

...

## Required Workflow

Numbered steps, in order.

## Compliance Checklist

- [ ] Checkable statements, one per rule or obligation.
```

A standard may add sections of its own between Purpose and Rules where its subject
warrants one. The required sections, their names, and their order do not change.

Documents that are not standards — architecture notes, setup guides, references — are
not bound to this skeleton, but are bound to the principle: title first, purpose
early, scope stated before detail.

### Rule 3 — Headings Form a Real Hierarchy

One H1 per document, and it is the title. Heading levels descend without skipping —
an H3 never appears directly under an H1.

Headings are written in Title Case and are descriptive rather than decorative:
"Rule 4 — Decisions Belong to the User", not "Some Notes on Decisions". A reader
scanning only the headings should be able to reconstruct the document's argument.

Heading text is stable once published. Headings are anchors, and rewriting one breaks
every link that points to it.

### Rule 4 — Structure Matches Content

Each structure carries a different kind of information, and the wrong one obscures the
content it holds:

| Structure | Use for |
|---|---|
| Prose | Reasoning, rationale, and anything with a "because" in it. |
| Ordered list | Sequences where the order is the point — workflows, procedures. |
| Unordered list | Sets of peers where order carries no meaning. |
| Table | Enumerable facts with consistent fields across rows. |
| Fenced code block | Anything to be typed, run, or copied verbatim. |
| Blockquote | Pointers to authority held elsewhere, and asides that are not the main line. |

Prose is the default. A document that is entirely bullet points has usually discarded
the reasoning that made it worth writing.

### Rule 5 — Code and Commands Are Fenced and Labelled

Every fenced block carries a language hint — `bash`, `powershell`, `json`, `markdown`.
Unlabelled fences lose syntax highlighting and hide what kind of thing is inside.

Commands are shown exactly as they are run, in the shell they are run in. Where a
project supports more than one shell, the document says which one each block assumes
rather than leaving the reader to discover it by failure.

Inline code formatting is used for file names, paths, commands, variable names, and
literal values, so that they survive being read quickly.

### Rule 6 — Paths Are Repository-Relative and Links Are Verified

Paths in documentation are relative to the repository root — `docs/decisions/`, not an
absolute path from one machine. Absolute paths do not survive being cloned, moved, or
read by anyone else.

Every link is checked against the repository before the document is presented or
committed. A link to a file that does not exist is a defect, whether it points at a
document not yet written or one that has since moved.

Where a document must refer to something not yet created, it refers to the containing
directory rather than inventing a filename that may never exist.

### Rule 7 — Terminology Is Fixed

One concept, one term, used consistently across every document in the repository.

Where this library has established a term, that term is used and not paraphrased:
*standard*, *rule*, *decision*, *assumption*, *explicit approval*, *the assistant*,
*the user*. Synonyms invented for variety make documents look inconsistent and make
search fail.

A term with a specific meaning in this repository is defined once, in the document
that owns it, and referenced from elsewhere rather than redefined.

### Rule 8 — Write for the Reader Who Arrives Cold

Documentation is written for someone with no memory of the conversation that produced
it — a future session, a teammate, or the user months later.

That means: present tense, direct statements, and the subject named rather than
implied. State the rule, then the reason. Say what must happen, not what would ideally
be nice. Avoid filler openings, restatements of the heading, and closing summaries
that add nothing.

Documents in this library refer to *the assistant* and *the user* rather than
addressing the reader as "you", so that a rule reads the same whoever encounters it.

### Rule 9 — Nothing Fabricated

A document contains only what is true of the repository as it exists.

No placeholder prose standing in for content not yet written. No example output that
was never produced. No file paths, commands, or configuration invented to look
plausible without being checked. No described behaviour that has not been verified.

Where a document must include material that is provisional, it is labelled as
provisional in the document itself. Unmarked content is a claim of fact.

## Required Workflow

Before creating or editing any document:

1. **Read the existing document**, in full, if it already exists. Establish its
   structure, terminology, and conventions before adding to it.
2. **Read a neighbouring document** of the same kind, and match it. Consistency across
   the set outranks local preference.
3. **Draft**, applying Rules 1–9.
4. **Self-review** against the Compliance Checklist below, and fix what fails.
5. **Verify every link and path** against the repository.
6. **Present or commit** only after steps 4 and 5 have actually been performed.

## Compliance Checklist

A document produced under this standard satisfies all of the following:

- [ ] It is Markdown, committed in the repository.
- [ ] It opens with a single H1 and states its purpose and scope before its detail.
- [ ] Standards follow the fixed skeleton: Status, Applies to, Purpose, Rules, Required Workflow, Compliance Checklist.
- [ ] Heading levels descend without skipping; headings are Title Case and descriptive.
- [ ] Structure matches content — tables for enumerable facts, ordered lists for sequences, prose for reasoning.
- [ ] Every fenced block carries a language hint.
- [ ] Every path is repository-relative; every link was verified to resolve.
- [ ] Established terminology is used without paraphrase.
- [ ] Nothing in it is placeholder, invented, or unverified without being labelled as provisional.

A document that fails any item is incomplete, however finished it appears.
