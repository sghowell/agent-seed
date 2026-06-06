# Local Repository Context

Copy this file to:

```text
.agent/LOCAL_CONTEXT.md
```

Then replace the template fields with facts about the target repository.

Do not invent commands or conventions. Mark unknowns clearly.

## Project Summary

```text
Project name: <fill in>
Purpose: <fill in>
Primary users: <fill in>
Current maturity: <prototype | internal tool | production | research | unknown>
Quality bar level: <minimal | standard | high-rigor | safety-critical | unknown>
```

## Repository Structure

Describe the major directories and files.

```text
<directory or file>: <purpose>
<directory or file>: <purpose>
<directory or file>: <purpose>
```

## Active Domain Overlays

List overlays copied or adopted from `.agent/DOMAINS/`.

```text
Active domain overlays:
- <overlay>: <why it applies and what it covers>
- <overlay>: <why it applies and what it covers>

Deferred overlays:
- <overlay>: <why it does not currently apply>
```

## Specialist Review Lanes

```text
Required lanes:
- <lane>: <trigger>
- <lane>: <trigger>

Optional lanes:
- <lane>: <when useful>
```

## Agent And Tool Permission Boundaries

```text
Allowed without approval: <commands, tools, paths, or actions>
Requires approval: <destructive, external, production, credential, privacy, safety, or financial actions>
Denied: <files, tools, commands, paths, networks, or actions>
Agent/tool identity: <what identity agents use, if any>
MCP/tool servers: <approved servers and scope>
```

## Supported Agent Ecosystems

List only the agents and coding tools maintainers actually use. Do not add bridge files or workflow rules for unused ecosystems just to be comprehensive.

```text
Primary/default agent: <Codex/OpenAI, Hermes Agent, Claude Code, Pi, OpenCode, Gemini CLI, GitHub Copilot, Cursor, Aider, other, or unknown>
Second-priority agents/tools: <Codex/OpenAI, Hermes Agent, Pi, Claude Code, OpenCode, Gemini CLI, GitHub Copilot, Cursor, Aider, other>
Lower-priority agents/tools: <agents/tools used occasionally or in narrow contexts>
Primary source of truth: <AGENTS.md/.agent/other>
Bridge files intentionally present: <CLAUDE.md, GEMINI.md, .github/copilot-instructions.md, opencode.json, other, or none>
Unused or deferred ecosystems: <tools not optimized for and why>
Adapter behavior checked on: <date and source, or not checked>
```

## Git And Review Workflow

Record the repository's real branch, commit, PR/MR, merge, push, and cleanup expectations. Use `.agent/GIT_AND_MR_WORKFLOW.md` as the reusable baseline and customize this section with local facts.

```text
Default branch: <main/master/other>
Feature branch naming: <pattern or not defined>
Commit style: <convention or not defined>
PR/MR required before merge: <yes/no/conditional/unknown>
Default PR/MR state: <draft/ready/not defined>
Merge strategy: <fast-forward/merge commit/squash/rebase/platform-managed/not defined>
Local pre-push checks: <commands or not defined>
Hosted checks/CI: <system and required checks, or not defined>
Post-merge validation: <commands or not defined>
Branch cleanup: <local/remote policy or not defined>
Release notes or changelog: <when required or not defined>
```

## Canonical Commands

Use real commands only.

```text
Setup:             <command or not defined>
Run locally:       <command or not defined>
Format:            <command or not defined>
Lint:              <command or not defined>
Type check:        <command or not defined>
Unit tests:        <command or not defined>
Integration tests: <command or not defined>
All tests:         <command or not defined>
All checks:        <command or not defined>
Docs:              <command or not defined>
Benchmarks:        <command or not defined>
Build/package:     <command or not defined>
Security checks:   <command or not defined>
Formal checks:     <command or not defined>
Hardware checks:   <command or not defined>
```

## Main Modules

```text
<module>: <responsibility>
<module>: <responsibility>
<module>: <responsibility>
```

## Architecture Notes

Summarize important architecture facts.

```text
<fill in>
```

## Data Flow

Describe important data flow, request flow, or execution flow.

```text
<fill in>
```

## Data, Model, And Artifact Governance

```text
Data sources: <fill in or none known>
Data licenses: <fill in or none known>
Model artifacts: <fill in or none known>
Generated artifacts: <fill in or none known>
Retention policy: <fill in or not defined>
Privacy constraints: <fill in or none known>
Reproducibility requirements: <fill in or not defined>
```

## Hardware And Runtime Environments

```text
Supported operating systems: <fill in>
CPU architectures: <fill in>
GPU/accelerator hardware: <fill in or none known>
Drivers/firmware/runtime: <fill in or none known>
Distributed/runtime topology: <fill in or none known>
Simulation environments: <fill in or none known>
Hardware/runtime environments: <fill in or none known>
```

## Safety-Sensitive Operations

```text
Safety-sensitive operations: <operations or none known>
Approval required before: <operations>
Operator override or rollback: <mechanism or not defined>
Field-test or production admission: <criteria or not defined>
```

## Public Interfaces

List interfaces that require compatibility care.

```text
APIs: <fill in or none known>
CLIs: <fill in or none known>
Config files: <fill in or none known>
Schemas: <fill in or none known>
File formats: <fill in or none known>
Environment variables: <fill in or none known>
External integrations: <fill in or none known>
Model/data artifacts: <fill in or none known>
Hardware interfaces: <fill in or none known>
```

## Testing Conventions

Describe how tests are organized and what kinds of tests are expected.

```text
<fill in>
```

## Documentation Conventions

Describe documentation locations and expectations.

```text
<fill in>
```

## Style Conventions

Describe naming, formatting, error handling, logging, and other local style expectations.

```text
<fill in>
```

## Dependency Conventions

Describe dependency policy.

```text
<fill in>
```

## Risky Areas

List files, modules, or behaviors that require extra care.

```text
<area>: <reason>
<area>: <reason>
<area>: <reason>
```

## Performance-Sensitive Areas

```text
<area>: <reason and relevant benchmark, if known>
<area>: <reason and relevant benchmark, if known>
```

## Security-Sensitive Areas

```text
<area>: <reason>
<area>: <reason>
```

## Generated, Vendored, Or External Files

List files that agents should avoid editing directly.

```text
<path>: <how it is generated or maintained>
<path>: <how it is generated or maintained>
```

## Release Or Deployment Notes

```text
<fill in>
```

## Known Pitfalls

```text
<pitfall>: <how to avoid it>
<pitfall>: <how to avoid it>
```

## Open Questions

Track missing local context that should be filled in later.

```text
<question>
<question>
<question>
```
