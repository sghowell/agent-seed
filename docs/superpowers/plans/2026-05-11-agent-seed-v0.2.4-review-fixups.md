# Agent Seed v0.2.4 Review Fixups Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Address the post-v0.2.3 review findings by correcting MCP HTTPS and PKCE guidance and recording v0.2.3 execution evidence.

**Architecture:** Treat this as a narrow v0.2.4 documentation correction. Keep `agent-seed` markdown-only and dependency-free; do not add tooling, CI, package metadata, lockfiles, generated docs, or vendor root bridge files. Preserve the v0.2.3 guidance while tightening source-accurate MCP authorization requirements and durable plan evidence.

**Tech Stack:** Markdown files only plus shell validation with `git`, `rg`, `find`, and `gh`.

---

## Review Findings To Address

1. MCP authorization server endpoint guidance incorrectly permits a local-development exception for authorization server endpoints.
2. MCP PKCE guidance does not explicitly require `code_challenge_methods_supported` to include `S256` when the client is technically capable.
3. The v0.2.3 plan has checked boxes but does not persist final execution evidence.

## Source References

Use these references while implementing. They were checked on May 11, 2026; re-check them during implementation if a later source is available.

- MCP authorization latest specification, version `2025-11-25`: https://modelcontextprotocol.io/specification/2025-11-25/basic/authorization
- OAuth 2.1 authorization code and PKCE references linked from the MCP authorization specification: https://datatracker.ietf.org/doc/html/draft-ietf-oauth-v2-1

## File Structure

### Modify Existing Files

- `VERSION`: bump from `0.2.3` to `0.2.4`.
- `CHANGELOG.md`: add a `0.2.4` corrective release section.
- `.agent/SECURITY.md`: require HTTPS authorization server endpoints, keep localhost allowance only for redirect URIs, and require advertised `S256` support when technically capable.
- `.agent/TEMPLATES/THREAT_MODEL.md`: mirror the HTTPS endpoint and `S256` support fields.
- `.agent/PROMPTS.md`: ask MCP reviewers to check HTTPS endpoint requirements and advertised `S256` support explicitly.
- `docs/superpowers/plans/2026-05-11-agent-seed-v0.2.3-review-fixups.md`: add final v0.2.3 execution evidence.
- `docs/superpowers/plans/2026-05-11-agent-seed-v0.2.4-review-fixups.md`: mark this plan executed and add final v0.2.4 execution evidence during closeout.

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
git switch -c agent-seed-v0.2.4-review-fixups
```

Expected:

- Work is isolated on `agent-seed-v0.2.4-review-fixups`.

---

## Task 1: Version And Changelog

**Files:**
- Modify: `VERSION`
- Modify: `CHANGELOG.md`

- [ ] **Step 1: Bump `VERSION`**

Replace the entire file with:

```text
0.2.4
```

- [ ] **Step 2: Add `CHANGELOG.md` section**

Add this section above `## 0.2.3`:

```markdown
## 0.2.4

Corrected the v0.2.3 review-fix release after a follow-up review.

Included:

- corrected MCP authorization server endpoint guidance to require HTTPS,
- kept localhost handling scoped to redirect URI risk controls,
- required advertised `S256` PKCE support when the client is technically capable,
- recorded v0.2.3 execution evidence.
```

- [ ] **Step 3: Validate version metadata**

Run:

```bash
rg -n "0\\.2\\.4|0\\.2\\.3" VERSION CHANGELOG.md
git diff --check
```

Expected:

- `VERSION` contains `0.2.4`.
- `CHANGELOG.md` has `0.2.4` above `0.2.3`.
- `git diff --check` exits 0.

- [ ] **Step 4: Commit**

Run:

```bash
git add VERSION CHANGELOG.md
git commit -m "Bump version for v0.2.4 fixups"
```

Expected:

- The version and changelog update is committed.

---

## Task 2: Correct MCP HTTPS And PKCE Guidance

**Files:**
- Modify: `.agent/SECURITY.md`
- Modify: `.agent/TEMPLATES/THREAT_MODEL.md`
- Modify: `.agent/PROMPTS.md`

- [ ] **Step 1: Tighten `.agent/SECURITY.md` endpoint and PKCE checks**

