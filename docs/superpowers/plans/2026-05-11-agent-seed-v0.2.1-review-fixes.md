# Agent Seed v0.2.1 Review Fixes Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Address the six post-v0.2 review findings while keeping `agent-seed` markdown-only, dependency-free, and careful about optional domain overlay adoption.

**Architecture:** Treat this as a corrective v0.2.1 documentation release. Keep root guidance compact, make adoption behavior safer, tighten current ecosystem/security guidance, and add a research-refresh workflow hook without adding tooling, CI, package metadata, lockfiles, generated docs, or vendor root configs.

**Tech Stack:** Markdown files only plus shell validation with `find`, `rg`, `wc`, and `git`.

---

## Review Findings To Address

1. Standard and quick adoption still copy every domain overlay.
2. `.gitignore` may block shared Aider configuration.
3. The planned research-refresh hook is missing from workflow guidance.
4. MCP security guidance is directionally correct but lacks current protocol-specific requirements.
5. Agentic-security guidance is not mapped to current Five Eyes/NSA risk categories and lifecycle language.
6. GitHub Copilot adapter guidance under-specifies current `AGENTS.md` agent-instruction support.

## Source References

Use these references while implementing. They were checked on May 11, 2026; re-check them during implementation if any source has changed or if implementation happens later.

- AGENTS.md format, nearest-file precedence, Aider bridge, and Gemini bridge: https://agents.md/
- OpenAI Codex AGENTS.md behavior and evidence expectations: https://openai.com/index/introducing-codex/
- GitHub Copilot repository instructions and agent instructions: https://docs.github.com/en/copilot/how-tos/copilot-on-github/customize-copilot/add-custom-instructions/add-repository-instructions
- Claude Code memory and settings: https://docs.claude.com/en/docs/claude-code/memory and https://docs.claude.com/en/docs/claude-code/settings
- Gemini CLI context files and configurable `context.fileName`: https://google-gemini.github.io/gemini-cli/docs/cli/gemini-md.html
- MCP authorization specification: https://modelcontextprotocol.io/specification/2025-06-18/basic/authorization
- OWASP Top 10 for Agentic Applications 2026: https://genai.owasp.org/resource/owasp-top-10-for-agentic-applications-for-2026/
- OWASP Agentic Skills Top 10: https://owasp.org/www-project-agentic-skills-top-10/
- NSA/Five Eyes guidance, “Careful Adoption of Agentic AI Services”: https://www.nsa.gov/Press-Room/Press-Releases-Statements/Press-Release-View/Article/4475134/nsa-joins-the-asds-acsc-and-others-to-release-guidance-on-agentic-artificial-in/

## File Structure

### Modify Existing Files

- `VERSION`: bump from `0.2.0` to `0.2.1`.
- `CHANGELOG.md`: add a `0.2.1` corrective release section.
- `README.md`: make quick adoption copy core files and templates, with selected overlays only.
- `ADOPTION.md`: make Mode 2 and standard adoption avoid copying all domain overlays by default.
- `.gitignore`: replace broad `.aider*` ignore with local-state patterns that preserve shared Aider configuration.
- `.agent/ADAPTERS.md`: tighten Copilot and Aider adapter guidance, and verify Gemini guidance still reflects current context-file behavior.
- `.agent/WORKFLOW.md`: add current-source/research refresh step and update numbering.
- `.agent/SECURITY.md`: add Five Eyes/NSA risk taxonomy mapping, lifecycle mapping, and MCP-specific security checklist.
- `.agent/TEMPLATES/THREAT_MODEL.md`: add MCP authorization, Five Eyes/NSA category, and current-source fields.
- `.agent/TEMPLATES/REPO_AUDIT.md`: add checks for standard adoption overlay restraint and current-source freshness.
- `.agent/TEMPLATES/EXEC_PLAN.md`: add a current-source refresh section.
- `.agent/PROMPTS.md`: add prompts for current-source refresh, MCP authorization review, and agentic risk taxonomy mapping.

### Do Not Create

- No CLI.
- No installer.
- No package manifest.
- No lockfile.
- No generated docs.
- No `.github/` files.
- No root `CLAUDE.md`, `GEMINI.md`, `.aider.conf.yml`, `.claude/`, or `.gemini/`.

