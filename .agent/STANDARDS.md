# Engineering standards

These standards define the default expectations for agent-assisted work in this repository.

They are intentionally generic. Project-specific standards should be added to `.agent/LOCAL_CONTEXT.md` or to this file after adoption.

## 1. Correctness

Correctness is the first priority.

Agents should:

- understand expected behavior before changing code,
- preserve existing behavior unless asked to change it,
- add regression coverage for bug fixes when practical,
- test important edge cases,
- treat error handling as part of correctness,
- and avoid making correctness depend on undocumented assumptions.

Agents should not:

- silently change public behavior,
- remove validation without replacement,
- ignore existing tests,
- or rely on superficial inspection when tests are available.

## 2. Maintainability

Changes should be easy for future maintainers to understand.

Prefer:

- simple control flow,
- clear names,
- local reasoning,
- explicit data structures,
- small functions with clear responsibilities,
- and comments that explain non-obvious choices.

Avoid:

- cleverness without need,
- speculative abstractions,
- broad rewrites,
- hidden coupling,
- copy-paste without justification,
- and mixing unrelated changes.

## 3. Minimal churn

A good diff changes what is necessary and little else.

Avoid:

- unrelated formatting changes,
- unnecessary file moves,
- renaming things unrelated to the task,
- touching generated files manually,
- changing lockfiles unnecessarily,
- and broad refactors disguised as small fixes.

Small cleanup is acceptable only when it directly supports the task and does not obscure the main change.

## 4. Tests

Tests should provide confidence that the change works and does not regress important behavior.

For behavior changes, agents should look for existing tests and add or update coverage.

Consider:

- unit tests for local behavior,
- integration tests for boundary behavior,
- regression tests for bugs,
- edge-case tests for tricky logic,
- property tests where invariants matter,
- snapshot or golden tests where appropriate,
- benchmark tests for performance-sensitive behavior.

Do not:

- delete tests to make a change pass,
- weaken assertions without justification,
- update snapshots blindly,
- ignore flaky tests without documenting the issue,
- or claim test coverage that does not exist.

## 5. Validation

Validation should match the risk of the change.

For each task, identify relevant checks such as:

- targeted tests,
- full tests,
- formatting,
- linting,
- type checking,
- static analysis,
- documentation build,
- examples,
- benchmarks,
- migration checks,
- security checks,
- dependency checks.

Report exactly what was run.

When validation is incomplete, explain why and identify the remaining risk.

## 6. Documentation

Documentation should stay aligned with behavior.

Update documentation when changing:

- setup steps,
- commands,
- public APIs,
- user-facing behavior,
- configuration,
- examples,
- architecture,
- deployment expectations,
- data formats,
- migration requirements,
- limitations.

Documentation should be clear, discoverable, and consistent with existing style.

Do not add long documentation where a concise update is enough.

## 7. Dependencies

Dependencies increase maintenance burden and risk.

Before adding a dependency, consider:

- whether existing code or dependencies can solve the problem,
- whether the dependency is actively maintained,
- licensing,
- security history,
- transitive dependencies,
- package size,
- performance implications,
- compatibility with existing tooling,
- and whether the dependency is needed in production or only development.

Document the reason for new production dependencies.

Do not add dependencies for trivial functionality without strong justification.

## 8. Public interfaces

Treat public interfaces carefully.

Public interfaces may include:

- exported functions,
- APIs,
- CLIs,
- configuration formats,
- environment variables,
- database schemas,
- file formats,
- documented behavior,
- event formats,
- network protocols.

When changing public interfaces:

- identify compatibility impact,
- update tests,
- update documentation,
- provide migration notes when needed,
- and avoid silent breaking changes.

## 9. Error handling

Error handling should be deliberate.

Agents should:

- preserve existing error handling conventions,
- avoid swallowing errors silently,
- make errors actionable when practical,
- test important failure paths,
- and avoid leaking sensitive information in errors.

Do not replace specific errors with vague errors unless there is a clear reason.

## 10. Security

Security-sensitive changes require extra care.

Security-sensitive areas may include:

- authentication,
- authorization,
- sessions,
- secrets,
- cryptography,
- permissions,
- sandboxing,
- input validation,
- deserialization,
- file system access,
- network access,
- dependency updates,
- logging,
- and data privacy.

Agents should:

- identify security-sensitive paths before editing,
- avoid logging secrets or personal data,
- validate untrusted input,
- preserve access controls,
- avoid weakening security checks,
- and report security assumptions clearly.

## 11. Performance

Performance work should be evidence-based.

For performance-sensitive changes:

- identify the performance goal,
- identify the hot path,
- measure baseline behavior when practical,
- measure after the change,
- document benchmark commands,
- document environment limitations,
- and avoid trading correctness for speed.

Do not assume a change improves performance without measurement when measurement is practical.

## 12. Concurrency and distributed behavior

Concurrency and distributed systems changes are high-risk.

Consider:

- races,
- deadlocks,
- ordering,
- idempotency,
- retries,
- timeouts,
- cancellation,
- partial failure,
- backpressure,
- consistency,
- resource leaks,
- and observability.

Add targeted tests or reasoning for important concurrent behavior when practical.

## 13. Data and migrations

Data changes should be explicit and reversible when possible.

For schema, migration, or format changes:

- identify compatibility impact,
- consider existing data,
- define migration path,
- update tests,
- update docs,
- consider rollback,
- and avoid destructive changes without clear instruction.

## 14. Build, packaging, and infrastructure

Build and infrastructure changes can affect every contributor.

When changing build, packaging, or infrastructure files:

- inspect existing workflows,
- preserve local developer experience,
- preserve CI behavior unless changing it is the task,
- avoid unnecessary dependency upgrades,
- document command changes,
- and validate with relevant commands.

## 15. Scientific, numerical, or research code

For scientific or numerical work, distinguish claims from evidence.

Agents should consider:

- units,
- dimensions,
- coordinate systems,
- numerical tolerances,
- random seeds,
- reproducibility,
- baseline comparisons,
- analytic test cases,
- data provenance,
- experiment configuration,
- and limitations of results.

Do not overstate conclusions from weak evidence.

## 16. Agent behavior

Agents should be transparent collaborators.

Agents should:

- explain assumptions,
- report validation honestly,
- identify uncertainty,
- avoid unnecessary questions when local inspection can answer them,
- ask for clarification when safe progress is blocked,
- and keep final responses useful for review.

Agents should not:

- pretend to have run checks,
- hide failures,
- make broad changes without need,
- invent project facts,
- or ignore local guidance.
