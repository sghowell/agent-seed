# Definition Of Done

This document defines what "done" means for agent-assisted work.

The checklist should be applied proportionally. A small documentation edit does not need the same validation as a schema migration. A risky change needs more evidence than a local typo fix.

## Completion Checklist

A change is done when the following are true or explicitly addressed.

## 1. Task Completion

- The requested change has been implemented.
- The implementation matches the user's actual objective.
- Non-goals were not accidentally included.
- The change is no broader than necessary.

## 2. Correctness

- Existing behavior is preserved unless intentionally changed.
- New behavior is covered by tests or otherwise validated.
- Important edge cases were considered.
- Failure modes were considered.
- Public behavior changes are documented.
- Unvalidated claims are labeled as assumptions.

## 3. Tests

- Relevant existing tests were identified.
- Tests were added or updated for behavior changes when practical.
- Bug fixes include regression coverage when practical.
- Tests were not removed or weakened to make the change pass.
- Snapshot or golden updates were reviewed rather than accepted blindly.

## 4. Validation

Relevant checks were run where possible.

Possible checks:

- targeted tests,
- full test suite,
- formatting,
- linting,
- type checking,
- docs build,
- examples,
- benchmark or performance checks,
- security checks,
- dependency checks,
- migration checks,
- smoke tests,
- fuzzing or property checks,
- formal checks,
- simulation, hardware, browser, or visual checks.

For each check, the final response should state whether it passed, failed, or was not run.

Final evidence must match the risk. High-risk work should not be closed with low-strength evidence unless the maintainer explicitly accepts the risk.

## 5. Documentation

Documentation was updated when the change affected:

- setup,
- commands,
- APIs,
- configuration,
- examples,
- user-visible behavior,
- architecture,
- deployment,
- data formats,
- known limitations,
- security or safety boundaries,
- evaluation or benchmark interpretation.

When documentation was not updated, that should be appropriate for the scope of the change.

## 6. Maintainability

- The solution follows local patterns.
- The implementation is understandable.
- Names are clear.
- The change avoids unnecessary abstractions.
- The change avoids unrelated cleanup.
- The diff is reviewable.

## 7. Dependencies And Supply Chain

- New dependencies are avoided unless clearly justified.
- Any new dependency has a documented reason.
- Dependency changes are limited to what the task requires.
- Lockfile changes, when present, are expected and understood.
- Package, model, dataset, binary, prompt, skill, hook, or MCP server provenance is considered where relevant.

## 8. Compatibility

Compatibility was considered for:

- public APIs,
- command-line behavior,
- config files,
- schemas,
- migrations,
- environment variables,
- persisted data,
- documented examples,
- integrations,
- model or dataset artifacts,
- hardware, firmware, runtime, or compiler versions.

Breaking changes are called out explicitly.

## 9. Performance

For performance-sensitive changes:

- baseline behavior was considered,
- benchmark or measurement strategy was identified,
- results were documented when measured,
- workload, environment, variance, and limitations were recorded,
- correctness checks were preserved,
- and unmeasured performance claims were avoided.

For non-performance-sensitive changes, no benchmark may be needed.

## 10. Security

For security-sensitive changes:

- input validation was considered,
- access control was preserved,
- least privilege and least agency were considered,
- secrets are not exposed,
- logs do not leak sensitive information,
- untrusted external content is treated as data rather than instructions,
- memory and context poisoning risks were considered,
- destructive action approval boundaries were respected,
- failure paths were considered,
- auditability was considered,
- and security assumptions were stated.

## 11. Reproducibility

For research, AI/ML, numerical, benchmark, hardware, or scientific work:

- commands are recorded,
- source data and artifacts are identified,
- versions and environment are recorded,
- seeds and tolerances are recorded where relevant,
- hardware and runtime topology are recorded where relevant,
- negative or inconclusive results are not hidden,
- and another expert has enough context to reproduce or challenge the result.

## 12. Specialist Review

Specialist, adversarial, or integration review is complete or explicitly deferred when the work is high-risk.

Review evidence should identify:

- review lane,
- scope reviewed,
- files or artifacts inspected,
- validation evidence inspected,
- blocking issues,
- non-blocking issues,
- evidence gaps,
- final recommendation,
- reviewer uncertainty.

Use `.agent/REVIEW_PROTOCOL.md` and `.agent/TEMPLATES/SPECIALIST_REVIEW.md`.

## 13. Rollback And Recovery

Rollback or recovery has been considered for high-risk changes.

This may include:

- reverting a commit,
- feature flags,
- migration rollback,
- model or dataset rollback,
- production deploy rollback,
- hardware disable path,
- operator override,
- backup restoration,
- incident response notes.

## 14. Final Self-Review

Before finalizing, review the diff for:

- accidental changes,
- missing tests,
- missing docs,
- confusing code,
- behavior drift,
- unnecessary churn,
- risk introduced by dependencies,
- performance concerns,
- security concerns,
- source-of-truth drift,
- unresolved reviewer findings,
- and incomplete risk notes.

## 15. Final Response

The final response should include:

```text
Summary:
- Brief bullets describing what changed and why.

Validation:
- Exact checks run and whether they passed.
- Checks not run and why.

Notes:
- Remaining risks, limitations, assumptions, review status, or follow-up work.
```

## Example Final Response

```text
Summary:
- Added validation for empty project names before project creation.
- Added regression tests covering empty and whitespace-only names.
- Updated the CLI help text to describe the validation rule.

Validation:
- Passed: pytest tests/test_project_create.py
- Passed: ruff check src tests
- Not run: full integration suite; it requires the local test database, which is not configured in this environment.

Notes:
- Remaining risk is limited to database-backed creation paths not covered by the targeted CLI tests.
```

## Not Done

A task is not done when:

- code changed but relevant tests were not considered,
- validation failures are hidden,
- the agent claims checks passed without running them,
- public behavior changed without documentation,
- risky changes lack a plan,
- security or safety boundaries changed without review,
- research or benchmark claims lack reproducibility metadata,
- unrelated rewrites obscure the diff,
- important uncertainty is not reported,
- or specialist review was required but neither completed nor explicitly deferred.