---

## Task 0: Preflight And Branch Setup

**Files:**
- No content edits expected.

- [ ] **Step 1: Confirm clean `main`**

Run:

```bash
git status --short --branch
git switch main
git pull --ff-only
git status --short --branch
```

Expected:

- `main` is clean.
- `main` is aligned with `origin/main`.
- No uncommitted user changes are present.

- [ ] **Step 2: Create the implementation branch**

Run:

```bash
git switch -c agent-seed-v0.2.1-review-fixes
```

Expected:

- Work is isolated on `agent-seed-v0.2.1-review-fixes`.

---

## Task 1: Version And Changelog

**Files:**
- Modify: `VERSION`
- Modify: `CHANGELOG.md`

- [ ] **Step 1: Bump `VERSION`**

Replace the entire file with:

```text
0.2.1
```

- [ ] **Step 2: Add `CHANGELOG.md` section**

Add this section above `## 0.2.0`:

```markdown
## 0.2.1

Corrected and tightened the v0.2 guidance after review.

Included:

- safer quick and standard adoption instructions that copy only relevant domain overlays,
- narrower local Aider ignore rules that preserve shared configuration,
- current-source refresh guidance for fast-moving ecosystems, standards, APIs, security guidance, and benchmark claims,
- MCP authorization/security checklist coverage,
- mapping to the Five Eyes/NSA agentic AI risk taxonomy and lifecycle language,
- updated GitHub Copilot adapter guidance for repository, path-specific, and agent instructions.
```

- [ ] **Step 3: Validate version metadata**

Run:

```bash
rg -n "0\\.2\\.1|0\\.2\\.0" VERSION CHANGELOG.md
git diff --check
```

Expected:

- `VERSION` contains `0.2.1`.
- `CHANGELOG.md` has `0.2.1` above `0.2.0`.
- `git diff --check` exits 0.

- [ ] **Step 4: Commit**

```bash
git add VERSION CHANGELOG.md
git commit -m "Bump version for v0.2.1 corrections"
```

---

## Task 2: Fix Adoption Overlay Copy Semantics

**Files:**
- Modify: `README.md`
- Modify: `ADOPTION.md`

- [ ] **Step 1: Replace README quick adoption command block**

In `README.md`, replace the command block under `## Quick Adoption` with:

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

- [ ] **Step 2: Add README selected-overlays note**

Immediately after the quick adoption command block, add:

````markdown
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
````

- [ ] **Step 3: Replace ADOPTION Mode 2 copy block**

In `ADOPTION.md`, replace the Mode 2 `Copy:` block with:

```text
AGENTS.md
.agent/WORKFLOW.md
.agent/STANDARDS.md
.agent/DONE.md
.agent/PROMPTS.md
.agent/LOCAL_CONTEXT.example.md
.agent/TEMPLATES/
```

- [ ] **Step 4: Update Mode 2 explanatory text**

Replace:

```text
This mode gives agents the full lightweight seed: workflow, standards, prompts, templates, and local context.
```

with:

```text
This mode gives agents the full lightweight seed: workflow, standards, prompts, templates, and local context. It does not copy domain overlays by default.
```

- [ ] **Step 5: Replace standard adoption copy commands**

In `ADOPTION.md`, replace the command block under `### 1. Copy The Files` with:

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

- [ ] **Step 6: Add explicit overlay copy example to ADOPTION**

Replace:

```text
For high-rigor adoption, remove domain overlays that do not apply after copying or copy only the relevant overlays.
```

with:

````markdown
For high-rigor adoption, copy high-rigor core files and only the relevant overlays:

```bash
cp .agent/QUALITY_BAR.md /path/to/target-repo/.agent/QUALITY_BAR.md
cp .agent/SECURITY.md /path/to/target-repo/.agent/SECURITY.md
cp .agent/REVIEW_PROTOCOL.md /path/to/target-repo/.agent/REVIEW_PROTOCOL.md
cp .agent/ADAPTERS.md /path/to/target-repo/.agent/ADAPTERS.md
cp .agent/NESTED_GUIDANCE.md /path/to/target-repo/.agent/NESTED_GUIDANCE.md
mkdir -p /path/to/target-repo/.agent/DOMAINS
cp .agent/DOMAINS/README.md /path/to/target-repo/.agent/DOMAINS/README.md
cp .agent/DOMAINS/AI_ML.md /path/to/target-repo/.agent/DOMAINS/AI_ML.md
```

