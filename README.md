# agent-seed

`agent-seed` is a lightweight, markdown-first starting point for making software repositories easier and safer for coding agents to work in.

It provides a small set of reusable files that establish:

- how an agent should approach work,
- when an agent should plan before editing,
- what standards an agent should preserve,
- what “done” means,
- how an agent should report validation and uncertainty,
- and which reusable prompts and templates can guide common tasks.

This is not an agent platform, installer, skill pack, CI framework, or replacement for project-specific tooling. It is a seed: small enough to copy into a repository, concrete enough to improve agent behavior, and easy to adapt to local conventions.

## Why this exists

Coding agents work better when repositories provide clear local guidance. Without that guidance, users often need to repeat the same instructions at the start of each session:

- inspect the repository before editing,
- keep diffs narrow,
- follow existing patterns,
- add or update tests,
- run relevant checks,
- do not weaken quality gates,
- update documentation when behavior changes,
- explain what was validated,
- and be honest about remaining uncertainty.

`agent-seed` turns those repeated instructions into persistent repository guidance.

## What this is

`agent-seed` is:

- **lightweight**: mostly a small set of markdown files,
- **portable**: usable across languages, tools, and agent providers,
- **copyable**: easy to add to a new or existing repository,
- **opinionated**: clear about safe engineering behavior,
- **non-magical**: no hidden automation or dependencies,
- **local-first**: designed to be customized for the target repository.

## What this is not

`agent-seed` is not:

- a package,
- a command-line tool,
- a CI system,
- a pre-commit setup,
- a language-specific style guide,
- a replacement for tests,
- a replacement for code review,
- or a guarantee that an agent will behave perfectly.

The seed gives agents better instructions. Repositories should still use real tooling to enforce formatting, linting, type checking, testing, security, performance, and documentation standards.

## Recommended target repository layout

When adopted in another repository, the recommended layout is:

```text
TARGET_REPOSITORY/
  AGENTS.md
  .agent/
    WORKFLOW.md
    STANDARDS.md
    DONE.md
    PROMPTS.md
    LOCAL_CONTEXT.md
    TEMPLATES/
      EXEC_PLAN.md
      DESIGN_NOTE.md
      REPO_AUDIT.md
      REVIEW.md
      BUG_REPORT.md
      BENCHMARK_NOTE.md
      CHANGE_SUMMARY.md
      DOCS_UPDATE.md
```

`LOCAL_CONTEXT.md` should be created by copying `.agent/LOCAL_CONTEXT.example.md` and replacing the placeholders with facts about the target repository.

## Quick adoption

From this repository, copy the seed files into a target repository:

```bash
cp AGENTS.md /path/to/target-repo/AGENTS.md
cp -R .agent /path/to/target-repo/.agent
cp .agent/LOCAL_CONTEXT.example.md /path/to/target-repo/.agent/LOCAL_CONTEXT.md
```

Then edit:

```text
/path/to/target-repo/AGENTS.md
/path/to/target-repo/.agent/LOCAL_CONTEXT.md
```

Add the target repository's real commands, conventions, and constraints. Do not invent commands that do not exist.

## Core files

### `AGENTS.md`

The compact operating agreement. This is the first file a coding agent should read. It defines principles, required behavior, planning triggers, and final response expectations.

### `.agent/WORKFLOW.md`

The practical workflow for non-trivial changes: inspect, plan, implement, validate, review, summarize.

### `.agent/STANDARDS.md`

General engineering standards for correctness, maintainability, tests, dependencies, documentation, performance, security, and infrastructure.

### `.agent/DONE.md`

A clear definition of done, including validation and final response requirements.

### `.agent/PROMPTS.md`

Reusable prompt snippets for common situations such as bootstrapping a repo, auditing agent-readiness, starting a feature, reviewing a diff, debugging a bug, and improving documentation.

### `.agent/LOCAL_CONTEXT.example.md`

A template for repository-specific facts: commands, architecture, risky areas, conventions, dependencies, deployment details, and known constraints.

### `.agent/TEMPLATES/`

Reusable templates for plans, design notes, reviews, repo audits, bug reports, benchmark notes, documentation updates, and final change summaries.

## How to use with a coding agent

After adopting the seed, a user can give shorter instructions such as:

```text
Use the repo guidance in AGENTS.md. Inspect the relevant files first, keep the change narrow, and report validation honestly.
```

For larger work:

```text
Use AGENTS.md and .agent/WORKFLOW.md. Create an execution plan using .agent/TEMPLATES/EXEC_PLAN.md before editing.
```

For review:

```text
Review the current diff using .agent/TEMPLATES/REVIEW.md. Focus on correctness, tests, unnecessary churn, docs drift, performance risk, and security risk.
```

For onboarding:

```text
Audit this repository using .agent/TEMPLATES/REPO_AUDIT.md. Do not edit files yet. Identify the canonical commands, main modules, quality gates, risks, and agent-readiness gaps.
```

## Customization guidance

The seed is intentionally generic. After copying it into a target repository, customize it.

Add local facts such as:

- setup commands,
- test commands,
- formatting commands,
- linting commands,
- type-checking commands,
- benchmark commands,
- documentation commands,
- deployment constraints,
- architectural boundaries,
- important modules,
- known risky areas,
- security-sensitive paths,
- performance-sensitive paths,
- coding conventions,
- testing conventions,
- documentation conventions,
- release process.

Remove sections that do not apply. Add stricter standards only when the repository has tooling or review practices that can support them.

## Maintenance philosophy

Keep the seed small.

The seed should remain:

- easy to read,
- easy to copy,
- easy to delete,
- easy to adapt,
- and useful without any external tooling.

When a repeated workflow becomes too detailed for `AGENTS.md`, move it into `.agent/WORKFLOW.md`, `.agent/STANDARDS.md`, or a template. Keep `AGENTS.md` compact and practical.

## Version

Current version: see `VERSION`.

## License

This repository is licensed under the MIT License. See `LICENSE`.