In `.agent/SECURITY.md`, replace the existing bullet that permits local-development authorization server endpoint exceptions with:

```markdown
- authorization server endpoints use HTTPS; local-development exceptions apply only to redirect URIs, not authorization server endpoints,
```

In the same file, replace:

```markdown
- clients refuse authorization when `code_challenge_methods_supported` is absent from authorization server metadata or provider metadata,
- clients use the `S256` code challenge method when technically capable,
```

with:

```markdown
- clients refuse authorization when `code_challenge_methods_supported` is absent from authorization server metadata or provider metadata,
- clients that are technically capable of `S256` refuse authorization unless `code_challenge_methods_supported` advertises `S256`,
- clients use the `S256` code challenge method when technically capable,
```

- [ ] **Step 2: Tighten `.agent/TEMPLATES/THREAT_MODEL.md` fields**

In `.agent/TEMPLATES/THREAT_MODEL.md`, replace the existing `Authorization server endpoint security` field that permits local-development authorization server endpoints with:

```text
Authorization server endpoint security: <HTTPS endpoints | non-HTTPS endpoint rejected | not applicable>
```

In the same file, replace:

```text
PKCE support discovery: <code_challenge_methods_supported metadata source and refusal behavior or not applicable>
```

with:

```text
PKCE support discovery: <code_challenge_methods_supported metadata source, S256 advertisement, and refusal behavior or not applicable>
```

- [ ] **Step 3: Tighten `.agent/PROMPTS.md` MCP review prompt**

In `.agent/PROMPTS.md`, replace:

```text
HTTPS endpoint policy
```

with:

```text
HTTPS-only authorization server endpoints
```

In the same prompt, replace:

```text
PKCE metadata discovery, `S256` use
```

with:

```text
PKCE metadata discovery, advertised `S256` support, `S256` use
```

- [ ] **Step 4: Validate MCP corrections**

Run:

```bash
rg -n 'authorization server endpoints use HTTPS; local-development exceptions apply only to redirect URIs|non-HTTPS endpoint rejected|advertises `S256`|advertised `S256` support|S256 advertisement' .agent/SECURITY.md .agent/TEMPLATES/THREAT_MODEL.md .agent/PROMPTS.md
rg -n "approved local-development endpoin[t]|authorization server endpoints use HTTPS excep[t]" .agent/SECURITY.md .agent/TEMPLATES/THREAT_MODEL.md .agent/PROMPTS.md
git diff --check
```

Expected:

- The first `rg` command exits 0 and finds the corrected HTTPS and `S256` guidance.
- The second `rg` command exits 1 with no stale local-development authorization server endpoint exception.
- `git diff --check` exits 0.

- [ ] **Step 5: Commit**

Run:

```bash
git add .agent/SECURITY.md .agent/TEMPLATES/THREAT_MODEL.md .agent/PROMPTS.md
git commit -m "Correct MCP HTTPS and PKCE guidance"
```

Expected:

- The MCP guidance correction is committed.

---

## Task 3: Record v0.2.3 Execution Evidence

**Files:**
- Modify: `docs/superpowers/plans/2026-05-11-agent-seed-v0.2.3-review-fixups.md`

- [ ] **Step 1: Add v0.2.3 execution evidence**

Add this section immediately before `## Acceptance Criteria`:

```markdown
## Execution Evidence

The v0.2.3 plan was executed and merged before the follow-up review.

- Final merged `main` commit: `c31a6990529e1c8cb06d63718b7fcdd6c02ee8ed`.
- Remote branch checked: `origin/main`.
- Local feature branch cleanup: `agent-seed-v0.2.3-review-fixups` deleted.
- Hosted CI check: `gh run list --limit 3 --json databaseId,status,conclusion,headSha,workflowName` returned `[]`, so no hosted GitHub Actions workflows existed for this repository.
- Validation evidence: clean `main`, `git diff --check HEAD` passed, executable/prohibited-file scans were empty, stale MCP scans were empty, unresolved-text scans for active artifacts were empty.
```

- [ ] **Step 2: Validate v0.2.3 execution evidence**

Run:

```bash
rg -n "Execution Evidence|c31a6990529e1c8cb06d63718b7fcdd6c02ee8ed|agent-seed-v0.2.3-review-fixups|returned \\[\\]" docs/superpowers/plans/2026-05-11-agent-seed-v0.2.3-review-fixups.md
rg -n "^- \\[ \\]" docs/superpowers/plans/2026-05-11-agent-seed-v0.2.3-review-fixups.md
git diff --check
```

Expected:

- The first `rg` command exits 0 and finds the execution evidence.
- The second `rg` command exits 1 with no unchecked v0.2.3 checklist entries.
- `git diff --check` exits 0.

- [ ] **Step 3: Commit**

Run:

```bash
git add docs/superpowers/plans/2026-05-11-agent-seed-v0.2.3-review-fixups.md
git commit -m "Record v0.2.3 execution evidence"
```

Expected:

- The v0.2.3 evidence repair is committed.

---

## Task 4: Plan Tracking And Cross-Document Validation

**Files:**
- Modify: `docs/superpowers/plans/2026-05-11-agent-seed-v0.2.4-review-fixups.md`
- Review: `VERSION`
- Review: `CHANGELOG.md`
- Review: `.agent/SECURITY.md`
- Review: `.agent/TEMPLATES/THREAT_MODEL.md`
- Review: `.agent/PROMPTS.md`
- Review: `docs/superpowers/plans/2026-05-11-agent-seed-v0.2.3-review-fixups.md`

- [ ] **Step 1: Mark v0.2.4 checklist steps complete**

In `docs/superpowers/plans/2026-05-11-agent-seed-v0.2.4-review-fixups.md`, replace every unchecked checkbox prefix with a checked checkbox prefix:

```text
unchecked: - [ ]
checked: - [x]
```

Only change checkbox prefixes in this file. Do not change command snippets or explanatory prose.

- [ ] **Step 2: Verify all findings map to changed surfaces**

Run:

```bash
rg -n '0\\.2\\.4|authorization server endpoints use HTTPS; local-development exceptions apply only to redirect URIs|non-HTTPS endpoint rejected|advertises `S256`|advertised `S256` support|S256 advertisement|c31a6990529e1c8cb06d63718b7fcdd6c02ee8ed|\\[x\\]' VERSION CHANGELOG.md .agent/SECURITY.md .agent/TEMPLATES/THREAT_MODEL.md .agent/PROMPTS.md docs/superpowers/plans/2026-05-11-agent-seed-v0.2.3-review-fixups.md docs/superpowers/plans/2026-05-11-agent-seed-v0.2.4-review-fixups.md
```

Expected:

- Version and changelog show `0.2.4`.
- MCP HTTPS endpoint and `S256` support corrections appear in security, template, and prompt surfaces.
- v0.2.3 plan evidence and v0.2.4 checked boxes are present.

- [ ] **Step 3: Check stale or prohibited text**

Run:

```bash
rg -n "approved local-development endpoin[t]|authorization server endpoints use HTTPS excep[t]|2025-0[6]-18|modelcontextprotocol.io/specification/2025-0[6]-18" README.md ADOPTION.md AGENTS.md .agent docs/superpowers/plans
rg -n "T[B]D|T[O]DO|F[I]XME|lo[r]em" README.md ADOPTION.md AGENTS.md .agent docs/superpowers/plans/2026-05-11-agent-seed-v0.2.1-review-fixes.md docs/superpowers/plans/2026-05-11-agent-seed-v0.2.2-review-fixups.md docs/superpowers/plans/2026-05-11-agent-seed-v0.2.3-review-fixups.md docs/superpowers/plans/2026-05-11-agent-seed-v0.2.4-review-fixups.md
```

Expected:

- Both `rg` commands exit 1 with no output.

- [ ] **Step 4: Check prohibited files and whitespace**

Run:

```bash
find . -path ./.git -prune -o -type f -perm -111 -print
find . -path ./.git -prune -o \( -name package.json -o -name pyproject.toml -o -name Cargo.toml -o -name go.mod -o -name Makefile -o -name justfile -o -name "*.lock" -o -path "./.github/*" -o -name CLAUDE.md -o -name GEMINI.md -o -name ".aider.conf.yml" -o -path "./.claude/*" -o -path "./.gemini/*" \) -print
git diff --check HEAD
```

Expected:

- No executable files.
- No package/build/CI/tooling files.
- No vendor-specific bridge files are added to the seed.
- `git diff --check HEAD` exits 0.

- [ ] **Step 5: Commit consistency edits**

Run:

```bash
git add docs/superpowers/plans/2026-05-11-agent-seed-v0.2.4-review-fixups.md
git commit -m "Polish v0.2.4 fixups"
```

Expected:

- The v0.2.4 plan tracking update is committed.

---

## Task 5: Merge, Push, Confirm, And Record v0.2.4 Evidence

**Files:**
- Modify after push: `docs/superpowers/plans/2026-05-11-agent-seed-v0.2.4-review-fixups.md`

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

From the feature branch, run:

```bash
git switch main
git pull --ff-only
git merge --ff-only agent-seed-v0.2.4-review-fixups
```

Expected:

- Fast-forward merge succeeds.

- [ ] **Step 3: Re-run final validation on `main`**

Run the full command set from Step 1 again.

Expected:

- Same successful result on merged `main`.

- [ ] **Step 4: Push and confirm**

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
- Remote `refs/heads/main` points to the v0.2.4 fixup commit.
- If GitHub Actions still returns an empty list, record that no hosted Actions runs exist for this repo.
- If GitHub Actions returns a run for the pushed commit, wait for it to complete and require success before cleanup.

- [ ] **Step 5: Add v0.2.4 execution evidence**

After push confirmation, record the pushed implementation tip before creating the evidence commit:

```bash
git rev-parse HEAD
```

Add this section immediately before `## Acceptance Criteria`, using the exact commit hash printed by `git rev-parse HEAD` as the implementation tip:

```markdown
## Execution Evidence

The v0.2.4 plan was executed and merged.

- Pushed v0.2.4 implementation tip before this evidence commit: `commit hash printed by git rev-parse HEAD`.
- Remote branch checked: `origin/main`.
- Local feature branch cleanup: `agent-seed-v0.2.4-review-fixups` deleted.
- Hosted CI check: `gh run list --limit 3 --json databaseId,status,conclusion,headSha,workflowName` returned `[]`, so no hosted GitHub Actions workflows existed for this repository.
- Validation evidence: clean `main`, `git diff --check HEAD` passed, executable/prohibited-file scans were empty, stale MCP scans were empty, unresolved-text scans for active artifacts were empty.
```

Commit and push the evidence:

```bash
git add docs/superpowers/plans/2026-05-11-agent-seed-v0.2.4-review-fixups.md
git commit -m "Record v0.2.4 execution evidence"
git push origin main
```

Expected:

- The v0.2.4 plan has final execution evidence.
- Remote `main` points to the execution-evidence commit.

- [ ] **Step 6: Cleanup merged feature branch**

Run:

```bash
git branch -d agent-seed-v0.2.4-review-fixups
git status --short --branch
git log -1 --oneline --decorate
```

Expected:

- Local feature branch deletes cleanly.
- `main` is clean and aligned with `origin/main`.

---

## Acceptance Criteria

v0.2.4 is complete when:

- `VERSION` is `0.2.4`.
- `CHANGELOG.md` documents the corrective release.
- `.agent/SECURITY.md` requires HTTPS authorization server endpoints and scopes localhost exceptions only to redirect URIs.
- `.agent/TEMPLATES/THREAT_MODEL.md` has a non-HTTPS authorization endpoint rejection field.
- `.agent/SECURITY.md`, `.agent/TEMPLATES/THREAT_MODEL.md`, and `.agent/PROMPTS.md` require or ask for advertised `S256` support when clients are technically capable of `S256`.
- `docs/superpowers/plans/2026-05-11-agent-seed-v0.2.3-review-fixups.md` includes v0.2.3 execution evidence.
- `docs/superpowers/plans/2026-05-11-agent-seed-v0.2.4-review-fixups.md` has no unchecked plan steps and includes final v0.2.4 execution evidence.
- No stale June 2025 MCP authorization references are present.
- No executable, package, build, CI, lockfile, generated-doc, or vendor-specific root bridge files are added.
- Final validation passes on merged `main`, and pushed `origin/main` is confirmed.

## Execution Recommendation

This is a compact corrective documentation pass. Inline execution with `superpowers:executing-plans` is sufficient.
