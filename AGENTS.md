# AGENTS.md

This repository is intended to be maintained with high engineering standards. Coding agents should optimize for correctness, clarity, maintainability, testability, and minimal unnecessary churn.

This file is the first operating guide for agents working in the repository. For more detailed guidance, see the files in `.agent/`.

## Core operating principles

- Understand before editing.
- Prefer narrow, reviewable changes.
- Preserve existing behavior unless the task explicitly asks for behavior change.
- Follow local conventions over generic preferences.
- Add or update tests when behavior changes.
- Update documentation when usage, behavior, architecture, or operational expectations change.
- Do not weaken tests, type checks, linting, benchmarks, documentation checks, CI, or security checks to make a task pass.
- Do not introduce dependencies without a clear reason.
- Do not perform broad rewrites unless the task explicitly requires one.
- Be explicit about assumptions, validation, uncertainty, and remaining risk.

## Read first

Before non-trivial edits, inspect the relevant local context:

```text
README.md
.agent/LOCAL_CONTEXT.md, when present
.agent/WORKFLOW.md
.agent/STANDARDS.md
.agent/DONE.md
relevant source files
relevant tests
relevant docs or examples
```

When `.agent/LOCAL_CONTEXT.md` is missing, infer local conventions from the repository and recommend creating it.

## Canonical commands

Project maintainers should replace this section with real commands for the repository.

Do not invent commands. Use only commands that exist or are clearly documented in the target repository.

```text
Setup:            <fill in, or state not defined>
Format:           <fill in, or state not defined>
Lint:             <fill in, or state not defined>
Type check:       <fill in, or state not defined>
Unit tests:       <fill in, or state not defined>
Integration tests:<fill in, or state not defined>
All checks:       <fill in, or state not defined>
Docs:             <fill in, or state not defined>
Benchmarks:       <fill in, or state not defined>
```

When commands are not documented, inspect the repository for likely commands before asking the user.

## Before editing

For non-trivial tasks:

1. Inspect the relevant files and tests.
2. Identify the smallest safe change.
3. Check existing naming, style, architecture, and test patterns.
4. Identify likely risks.
5. Decide whether a plan is needed.

Do not start with code changes when the task requires architectural judgment, touches many files, changes public behavior, alters data formats, affects performance-sensitive paths, or modifies security-sensitive logic.

## When to write a plan first

Write a short plan before editing when the task involves any of the following:

- multiple modules or subsystems,
- public API changes,
- data model or schema changes,
- migrations,
- authentication or authorization,
- security-sensitive code,
- performance-sensitive code,
- concurrency or distributed systems behavior,
- build, packaging, or deployment changes,
- large refactors,
- ambiguous requirements,
- high risk of regression.

Use `.agent/TEMPLATES/EXEC_PLAN.md` for substantial work.

For small, localized changes, a brief inline plan is enough.

## While editing

- Keep the diff focused on the task.
- Reuse existing patterns before introducing new ones.
- Prefer simple, explicit code over clever code.
- Preserve public interfaces unless the task requires changing them.
- Add comments only when they clarify non-obvious decisions.
- Avoid unrelated cleanup.
- Avoid speculative abstractions.
- Treat generated files, vendored files, migrations, and lockfiles carefully.

## Testing and validation

Before finalizing, run the most relevant checks available in the repository.

At minimum, consider:

- targeted tests for changed behavior,
- broader tests for affected subsystems,
- formatting,
- linting,
- type checking,
- documentation checks,
- benchmarks for performance-sensitive changes,
- security or dependency checks for sensitive changes.

Never claim that a check passed unless it was actually run and passed.

When a check cannot be run, state:

- which check was not run,
- why it was not run,
- what validation was performed instead,
- and what risk remains.

## Definition of done

A change is done only when:

- the requested behavior is implemented,
- the change is as small as practical,
- relevant tests are added or updated,
- relevant checks are run where possible,
- documentation is updated when needed,
- compatibility and migration issues are considered,
- performance-sensitive changes are measured or explicitly scoped,
- security-sensitive changes are reviewed carefully,
- and remaining risks are stated clearly.

See `.agent/DONE.md` for the fuller checklist.

## Final response format

After code changes, final responses should include:

```text
Summary:
- What changed and why.

Validation:
- Checks run and results.

Notes:
- Risks, limitations, follow-up work, or checks not run.
```

Keep the final response concise but specific. Include exact validation commands when available.

## Prohibited shortcuts

Do not:

- remove tests to make a task pass,
- weaken assertions without justification,
- ignore failing checks,
- hide validation failures,
- claim validation that was not performed,
- rewrite broad areas without need,
- introduce dependencies casually,
- change public behavior silently,
- delete documentation because it is stale instead of updating it,
- or treat this guidance as a substitute for local repository facts.

## Useful supporting files

```text
.agent/WORKFLOW.md                  Step-by-step workflow for substantial changes.
.agent/STANDARDS.md                 Engineering standards.
.agent/DONE.md                      Definition of done.
.agent/PROMPTS.md                   Reusable prompts.
.agent/LOCAL_CONTEXT.md             Repository-specific context, when present.
.agent/TEMPLATES/EXEC_PLAN.md       Plan template.
.agent/TEMPLATES/REVIEW.md          Review template.
.agent/TEMPLATES/REPO_AUDIT.md      Repository audit template.
```