The `AI_ML.md` command is an example. Select the overlays that match actual repository work.
````

- [ ] **Step 7: Validate adoption semantics**

Run:

```bash
rg -n "cp -R \\.agent|selected \\.agent/DOMAINS|do not copy every overlay|does not copy domain overlays" README.md ADOPTION.md
git diff --check
```

Expected:

- `README.md` and `ADOPTION.md` no longer instruct standard/quick adopters to copy all of `.agent/`.
- High-rigor adoption still documents selected overlays.
- `git diff --check` exits 0.

- [ ] **Step 8: Commit**

```bash
git add README.md ADOPTION.md
git commit -m "Fix overlay adoption guidance"
```

---

## Task 3: Narrow Aider Ignore Rules And Adapter Guidance

**Files:**
- Modify: `.gitignore`
- Modify: `.agent/ADAPTERS.md`
- Modify: `ADOPTION.md`

- [ ] **Step 1: Replace broad Aider ignore**

In `.gitignore`, replace:

```gitignore
.aider*
```

with:

```gitignore
.aider.chat.history.md
.aider.input.history
.aider.tags.cache.v4/
!.aider.conf.yml
```

- [ ] **Step 2: Tighten Aider adapter section**

In `.agent/ADAPTERS.md`, replace the `## Aider` section with:

````markdown
## Aider

Configure Aider to read `AGENTS.md` through shared project configuration when the target repository uses Aider.

Recommended `.aider.conf.yml` bridge:

```yaml
read:
  - AGENTS.md
  - .agent/LOCAL_CONTEXT.md
```

High-rigor tasks may add selected `.agent/*` files to Aider's read context. Do not ignore `.aider.conf.yml`; it can be shared repository guidance. Ignore only local chat history, input history, tags caches, and other machine-local Aider state.

For short tasks, ensure the Aider context includes:

```text
AGENTS.md
.agent/LOCAL_CONTEXT.md
relevant source files
relevant tests
```
````

- [ ] **Step 3: Update ADOPTION adapter list**

In `ADOPTION.md`, replace:

```text
- Aider read-file configuration.
```

with:

```text
- `.aider.conf.yml` for shared Aider read-file configuration.
```

- [ ] **Step 4: Validate Aider guidance**

Run:

```bash
rg -n "\\.aider\\*|\\.aider\\.conf\\.yml|aider\\.chat|Aider" .gitignore .agent/ADAPTERS.md ADOPTION.md
git diff --check
```

Expected:

- No `.aider*` ignore remains.
- `.aider.conf.yml` is explicitly allowed.
- `.agent/ADAPTERS.md` says `.aider.conf.yml` can be shared guidance.

- [ ] **Step 5: Commit**

```bash
git add .gitignore .agent/ADAPTERS.md ADOPTION.md
git commit -m "Preserve shared Aider configuration"
```

---

## Task 4: Add Current-Source Refresh Workflow

**Files:**
- Modify: `.agent/WORKFLOW.md`
- Modify: `.agent/TEMPLATES/EXEC_PLAN.md`
- Modify: `.agent/TEMPLATES/REPO_AUDIT.md`
- Modify: `.agent/PROMPTS.md`

- [ ] **Step 1: Update workflow summary**

In `.agent/WORKFLOW.md`, replace the workflow summary block with:

```text
1. Understand the task.
2. Inspect the repository.
3. Refresh current external sources when the task depends on fast-moving facts.
4. Identify the smallest safe change.
5. Plan when risk warrants planning.
6. Model security and safety risk when relevant.
7. Implement narrowly.
8. Validate with relevant checks.
9. Review the diff.
10. Request specialist review when risk warrants it.
11. Summarize honestly.
```

- [ ] **Step 2: Add current-source refresh section**

