# Review Protocol

This protocol defines how agent-assisted work should be reviewed. Apply it proportionally: a small documentation fix may only need self-review, while high-risk work may require specialist, adversarial, and integration review.

## Review Layers

### Self-Review

Required for all changes.

The implementing agent should inspect the final diff for:

- correctness,
- missing tests or validation,
- documentation drift,
- unnecessary churn,
- compatibility impact,
- performance risk,
- security risk,
- incomplete cleanup,
- unvalidated claims.

### Peer Or Specialist Review

Required for high-risk or domain-specific work.

Specialist review should be requested when the change affects an area where ordinary application-code review is not enough. Use `.agent/TEMPLATES/SPECIALIST_REVIEW.md`.

### Adversarial Review

Required for security, autonomy, data/model, privacy, and safety-sensitive work.

Adversarial review should try to break assumptions, find abuse paths, identify missing threat boundaries, and challenge the validation evidence.

### Integration Review

Required before finalizing multi-file, multi-module, or multi-domain changes.

Integration review checks that individual pieces work together, source-of-truth docs agree, validation evidence covers the whole change, and final risk is stated.

## Specialist Review Lanes

Use the lane or lanes that match the work:

- Security and agentic AI.
- AI/ML and evaluation.
- Systems, kernel, unsafe code, firmware, and drivers.
- Accelerators and performance.
- Compilers, language semantics, and runtimes.
- Quantum computing.
- Formal verification and mathematics.
- Robotics, autonomy, and safety.
- Frontend, product, accessibility, and visual behavior.
- Documentation and source-of-truth consistency.

## Subagent Review Rules

When subagents or independent agent reviewers are available:

- use fresh context for independent review when possible,
- give reviewers exact scope, files, source-of-truth docs, checks, and expected output,
- assign disjoint review lanes when multiple reviewers are used,
- ask reviewers to inspect evidence, not just summaries,
- require findings first, ordered by severity,
- allow reviewers to say `insufficient evidence`,
- preserve reviewer uncertainty,
- and keep final accountability with the integrating agent or maintainer.

Do not delegate destructive, production, credential, legal, privacy, or safety decisions away from the maintainer or integrating agent.

## Reviewer Brief Template

Give specialist reviewers:

```text
Review lane:
Goal:
Scope:
Files to inspect:
Source-of-truth docs:
Diff or artifacts:
Validation evidence:
Known risks:
Expected output template:
```

## Findings Format

Findings should lead. Each finding should include:

- severity,
- file/path or artifact reference,
- concrete issue,
- why it matters,
- suggested fix or required evidence.

Avoid burying blockers under general commentary.

## Disagreement Policy

If reviewers disagree:

- preserve both positions,
- identify the evidence each position relies on,
- identify what evidence would resolve the disagreement,
- let the stricter safety, security, or correctness position govern until the maintainer decides,
- record accepted risk in final notes, a design record, or release evidence.

## Accountability

Review improves evidence; it does not move accountability away from the person or agent integrating the change.

Before finalizing, the integrating agent or maintainer should confirm:

- required review lanes were completed or explicitly deferred,
- blocking findings were resolved,
- accepted risks are recorded,
- validation evidence is accurate,
- and final notes do not overstate certainty.
