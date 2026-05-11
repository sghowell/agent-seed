# Agent Seed v0.2.3 Review Fixups Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Address the follow-up review findings by tightening MCP OAuth authorization guidance and repairing v0.2.2 execution tracking evidence.

**Architecture:** Treat this as a narrow v0.2.3 documentation correction. Keep `agent-seed` markdown-only and dependency-free; do not add tooling, CI, package metadata, lockfiles, generated docs, or vendor root bridge files. Preserve the v0.2.2 design while making the latest MCP authorization requirements and plan-execution evidence explicit.

**Tech Stack:** Markdown files only plus shell validation with `git`, `rg`, `find`, and `gh`.

---

## Review Findings To Address

1. MCP authorization-code guidance is too generic for the current MCP authorization specification.
2. Protected-resource metadata guidance does not explicitly name the `authorization_servers` field or multiple-authorization-server selection.
3. The v0.2.2 implementation plan still reads as unexecuted because all tracking checkboxes remain unchecked.

## Source References

Use these references while implementing. They were checked on May 11, 2026; re-check them during implementation if a later source is available.

- MCP authorization latest specification, version `2025-11-25`: https://modelcontextprotocol.io/specification/2025-11-25/basic/authorization
- OAuth 2.1 authorization code and PKCE references linked from the MCP authorization specification: https://datatracker.ietf.org/doc/html/draft-ietf-oauth-v2-1

## File Structure

### Modify Existing Files

- `VERSION`: bump from `0.2.2` to `0.2.3`.
- `CHANGELOG.md`: add a `0.2.3` corrective release section.
- `.agent/SECURITY.md`: make MCP authorization-code, `authorization_servers`, PKCE metadata, `S256`, state, and open-redirect checks explicit.
- `.agent/TEMPLATES/THREAT_MODEL.md`: add explicit fields for `authorization_servers`, PKCE support discovery, `S256`, state binding, and open-redirect controls.
- `.agent/PROMPTS.md`: update the MCP authorization review prompt so agents ask for those details directly.
- `docs/superpowers/plans/2026-05-11-agent-seed-v0.2.2-review-fixups.md`: mark completed steps and add execution evidence for the already-merged v0.2.2 work.

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

- [x] **Step 1: Confirm clean `main`**

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

- [x] **Step 2: Create the implementation branch**

Run:

```bash
git switch -c agent-seed-v0.2.3-review-fixups
```

Expected:

- Work is isolated on `agent-seed-v0.2.3-review-fixups`.

---

## Task 1: Version And Changelog

**Files:**
- Modify: `VERSION`
- Modify: `CHANGELOG.md`

- [x] **Step 1: Bump `VERSION`**

Replace the entire file with:

```text
0.2.3
```

- [x] **Step 2: Add `CHANGELOG.md` section**

Add this section above `## 0.2.2`:

```markdown
## 0.2.3

Corrected the v0.2.2 review-fix release after a follow-up review.

Included:

- explicit MCP `authorization_servers` metadata and selection guidance,
- explicit MCP PKCE metadata, `S256`, state, and open-redirect checks,
- expanded threat-model fields for authorization-code and metadata risks,
- completed v0.2.2 implementation-plan tracking evidence.
```

- [x] **Step 3: Validate version metadata**

Run:

```bash
rg -n "0\\.2\\.3|0\\.2\\.2" VERSION CHANGELOG.md
git diff --check
```

Expected:

- `VERSION` contains `0.2.3`.
- `CHANGELOG.md` has `0.2.3` above `0.2.2`.
- `git diff --check` exits 0.

- [x] **Step 4: Commit**

Run:

```bash
git add VERSION CHANGELOG.md
git commit -m "Bump version for v0.2.3 fixups"
```

Expected:

- The version and changelog update is committed.

---

## Task 2: Tighten MCP Authorization Guidance

**Files:**
- Modify: `.agent/SECURITY.md`
- Modify: `.agent/TEMPLATES/THREAT_MODEL.md`
- Modify: `.agent/PROMPTS.md`

- [x] **Step 1: Replace MCP checklist in `.agent/SECURITY.md`**

Replace the existing `### MCP Authorization Checklist` section with:

