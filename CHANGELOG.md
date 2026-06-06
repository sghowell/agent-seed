# Changelog

## 0.2.5

Corrected adapter adoption guidance so the seed optimizes for maintainers' actual agent workflows instead of irrelevant vendor ecosystems.

Included:

- reusable git and PR/MR workflow guidance for branch, commit, review, merge, push, hosted-check, and cleanup work,
- standard adoption references for `.agent/GIT_AND_MR_WORKFLOW.md`,
- local-context fields for branch naming, commit style, PR/MR requirements, merge strategy, hosted checks, and cleanup,
- explicit relevance gate for agent adapter files,
- first-class mention of Codex/OpenAI agents, Hermes Agent, Claude Code, Pi, and OpenCode,
- primary/default agent fields so repositories can weight guidance toward the most-used agent,
- second-priority agent fields and local context for Hermes Agent, Pi, and Claude Code,
- explicit lower-priority classification for other ecosystems so they do not constrain defaults,
- project-local context recording that `agent-seed` itself is Codex-first and AGENTS.md-first,
- explicit willingness to prefer Codex strength over broad multi-agent compatibility for this seed,
- demotion of Copilot-specific files to optional bridges only when Copilot is actually used,
- local-context and repo-audit fields for supported, unused, and deferred agent ecosystems.

## 0.2.4

Corrected the v0.2.3 review-fix release after a follow-up review.

Included:

- corrected MCP authorization server endpoint guidance to require HTTPS,
- kept localhost handling scoped to redirect URI risk controls,
- required advertised `S256` PKCE support when the client is technically capable,
- recorded v0.2.3 execution evidence.

## 0.2.3

Corrected the v0.2.2 review-fix release after a follow-up review.

Included:

- explicit MCP `authorization_servers` metadata and selection guidance,
- explicit MCP PKCE metadata, `S256`, state, and open-redirect checks,
- expanded threat-model fields for authorization-code and metadata risks,
- completed v0.2.2 implementation-plan tracking evidence.

## 0.2.2

Corrected the v0.2.1 review-fix release after a follow-up review.

Included:

- updated MCP authorization guidance for the latest `2025-11-25` specification,
- current-source refresh fields in the threat-model template,
- clearer distinction between `AGENTS.md` source-of-truth files and vendor bridge files,
- repaired `zsh`-safe validation commands in the v0.2.1 implementation plan.

## 0.2.1

Corrected and tightened the v0.2 guidance after review.

Included:

- safer quick and standard adoption instructions that copy only relevant domain overlays,
- narrower local Aider ignore rules that preserve shared configuration,
- current-source refresh guidance for fast-moving ecosystems, standards, APIs, security guidance, and benchmark claims,
- MCP authorization/security checklist coverage,
- mapping to the Five Eyes/NSA agentic AI risk taxonomy and lifecycle language,
- updated GitHub Copilot adapter guidance for repository, path-specific, and agent instructions.

## 0.2.0

Expanded `agent-seed` from a compact generic seed into a layered high-rigor guidance set.

Included:

- explicit elite quality bar guidance,
- agentic AI and tool security guidance,
- adapter guidance for major coding-agent ecosystems,
- nested and monorepo guidance,
- specialist and subagent review protocol,
- optional domain overlays,
- stronger benchmark, AI/ML, research, formal methods, and safety templates,
- adoption guidance for license handling and high-rigor repositories.

The v0.2 release remains markdown-only, dependency-free, and intentionally free of package metadata, installers, lockfiles, CI configuration, generated docs, and vendor-specific root agent files.

## 0.1.1

Restored the repository MIT license and updated the README license note.

## 0.1.0

Initial lightweight `agent-seed` release.

Included:

- root `AGENTS.md` operating agreement,
- adoption guide,
- workflow guidance,
- engineering standards,
- definition of done,
- reusable prompt snippets,
- local context example,
- templates for execution plans, design notes, repo audits, reviews, bug reports, benchmark notes, change summaries, and documentation updates.

The initial release is intentionally markdown-only and tool-agnostic.