Add this section after `## 2. Inspect The Repository`:

```markdown
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
```

- [ ] **Step 3: Renumber later workflow headings**

Renumber the following headings in `.agent/WORKFLOW.md`:

```text
## 3. Identify The Smallest Safe Change -> ## 4. Identify The Smallest Safe Change
## 4. Decide Whether To Plan First -> ## 5. Decide Whether To Plan First
## 5. Model Security And Safety Risk -> ## 6. Model Security And Safety Risk
## 6. Implement Narrowly -> ## 7. Implement Narrowly
## 7. Validate -> ## 8. Validate
## 8. Review The Diff -> ## 9. Review The Diff
## 9. Request Specialist Review When Needed -> ## 10. Request Specialist Review When Needed
## 10. Summarize Honestly -> ## 11. Summarize Honestly
```

- [ ] **Step 4: Update `EXEC_PLAN.md`**

In `.agent/TEMPLATES/EXEC_PLAN.md`, add this section after `## 5. Active Domain Overlays` and renumber following headings:

````markdown
## 6. Current-Source Refresh

```text
Sources checked:
- <source title and URL or local path>
Date checked:
Version or publication date:
Decision depending on source:
Drift risk:
```
````

When implementing, keep the existing template style. The angle-bracket fields are intentional template fields.

- [ ] **Step 5: Update `REPO_AUDIT.md`**

In `.agent/TEMPLATES/REPO_AUDIT.md`, add this field under `## 13. Agent-Readiness Assessment`:

```text
Current-source refresh guidance: <rating>
```

Add this field under `## 15. Suggested Seed Adoption`:

```text
Current-source refresh needs: <sources or none>
```

- [ ] **Step 6: Add prompt**

In `.agent/PROMPTS.md`, add this prompt before `## 44. Final Pre-Submit Review` and renumber following prompt headings:

````markdown
## 44. Current-Source Refresh

```text
Use .agent/WORKFLOW.md. Before planning or editing, refresh current primary sources for any facts that can drift: agent ecosystem behavior, MCP/tool behavior, security guidance, standards, APIs, package behavior, model/data/benchmark claims, hardware/runtime behavior, laws, or release facts. Record source title, URL or local path, date checked, version or publication date, decision depending on the source, and remaining drift risk.
```
````

- [ ] **Step 7: Validate current-source coverage**

Run:

```bash
rg -n "current-source|current external sources|date checked|drift risk|primary sources|fast-moving" .agent/WORKFLOW.md .agent/TEMPLATES/EXEC_PLAN.md .agent/TEMPLATES/REPO_AUDIT.md .agent/PROMPTS.md
git diff --check
```

Expected:

- Workflow includes a current-source refresh step.
- Execution plan and audit templates capture source freshness.
- Prompt library includes a current-source refresh prompt.

- [ ] **Step 8: Commit**

```bash
git add .agent/WORKFLOW.md .agent/TEMPLATES/EXEC_PLAN.md .agent/TEMPLATES/REPO_AUDIT.md .agent/PROMPTS.md
git commit -m "Add current-source refresh guidance"
```

---

## Task 5: Add MCP Authorization Checklist

**Files:**
- Modify: `.agent/SECURITY.md`
- Modify: `.agent/TEMPLATES/THREAT_MODEL.md`
- Modify: `.agent/PROMPTS.md`

- [ ] **Step 1: Add MCP checklist to `.agent/SECURITY.md`**

Add this subsection after the existing `## Tool And MCP Security` bullets:

```markdown
### MCP Authorization Checklist

For HTTP-based MCP servers and clients, verify:

- authorization follows the current MCP authorization specification when supported,
- resource indicators identify the intended MCP server,
- access tokens are audience-bound to the MCP server that receives them,
- MCP servers reject tokens issued for other resources,
- tokens are not passed through to downstream services,
- access tokens are sent in authorization headers rather than URI query strings,
- authorization and protected-resource metadata discovery are handled deliberately,
- PKCE protects authorization-code flows,
- redirect URIs are exact-registered and limited to HTTPS or localhost,
- refresh tokens and stored credentials are protected and rotated where supported,
- invalid or expired tokens receive the expected authorization failure response,
- logs, traces, screenshots, and final summaries do not expose tokens.
```

