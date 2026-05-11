# Agent Seed v0.2.2 Review Fixups Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Address the post-v0.2.1 review findings by updating MCP authorization guidance to the latest spec, completing the missed threat-model current-source section, clarifying Copilot adoption wording, and repairing shell-fragile validation commands in the v0.2.1 plan artifact.

**Architecture:** Treat this as a narrow v0.2.2 documentation correction. Keep `agent-seed` markdown-only and dependency-free; do not add tooling, CI, package metadata, lockfiles, generated docs, or vendor root bridge files. Preserve the v0.2.1 design while tightening source freshness, execution quality, and adopter clarity.

**Tech Stack:** Markdown files only plus shell validation with `git`, `rg`, and `find`.

---

## Review Findings To Address

1. MCP guidance is not current against the latest MCP authorization specification.
2. `.agent/TEMPLATES/THREAT_MODEL.md` did not receive the current-source fields promised by the v0.2.1 plan.
3. `ADOPTION.md` conflates `AGENTS.md` source-of-truth files with vendor-specific bridge files.
4. Two v0.2.1 plan validation commands are shell-fragile in `zsh` because double-quoted `rg` patterns contain backticked `` `AGENTS.md` ``.

## Source References

Use these references while implementing. They were checked on May 11, 2026; re-check them during implementation if a later source is available.

- MCP authorization latest specification, version `2025-11-25`: https://modelcontextprotocol.io/specification/2025-11-25/basic/authorization
- GitHub Copilot repository custom instructions and agent instructions: https://docs.github.com/en/copilot/how-tos/copilot-on-github/customize-copilot/add-custom-instructions/add-repository-instructions
- AGENTS.md format and ecosystem support: https://agents.md/
- NSA/Five Eyes guidance, “Careful Adoption of Agentic AI Services”: https://www.nsa.gov/Press-Room/Press-Releases-Statements/Press-Release-View/Article/4475134/nsa-joins-the-asds-acsc-and-others-to-release-guidance-on-agentic-artificial-in/

## File Structure

### Modify Existing Files

- `VERSION`: bump from `0.2.1` to `0.2.2`.
- `CHANGELOG.md`: add a `0.2.2` corrective release section.
- `.agent/SECURITY.md`: replace the MCP authorization checklist with latest-spec coverage.
- `.agent/TEMPLATES/THREAT_MODEL.md`: add current-source refresh fields and expand MCP authorization fields.
- `.agent/PROMPTS.md`: update MCP review prompts so agents ask for latest-spec facts.
- `ADOPTION.md`: separate source-of-truth instruction files from vendor bridge files.
- `docs/superpowers/plans/2026-05-11-agent-seed-v0.2.1-review-fixes.md`: repair stale MCP source URL and `zsh`-fragile validation command quoting.

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
git switch -c agent-seed-v0.2.2-review-fixups
```

Expected:

- Work is isolated on `agent-seed-v0.2.2-review-fixups`.

---

## Task 1: Version And Changelog

**Files:**
- Modify: `VERSION`
- Modify: `CHANGELOG.md`

- [ ] **Step 1: Bump `VERSION`**

Replace the entire file with:

```text
0.2.2
```

- [ ] **Step 2: Add `CHANGELOG.md` section**

Add this section above `## 0.2.1`:

```markdown
## 0.2.2

Corrected the v0.2.1 review-fix release after a follow-up review.

Included:

- updated MCP authorization guidance for the latest `2025-11-25` specification,
- current-source refresh fields in the threat-model template,
- clearer distinction between `AGENTS.md` source-of-truth files and vendor bridge files,
- repaired `zsh`-safe validation commands in the v0.2.1 implementation plan.
```

- [ ] **Step 3: Validate version metadata**

Run:

```bash
rg -n "0\\.2\\.2|0\\.2\\.1" VERSION CHANGELOG.md
git diff --check
```

Expected:

- `VERSION` contains `0.2.2`.
- `CHANGELOG.md` has `0.2.2` above `0.2.1`.
- `git diff --check` exits 0.

- [ ] **Step 4: Commit**

```bash
git add VERSION CHANGELOG.md
git commit -m "Bump version for v0.2.2 fixups"
```

---

