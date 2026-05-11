# agent-seed

`agent-seed` is a lightweight, markdown-first starting point for making software and research repositories easier and safer for coding agents to work in.

It provides reusable repository guidance for:

- how an agent should approach work,
- when an agent should plan before editing,
- what standards an agent should preserve,
- what "done" means,
- how an agent should handle security, tools, evidence, and uncertainty,
- how high-rigor projects should request specialist review,
- and which reusable prompts and templates can guide common tasks.

This is not an agent platform, installer, skill pack, CI framework, or replacement for project-specific tooling. It is a seed: small enough to copy into a repository, concrete enough to improve agent behavior, and easy to adapt to local conventions.

## Why This Exists

Coding agents work better when repositories provide clear local guidance. Without that guidance, users often need to repeat the same instructions at the start of each session:

- inspect the repository before editing,
- keep diffs narrow,
- follow existing patterns,
- add or update tests,
- run relevant checks,
- do not weaken quality gates,
- update documentation when behavior changes,
- handle security-sensitive actions deliberately,
- explain what was validated,
- and be honest about remaining uncertainty.

`agent-seed` turns those repeated instructions into persistent repository guidance.

## What This Is

`agent-seed` is:

- **lightweight**: markdown files only,
- **portable**: usable across languages, tools, and agent providers,
- **copyable**: easy to add to a new or existing repository,
- **opinionated**: clear about safe engineering behavior,
- **layered**: compact root guidance plus optional deeper modules,
- **non-magical**: no hidden automation or dependencies,
- **local-first**: designed to be customized for the target repository.

## What This Is Not

`agent-seed` is not:

- a package,
- a command-line tool,
- a CI system,
- a pre-commit setup,
- a language-specific style guide,
- a replacement for tests,
- a replacement for code review,
- or a guarantee that an agent will behave perfectly.

The seed gives agents better instructions. Repositories should still use real tooling to enforce formatting, linting, type checking, testing, security, performance, documentation, and release standards.

## v0.2 Structure

v0.2 keeps the root seed markdown-only and dependency-free. It adds optional depth without turning `AGENTS.md` into a manual.

Core guidance is always useful:

```text
AGENTS.md
.agent/WORKFLOW.md
.agent/STANDARDS.md
.agent/DONE.md
.agent/PROMPTS.md
.agent/LOCAL_CONTEXT.example.md
```

High-rigor repositories should also consider:

```text
.agent/QUALITY_BAR.md
.agent/SECURITY.md
.agent/ADAPTERS.md
.agent/REVIEW_PROTOCOL.md
.agent/NESTED_GUIDANCE.md
selected .agent/DOMAINS/*
.agent/TEMPLATES/*
```

Optional domain overlays should be copied only when relevant. They are intended for projects where correctness, safety, reproducibility, performance, or scientific validity requires more discipline than generic software guidance.

## Recommended Target Repository Layout

When adopted in another repository, the full high-rigor layout is:

```text
TARGET_REPOSITORY/
  AGENTS.md
  .agent/
    WORKFLOW.md
    STANDARDS.md
    DONE.md
    QUALITY_BAR.md
    SECURITY.md
    ADAPTERS.md
    REVIEW_PROTOCOL.md
    NESTED_GUIDANCE.md
    PROMPTS.md
    LOCAL_CONTEXT.md
    DOMAINS/
      README.md
      AI_ML.md
      SYSTEMS_KERNELS.md
      ACCELERATORS.md
      COMPILERS.md
      QUANTUM.md
      FORMAL_VERIFICATION.md
      ROBOTICS_AUTONOMY.md
      FRONTENDS.md
      AUTONOMOUS_RESEARCH.md
    TEMPLATES/
      EXEC_PLAN.md
      DESIGN_NOTE.md
      REPO_AUDIT.md
      REVIEW.md
      SPECIALIST_REVIEW.md
      THREAT_MODEL.md
      BUG_REPORT.md
      BENCHMARK_NOTE.md
      HARDWARE_BENCHMARK.md
      CHANGE_SUMMARY.md
      DOCS_UPDATE.md
      DOMAIN_OVERLAY_ADOPTION.md
      MODEL_CARD.md
      DATASET_CARD.md
      EVAL_REPORT.md
      EXPERIMENT_LOG.md
      TRAINING_RUN.md
      INFERENCE_DEPLOYMENT.md
      DATA_PROVENANCE.md
      RESEARCH_CLAIM.md
      FORMAL_PROOF_NOTE.md
      INTERFACE_CONTRACT.md
      SAFETY_CASE.md
```

`LOCAL_CONTEXT.md` should be created by copying `.agent/LOCAL_CONTEXT.example.md` and replacing the generic entries with facts about the target repository.

## Quick Adoption

From this repository, copy the seed files into a target repository:

```bash
mkdir -p /path/to/target-repo/.agent
cp AGENTS.md /path/to/target-repo/AGENTS.md
cp .agent/WORKFLOW.md /path/to/target-repo/.agent/WORKFLOW.md
cp .agent/STANDARDS.md /path/to/target-repo/.agent/STANDARDS.md
cp .agent/DONE.md /path/to/target-repo/.agent/DONE.md
cp .agent/PROMPTS.md /path/to/target-repo/.agent/PROMPTS.md
cp .agent/LOCAL_CONTEXT.example.md /path/to/target-repo/.agent/LOCAL_CONTEXT.md
cp -R .agent/TEMPLATES /path/to/target-repo/.agent/TEMPLATES
```

For high-rigor repositories, also copy the high-rigor core files:

```bash
cp .agent/QUALITY_BAR.md /path/to/target-repo/.agent/QUALITY_BAR.md
cp .agent/SECURITY.md /path/to/target-repo/.agent/SECURITY.md
cp .agent/ADAPTERS.md /path/to/target-repo/.agent/ADAPTERS.md
cp .agent/REVIEW_PROTOCOL.md /path/to/target-repo/.agent/REVIEW_PROTOCOL.md
cp .agent/NESTED_GUIDANCE.md /path/to/target-repo/.agent/NESTED_GUIDANCE.md
```

Copy domain overlays only when they match real repository work:

```bash
mkdir -p /path/to/target-repo/.agent/DOMAINS
cp .agent/DOMAINS/README.md /path/to/target-repo/.agent/DOMAINS/README.md
cp .agent/DOMAINS/AI_ML.md /path/to/target-repo/.agent/DOMAINS/AI_ML.md
```

The `AI_ML.md` command is an example. Select the actual overlays from `.agent/DOMAINS/README.md`; do not copy every overlay by default.

Then edit:

```text
/path/to/target-repo/AGENTS.md
/path/to/target-repo/.agent/LOCAL_CONTEXT.md
```

Add the target repository's real commands, conventions, constraints, active domain overlays, agent/tool permissions, and validation expectations. Do not invent commands that do not exist.

## Core Files

### `AGENTS.md`

The compact operating agreement. This is the first file a coding agent should read. It defines principles, required behavior, planning triggers, validation expectations, and final response expectations.

### `.agent/WORKFLOW.md`

The practical workflow for non-trivial changes: inspect, plan, implement, validate, review, summarize. It includes security and specialist-review triggers for high-risk work.

### `.agent/STANDARDS.md`

General engineering standards for correctness, maintainability, tests, dependencies, documentation, performance, security, infrastructure, scientific work, and agent behavior.

### `.agent/DONE.md`

A clear definition of done, including evidence, validation, review, reproducibility, risk, and final response requirements.

### `.agent/QUALITY_BAR.md`

The high-rigor standard for principal or distinguished engineer/scientist-level work. It defines the evidence ladder used when ordinary inspection is not enough.

### `.agent/SECURITY.md`

Agentic AI, tool, MCP, secrets, memory/context, supply-chain, autonomy, and audit guidance.

### `.agent/ADAPTERS.md`

How to adapt the seed to Codex, Claude Code, Gemini CLI, GitHub Copilot, Cursor, Aider, and generic agents without duplicating conflicting instructions.

### `.agent/REVIEW_PROTOCOL.md`

Self-review, specialist review, subagent review, adversarial review, integration review, and disagreement handling.

### `.agent/NESTED_GUIDANCE.md`

How to use nested `AGENTS.md` files in monorepos or multi-package repositories.

### `.agent/DOMAINS/`

Optional overlays for AI/ML, autonomous research, systems/kernels, accelerators, compilers, quantum, formal verification, robotics/autonomy, and frontends.

### `.agent/PROMPTS.md`

Reusable prompt snippets for common situations such as bootstrapping a repo, auditing agent-readiness, starting a feature, reviewing a diff, debugging a bug, improving documentation, threat modeling, and requesting specialist review.

### `.agent/LOCAL_CONTEXT.example.md`

A template for repository-specific facts: commands, architecture, risky areas, conventions, dependencies, deployment details, active overlays, hardware/runtime environments, safety constraints, and known gaps.

### `.agent/TEMPLATES/`

Reusable templates for plans, design notes, reviews, repo audits, bug reports, benchmark notes, threat models, specialist reviews, AI/ML artifacts, research claims, formal proof notes, interface contracts, safety cases, documentation updates, and final change summaries.

## How To Use With A Coding Agent

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
Review the current diff using .agent/TEMPLATES/REVIEW.md and .agent/REVIEW_PROTOCOL.md. Focus on correctness, tests, unnecessary churn, docs drift, performance risk, security risk, and whether specialist review is required.
```

For high-rigor adoption:

```text
Use AGENTS.md, .agent/QUALITY_BAR.md, .agent/SECURITY.md, .agent/REVIEW_PROTOCOL.md, and the relevant .agent/DOMAINS/* overlays. Produce evidence appropriate to the risk level.
```

For onboarding:

```text
Audit this repository using .agent/TEMPLATES/REPO_AUDIT.md. Do not edit files yet. Identify the canonical commands, main modules, quality gates, risks, active domain overlays, and agent-readiness gaps.
```

## Customization Guidance

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
- active domain overlays,
- agent and tool permission boundaries,
- data, model, and artifact governance,
- hardware and runtime environments,
- safety constraints,
- coding conventions,
- testing conventions,
- documentation conventions,
- release process.

Remove sections that do not apply. Add stricter standards only when the repository has tooling or review practices that can support them.

## Adapter Guidance

Keep `AGENTS.md` as the source-of-truth contract when possible. Use `.agent/ADAPTERS.md` to create lightweight bridge files for tools that need different filenames, such as `CLAUDE.md`, `GEMINI.md`, or Copilot instruction files.

Do not add vendor-specific files to this seed by default. Target repositories should add them only when they actually use that ecosystem and can keep the bridge file synchronized with the seed guidance.

## Maintenance Philosophy

Keep the root guidance small.

The seed should remain:

- easy to read,
- easy to copy,
- easy to delete,
- easy to adapt,
- and useful without any external tooling.

When a repeated workflow becomes too detailed for `AGENTS.md`, move it into `.agent/WORKFLOW.md`, `.agent/STANDARDS.md`, `.agent/SECURITY.md`, `.agent/REVIEW_PROTOCOL.md`, a domain overlay, or a template. Keep `AGENTS.md` compact and practical.

## Version

Current version: see `VERSION`.

## License

This repository is licensed under the MIT License. See `LICENSE`.

The MIT license covers the `agent-seed` content in this repository. Target repositories should keep their own project license and should not replace it accidentally when copying seed guidance.
