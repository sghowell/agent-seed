# Local Repository Context

This file describes `agent-seed` itself. Target repositories should create their own `.agent/LOCAL_CONTEXT.md` from `.agent/LOCAL_CONTEXT.example.md`.

## Project Summary

```text
Project name: agent-seed
Purpose: markdown-first repository guidance for safer, more consistent coding-agent work
Primary users: the maintainer and coding agents working with the maintainer
Current maturity: internal tool
Quality bar level: high-rigor
```

## Repository Structure

```text
AGENTS.md: compact operating guide intended to be copied into target repositories
README.md: human-facing overview of the seed
ADOPTION.md: adoption modes and copy/customization workflow
.agent/: supporting guidance, templates, domain overlays, and adapter guidance
docs/superpowers/plans/: retained implementation and review plans
```

## Supported Agent Ecosystems

`agent-seed` is maintained for a Codex-first, AGENTS.md-first workflow. Other ecosystems matter when they are part of the maintainer's real workflow or when a target repository explicitly uses them. If broad multi-agent compatibility conflicts with Codex effectiveness for this repository, prefer Codex effectiveness.

```text
Primary/default agent: Codex/OpenAI agents
Second-priority agents/tools: Hermes Agent, Pi, Claude Code
Lower-priority agents/tools: OpenCode and any other AGENTS-compatible or bridge-based tools, only when specifically relevant
Primary source of truth: AGENTS.md and .agent/
Bridge files intentionally present: none in the seed root
Unused or deferred ecosystems: GitHub Copilot, Gemini CLI, Cursor, and Aider are documented only as optional target-repository bridges when actually used
Adapter behavior checked on: 2026-05-12 against current primary documentation where practical
```

## Canonical Commands

This repository is markdown-only and does not define package, build, test, lint, or docs commands.

```text
Setup:             not defined
Run locally:       not defined
Format:            not defined
Lint:              not defined
Type check:        not defined
Unit tests:        not defined
Integration tests: not defined
All tests:         not defined
All checks:        not defined
Docs:              not defined
Benchmarks:        not defined
Build/package:     not defined
Security checks:   not defined
Formal checks:     not defined
Hardware checks:   not defined
```

## Git And Review Workflow

`agent-seed` uses a Codex-first short-lived feature branch workflow. For non-trivial work, preserve dirty work on a `codex/<short-description>` branch, commit coherent documentation slices, merge locally to `main`, push `main` to GitHub, and verify the remote state. This markdown-only repository has no CI or package checks defined, so validation is by diff review, documentation cross-reference checks, and exact git/remote verification unless future tooling is added.

```text
Default branch: main
Feature branch naming: codex/<short-description>
Commit style: concise descriptive messages
PR/MR required before merge: not currently required for maintainer-requested local closeout
Default PR/MR state: draft when a PR is opened
Merge strategy: fast-forward local merge when possible
Local pre-push checks: no command defined; inspect diff and cross-references
Hosted checks/CI: not currently defined
Post-merge validation: git status, log, and remote branch verification
Branch cleanup: delete local topic branch after pushed main is verified
Release notes or changelog: update CHANGELOG.md and VERSION when publishing seed release guidance
```

## Documentation Conventions

Keep root guidance compact. Put reusable details in `.agent/`, adoption flow in `ADOPTION.md`, and human overview material in `README.md`.

## Risky Areas

```text
Adapter guidance: high drift risk; refresh current primary sources before changing agent-specific behavior.
Adoption copy lists: avoid adding irrelevant files or domain overlays by default.
Root AGENTS.md: avoid bloating it because it is intended to be copied into target repositories.
Seed root: avoid adding vendor-specific bridge files by default.
```

## Known Pitfalls

```text
Vendor bias: do not let Copilot, IDE-specific, or unused-agent conventions shape defaults.
False neutrality: do not weaken Codex guidance merely to keep every agent ecosystem equally supported.
Over-copying: target repositories should copy only relevant overlays and bridge files.
False commands: do not invent validation commands for this markdown-only repository.
```