## Task 2: Update MCP Authorization Guidance To Latest Spec

**Files:**
- Modify: `.agent/SECURITY.md`
- Modify: `.agent/TEMPLATES/THREAT_MODEL.md`
- Modify: `.agent/PROMPTS.md`

- [ ] **Step 1: Replace MCP checklist in `.agent/SECURITY.md`**

Replace the existing `### MCP Authorization Checklist` section with:

```markdown
### MCP Authorization Checklist

For HTTP-based MCP servers and clients, verify against the current MCP authorization specification. As of May 11, 2026, the latest MCP authorization specification is `2025-11-25`.

Verify:

- authorization is treated as optional for MCP, but HTTP-based implementations that support authorization follow the current MCP authorization specification,
- STDIO transports do not use the HTTP authorization flow and instead retrieve credentials from the environment or another approved local mechanism,
- MCP servers expose OAuth 2.0 Protected Resource Metadata and clients use it for authorization-server discovery,
- `WWW-Authenticate` responses include `resource_metadata` when required and include scope guidance when the server can provide it,
- clients support both protected-resource metadata discovery mechanisms: `WWW-Authenticate` `resource_metadata` and well-known protected-resource metadata URIs,
- authorization-server discovery supports both OAuth 2.0 Authorization Server Metadata and OpenID Connect Discovery,
- client registration uses the right approach for the deployment: pre-registration, OAuth Client ID Metadata Documents, Dynamic Client Registration fallback, or explicit user-provided client information,
- Client ID Metadata Documents, when used, are HTTPS URLs with path components, contain required client metadata, match `client_id` exactly, validate redirect URIs, and are fetched, cached, and validated deliberately,
- clients request the minimum required scopes and handle scope challenges from `WWW-Authenticate` responses as authoritative for the current request,
- clients can handle runtime insufficient-scope responses, including `403` errors with `insufficient_scope`, `scope`, and `resource_metadata` when provided,
- clients include the OAuth Resource Indicators `resource` parameter in both authorization requests and token requests,
- the resource indicator identifies the intended MCP server using a canonical server URI,
- access tokens are sent in authorization headers for every HTTP request and are never sent in URI query strings,
- MCP servers validate that access tokens were issued for that server as the intended audience,
- MCP servers reject invalid, expired, wrong-audience, or insufficient-scope tokens with the expected authorization failure response,
- MCP servers do not accept, forward, or pass through tokens issued for other resources,
- authorization-code flows use PKCE and exact redirect URI validation according to the current OAuth and MCP requirements,
- localhost redirect URIs are restricted to local development use and reviewed for interception risk,
- trust policies define which authorization servers, clients, metadata documents, redirect URIs, and scopes are acceptable,
- refresh tokens, stored credentials, and client credentials are protected, scoped, rotated, and revoked where supported,
- logs, traces, screenshots, benchmark artifacts, and final summaries do not expose tokens, codes, client secrets, refresh tokens, private keys, or authorization metadata that would enable misuse.
```

- [ ] **Step 2: Replace MCP fields in threat model**

In `.agent/TEMPLATES/THREAT_MODEL.md`, replace the existing `## MCP Authorization` fenced text block with:

````markdown
## MCP Authorization

```text
HTTP-based MCP involved: <yes/no>
MCP authorization spec version checked: <version/date or not applicable>
Transport credential model: <HTTP authorization | STDIO environment credentials | other approved mechanism | not applicable>
Protected resource metadata discovery: <WWW-Authenticate resource_metadata | well-known URI | both | not applicable>
Authorization server discovery: <OAuth metadata | OpenID Connect discovery | both | not applicable>
Client registration approach: <pre-registered | Client ID Metadata Document | Dynamic Client Registration | user-provided | not applicable>
Client ID Metadata Document validation: <validation plan or not applicable>
Requested scopes: <scopes and least-privilege rationale or not applicable>
Scope challenge and step-up handling: <handling plan or not applicable>
Resource indicator: <canonical MCP server resource or not applicable>
Token transport: <Authorization header every request | not applicable>
Token audience validation: <validation plan or not applicable>
Token passthrough prevented: <yes/no/not applicable>
Authorization error handling: <401/403/insufficient_scope handling or not applicable>
PKCE and redirect URI policy: <PKCE and exact redirect URI policy or not applicable>
Trust policy: <trusted authorization servers, clients, metadata documents, redirect URIs, scopes>
Token storage and logging controls: <controls>
```
````

