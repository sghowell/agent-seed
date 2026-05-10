# Definition of done

This document defines what “done” means for agent-assisted work.

The checklist should be applied proportionally. A small documentation edit does not need the same validation as a schema migration. A risky change needs more evidence than a local typo fix.

## Completion checklist

A change is done when the following are true or explicitly addressed.

## 1. Task completion

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
- smoke tests.

For each check, the final response should state whether it passed, failed, or was not run.

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
- known limitations.

When documentation was not updated, that should be appropriate for the scope of the change.

## 6. Maintainability

- The solution follows local patterns.
- The implementation is understandable.
- Names are clear.
- The change avoids unnecessary abstractions.
- The change avoids unrelated cleanup.
- The diff is reviewable.

## 7. Dependencies

- New dependencies are avoided unless clearly justified.
- Any new dependency has a documented reason.
- Dependency changes are limited to what the task requires.
- Lockfile changes, when present, are expected and understood.

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
- integrations.

Breaking changes are called out explicitly.

## 9. Performance

For performance-sensitive changes:

- baseline behavior was considered,
- benchmark or measurement strategy was identified,
- results were documented when measured,
- tradeoffs were stated,
- and unmeasured performance claims were avoided.

For non-performance-sensitive changes, no benchmark may be needed.

## 10. Security

For security-sensitive changes:

- input validation was considered,
- access control was preserved,
- secrets are not exposed,
- logs do not leak sensitive information,
- failure paths were considered,
- and security assumptions were stated.

## 11. Final self-review

Before finalizing, review the diff for:

- accidental changes,
- missing tests,
- missing docs,
- confusing code,
- behavior drift,
- unnecessary churn,
- risk introduced by dependencies,
- performance concerns,
- security concerns.

## 12. Final response

The final response should include:

```text
Summary:
- Brief bullets describing what changed and why.

Validation:
- Exact checks run and whether they passed.
- Checks not run and why.

Notes:
- Remaining risks, limitations, assumptions, or follow-up work.
```

## Example final response

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

## Not done

A task is not done when:

- code changed but relevant tests were not considered,
- validation failures are hidden,
- the agent claims checks passed without running them,
- public behavior changed without documentation,
- risky changes lack a plan,
- unrelated rewrites obscure the diff,
- or important uncertainty is not reported.
