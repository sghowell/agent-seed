# Agent workflow

This workflow guides coding agents through safe, reviewable work.

Use the full workflow for substantial changes. For tiny changes, use the same principles in a lighter form.

## Workflow summary

```text
1. Understand the task.
2. Inspect the repository.
3. Identify the smallest safe change.
4. Plan when risk warrants planning.
5. Implement narrowly.
6. Validate with relevant checks.
7. Review the diff.
8. Summarize honestly.
```

## 1. Understand the task

Before editing, clarify the actual objective.

Identify:

- the requested outcome,
- explicit constraints from the user,
- implicit constraints from the repository,
- likely affected files,
- expected behavior change,
- and what would count as success.

When the task is ambiguous but progress is still possible, make a reasonable assumption, state it, and proceed carefully. Ask for clarification only when the ambiguity blocks safe progress.

## 2. Inspect the repository

Before changing code, inspect enough context to avoid accidental damage.

Look for:

- README or onboarding docs,
- local agent guidance,
- package or build files,
- existing tests,
- examples,
- existing implementation patterns,
- naming conventions,
- error handling conventions,
- dependency patterns,
- performance-sensitive areas,
- security-sensitive areas,
- generated or vendored files.

Do not assume a convention before checking whether the repository already has one.

## 3. Identify the smallest safe change

Prefer the smallest coherent change that solves the task.

A good change is:

- focused,
- easy to review,
- consistent with existing patterns,
- covered by appropriate validation,
- and free of unrelated cleanup.

Avoid:

- broad rewrites,
- speculative abstractions,
- style churn,
- drive-by dependency changes,
- unnecessary file moves,
- and changes to unrelated behavior.

## 4. Decide whether to plan first

A plan is required when the change is substantial or risky.

Use a plan for:

- multi-file or multi-module changes,
- architectural changes,
- public API changes,
- data model changes,
- schema changes,
- migrations,
- performance-sensitive changes,
- security-sensitive changes,
- concurrency changes,
- build or deployment changes,
- unclear requirements,
- or large refactors.

Use `.agent/TEMPLATES/EXEC_PLAN.md` for larger plans.

A plan should include:

- goal,
- non-goals,
- current state,
- proposed approach,
- affected files,
- validation strategy,
- risks,
- rollback or mitigation approach,
- and open questions.

For a small localized change, a short inline plan is sufficient.

## 5. Implement narrowly

During implementation:

- edit only files required for the task,
- preserve existing style,
- prefer simple code,
- keep public behavior stable unless changing it is the goal,
- update nearby tests,
- update docs when usage or behavior changes,
- avoid adding dependencies unless clearly justified,
- and keep the working tree understandable.

When a discovered issue is outside the task, note it separately instead of fixing it opportunistically.

## 6. Validate

Run the most relevant available checks.

Possible checks include:

- targeted tests,
- full test suite,
- formatting,
- linting,
- type checking,
- docs build,
- examples,
- benchmarks,
- security checks,
- dependency checks,
- migration checks,
- smoke tests.

Choose checks based on risk and scope.

For example:

- A one-line documentation change may only require a markdown or docs check.
- A parser change may require unit tests, edge-case tests, and possibly fuzz or property tests.
- A performance change may require a benchmark before and after.
- A security-sensitive change may require additional review and targeted abuse cases.

Never claim a check passed unless it was actually run and passed.

## 7. Review the diff

Before finalizing, review the diff as if reviewing another engineer's work.

Check for:

- correctness issues,
- missed edge cases,
- missing tests,
- weakened tests,
- unnecessary churn,
- behavior changes not requested,
- dependency risk,
- documentation drift,
- performance regressions,
- security regressions,
- confusing names,
- dead code,
- and incomplete cleanup.

Use `.agent/TEMPLATES/REVIEW.md` for a structured review.

## 8. Summarize honestly

Final summaries should be brief but evidence-based.

Include:

- what changed,
- why it changed,
- what validation was run,
- what failed or could not be run,
- and what risks remain.

Do not overstate certainty. Do not hide failures. Do not imply that unrun checks passed.

## Handling failures

When validation fails:

1. Read the failure carefully.
2. Determine whether the failure is caused by the change.
3. Fix failures within the task scope.
4. Rerun relevant checks when practical.
5. Report any remaining failures clearly.

Do not weaken checks or tests to make failures disappear.

## Handling uncertainty

When unsure:

- inspect more local context,
- prefer reversible changes,
- make assumptions explicit,
- choose narrower changes,
- and identify validation that would reduce uncertainty.

When uncertainty affects correctness or safety, state it clearly.

## Handling local conventions

Local repository conventions take priority over generic guidance.

Examples:

- Use the repository's existing test framework.
- Use the repository's existing formatter.
- Use the repository's existing error handling style.
- Use the repository's existing naming conventions.
- Use the repository's existing documentation style.

When local conventions are unclear, infer them from nearby code and mention the inference.

## Handling generated, vendored, or external files

Be careful with files that may not be intended for direct editing.

Before editing generated, vendored, or external files, look for:

- generation scripts,
- comments indicating generated status,
- lockfile conventions,
- vendor directories,
- submodules,
- codegen configuration,
- schema generation tools.

Prefer editing the source that generates the file.

## Handling dependencies

Before adding a dependency, consider:

- whether existing dependencies can solve the problem,
- whether a small local implementation is safer,
- package maturity,
- license implications,
- security risk,
- maintenance burden,
- transitive dependencies,
- performance impact,
- and compatibility with existing tooling.

Document the reason for any new production dependency.

## Handling documentation

Documentation should change when user-visible behavior, APIs, architecture, setup, operations, or examples change.

Documentation updates should be:

- accurate,
- minimal,
- located where users will find them,
- consistent with existing style,
- and honest about limitations.

Use `.agent/TEMPLATES/DOCS_UPDATE.md` for structured documentation updates.

## Handling performance-sensitive changes

For performance-sensitive work:

- identify the hot path,
- establish a baseline when practical,
- measure after the change,
- avoid relying only on intuition,
- document benchmark commands and environment,
- and state limitations of the measurement.

Use `.agent/TEMPLATES/BENCHMARK_NOTE.md` for structured performance notes.

## Handling bugs

For bug fixes:

- reproduce or characterize the bug,
- identify the root cause when practical,
- add a regression test when possible,
- fix the smallest cause,
- validate the fix,
- and document remaining uncertainty.

Use `.agent/TEMPLATES/BUG_REPORT.md` for structured bug work.