The angle-bracket fields are intentional template fields.

- [ ] **Step 3: Update MCP prompt coverage**

In `.agent/PROMPTS.md`, replace the `## 16. MCP Authorization Review` prompt body with:

```text
Use .agent/SECURITY.md and .agent/TEMPLATES/THREAT_MODEL.md. Review this MCP integration against the latest MCP authorization specification. Verify transport applicability, protected resource metadata discovery, authorization server discovery, client registration approach, Client ID Metadata Document handling, scope selection, scope challenges, runtime insufficient-scope handling, resource indicators, token audience binding, token passthrough prevention, authorization-header token use, authorization-code protections, PKCE, exact redirect URI handling, localhost redirect constraints, trust policy, token storage, token logging, and scoped credentials. Findings first, ordered by severity.
```

- [ ] **Step 4: Validate MCP latest-spec coverage**

Run:

```bash
rg -n "2025-11-25|Client ID Metadata|OpenID Connect|resource_metadata|insufficient_scope|scope challenge|Resource Indicators|Authorization header|Token audience|localhost redirect|Trust policy" .agent/SECURITY.md .agent/TEMPLATES/THREAT_MODEL.md .agent/PROMPTS.md
git diff --check
```

Expected:

- `.agent/SECURITY.md` names `2025-11-25` and covers the latest MCP authorization mechanics.
- `.agent/TEMPLATES/THREAT_MODEL.md` captures MCP discovery, registration, scope, token, error, and trust-policy details.
- `.agent/PROMPTS.md` requests latest-spec MCP review explicitly.
- `git diff --check` exits 0.

- [ ] **Step 5: Commit**

```bash
git add .agent/SECURITY.md .agent/TEMPLATES/THREAT_MODEL.md .agent/PROMPTS.md
git commit -m "Update MCP authorization guidance"
```

---

## Task 3: Add Current-Source Fields To Threat Model

**Files:**
- Modify: `.agent/TEMPLATES/THREAT_MODEL.md`
- Modify: `.agent/PROMPTS.md`

- [ ] **Step 1: Add current-source section to threat model**

In `.agent/TEMPLATES/THREAT_MODEL.md`, add this section after `## System Or Change` and before `## Assets`:

````markdown
## Current-Source Refresh

Use this section when security, tool, MCP, agent, model, dataset, benchmark, hardware, API, legal, or standards facts may have drifted.

```text
Sources checked:
- <source title and URL or local path>
Date checked:
Version or publication date:
Decision depending on source:
Drift risk:
```
````

The angle-bracket field is an intentional template field.

- [ ] **Step 2: Update threat-model prompt**

In `.agent/PROMPTS.md`, replace the `## 14. Agentic AI Threat Model` prompt body with:

```text
Use .agent/SECURITY.md and .agent/TEMPLATES/THREAT_MODEL.md. For drift-prone security, tool, MCP, agent, model, dataset, benchmark, hardware, API, legal, or standards facts, refresh current primary sources before threat modeling and record them in the template. Threat-model this agentic system or change. Focus on prompt injection, goal hijack, tool misuse, excessive permissions, identity abuse, memory or context poisoning, data exfiltration, unsafe code execution, supply-chain risk, autonomy boundaries, approval gates, auditability, and residual risk.
```

- [ ] **Step 3: Validate current-source coverage**

Run:

```bash
rg -n "Current-Source Refresh|Sources checked|Date checked|Version or publication date|Decision depending on source|Drift risk|refresh current primary sources" .agent/TEMPLATES/THREAT_MODEL.md .agent/PROMPTS.md
git diff --check
```

Expected:

- The threat model has a current-source refresh section.
- The agentic threat-model prompt instructs agents to refresh drift-prone facts.
- `git diff --check` exits 0.

- [ ] **Step 4: Commit**

```bash
git add .agent/TEMPLATES/THREAT_MODEL.md .agent/PROMPTS.md
git commit -m "Add threat-model source refresh fields"
```

---

