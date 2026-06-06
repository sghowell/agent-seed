# Agent Workflow

This workflow guides coding agents through safe, reviewable work.

Use the full workflow for substantial changes. For tiny changes, use the same principles in a lighter form.

## Workflow Summary

```text
1. Understand the task.
2. Inspect the repository.
3. Refresh current external sources when the task depends on fast-moving facts.
4. Identify the smallest safe change.
5. Plan when risk warrants planning.
6. Use clean git and PR/MR workflow for branch, commit, review, merge, push, and cleanup work.
7. Model security and safety risk when relevant.
8. Implement narrowly.
9. Validate with relevant checks.
10. Review the diff.
11. Request specialist review when risk warrants it.
12. Summarize honestly.
```

## 1. Understand The Task

Before editing, clarify the actual objective.

Identify:

- the requested outcome,
- explicit constraints from the user,
- implicit constraints from the repository,
- likely affected files,
- expected behavior change,
- active domain overlays,
- security, privacy, safety, performance, or scientific risks,
- and what would count as success.

When the task is ambiguous but progress is still possible, make a reasonable assumption, state it, and proceed carefully. Ask for clarification only when the ambiguity blocks safe progress.

## 2. Inspect The Repository

Before changing code, inspect enough context to avoid accidental damage.

Look for:

- README or onboarding docs,
- local agent guidance,
- `.agent/LOCAL_CONTEXT.md`,
- active domain overlays,
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

## 3. Refresh Current External Sources When Needed

Refresh current sources before planning or editing when the task depends on information that can drift.

Refresh is required for:

- agent ecosystem behavior,
- tool, MCP, plugin, skill, or adapter behavior,
- security guidance,
- laws, standards, policies, or compliance requirements,
- model, dataset, benchmark, or hardware claims,
- package, API, framework, runtime, or cloud-provider behavior,
- public product behavior,
- release, deployment, pricing, or availability facts.

Prefer primary sources: official documentation, specifications, standards, release notes, project repositories, research papers, benchmark reports, or source-of-truth project docs.

Record:

- source title,
- URL or local path,
- date checked,
- relevant version or publication date,
- what decision depends on the source,
- uncertainty or drift risk.

Do not freeze stale assumptions into repository guidance when a current primary source is practical to check.

## 4. Identify The Smallest Safe Change

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

## 5. Decide Whether To Plan First

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
- agent/tool/MCP/autonomy changes,
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
- domain overlays,
- validation strategy,
- security or safety model when relevant,
- specialist review plan,
- risks,
- rollback or mitigation approach,
- and open questions.

For a small localized change, a short inline plan is sufficient.

## 6. Use Clean Git And PR/MR Workflow

For branch, commit, PR/MR, merge, push, or cleanup work, use `.agent/GIT_AND_MR_WORKFLOW.md`.

At minimum:

- preserve existing user changes,
- use a feature branch for non-trivial work,
- keep commits focused and descriptive,
- stage only intentional files unless the user confirms the whole worktree is in scope,
- validate before publishing,
- use PR/MR review when required or expected,
- merge only when policy and checks allow it,
- push the merged result when the user asked for full closeout,
- confirm hosted checks when they exist,
- and clean up branches only after the merged result is verified.

Do not stop at a local commit, branch push, or PR/MR creation when the user requested merge, push, CI confirmation, and cleanup.

## 7. Model Security And Safety Risk

For agent, MCP/tool, identity, secrets, network, sandbox, data, model, privacy, physical-world, or production-adjacent changes, create or update a threat model before implementation.

Use `.agent/SECURITY.md` and `.agent/TEMPLATES/THREAT_MODEL.md`.

Security-sensitive work should identify:

- assets,
- trust boundaries,
- actors and identities,
- tools and permissions,
- untrusted inputs,
- prompt-injection or goal-hijack risks,
- memory or context poisoning risks,
- data exfiltration paths,
- secrets and privacy risks,
- supply-chain provenance,
- approval boundaries,
- mitigations,
- validation,
- residual risk.

Request specialist or adversarial review when the change is high-risk.

## 8. Implement Narrowly

During implementation:

- edit only files required for the task,
- preserve existing style,
- prefer simple code,
- keep public behavior stable unless changing it is the goal,
- update nearby tests,
- update docs when usage or behavior changes,
- avoid adding dependencies unless clearly justified,
- preserve security, privacy, and safety boundaries,
- and keep the working tree understandable.

When a discovered issue is outside the task, note it separately instead of fixing it opportunistically.

## 9. Validate

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
- smoke tests,
- fuzzing or property tests,
- formal checks,
- browser or visual checks,
- simulation or hardware checks.

