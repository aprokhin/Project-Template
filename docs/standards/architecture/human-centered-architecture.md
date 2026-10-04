# Human-Centered Architecture Inheritance Standard

## Status

Required cross-project architecture standard.

## Canonical principle

Projects created from this template inherit the Business & Life Assistant Human-Centered Architecture Principles maintained in:

`aprokhin/Life-Assistant-Agent/docs/human-centered-architecture-principles.md`

The canonical principles include the Human Potential / River Principle, no-permanent-label rule, hypothesis-feedback method, Discovery/Interview boundary, multimodal Voice Agent constraints, Multi-AI Control Center boundary, context/memory requirements, and human-centered UI requirements.

## Project requirement

Every new project must document, in its architecture or root project documentation:

1. whether the project interacts directly with people;
2. how it applies the canonical human-centered principles;
3. which domain constraints bound adaptation (for example safety, legal, accounting, production, quality, permissions, or traceability);
4. which aspects of the user experience may adapt to the person;
5. which canonical facts must never be personalized;
6. how observations about people remain provisional and feedback-testable rather than permanent labels;
7. how relevant context, provenance, and freshness are recovered before consequential reasoning or action.

A project may add stricter domain rules but must not silently contradict the canonical principles.

## Operational UI rule

For user-facing operational software:

**Software adapts to the human wherever adaptation does not compromise the objective requirements of the process.**

**Human adaptation is bounded by process integrity.**

Personalize the path to correct action, not the underlying operational truth.

## Change control

Do not fork or rewrite the platform philosophy independently inside each project. Update the canonical document when the platform principle changes, then update project-specific application notes only where the change affects that domain.