## Task 4: Clarify Copilot And Bridge File Wording

**Files:**
- Modify: `ADOPTION.md`
- Modify: `.agent/ADAPTERS.md`

- [ ] **Step 1: Replace ADOPTION adapter introduction**

In `ADOPTION.md`, replace the text from:

```text
Use `.agent/ADAPTERS.md` to decide whether the target repository needs vendor-specific bridge files.

Do not add vendor-specific files to the seed by default. In target repositories, add bridge files only when maintainers use that ecosystem and can keep them synchronized.

Common bridge files include:
```

through the list ending in:

```text
- `.aider.conf.yml` for shared Aider read-file configuration.
```

with:

````markdown
Use `.agent/ADAPTERS.md` to decide which instruction surfaces the target repository needs.

Keep `AGENTS.md` and nested `AGENTS.md` files as source-of-truth agent instructions when the ecosystem supports them. Add vendor-specific bridge files only when maintainers use that ecosystem and can keep the bridge synchronized.

Common source-of-truth and bridge surfaces include:

- `AGENTS.md` and nested `AGENTS.md` files for GitHub Copilot agent instructions and other compatible agents,
- `.github/copilot-instructions.md` for Copilot-specific repository-wide instructions,
- `.github/instructions/*.instructions.md` for Copilot path-specific instructions,
- `CLAUDE.md` for Claude Code bridge guidance,
- `GEMINI.md` for Gemini CLI bridge guidance,
- Cursor project rules,
- `.aider.conf.yml` for shared Aider read-file configuration.
````

- [ ] **Step 2: Replace bridge policy sentence**

In `ADOPTION.md`, replace:

```text
Bridge files should point back to `AGENTS.md` and `.agent/`, not fork policy into inconsistent copies.
```

with:

```text
Vendor-specific bridge files should point back to `AGENTS.md` and `.agent/`, not fork policy into inconsistent copies.
```

- [ ] **Step 3: Tighten Copilot section in `.agent/ADAPTERS.md`**

In `.agent/ADAPTERS.md`, replace this line in the GitHub Copilot `Recommended default` list:

```text
- keep `CLAUDE.md` and `GEMINI.md` as optional bridges for ecosystems that require those names.
```

with:

```text
- use root `CLAUDE.md` or `GEMINI.md` only as a Copilot-recognized single-file alternative when maintainers deliberately choose that bridge instead of `AGENTS.md`.
```

- [ ] **Step 4: Validate Copilot wording**

Run:

```bash
rg -n "source-of-truth agent instructions|vendor-specific bridge files|Copilot-specific repository-wide|path-specific instructions|single-file alternative" ADOPTION.md .agent/ADAPTERS.md
git diff --check
```

Expected:

- `ADOPTION.md` no longer classifies `AGENTS.md` itself as a vendor bridge file.
- Copilot repository-wide, path-specific, and agent-instruction surfaces remain documented.
- `.agent/ADAPTERS.md` no longer implies `CLAUDE.md` and `GEMINI.md` are generic Copilot defaults.
- `git diff --check` exits 0.

- [ ] **Step 5: Commit**

```bash
git add ADOPTION.md .agent/ADAPTERS.md
git commit -m "Clarify adapter and bridge wording"
```

---

## Task 5: Repair v0.2.1 Plan Artifact

**Files:**
- Modify: `docs/superpowers/plans/2026-05-11-agent-seed-v0.2.1-review-fixes.md`

- [ ] **Step 1: Update MCP source reference**

In `docs/superpowers/plans/2026-05-11-agent-seed-v0.2.1-review-fixes.md`, replace:

```text
- MCP authorization specification: https://modelcontextprotocol.io/specification/2025-06-18/basic/authorization
```

with:

```text
- MCP authorization latest specification, version `2025-11-25`: https://modelcontextprotocol.io/specification/2025-11-25/basic/authorization
```

- [ ] **Step 2: Fix Copilot validation quoting**

In the same plan file, replace:

```bash
rg -n "GitHub Copilot|nearest `AGENTS.md`|nested `AGENTS.md`|copilot-instructions|instructions/\\*\\.instructions|prefer AGENTS.md" .agent/ADAPTERS.md ADOPTION.md .agent/PROMPTS.md
```