Choose checks based on risk and scope.

For example:

- A one-line documentation change may only require inspection or a docs check.
- A parser change may require unit tests, negative tests, and fuzz or property tests.
- A performance change may require a benchmark before and after.
- A security-sensitive change may require threat modeling, abuse cases, and adversarial review.
- A robotics or autonomy change may require simulation evidence and explicit approval before hardware or field use.
- An AI/ML change may require dataset, model, eval, and reproducibility evidence.

Never claim a check passed unless it was actually run and passed.

## 10. Review The Diff

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
- incomplete cleanup,
- incomplete evidence,
- and unresolved review findings.

Use `.agent/TEMPLATES/REVIEW.md` for a structured review.

## 11. Request Specialist Review When Needed

Use `.agent/REVIEW_PROTOCOL.md` for review lanes, reviewer instructions, and disagreement handling.

Specialist review is triggered by:

- security-sensitive code,
- agent/tool/MCP/autonomy changes,
- AI/ML model, data, training, inference, or eval work,
- kernel, unsafe, driver, firmware, or low-level systems work,
- concurrency or distributed systems behavior,
- accelerator, hardware, or performance-sensitive kernels,
- compiler, language, runtime, or semantic changes,
- formal proof, theorem, or model-checking work,
- robotics, actuation, autonomy, or safety work,
- user-facing frontend workflow or accessibility changes,
- broad documentation or source-of-truth rewrites.

If specialist review is not available, record the gap and compensate with stronger local evidence where practical.

## 12. Summarize Honestly

Final summaries should be brief but evidence-based.

Include:

- what changed,
- why it changed,
- what validation was run,
- what failed or could not be run,
- what review was performed or deferred,
- and what risks remain.

Do not overstate certainty. Do not hide failures. Do not imply that unrun checks passed.

## Handling Failures

When validation fails:

1. Read the failure carefully.
2. Determine whether the failure is caused by the change.
3. Fix failures within the task scope.
4. Rerun relevant checks when practical.
5. Report any remaining failures clearly.

Do not weaken checks or tests to make failures disappear.

## Handling Uncertainty

When unsure:

- inspect more local context,
- prefer reversible changes,
- make assumptions explicit,
- choose narrower changes,
- identify validation that would reduce uncertainty,
- and label unvalidated claims as assumptions.

When uncertainty affects correctness, security, safety, or scientific validity, state it clearly.

## Handling Local Conventions

Local repository conventions take priority over generic guidance.

Examples:

- Use the repository's existing test framework.
- Use the repository's existing formatter.
- Use the repository's existing error handling style.
- Use the repository's existing naming conventions.
- Use the repository's existing documentation style.

When local conventions are unclear, infer them from nearby code and mention the inference.

## Handling Generated, Vendored, Or External Files

Be careful with files that may not be intended for direct editing.

Before editing generated, vendored, or external files, look for:

- generation scripts,
- comments indicating generated status,
- lockfile conventions,
- vendor directories,
- submodules,
- codegen configuration,
- schema generation tools,
- model or dataset provenance,
- license and redistribution constraints.

Prefer editing the source that generates the file.

## Handling Dependencies

Before adding a dependency, consider:

- whether existing dependencies can solve the problem,
- whether a small local implementation is safer,
- package maturity,
- license implications,
- security risk,
- maintenance burden,
- transitive dependencies,
- performance impact,
- compatibility with existing tooling,
- supply-chain provenance,
- and whether the dependency is needed in production or only development.

Document the reason for any new production dependency.

## Handling Documentation

Documentation should change when user-visible behavior, APIs, architecture, setup, operations, examples, assumptions, or evidence requirements change.

Documentation updates should be:

- accurate,
- minimal,
- located where users will find them,
- consistent with existing style,
- and honest about limitations.

Use `.agent/TEMPLATES/DOCS_UPDATE.md` for structured documentation updates.

## Handling Performance-Sensitive Changes

For performance-sensitive work:

- identify the hot path,
- establish a baseline when practical,
- measure after the change,
- avoid relying only on intuition,
- document benchmark commands and environment,
- document workload and variance,
- preserve correctness validation,
- and state limitations of the measurement.

Use `.agent/TEMPLATES/BENCHMARK_NOTE.md` or `.agent/TEMPLATES/HARDWARE_BENCHMARK.md` for structured performance notes.

## Handling Bugs

For bug fixes:

- reproduce or characterize the bug,
- identify the root cause when practical,
- add a regression test when possible,
- fix the smallest cause,
- validate the fix,
- and document remaining uncertainty.

Use `.agent/TEMPLATES/BUG_REPORT.md` for structured bug work.