- [ ] **Step 2: Add MCP fields to threat model**

In `.agent/TEMPLATES/THREAT_MODEL.md`, add this section after `## Tools And Permissions`:

````markdown
## MCP Authorization

```text
HTTP-based MCP involved: <yes/no>
Authorization spec version: <version/date or not applicable>
Resource indicator: <intended MCP server resource or not applicable>
Token audience validation: <validation plan or not applicable>
Token passthrough prevented: <yes/no/not applicable>
PKCE required: <yes/no/not applicable>
Redirect URI policy: <exact HTTPS/localhost policy or not applicable>
Token storage and logging controls: <controls>
```
````

The angle-bracket fields are intentional template fields.

- [ ] **Step 3: Add MCP authorization prompt**

In `.agent/PROMPTS.md`, add this prompt after `## 15. MCP Or Tool Review`:

````markdown
## 16. MCP Authorization Review

```text
Use .agent/SECURITY.md and .agent/TEMPLATES/THREAT_MODEL.md. Review this MCP integration for resource indicators, audience-bound tokens, token passthrough prevention, authorization-header token use, metadata discovery, PKCE, exact redirect URI handling, HTTPS or localhost redirect constraints, token storage, token logging, and scoped credentials. Findings first, ordered by severity.
```
````

Renumber later prompt headings.

- [ ] **Step 4: Validate MCP coverage**

Run:

```bash
rg -n "resource indicators|audience-bound|token passthrough|authorization headers|PKCE|redirect URI|MCP Authorization" .agent/SECURITY.md .agent/TEMPLATES/THREAT_MODEL.md .agent/PROMPTS.md
git diff --check
```

Expected:

- MCP authorization checklist appears in security guidance.
- Threat model captures MCP-specific authorization facts.
- Prompt library has a dedicated MCP authorization review.

- [ ] **Step 5: Commit**

```bash
git add .agent/SECURITY.md .agent/TEMPLATES/THREAT_MODEL.md .agent/PROMPTS.md
git commit -m "Add MCP authorization checklist"
```

---

## Task 6: Map Agentic Security To Five Eyes/NSA Risk Taxonomy

**Files:**
- Modify: `.agent/SECURITY.md`
- Modify: `.agent/TEMPLATES/THREAT_MODEL.md`
- Modify: `.agent/TEMPLATES/REPO_AUDIT.md`
- Modify: `.agent/PROMPTS.md`

- [ ] **Step 1: Add taxonomy section to `.agent/SECURITY.md`**

Add this section after `## Threat Surfaces`:

````markdown
## Five Eyes/NSA Agentic AI Risk Categories

For enterprise, critical-infrastructure, defense, production, safety-sensitive, or regulated uses, map risks to these categories:

```text
Privilege risks: over-privileged agents, credential abuse, excessive tool authority, weak least-agency controls.
Design and configuration risks: insecure provisioning, unsafe defaults, weak sandboxing, unclear approval gates, brittle policy wiring.
Behavior risks: goal misalignment, specification gaming, deceptive behavior, uncontrolled loops, unexpected emergent capability.
Structural risks: complex tool chains, insecure inter-agent communication, opaque dependencies, cross-system attack paths.
Accountability risks: weak audit trails, unclear ownership, untraceable decisions, missing approval records, poor incident reconstruction.
```

Use these categories alongside ordinary security threat modeling. They are a governance and review lens, not a replacement for concrete abuse cases.
````

- [ ] **Step 2: Add lifecycle section to `.agent/SECURITY.md`**

Add this section after the taxonomy section:

````markdown
## Agentic AI Security Lifecycle

For agentic systems, consider controls across the lifecycle:

```text
Designing secure agents: define authority, data access, approval gates, fail-safe behavior, and human oversight.
Developing secure agents: test prompt-injection, tool-misuse, context-poisoning, and unsafe-code-execution cases.
Managing third-party components: review skills, MCP servers, prompts, hooks, plugins, models, datasets, and connectors as supply chain.
Deploying agents securely: use staged rollout, least privilege, isolation, monitoring, rollback, and explicit operator ownership.
Operating agents securely: monitor behavior drift, audit tool calls, review incidents, rotate credentials, and reassess threat models.
```
````