with:

```bash
rg -n 'GitHub Copilot|nearest `AGENTS.md`|nested `AGENTS.md`|copilot-instructions|instructions/\\*\\.instructions|prefer AGENTS.md' .agent/ADAPTERS.md ADOPTION.md .agent/PROMPTS.md
```

- [ ] **Step 3: Fix cross-document validation quoting**

In the same plan file, replace:

```bash
rg -n "does not copy domain overlays|do not copy every overlay|\\.aider\\.conf\\.yml|current-source|MCP Authorization|Privilege risks|nearest `AGENTS.md`|GEMINI.md|context.fileName" README.md ADOPTION.md .gitignore .agent/ADAPTERS.md .agent/WORKFLOW.md .agent/SECURITY.md .agent/TEMPLATES/THREAT_MODEL.md .agent/TEMPLATES/REPO_AUDIT.md .agent/TEMPLATES/EXEC_PLAN.md .agent/PROMPTS.md
```

with:

```bash
rg -n 'does not copy domain overlays|do not copy every overlay|\\.aider\\.conf\\.yml|current-source|MCP Authorization|Privilege risks|nearest `AGENTS.md`|GEMINI.md|context.fileName' README.md ADOPTION.md .gitignore .agent/ADAPTERS.md .agent/WORKFLOW.md .agent/SECURITY.md .agent/TEMPLATES/THREAT_MODEL.md .agent/TEMPLATES/REPO_AUDIT.md .agent/TEMPLATES/EXEC_PLAN.md .agent/PROMPTS.md
```

- [ ] **Step 4: Validate plan artifact**

Run:

```bash
rg -n "2025-06-18|rg -n \"GitHub Copilot|rg -n \"does not copy domain overlays" docs/superpowers/plans/2026-05-11-agent-seed-v0.2.1-review-fixes.md
rg -n "2025-11-25|rg -n 'GitHub Copilot|rg -n 'does not copy domain overlays" docs/superpowers/plans/2026-05-11-agent-seed-v0.2.1-review-fixes.md
git diff --check
```

Expected:

- The first `rg` command exits 1 with no stale or fragile matches.
- The second `rg` command exits 0 with the updated MCP source and single-quoted `rg` commands.
- `git diff --check` exits 0.

- [ ] **Step 5: Commit**

```bash
git add docs/superpowers/plans/2026-05-11-agent-seed-v0.2.1-review-fixes.md
git commit -m "Repair v0.2.1 plan references"
```

---

## Task 6: Cross-Document Consistency And Final Validation

**Files:**
- Modify as needed: `VERSION`, `CHANGELOG.md`, `ADOPTION.md`, `.agent/ADAPTERS.md`, `.agent/SECURITY.md`, `.agent/TEMPLATES/THREAT_MODEL.md`, `.agent/PROMPTS.md`, `docs/superpowers/plans/2026-05-11-agent-seed-v0.2.1-review-fixes.md`

- [ ] **Step 1: Verify findings map to changed surfaces**

Run:

```bash
rg -n "2025-11-25|Client ID Metadata|OpenID Connect|resource_metadata|insufficient_scope|scope challenge|current primary sources|Current-Source Refresh|source-of-truth agent instructions|vendor-specific bridge files|rg -n 'GitHub Copilot" .agent/SECURITY.md .agent/TEMPLATES/THREAT_MODEL.md .agent/PROMPTS.md ADOPTION.md .agent/ADAPTERS.md docs/superpowers/plans/2026-05-11-agent-seed-v0.2.1-review-fixes.md
```

Expected:

- Latest MCP authorization details appear in security, threat model, and prompt guidance.
- Threat model includes current-source refresh fields.
- ADOPTION separates source-of-truth agent instructions from vendor bridge files.
- The v0.2.1 plan uses single-quoted shell-safe `rg` patterns.

- [ ] **Step 2: Check stale MCP references**

Run:

```bash
rg -n "2025-06-18|modelcontextprotocol.io/specification/2025-06-18" README.md ADOPTION.md AGENTS.md .agent docs/superpowers/plans
```

Expected:

- Exit 1 with no output.

- [ ] **Step 3: Check prohibited files**

Run:

```bash
find . -path ./.git -prune -o -type f -perm -111 -print
find . -path ./.git -prune -o \( -name package.json -o -name pyproject.toml -o -name Cargo.toml -o -name go.mod -o -name Makefile -o -name justfile -o -name "*.lock" -o -path "./.github/*" -o -name CLAUDE.md -o -name GEMINI.md -o -name ".aider.conf.yml" -o -path "./.claude/*" -o -path "./.gemini/*" \) -print
```

Expected:

- No executable files.
- No package/build/CI/tooling files.
- No vendor-specific bridge files are added to the seed.

- [ ] **Step 4: Unresolved text scan**

Run:

```bash
rg -n "T[B]D|T[O]DO|F[I]XME|lo[r]em" README.md ADOPTION.md AGENTS.md .agent docs/superpowers/plans/2026-05-11-agent-seed-v0.2.1-review-fixes.md
```

Expected:

- Exit 1 with no accidental unresolved planning text.
- Intentional angle-bracket template fields are not matched by this scan.

- [ ] **Step 5: Version and markdown whitespace checks**

Run:

```bash
rg -n "0\\.2\\.2" VERSION CHANGELOG.md
git diff --check HEAD
```

Expected:

- `VERSION` and `CHANGELOG.md` both show `0.2.2`.
- `git diff --check HEAD` exits 0.

- [ ] **Step 6: Commit any consistency edits**

If Step 1 through Step 5 required edits, run:

```bash
git add VERSION CHANGELOG.md ADOPTION.md .agent docs/superpowers/plans/2026-05-11-agent-seed-v0.2.1-review-fixes.md
git commit -m "Polish v0.2.2 fixups"
```

If no files changed, skip this commit.

---

## Task 7: Merge, Push, And Confirm

**Files:**
- No content edits expected.

- [ ] **Step 1: Final branch validation**

Run:

```bash
git status --short --branch
git log --oneline --decorate -10
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
git merge --ff-only agent-seed-v0.2.2-review-fixups
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
gh run list --limit 3 --json databaseId,status,conclusion,headSha,workflowName
```

Expected:

- `main` is clean and aligned with `origin/main`.
- Remote `refs/heads/main` points to the v0.2.2 fixup commit.
- If GitHub Actions still returns an empty list, record that no hosted Actions runs exist for this repo.
- If GitHub Actions returns a run for the pushed commit, wait for it to complete and require success before cleanup.

- [ ] **Step 5: Cleanup merged feature branch**

```bash
git branch -d agent-seed-v0.2.2-review-fixups
```

Expected:

- Local feature branch deletes cleanly.

---

## Acceptance Criteria

v0.2.2 is complete when:

- `VERSION` is `0.2.2`.
- `CHANGELOG.md` documents the corrective release.
- MCP authorization guidance references the latest `2025-11-25` MCP authorization specification.
- `.agent/SECURITY.md` covers protected resource metadata discovery, authorization-server discovery, Client ID Metadata Documents, scope challenge handling, runtime insufficient-scope handling, resource indicators, token transport, token audience binding, token passthrough prevention, authorization-code protections, redirect URI policy, trust policy, and token logging controls.
- `.agent/TEMPLATES/THREAT_MODEL.md` captures current-source refresh facts and latest MCP authorization facts.
- `.agent/PROMPTS.md` asks for current-source refresh before agentic threat modeling and latest-spec MCP authorization review.
- `ADOPTION.md` distinguishes `AGENTS.md` source-of-truth instruction files from vendor-specific bridge files.
- `.agent/ADAPTERS.md` keeps Copilot guidance accurate without implying `CLAUDE.md` or `GEMINI.md` are generic Copilot defaults.
- The v0.2.1 plan artifact no longer references the stale MCP `2025-06-18` authorization spec.
- The v0.2.1 plan artifact uses `zsh`-safe single-quoted `rg` commands where patterns include backticked text.
- No executable, package, build, CI, lockfile, generated-doc, or vendor-specific root bridge files are added.
- Final validation passes on merged `main`.

## Execution Recommendation

This is a compact corrective documentation pass. Inline execution with `superpowers:executing-plans` is sufficient. A subagent review would be useful only for the MCP authorization section because it has the highest risk of drifting from the live specification.