```markdown
### MCP Authorization Checklist

For HTTP-based MCP servers and clients, verify against the current MCP authorization specification. As of May 11, 2026, the latest MCP authorization specification is `2025-11-25`.

Verify:

- authorization is treated as optional for MCP, but HTTP-based implementations that support authorization follow the current MCP authorization specification,
- STDIO transports do not use the HTTP authorization flow and instead retrieve credentials from the environment or another approved local mechanism,
- MCP servers expose OAuth 2.0 Protected Resource Metadata and clients use it for authorization-server discovery,
- protected resource metadata includes `authorization_servers` with at least one acceptable authorization server for the protected MCP resource,
- clients document how they choose among multiple advertised `authorization_servers` and constrain that choice with the trust policy,
- `WWW-Authenticate` responses include `resource_metadata` when required and include scope guidance when the server can provide it,
- clients support both protected-resource metadata discovery mechanisms: `WWW-Authenticate` `resource_metadata` and well-known protected-resource metadata URIs,
- authorization-server discovery supports both OAuth 2.0 Authorization Server Metadata and OpenID Connect Discovery,
- authorization server endpoints use HTTPS except for explicitly approved local-development endpoints,
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
- authorization-code flows verify PKCE support from authorization server metadata before proceeding,
- clients refuse authorization when `code_challenge_methods_supported` is absent from authorization server metadata or provider metadata,
- clients use the `S256` code challenge method when technically capable,
- clients use state parameters in authorization-code flows and discard responses with missing or mismatched state,
- redirect URIs are registered with the authorization server and validated by exact match,
- redirect URI policy rejects open-redirect patterns and treats untrusted redirect destinations as authorization failures,
- localhost redirect URIs are restricted to local development use and reviewed for interception and impersonation risk,
- trust policies define which authorization servers, clients, metadata documents, redirect URIs, scopes, and redirect destinations are acceptable,
- refresh tokens, stored credentials, and client credentials are protected, scoped, rotated, and revoked where supported,
- logs, traces, screenshots, benchmark artifacts, and final summaries do not expose tokens, codes, client secrets, refresh tokens, private keys, state values, or authorization metadata that would enable misuse.
```

- [x] **Step 2: Replace MCP fields in `.agent/TEMPLATES/THREAT_MODEL.md`**

Replace the existing `## MCP Authorization` fenced text block with:

````markdown
## MCP Authorization

```text
HTTP-based MCP involved: <yes/no>
MCP authorization spec version checked: <version/date or not applicable>
Transport credential model: <HTTP authorization | STDIO environment credentials | other approved mechanism | not applicable>
Protected resource metadata discovery: <WWW-Authenticate resource_metadata | well-known URI | both | not applicable>
Protected resource metadata authorization_servers: <present with one server | present with multiple servers and selection policy | absent and rejected | not applicable>
Authorization server discovery: <OAuth metadata | OpenID Connect discovery | both | not applicable>
Authorization server endpoint security: <HTTPS endpoints | approved local-development endpoint | not applicable>
Client registration approach: <pre-registered | Client ID Metadata Document | Dynamic Client Registration | user-provided | not applicable>
Client ID Metadata Document validation: <validation plan or not applicable>
Requested scopes: <scopes and least-privilege rationale or not applicable>
Scope challenge and step-up handling: <handling plan or not applicable>
Resource indicator: <canonical MCP server resource or not applicable>
Token transport: <Authorization header every request | not applicable>
Token audience validation: <validation plan or not applicable>
Token passthrough prevented: <yes/no/not applicable>
Authorization error handling: <401/403/insufficient_scope handling or not applicable>
PKCE support discovery: <code_challenge_methods_supported metadata source and refusal behavior or not applicable>
PKCE method: <S256 | other with justification | not applicable>
Authorization state binding: <state generation, storage, verification, and mismatch handling or not applicable>
Redirect URI policy: <exact registered redirect URI policy, HTTPS/localhost constraints, and open-redirect prevention or not applicable>
Localhost redirect risk controls: <development-only constraint, warning, attestation, or not applicable>
Trust policy: <trusted authorization servers, clients, metadata documents, redirect URIs, redirect destinations, scopes>
Token storage and logging controls: <controls>
```
````

The angle-bracket fields are intentional template fields.

- [x] **Step 3: Replace MCP authorization prompt in `.agent/PROMPTS.md`**

Replace the `## 16. MCP Authorization Review` prompt body with:

```text
Use .agent/SECURITY.md and .agent/TEMPLATES/THREAT_MODEL.md. Review this MCP integration against the latest MCP authorization specification. Verify transport applicability, protected resource metadata discovery, `authorization_servers` handling, multiple-authorization-server selection, authorization server discovery, HTTPS endpoint policy, client registration approach, Client ID Metadata Document handling, scope selection, scope challenges, runtime insufficient-scope handling, resource indicators, token audience binding, token passthrough prevention, authorization-header token use, authorization-code protections, PKCE metadata discovery, `S256` use, state-parameter binding, exact redirect URI handling, open-redirect prevention, localhost redirect constraints, trust policy, token storage, token logging, and scoped credentials. Findings first, ordered by severity.
```

- [x] **Step 4: Validate MCP hardening coverage**

Run:

```bash
rg -n "authorization_servers|multiple advertised|code_challenge_methods_supported|S256|state parameters|mismatched state|open-redirect|Authorization state binding|PKCE support discovery|Redirect URI policy|HTTPS endpoints" .agent/SECURITY.md .agent/TEMPLATES/THREAT_MODEL.md .agent/PROMPTS.md
git diff --check
```

Expected:

- `.agent/SECURITY.md` explicitly covers `authorization_servers`, multiple-server selection, PKCE metadata discovery, `S256`, state, and open-redirect prevention.
- `.agent/TEMPLATES/THREAT_MODEL.md` has fields for the same MCP authorization risks.
- `.agent/PROMPTS.md` asks reviewers to check those facts directly.
- `git diff --check` exits 0.

- [x] **Step 5: Commit**

Run:

```bash
git add .agent/SECURITY.md .agent/TEMPLATES/THREAT_MODEL.md .agent/PROMPTS.md
git commit -m "Tighten MCP OAuth authorization guidance"
```

Expected:

- The MCP hardening changes are committed.

---

## Task 3: Record v0.2.2 Plan Execution Evidence

**Files:**
- Modify: `docs/superpowers/plans/2026-05-11-agent-seed-v0.2.2-review-fixups.md`

- [x] **Step 1: Mark v0.2.2 checklist steps complete**

In `docs/superpowers/plans/2026-05-11-agent-seed-v0.2.2-review-fixups.md`, replace every unchecked checkbox prefix with a checked checkbox prefix:

```text
unchecked: - [ ]
checked: - [x]
```

Only change checkbox prefixes in this file. Do not change command snippets or explanatory prose.

- [x] **Step 2: Add execution evidence section**

Add this section immediately before `## Acceptance Criteria`:

```markdown
## Execution Evidence

The v0.2.2 plan was executed and merged before the follow-up review.

- Final merged `main` commit: `41b609e04902f1b515dfb24047cab5bda5b1c884`.
- Remote branch checked: `origin/main`.
- Local feature branch cleanup: `agent-seed-v0.2.2-review-fixups` deleted.
- Hosted CI check: `gh run list --limit 3 --json databaseId,status,conclusion,headSha,workflowName` returned `[]`, so no hosted GitHub Actions workflows existed for this repository.
- Validation evidence: clean `main`, `git diff --check HEAD` passed, executable/prohibited-file scans were empty, stale MCP scans were empty, unresolved-text scans for active artifacts were empty.
```

- [x] **Step 3: Validate v0.2.2 plan tracking**

Run:

```bash
rg -n "^- \\[ \\]" docs/superpowers/plans/2026-05-11-agent-seed-v0.2.2-review-fixups.md
rg -n "^- \\[[xX]\\]" docs/superpowers/plans/2026-05-11-agent-seed-v0.2.2-review-fixups.md
rg -n "Execution Evidence|41b609e04902f1b515dfb24047cab5bda5b1c884|gh run list|returned \\[\\]" docs/superpowers/plans/2026-05-11-agent-seed-v0.2.2-review-fixups.md
git diff --check
```

Expected:

- The first `rg` command exits 1 with no unchecked v0.2.2 checklist entries.
- The second `rg` command exits 0 and returns 36 checked v0.2.2 checklist entries.
- The third `rg` command exits 0 and finds the execution evidence.
- `git diff --check` exits 0.

- [x] **Step 4: Commit**

Run:

```bash
git add docs/superpowers/plans/2026-05-11-agent-seed-v0.2.2-review-fixups.md
git commit -m "Record v0.2.2 execution evidence"
```

Expected:

- The v0.2.2 plan-tracking repair is committed.

---

## Task 4: Cross-Document Consistency And Final Validation

**Files:**
- Review: `VERSION`
- Review: `CHANGELOG.md`
- Review: `.agent/SECURITY.md`
- Review: `.agent/TEMPLATES/THREAT_MODEL.md`
- Review: `.agent/PROMPTS.md`
- Review: `docs/superpowers/plans/2026-05-11-agent-seed-v0.2.2-review-fixups.md`
- Review: `docs/superpowers/plans/2026-05-11-agent-seed-v0.2.3-review-fixups.md`

- [x] **Step 1: Verify all findings map to changed surfaces**

Run:

```bash
rg -n "0\\.2\\.3|authorization_servers|code_challenge_methods_supported|S256|state parameters|open-redirect|Execution Evidence|\\[x\\]" VERSION CHANGELOG.md .agent/SECURITY.md .agent/TEMPLATES/THREAT_MODEL.md .agent/PROMPTS.md docs/superpowers/plans/2026-05-11-agent-seed-v0.2.2-review-fixups.md
```

Expected:

- Version and changelog show `0.2.3`.
- MCP OAuth hardening terms appear in the security checklist, threat model, and prompt.
- v0.2.2 plan evidence and checked boxes are present.

- [x] **Step 2: Check stale MCP references**