- [ ] **Step 3: Add taxonomy fields to threat model**

In `.agent/TEMPLATES/THREAT_MODEL.md`, add this section after `## Threat Surfaces` if a threat-surfaces section exists after implementation, otherwise add it after `## Actors And Identities`:

````markdown
## Agentic AI Risk Taxonomy

```text
Privilege risks:
Design and configuration risks:
Behavior risks:
Structural risks:
Accountability risks:
Lifecycle stage: <designing | developing | managing third-party components | deploying | operating | not applicable>
```
````

- [ ] **Step 4: Add audit fields**

In `.agent/TEMPLATES/REPO_AUDIT.md`, add these fields under `## 6. Agentic Security Readiness`:

```text
Privilege risks: <summary>
Design/configuration risks: <summary>
Behavior risks: <summary>
Structural risks: <summary>
Accountability risks: <summary>
Lifecycle coverage: <summary>
```

- [ ] **Step 5: Add prompt**

In `.agent/PROMPTS.md`, add this prompt after the MCP authorization prompt:

````markdown
## 17. Agentic Risk Taxonomy Mapping

```text
Use .agent/SECURITY.md. Map this agentic system or change to the Five Eyes/NSA risk categories: privilege, design and configuration, behavior, structural, and accountability risks. Then map controls across designing, developing, managing third-party components, deploying, and operating. Identify missing controls and residual risk.
```
````

Renumber later prompt headings.

- [ ] **Step 6: Validate taxonomy coverage**

Run:

```bash
rg -n "Privilege risks|Design and configuration risks|Behavior risks|Structural risks|Accountability risks|Designing secure agents|Operating agents securely|Lifecycle coverage" .agent/SECURITY.md .agent/TEMPLATES/THREAT_MODEL.md .agent/TEMPLATES/REPO_AUDIT.md .agent/PROMPTS.md
git diff --check
```

Expected:

- Security guidance maps to the Five Eyes/NSA risk categories.
- Threat model and audit templates capture the taxonomy.
- Prompt library can request the mapping directly.

- [ ] **Step 7: Commit**

```bash
git add .agent/SECURITY.md .agent/TEMPLATES/THREAT_MODEL.md .agent/TEMPLATES/REPO_AUDIT.md .agent/PROMPTS.md
git commit -m "Map agentic AI security risks"
```

---

## Task 7: Update Copilot Adapter Guidance

**Files:**
- Modify: `.agent/ADAPTERS.md`
- Modify: `ADOPTION.md`
- Modify: `.agent/PROMPTS.md`

- [ ] **Step 1: Replace Copilot section**

In `.agent/ADAPTERS.md`, replace the `## GitHub Copilot` section with:

````markdown
## GitHub Copilot

GitHub Copilot repositories may use:

```text
AGENTS.md
nested AGENTS.md files
.github/copilot-instructions.md
.github/instructions/*.instructions.md
root CLAUDE.md or GEMINI.md, when a single bridge file is preferred
```

Current Copilot guidance supports repository-wide custom instructions, path-specific instructions, and agent instructions. `AGENTS.md` files can live anywhere in the repository; when Copilot is working, the nearest `AGENTS.md` file in the directory tree takes precedence.

Recommended default:

- use `AGENTS.md` and nested `AGENTS.md` files for agent instructions,
- use `.github/copilot-instructions.md` only when the repository needs Copilot-specific repository-wide instructions,
- use `.github/instructions/*.instructions.md` only for path-specific Copilot behavior that cannot be expressed cleanly through nested `AGENTS.md`,
- keep `CLAUDE.md` and `GEMINI.md` as optional bridges for ecosystems that require those names.

Recommended Copilot bridge pattern:

```markdown
Follow `AGENTS.md` and the supporting files under `.agent/`. Keep changes narrow, run documented checks, and report validation honestly.
```

Path-specific instruction files should add local facts for a subtree. They should not fork global policy.
````

- [ ] **Step 2: Update ADOPTION adapter list**

In `ADOPTION.md`, replace the Copilot bullet:

```text
- `.github/copilot-instructions.md` and `.github/instructions/*.instructions.md` for GitHub Copilot,
```

with:

```text
- `AGENTS.md`, nested `AGENTS.md`, `.github/copilot-instructions.md`, and `.github/instructions/*.instructions.md` for GitHub Copilot,
```

- [ ] **Step 3: Update adapter prompt**

In `.agent/PROMPTS.md`, find the adapter prompt and replace:

```text
Recommend minimal bridge files for Codex/OpenAI, Claude Code, Gemini CLI, GitHub Copilot, Cursor, Aider, or generic agents.
```

with:

```text
Recommend minimal bridge files for Codex/OpenAI, Claude Code, Gemini CLI, GitHub Copilot, Cursor, Aider, or generic agents. For Copilot, prefer AGENTS.md and nested AGENTS.md before adding .github bridge files.
```

- [ ] **Step 4: Validate Copilot guidance**

Run:

```bash
rg -n "GitHub Copilot|nearest `AGENTS.md`|nested `AGENTS.md`|copilot-instructions|instructions/\\*\\.instructions|prefer AGENTS.md" .agent/ADAPTERS.md ADOPTION.md .agent/PROMPTS.md
git diff --check
```

Expected:

- Copilot section documents `AGENTS.md` and nearest-file precedence.
- `.github` bridge files are optional rather than implied default.

- [ ] **Step 5: Commit**

```bash
git add .agent/ADAPTERS.md ADOPTION.md .agent/PROMPTS.md
git commit -m "Update Copilot adapter guidance"
```

---

## Task 8: Cross-Document Consistency And Final Validation

**Files:**
- Modify as needed: `README.md`, `ADOPTION.md`, `.agent/ADAPTERS.md`, `.agent/WORKFLOW.md`, `.agent/SECURITY.md`, `.agent/TEMPLATES/*`, `.agent/PROMPTS.md`, `CHANGELOG.md`, `VERSION`, `.gitignore`

- [ ] **Step 1: Verify all six findings map to changed surfaces**

Run:

```bash
rg -n "does not copy domain overlays|do not copy every overlay|\\.aider\\.conf\\.yml|current-source|MCP Authorization|Privilege risks|nearest `AGENTS.md`|GEMINI.md|context.fileName" README.md ADOPTION.md .gitignore .agent/ADAPTERS.md .agent/WORKFLOW.md .agent/SECURITY.md .agent/TEMPLATES/THREAT_MODEL.md .agent/TEMPLATES/REPO_AUDIT.md .agent/TEMPLATES/EXEC_PLAN.md .agent/PROMPTS.md
```

Expected:

- Adoption overlay restraint appears in README and ADOPTION.
- `.aider.conf.yml` appears in `.gitignore` and adapter docs.
- Current-source refresh appears in workflow/templates/prompts.
- MCP authorization appears in security/threat model/prompts.
- Five Eyes/NSA risk categories appear in security/threat model/audit/prompts.
- Copilot nearest `AGENTS.md` guidance appears in adapters/adoption/prompts.
- Existing Gemini bridge guidance still mentions `GEMINI.md` and configurable `context.fileName`.

- [ ] **Step 2: Check prohibited files**

Run:

```bash
find . -path ./.git -prune -o -type f -perm -111 -print
find . -path ./.git -prune -o \( -name package.json -o -name pyproject.toml -o -name Cargo.toml -o -name go.mod -o -name Makefile -o -name justfile -o -name "*.lock" -o -path "./.github/*" -o -name CLAUDE.md -o -name GEMINI.md -o -name ".aider.conf.yml" -o -path "./.claude/*" -o -path "./.gemini/*" \) -print
```

Expected:

- No executable files.
- No package/build/CI/tooling files.
- No vendor-specific bridge files are added to the seed.

- [ ] **Step 3: Placeholder scan**

Run:

```bash
rg -n "TBD|TODO|FIXME|lorem|placeholder" README.md ADOPTION.md AGENTS.md .agent
```

Expected:

- No accidental placeholders in guidance files.
- Existing template fields are acceptable when they are intentional form fields.

- [ ] **Step 4: Version and changelog check**

Run:

```bash
rg -n "0\\.2\\.1" VERSION CHANGELOG.md
```

Expected:

- `VERSION` and `CHANGELOG.md` both show `0.2.1`.

- [ ] **Step 5: Markdown whitespace check**

Run:

```bash
git diff --check HEAD
```

Expected:

- Exit 0.

- [ ] **Step 6: Commit any consistency edits**

If Step 1 through Step 5 required edits, run:

```bash
git add README.md ADOPTION.md .gitignore .agent CHANGELOG.md VERSION
git commit -m "Polish v0.2.1 review fixes"
```

If no files changed, skip this commit.

---

## Task 9: Merge, Push, And Confirm

**Files:**
- No content edits expected.

- [ ] **Step 1: Final branch validation**

Run:

```bash
git status --short --branch
git log --oneline --decorate -8
git diff --check HEAD
find . -path ./.git -prune -o -type f -perm -111 -print
find . -path ./.git -prune -o \( -name package.json -o -name pyproject.toml -o -name Cargo.toml -o -name go.mod -o -name Makefile -o -name justfile -o -name "*.lock" -o -path "./.github/*" -o -name CLAUDE.md -o -name GEMINI.md -o -name ".aider.conf.yml" -o -path "./.claude/*" -o -path "./.gemini/*" \) -print
```

Expected:

- Working tree clean.
- `git diff --check HEAD` exits 0.
- No executable files.
- No prohibited package/build/CI/vendor bridge files.

- [ ] **Step 2: Merge locally**

From the feature branch:

```bash
git switch main
git pull --ff-only
git merge --ff-only agent-seed-v0.2.1-review-fixes
```

Expected:

- Fast-forward merge succeeds.

- [ ] **Step 3: Re-run final validation on `main`**

Run the full command set from Step 1 again.

Expected:

- Same successful result on merged `main`.

- [ ] **Step 4: Push and confirm**

```bash
git push origin main
git status --short --branch
git ls-remote origin refs/heads/main
git log -1 --oneline --decorate
```

Expected:

- `main` is clean and aligned with `origin/main`.
- Remote `refs/heads/main` points to the v0.2.1 corrective commit.

- [ ] **Step 5: Cleanup merged feature branch**

```bash
git branch -d agent-seed-v0.2.1-review-fixes
```

Expected:

- Local feature branch deletes cleanly.

---

## Acceptance Criteria

v0.2.1 is complete when:

- `VERSION` is `0.2.1`.
- `CHANGELOG.md` documents the corrective release.
- Quick and standard adoption no longer copy every domain overlay by default.
- High-rigor adoption still explains how to copy selected overlays.
- `.gitignore` preserves shared `.aider.conf.yml` while ignoring local Aider state.
- `.agent/ADAPTERS.md` documents Aider, Gemini, and Copilot current behavior accurately enough for adopters to avoid redundant or conflicting bridge files.
- `.agent/WORKFLOW.md` includes current-source refresh behavior for fast-moving facts.
- `.agent/TEMPLATES/EXEC_PLAN.md`, `.agent/TEMPLATES/REPO_AUDIT.md`, and `.agent/PROMPTS.md` surface current-source refresh.
- `.agent/SECURITY.md` includes MCP authorization checklist coverage.
- `.agent/TEMPLATES/THREAT_MODEL.md` captures MCP authorization facts.
- `.agent/SECURITY.md` maps agentic AI security to Five Eyes/NSA privilege, design/configuration, behavior, structural, and accountability risks.
- Threat model, repo audit, and prompt surfaces include that taxonomy.
- No executable, package, build, CI, lockfile, generated-doc, or vendor-specific root bridge files are added.
- Final validation passes on merged `main`.

## Execution Recommendation

This is a compact corrective pass. Inline execution with `superpowers:executing-plans` is sufficient. If subagents are available, the most useful split is:

- Reviewer A: adoption and adapter semantics.
- Reviewer B: security, MCP, and Five Eyes/NSA taxonomy.
- Integrating agent: versioning, workflow/template consistency, validation, merge, push, and cleanup.