Run:

```bash
rg -n "2025-0[6]-18|modelcontextprotocol.io/specification/2025-0[6]-18" README.md ADOPTION.md AGENTS.md .agent docs/superpowers/plans
```

Expected:

- Exit 1 with no output.

- [x] **Step 3: Check prohibited files**

Run:

```bash
find . -path ./.git -prune -o -type f -perm -111 -print
find . -path ./.git -prune -o \( -name package.json -o -name pyproject.toml -o -name Cargo.toml -o -name go.mod -o -name Makefile -o -name justfile -o -name "*.lock" -o -path "./.github/*" -o -name CLAUDE.md -o -name GEMINI.md -o -name ".aider.conf.yml" -o -path "./.claude/*" -o -path "./.gemini/*" \) -print
```

Expected:

- No executable files.
- No package/build/CI/tooling files.
- No vendor-specific bridge files are added to the seed.

- [x] **Step 4: Unresolved text scan**

Run:

```bash
rg -n "T[B]D|T[O]DO|F[I]XME|lo[r]em" README.md ADOPTION.md AGENTS.md .agent docs/superpowers/plans/2026-05-11-agent-seed-v0.2.1-review-fixes.md docs/superpowers/plans/2026-05-11-agent-seed-v0.2.2-review-fixups.md docs/superpowers/plans/2026-05-11-agent-seed-v0.2.3-review-fixups.md
```

Expected:

- Exit 1 with no accidental unresolved planning text.
- Intentional angle-bracket template fields are not matched by this scan.

- [x] **Step 5: Markdown whitespace check**

Run:

```bash
git diff --check HEAD
```

Expected:

- Exit 0.

- [x] **Step 6: Commit any consistency edits**

If Step 1 through Step 5 required edits, run:

```bash
git add VERSION CHANGELOG.md .agent/SECURITY.md .agent/TEMPLATES/THREAT_MODEL.md .agent/PROMPTS.md docs/superpowers/plans/2026-05-11-agent-seed-v0.2.2-review-fixups.md docs/superpowers/plans/2026-05-11-agent-seed-v0.2.3-review-fixups.md
git commit -m "Polish v0.2.3 fixups"
```

Expected:

- Any consistency edits are committed.
- If no files changed after validation, no extra commit is created.

---

## Task 5: Merge, Push, And Confirm

**Files:**
- No content edits expected.

- [x] **Step 1: Final branch validation**

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

- [x] **Step 2: Merge locally**

From the feature branch, run:

```bash
git switch main
git pull --ff-only
git merge --ff-only agent-seed-v0.2.3-review-fixups
```

Expected:

- Fast-forward merge succeeds.

- [x] **Step 3: Re-run final validation on `main`**

Run the full command set from Step 1 again.

Expected:

- Same successful result on merged `main`.

- [x] **Step 4: Push and confirm**

Run:

```bash
git push origin main
git status --short --branch
git ls-remote origin refs/heads/main
git log -1 --oneline --decorate
gh run list --limit 3 --json databaseId,status,conclusion,headSha,workflowName
```

Expected:

- `main` is clean and aligned with `origin/main`.
- Remote `refs/heads/main` points to the v0.2.3 fixup commit.
- If GitHub Actions still returns an empty list, record that no hosted Actions runs exist for this repo.
- If GitHub Actions returns a run for the pushed commit, wait for it to complete and require success before cleanup.

- [x] **Step 5: Cleanup merged feature branch**

Run:

```bash
git branch -d agent-seed-v0.2.3-review-fixups
```

Expected:

- Local feature branch deletes cleanly.

---

## Acceptance Criteria

v0.2.3 is complete when:

- `VERSION` is `0.2.3`.
- `CHANGELOG.md` documents the corrective release.
- `.agent/SECURITY.md` explicitly covers `authorization_servers`, multiple-authorization-server selection, PKCE support discovery, `code_challenge_methods_supported`, `S256`, authorization state binding, exact redirect URI validation, and open-redirect prevention.
- `.agent/TEMPLATES/THREAT_MODEL.md` captures the same MCP authorization-code and protected-resource metadata details.
- `.agent/PROMPTS.md` asks MCP authorization reviewers to check those details directly.
- `docs/superpowers/plans/2026-05-11-agent-seed-v0.2.2-review-fixups.md` has no unchecked plan steps and includes execution evidence for the already-merged v0.2.2 work.
- No stale June 2025 MCP authorization references are present.
- No executable, package, build, CI, lockfile, generated-doc, or vendor-specific root bridge files are added.
- Final validation passes on merged `main`.

## Execution Recommendation

This is a compact corrective documentation pass. Inline execution with `superpowers:executing-plans` is sufficient. A short review after Task 2 is advisable because MCP OAuth wording is the only high-risk source-accuracy surface.
