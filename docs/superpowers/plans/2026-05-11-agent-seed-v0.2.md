# Agent Seed v0.2 Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build `agent-seed` v0.2 as a layered, markdown-first guidance set for elite agent-assisted engineering and research work across security-sensitive, AI/ML, systems, accelerator, compiler, quantum, formal, robotics, frontend, and autonomous-research projects.

**Architecture:** Keep `AGENTS.md` compact as the root operating contract. Add optional `.agent/` modules for quality, security, adapters, review protocol, domain overlays, and richer templates so serious repositories can opt into more rigor without turning the root file into a manual. Treat v0.2 as guidance and templates only: no CLI, no installer, no CI, no package metadata, no lockfiles, no generated docs.

**Tech Stack:** Markdown files only, shell validation with existing system tools (`find`, `sort`, `wc`, `rg`, `git`). No dependencies.

---

## Source Inputs

Use these sources and current repo files as the v0.2 source of truth:

- Current repo files on `main`, especially `AGENTS.md`, `README.md`, `ADOPTION.md`, `.agent/WORKFLOW.md`, `.agent/STANDARDS.md`, `.agent/DONE.md`, `.agent/PROMPTS.md`, `.agent/LOCAL_CONTEXT.example.md`, and `.agent/TEMPLATES/*`.
- User quality bar: standards should reflect principal or distinguished engineer/scientist rigor at the top of the field.
- Review findings from the v0.1 pass:
  1. Agentic AI security is too generic.
  2. Domain rigor is too shallow for the user's project areas.
  3. The elite quality bar is not explicit enough.
  4. Ecosystem adapter guidance is missing.
  5. Nested instruction precedence is underdocumented.
  6. Benchmark/performance templates need more rigor.
  7. AI/ML lifecycle guidance is missing.
  8. Formal/research evidence guidance is too shallow.
  9. License adoption guidance is missing.
  10. Specialist/subagent review procedure is missing.
- Current external references as of mid-May 2026:
  - AGENTS.md ecosystem and nested precedence: https://agents.md/
  - OpenAI Codex AGENTS.md behavior: https://openai.com/index/introducing-codex/
  - GitHub Copilot repository, path-specific, and agent instructions: https://docs.github.com/en/copilot/how-tos/custom-instructions/adding-repository-custom-instructions-for-github-copilot
  - Claude Code memory/settings and permissions: https://docs.anthropic.com/en/docs/claude-code/memory and https://docs.anthropic.com/en/docs/claude-code/settings
  - Gemini CLI context files and configuration: https://google-gemini.github.io/gemini-cli/docs/cli/gemini-md.html and https://google-gemini.github.io/gemini-cli/docs/cli/configuration.html
  - Five Eyes/NSA agentic AI guidance: https://www.nsa.gov/Press-Room/Press-Releases-Statements/Press-Release-View/Article/4475134/nsa-joins-the-asds-acsc-and-others-to-release-guidance-on-agentic-artificial-in/
  - OWASP Top 10 for Agentic Applications 2026: https://genai.owasp.org/resource/owasp-top-10-for-agentic-applications-for-2026/
  - OWASP Agentic Skills Top 10: https://owasp.org/www-project-agentic-skills-top-10/
  - NIST AI RMF and GenAI profile: https://www.nist.gov/itl/ai-risk-management-framework and https://www.nist.gov/publications/artificial-intelligence-risk-management-framework-generative-artificial-intelligence
  - NIST SSDF and SP 800-218A for generative AI/foundation model development: https://csrc.nist.gov/projects/ssdf and https://csrc.nist.gov/pubs/sp/800/218/a/final
  - MCP authorization/security model: https://modelcontextprotocol.io/specification/2025-11-25/basic/authorization
  - OpenSSF Scorecard and SLSA: https://openssf.org/projects/scorecard/ and https://openssf.org/projects/slsa/
  - Hugging Face model cards and dataset cards: https://huggingface.co/docs/hub/en/model-cards and https://huggingface.co/docs/datasets/v2.19.0/en/dataset_card
  - MLCommons MLPerf Inference v6.0: https://mlcommons.org/2026/04/mlperf-inference-v6-0-results/
  - CUDA best practices: https://docs.nvidia.com/cuda/cuda-c-best-practices-guide/index.html
  - Linux kernel selftests: https://docs.kernel.org/dev-tools/kselftest.html
  - LLVM developer policy: https://llvm.org/docs/DeveloperPolicy.html
  - Rust unsafe and undefined behavior reference: https://doc.rust-lang.org/reference/unsafety.html and https://doc.rust-lang.org/reference/behavior-considered-undefined.html
  - OpenQASM 3.1 and QIR: https://openqasm.com/versions/3.1/ and https://quantum.microsoft.com/en-us/insights/education/concepts/quantum-intermediate-representation
  - Rocq rename/releases and Lean/mathlib status: https://rocq-prover.org/changelog and https://reservoir.lean-lang.org/%40leanprover-community/mathlib
  - ROS 2 quality/security/QoS guidance: https://docs.ros.org/en/rolling/The-ROS2-Project/Contributing/Quality-Guide.html and https://docs.ros.org/en/ros2_documentation/kilted/Concepts/Intermediate/About-Security.html

## File Structure

### Modify Existing Files

- `AGENTS.md`: keep compact; add quality bar pointer, agentic security pointer, nested guidance pointer, review protocol pointer, and updated useful supporting files.
- `README.md`: document v0.2 structure, optional overlays, adapter guidance, review protocol, and license/adoption position.
- `ADOPTION.md`: add high-rigor adoption mode, domain overlay selection, license-adoption notes, nested/monorepo setup, and adapter guidance.
- `CHANGELOG.md`: add `0.2.0` section.
- `VERSION`: change to `0.2.0`.
- `.agent/WORKFLOW.md`: add research refresh, source-of-truth discipline, review protocol entry point, and risk-based specialist review trigger.
- `.agent/STANDARDS.md`: add stronger quality bar, agentic security, AI/ML, systems/kernel, accelerators, compilers, formal methods, robotics/autonomy, frontends, and supply-chain criteria while still pointing domain detail to overlays.
- `.agent/DONE.md`: add evidence-grade completion criteria, specialist review evidence, reproducibility, and final risk/accountability language.
- `.agent/PROMPTS.md`: add prompts for threat modeling, adapter setup, subagent/specialist review, AI/ML eval, benchmark, formal proof review, autonomous research review, and domain overlay adoption.
- `.agent/LOCAL_CONTEXT.example.md`: add fields for quality bar, domain overlays, agent/tool permissions, data/model/artifact governance, hardware topology, safety constraints, and specialist review lanes.
- `.agent/TEMPLATES/BENCHMARK_NOTE.md`: expand performance evidence requirements.
- `.agent/TEMPLATES/REVIEW.md`: align with review protocol and specialist review lanes.
- `.agent/TEMPLATES/REPO_AUDIT.md`: add agentic security, adapter, nested guidance, domain, and review-readiness sections.
- `.agent/TEMPLATES/EXEC_PLAN.md`: add quality bar, review plan, domain overlay, evidence plan, and rollback/accountability details.
- `.gitignore`: add local-only agent/tool state files if needed without excluding seed files.

### Create New Core Guidance Files

- `.agent/QUALITY_BAR.md`: elite engineering/scientific standards and evidence ladder.
- `.agent/SECURITY.md`: agentic AI, tool/MCP, secrets, memory/context, supply-chain, autonomy, and operational security guidance.
- `.agent/ADAPTERS.md`: how to adapt the seed to Codex, Claude Code, Gemini CLI, GitHub Copilot, Cursor, Aider, and generic agents.
- `.agent/REVIEW_PROTOCOL.md`: self-review, specialist subagent review, adversarial review, integration review, and disagreement resolution.
- `.agent/NESTED_GUIDANCE.md`: monorepo/subproject `AGENTS.md` strategy, precedence, and conflict handling.

### Create Domain Overlays

- `.agent/DOMAINS/README.md`: how to select and use overlays.
- `.agent/DOMAINS/AI_ML.md`: models, data, training, inference, evals, safety, security, reproducibility.
- `.agent/DOMAINS/SYSTEMS_KERNELS.md`: OS, kernels, drivers, firmware, ABI/API, undefined behavior, testing, safety.
- `.agent/DOMAINS/ACCELERATORS.md`: heterogeneous hardware, GPU/TPU/NPU kernels, profiling, numerical correctness, determinism.
- `.agent/DOMAINS/COMPILERS.md`: IR, lowering, optimization, correctness, diagnostics, compatibility, tests.
- `.agent/DOMAINS/QUANTUM.md`: circuits, OpenQASM/QIR, simulators, hardware constraints, error models, reproducibility.
- `.agent/DOMAINS/FORMAL_VERIFICATION.md`: Lean, Rocq, SMT, model checking, theorem status, assumptions, proof artifacts.
- `.agent/DOMAINS/ROBOTICS_AUTONOMY.md`: ROS 2, safety cases, simulation, hardware tests, QoS, security, observability.
- `.agent/DOMAINS/FRONTENDS.md`: accessible UI, visual verification, browser testing, product ergonomics, state and data contracts.
- `.agent/DOMAINS/AUTONOMOUS_RESEARCH.md`: autonomous literature review, experiment planning, claim tracking, replication, artifact hygiene.

### Create New Templates

- `.agent/TEMPLATES/THREAT_MODEL.md`: security and agentic AI threat model.
- `.agent/TEMPLATES/SPECIALIST_REVIEW.md`: specialist/subagent review output format.
- `.agent/TEMPLATES/DOMAIN_OVERLAY_ADOPTION.md`: document which overlays apply to a target repo.
- `.agent/TEMPLATES/MODEL_CARD.md`: model documentation.
- `.agent/TEMPLATES/DATASET_CARD.md`: dataset documentation.
- `.agent/TEMPLATES/EVAL_REPORT.md`: model/system evaluation report.
- `.agent/TEMPLATES/EXPERIMENT_LOG.md`: scientific/engineering experiment record.
- `.agent/TEMPLATES/TRAINING_RUN.md`: AI/ML training run record.
- `.agent/TEMPLATES/INFERENCE_DEPLOYMENT.md`: inference serving/deployment evidence.
- `.agent/TEMPLATES/DATA_PROVENANCE.md`: data lineage and licensing record.
- `.agent/TEMPLATES/RESEARCH_CLAIM.md`: claim, evidence, uncertainty, and replication status.
- `.agent/TEMPLATES/FORMAL_PROOF_NOTE.md`: theorem/proof status and assumptions.
- `.agent/TEMPLATES/HARDWARE_BENCHMARK.md`: hardware/accelerator benchmark evidence.
- `.agent/TEMPLATES/INTERFACE_CONTRACT.md`: API/UI/protocol/schema contract review.
- `.agent/TEMPLATES/SAFETY_CASE.md`: robotics/autonomy/safety-sensitive argument and evidence.

---

## Task 1: Version and Navigation Skeleton

**Files:**
- Modify: `README.md`
- Modify: `ADOPTION.md`
- Modify: `CHANGELOG.md`
- Modify: `VERSION`
- Modify: `AGENTS.md`

- [x] **Step 1: Update version metadata**

Set `VERSION` to:

```text
0.2.0
```

Add a top `CHANGELOG.md` section:

```markdown
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
```

- [x] **Step 2: Update root navigation without bloating `AGENTS.md`**

In `AGENTS.md`, add short bullets pointing to these new files:

```text
.agent/QUALITY_BAR.md              Highest-standard engineering and scientific expectations.
.agent/SECURITY.md                 Agentic AI, tool, data, and supply-chain security.
.agent/ADAPTERS.md                 Adapting guidance to Codex, Claude, Gemini, Copilot, Cursor, Aider, and generic agents.
.agent/REVIEW_PROTOCOL.md          Self-review, specialist review, adversarial review, and integration review.
.agent/NESTED_GUIDANCE.md          Monorepo and nested instruction guidance.
.agent/DOMAINS/                    Optional domain overlays.
```

- [x] **Step 3: Update `README.md` structure**

Add sections that explain:

- v0.2 keeps the root seed markdown-only and dependency-free.
- core guidance is always useful.
- overlays are optional and should be copied only when relevant.
- high-rigor projects can adopt `.agent/QUALITY_BAR.md`, `.agent/SECURITY.md`, `.agent/REVIEW_PROTOCOL.md`, and selected `.agent/DOMAINS/*`.
- `LICENSE` is MIT for the seed content.

- [x] **Step 4: Update `ADOPTION.md` modes**

Add a fourth adoption mode:

```text
Mode 4: High-rigor adoption
```

This mode should copy:

```text
AGENTS.md
.agent/WORKFLOW.md
.agent/STANDARDS.md
.agent/DONE.md
.agent/QUALITY_BAR.md
.agent/SECURITY.md
.agent/REVIEW_PROTOCOL.md
.agent/ADAPTERS.md
.agent/NESTED_GUIDANCE.md
.agent/LOCAL_CONTEXT.example.md
.agent/TEMPLATES/
selected .agent/DOMAINS/
```

Add license guidance:

- `agent-seed` is MIT licensed.
- Target repositories should keep their own project license.
- If copying seed content, preserve attribution where appropriate for the organization's policy.
- Do not replace a target repository license accidentally.

- [x] **Step 5: Validate skeleton**

Run:

```bash
find . -path ./.git -prune -o -maxdepth 4 -type f -print | sort
rg -n "0\\.2\\.0|QUALITY_BAR|SECURITY|ADAPTERS|REVIEW_PROTOCOL|NESTED_GUIDANCE|DOMAINS" README.md ADOPTION.md AGENTS.md CHANGELOG.md VERSION
git diff --stat
```

Expected:

- New files are referenced but not yet all created until later tasks.
- No package, CI, lockfile, or executable tooling appears.

- [x] **Step 6: Commit**

```bash
git add README.md ADOPTION.md AGENTS.md CHANGELOG.md VERSION
git commit -m "Plan v0.2 navigation and versioning"
```

---

## Task 2: Elite Quality Bar

**Files:**
- Create: `.agent/QUALITY_BAR.md`
- Modify: `.agent/STANDARDS.md`
- Modify: `.agent/DONE.md`
- Modify: `AGENTS.md`

- [x] **Step 1: Create `.agent/QUALITY_BAR.md`**

Create the file with these sections and concrete expectations:

```markdown
# Quality bar

This repository expects agent-assisted work to meet a principal or distinguished engineer/scientist standard.

## Core expectation

Work should be precise, evidence-driven, reviewable, reversible, and honest about uncertainty.

## Engineering standard

- Prefer source-of-truth evidence over summaries.
- Preserve compatibility unless the task explicitly changes it.
- Make narrow changes that solve the actual problem.
- Use existing abstractions before inventing new ones.
- Prove behavior with tests, checks, benchmarks, traces, or formal arguments appropriate to the risk.
- Do not trade correctness, security, maintainability, or reproducibility for speed without explicit approval.

## Scientific standard

- Separate claims from evidence.
- State assumptions, units, tolerances, datasets, hardware, seeds, and environment.
- Preserve enough metadata for another expert to reproduce or challenge the result.
- Treat negative results as evidence when they are measured carefully.
- Avoid overstating conclusions from weak or narrow measurements.

## Evidence ladder

Evidence strength, from weakest to strongest:

1. Reasoned inspection.
2. Targeted manual reproduction.
3. Targeted automated tests.
4. Broad automated checks.
5. Benchmarks with environment and variance.
6. Cross-platform or cross-backend validation.
7. Independent specialist review.
8. Formal proof or mechanically checked invariant.
9. Production or field evidence with monitoring and rollback.

Use the strongest practical evidence for the risk level.

## Review posture

- Review your own diff before asking others to trust it.
- Invite specialist review for areas outside ordinary application code.
- Treat unresolved reviewer disagreement as a risk, not as noise.
- Final accountability stays with the integrating agent or maintainer.
```

- [x] **Step 2: Tighten `.agent/STANDARDS.md`**

Add a short section near the top:

```markdown
## 0. Quality bar

For high-rigor repositories, use `.agent/QUALITY_BAR.md` as the governing standard. Generic guidance in this file is a floor, not a ceiling.
```

Add references to stronger evidence requirements in correctness, tests, validation, performance, security, and scientific sections.

- [x] **Step 3: Tighten `.agent/DONE.md`**

Add criteria:

- final evidence must match risk,
- specialist review is complete or explicitly deferred,
- unvalidated claims are labeled as assumptions,
- reproducibility metadata exists for research/performance work,
- rollback or recovery has been considered for high-risk changes.

- [x] **Step 4: Keep `AGENTS.md` compact**

Add one root-level principle:

```markdown
- Treat `.agent/QUALITY_BAR.md` as the standard for high-rigor work; generic guidance is a floor, not a ceiling.
```

- [x] **Step 5: Validate quality-bar integration**

Run:

```bash
rg -n "principal|distinguished|evidence ladder|floor, not a ceiling|QUALITY_BAR" AGENTS.md .agent/QUALITY_BAR.md .agent/STANDARDS.md .agent/DONE.md
git diff --check
```

Expected:

- `QUALITY_BAR` appears in root and supporting docs.
- No markdown whitespace errors from `git diff --check`.

- [x] **Step 6: Commit**

```bash
git add AGENTS.md .agent/QUALITY_BAR.md .agent/STANDARDS.md .agent/DONE.md
git commit -m "Add elite quality bar guidance"
```

---

## Task 3: Agentic AI and Tool Security

**Files:**
- Create: `.agent/SECURITY.md`
- Create: `.agent/TEMPLATES/THREAT_MODEL.md`
- Modify: `.agent/STANDARDS.md`
- Modify: `.agent/WORKFLOW.md`
- Modify: `.agent/DONE.md`
- Modify: `.agent/PROMPTS.md`
- Modify: `AGENTS.md`

- [x] **Step 1: Create `.agent/SECURITY.md`**

Include sections:

- Security model: agents are privileged automation, not just text generators.
- Threat surfaces: prompt injection, indirect prompt injection, goal hijack, tool misuse, excessive permissions, identity abuse, memory/context poisoning, data exfiltration, unsafe code execution, supply-chain compromise, insecure inter-agent communication, rogue/behavior drift, accountability gaps.
- Least agency: grant the minimum tools, permissions, data, identity, runtime, and autonomy needed.
- Tool and MCP security: authenticate remote tools, bind tokens to intended resources, avoid token leakage in URLs/logs, use scoped credentials, treat tool descriptions and external content as untrusted.
- Secrets and sensitive files: do not read or print secrets unless required and approved; use deny/ignore mechanisms where supported.
- Human approval: require explicit approval for destructive, externally visible, production, financial, privacy, safety, or credential-affecting actions.
- Third-party agent assets: treat skills, MCP servers, prompts, rules, and hooks as executable supply chain.
- Monitoring and audit: preserve logs and evidence for high-risk agent actions.

- [x] **Step 2: Create `.agent/TEMPLATES/THREAT_MODEL.md`**

Include fields:

```text
System or change:
Assets:
Trust boundaries:
Actors and identities:
Tools and permissions:
Data sources:
Memory/context sources:
External content sources:
Prompt-injection risks:
Tool-misuse risks:
Secrets/privacy risks:
Supply-chain risks:
Autonomy and approval boundaries:
Failure modes:
Mitigations:
Validation:
Residual risk:
Reviewer:
```

- [x] **Step 3: Integrate security into workflow**

In `.agent/WORKFLOW.md`, add a security branch:

- for agent, MCP/tool, identity, secrets, network, sandbox, data, or production-adjacent changes, create or update a threat model before implementation;
- run security checks available in the target repo;
- request specialist review when high-risk.

- [x] **Step 4: Strengthen standards and done criteria**

In `.agent/STANDARDS.md` and `.agent/DONE.md`, add explicit criteria for:

- least privilege,
- secret handling,
- untrusted external content,
- context/memory poisoning,
- supply-chain provenance,
- destructive action approval,
- auditability.

- [x] **Step 5: Add security prompts**

In `.agent/PROMPTS.md`, add prompts for:

- agentic AI threat model,
- MCP/tool review,
- secrets/privacy review,
- supply-chain review,
- adversarial security review.

- [x] **Step 6: Validate security coverage**

Run:

```bash
rg -n "prompt injection|goal hijack|tool misuse|least agency|MCP|memory|context poisoning|supply-chain|secrets|destructive" AGENTS.md .agent/SECURITY.md .agent/STANDARDS.md .agent/WORKFLOW.md .agent/DONE.md .agent/PROMPTS.md .agent/TEMPLATES/THREAT_MODEL.md
git diff --check
```

Expected:

- Each major agentic AI risk class appears at least once.
- The root file points to `.agent/SECURITY.md` without becoming long.

- [x] **Step 7: Commit**

```bash
git add AGENTS.md .agent/SECURITY.md .agent/STANDARDS.md .agent/WORKFLOW.md .agent/DONE.md .agent/PROMPTS.md .agent/TEMPLATES/THREAT_MODEL.md
git commit -m "Add agentic AI security guidance"
```

---

## Task 4: Ecosystem Adapters and Nested Guidance

**Files:**
- Create: `.agent/ADAPTERS.md`
- Create: `.agent/NESTED_GUIDANCE.md`
- Modify: `README.md`
- Modify: `ADOPTION.md`
- Modify: `.agent/PROMPTS.md`
- Modify: `.gitignore`

- [x] **Step 1: Create `.agent/ADAPTERS.md`**

Include sections:

- Purpose: adapt the seed to agent ecosystems without duplicating conflicting instructions.
- Codex/OpenAI: `AGENTS.md`, nested scope, checks, final evidence.
- Claude Code: `CLAUDE.md`, `.claude/settings.json`, deny rules for sensitive files, imports, local settings.
- Gemini CLI: `GEMINI.md`, configurable `context.fileName`, memory commands, `.geminiignore`.
- GitHub Copilot: `.github/copilot-instructions.md`, `.github/instructions/*.instructions.md`, `AGENTS.md`, `CLAUDE.md`, `GEMINI.md`.
- Cursor/other IDE agents: use project rules where supported, keep root seed as source of truth.
- Aider: configure `AGENTS.md` as a read file.
- Generic agents: read `AGENTS.md`, then `.agent/LOCAL_CONTEXT.md`, then selected overlays.
- Conflict policy: one source of truth, adapters should point back to seed files.

- [x] **Step 2: Create `.agent/NESTED_GUIDANCE.md`**

Include sections:

- When to add nested `AGENTS.md`.
- Monorepo examples.
- Precedence: nearer file wins for files in scope; direct user instructions override repo guidance.
- Avoid duplication: nested files should add local facts, not repeat root policy.
- Required nested sections: commands, local risks, local tests, local ownership, local done criteria.
- Conflict handling and review.

- [x] **Step 3: Update adoption docs**

In `ADOPTION.md`, add instructions for:

- selecting adapter files,
- using symlinks or lightweight bridge files only when desired by a target repo,
- not adding vendor-specific files to the seed by default,
- adding nested files for packages/components in monorepos.

- [x] **Step 4: Update prompts**

Add prompts:

- "Create adapter guidance for this repository."
- "Audit nested instruction coverage for this monorepo."
- "Convert existing CLAUDE/GEMINI/Copilot instructions into AGENTS.md without losing local facts."

- [x] **Step 5: Update `.gitignore` for local agent settings**

Add only local/private files, not shared config:

```gitignore
# Local agent tool state
.claude/settings.local.json
.gemini/.cache/
.aider*
```

Do not ignore shared guidance files such as `AGENTS.md`, `CLAUDE.md`, `GEMINI.md`, or `.github/copilot-instructions.md`.

- [x] **Step 6: Validate adapters**

Run:

```bash
rg -n "Codex|Claude|Gemini|Copilot|Cursor|Aider|nested|precedence|monorepo|nearest" README.md ADOPTION.md .agent/ADAPTERS.md .agent/NESTED_GUIDANCE.md .agent/PROMPTS.md .gitignore
git diff --check
```

Expected:

- Adapter guidance is informative but vendor-specific files are not added to the seed root.

- [x] **Step 7: Commit**

```bash
git add README.md ADOPTION.md .agent/ADAPTERS.md .agent/NESTED_GUIDANCE.md .agent/PROMPTS.md .gitignore
git commit -m "Add adapter and nested guidance"
```

---

## Task 5: Specialist and Subagent Review Protocol

**Files:**
- Create: `.agent/REVIEW_PROTOCOL.md`
- Create: `.agent/TEMPLATES/SPECIALIST_REVIEW.md`
- Modify: `.agent/TEMPLATES/REVIEW.md`
- Modify: `.agent/WORKFLOW.md`
- Modify: `.agent/DONE.md`
- Modify: `.agent/PROMPTS.md`
- Modify: `AGENTS.md`

- [x] **Step 1: Create `.agent/REVIEW_PROTOCOL.md`**

Define review layers:

- Self-review: required for all changes.
- Peer/specialist review: required for high-risk or domain-specific work.
- Adversarial review: required for security, autonomy, data/model, and safety-sensitive work.
- Integration review: required before finalizing multi-file or multi-domain changes.

Define specialist review lanes:

- Security and agentic AI.
- AI/ML and evaluation.
- Systems/kernel/unsafe/firmware.
- Accelerators/performance.
- Compilers/language/runtime.
- Quantum.
- Formal verification/math.
- Robotics/autonomy/safety.
- Frontend/product/accessibility.
- Documentation/source-of-truth.

Define subagent rules:

- Use fresh context for independent review when available.
- Give reviewers exact scope, files, source-of-truth docs, checks, and expected output.
- Reviewers must inspect evidence, not just summaries.
- Findings lead, ordered by severity.
- A reviewer may say "insufficient evidence".
- Final accountability stays with the integrating agent/maintainer.
- Destructive, production, credential, legal, privacy, or safety decisions cannot be delegated away.

Define disagreement policy:

- If reviewers disagree, preserve both positions.
- The stricter safety/security/correctness position governs until the maintainer decides.
- Record accepted risk in final notes or design record.

- [x] **Step 2: Create `.agent/TEMPLATES/SPECIALIST_REVIEW.md`**

Include fields:

```text
Review lane:
Scope reviewed:
Source-of-truth files inspected:
Diff or artifacts inspected:
Validation evidence inspected:
Findings:
Blocking issues:
Non-blocking issues:
Evidence gaps:
Recommended follow-up:
Final recommendation:
Reviewer uncertainty:
```

- [x] **Step 3: Update generic review template**

In `.agent/TEMPLATES/REVIEW.md`, add:

- review lane,
- whether specialist review is required,
- whether adversarial review is required,
- evidence inspected,
- source-of-truth drift,
- final accountability.

- [x] **Step 4: Add workflow triggers**

In `.agent/WORKFLOW.md`, define triggers for specialist review:

- security-sensitive,
- agent/tool/MCP/autonomy,
- AI/ML model/data/eval,
- kernel/unsafe/concurrency,
- accelerator/performance,
- compiler/language semantics,
- formal proof,
- robotics/safety,
- user-facing frontend workflows,
- broad docs/source-of-truth rewrites.

- [x] **Step 5: Add prompts**

Add prompts for:

- specialist review,
- adversarial security review,
- domain review,
- integration review,
- resolving review disagreement.

- [x] **Step 6: Validate review protocol**

Run:

```bash
rg -n "specialist|subagent|adversarial|integration review|review lane|accountability|disagreement" AGENTS.md .agent/REVIEW_PROTOCOL.md .agent/TEMPLATES/SPECIALIST_REVIEW.md .agent/TEMPLATES/REVIEW.md .agent/WORKFLOW.md .agent/DONE.md .agent/PROMPTS.md
git diff --check
```

Expected:

- Review protocol is explicit, tool-agnostic, and domain-aware.

- [x] **Step 7: Commit**

```bash
git add AGENTS.md .agent/REVIEW_PROTOCOL.md .agent/TEMPLATES/SPECIALIST_REVIEW.md .agent/TEMPLATES/REVIEW.md .agent/WORKFLOW.md .agent/DONE.md .agent/PROMPTS.md
git commit -m "Add specialist review protocol"
```

---

## Task 6: Domain Overlay Framework

**Files:**
- Create: `.agent/DOMAINS/README.md`
- Create: `.agent/TEMPLATES/DOMAIN_OVERLAY_ADOPTION.md`
- Modify: `README.md`
- Modify: `ADOPTION.md`
- Modify: `.agent/LOCAL_CONTEXT.example.md`
- Modify: `.agent/PROMPTS.md`

- [x] **Step 1: Create `.agent/DOMAINS/README.md`**

Define:

- overlays are optional,
- target repos should copy only relevant overlays,
- local context should list active overlays,
- overlays do not override local source-of-truth facts,
- overlays can require stronger validation than generic guidance,
- if overlays conflict, the more safety-critical or specific rule governs until maintainers decide.

- [x] **Step 2: Create `.agent/TEMPLATES/DOMAIN_OVERLAY_ADOPTION.md`**

Include:

```text
Target repository:
Active overlays:
Why each overlay applies:
Files/modules covered:
Commands and checks:
Specialist review lanes:
Domain-specific risks:
Evidence requirements:
Maintainer decisions:
Deferred overlays:
```

- [x] **Step 3: Update local context example**

Add fields:

```text
Active domain overlays:
Specialist review lanes:
Quality bar level:
Agent/tool permission boundaries:
Safety-sensitive operations:
Hardware/runtime environments:
Data/model/artifact governance:
Reproducibility requirements:
```

- [x] **Step 4: Update adoption and prompts**

Add:

- overlay selection checklist,
- prompt for adopting overlays,
- prompt for auditing whether overlays are missing,
- prompt for pruning overlays that do not apply.

- [x] **Step 5: Validate framework**

Run:

```bash
rg -n "overlay|DOMAINS|DOMAIN_OVERLAY|specialist review lanes|Quality bar level|permission boundaries" README.md ADOPTION.md .agent/DOMAINS/README.md .agent/TEMPLATES/DOMAIN_OVERLAY_ADOPTION.md .agent/LOCAL_CONTEXT.example.md .agent/PROMPTS.md
git diff --check
```

Expected:

- Overlay framework exists before domain-specific files are added.

- [x] **Step 6: Commit**

```bash
git add README.md ADOPTION.md .agent/DOMAINS/README.md .agent/TEMPLATES/DOMAIN_OVERLAY_ADOPTION.md .agent/LOCAL_CONTEXT.example.md .agent/PROMPTS.md
git commit -m "Add domain overlay framework"
```

---

## Task 7: AI/ML, Data, Evaluation, and Autonomous Research Overlays

**Files:**
- Create: `.agent/DOMAINS/AI_ML.md`
- Create: `.agent/DOMAINS/AUTONOMOUS_RESEARCH.md`
- Create: `.agent/TEMPLATES/MODEL_CARD.md`
- Create: `.agent/TEMPLATES/DATASET_CARD.md`
- Create: `.agent/TEMPLATES/EVAL_REPORT.md`
- Create: `.agent/TEMPLATES/EXPERIMENT_LOG.md`
- Create: `.agent/TEMPLATES/TRAINING_RUN.md`
- Create: `.agent/TEMPLATES/INFERENCE_DEPLOYMENT.md`
- Create: `.agent/TEMPLATES/DATA_PROVENANCE.md`
- Create: `.agent/TEMPLATES/RESEARCH_CLAIM.md`
- Modify: `.agent/STANDARDS.md`
- Modify: `.agent/PROMPTS.md`

- [x] **Step 1: Create `.agent/DOMAINS/AI_ML.md`**

Include sections:

- applicability,
- model/data/artifact source of truth,
- data provenance and licensing,
- contamination and leakage checks,
- train/eval/test split discipline,
- reproducibility: seeds, versions, hardware, runtime, checkpoints,
- evaluation: baselines, metrics, confidence intervals or variance, failure slices,
- safety/security: prompt injection, data exfiltration, model supply chain, jailbreak/red-team where relevant,
- inference: latency, throughput, memory, precision, batching, quantization, fallback behavior,
- training: optimizer, schedule, checkpointing, resume, distributed failure, cost,
- documentation: model cards, dataset cards, eval reports.

- [x] **Step 2: Create `.agent/DOMAINS/AUTONOMOUS_RESEARCH.md`**

Include:

- literature source-of-truth,
- claim graph or claim inventory,
- hypothesis and experiment separation,
- autonomous agent boundaries,
- replication requirements,
- negative result handling,
- artifact retention,
- human review before external publication or high-impact claims.

- [x] **Step 3: Create AI/ML templates**

Create templates with explicit fields:

- `MODEL_CARD.md`: intended use, limitations, training data, evals, safety, license, provenance, version.
- `DATASET_CARD.md`: source, license, collection process, consent/privacy, schema, splits, bias, restrictions.
- `EVAL_REPORT.md`: system under test, metrics, datasets, baselines, statistical treatment, failure cases, limitations.
- `EXPERIMENT_LOG.md`: hypothesis, setup, commands, environment, artifacts, results, interpretation, next step.
- `TRAINING_RUN.md`: data, config, hardware, distributed setup, checkpoints, failures, cost, metrics.
- `INFERENCE_DEPLOYMENT.md`: model/runtime, hardware, SLOs, load shape, fallback, monitoring, rollback.
- `DATA_PROVENANCE.md`: origin, license, transformation, lineage, retention, privacy, reproducibility.
- `RESEARCH_CLAIM.md`: claim, evidence, counterevidence, assumptions, replication status, confidence.

- [x] **Step 4: Integrate lightly**

In `.agent/STANDARDS.md`, add a short AI/ML lifecycle section that points to the overlay and templates.

In `.agent/PROMPTS.md`, add prompts for:

- model card creation,
- dataset card creation,
- eval report,
- experiment log,
- autonomous research audit.

- [x] **Step 5: Validate AI/ML coverage**

Run:

```bash
rg -n "model card|dataset card|contamination|leakage|eval|training|inference|provenance|replication|autonomous research" .agent/DOMAINS/AI_ML.md .agent/DOMAINS/AUTONOMOUS_RESEARCH.md .agent/TEMPLATES/*.md .agent/STANDARDS.md .agent/PROMPTS.md
git diff --check
```

Expected:

- AI/ML lifecycle is covered from data to training to eval to inference.

- [x] **Step 6: Commit**

```bash
git add .agent/DOMAINS/AI_ML.md .agent/DOMAINS/AUTONOMOUS_RESEARCH.md .agent/TEMPLATES/MODEL_CARD.md .agent/TEMPLATES/DATASET_CARD.md .agent/TEMPLATES/EVAL_REPORT.md .agent/TEMPLATES/EXPERIMENT_LOG.md .agent/TEMPLATES/TRAINING_RUN.md .agent/TEMPLATES/INFERENCE_DEPLOYMENT.md .agent/TEMPLATES/DATA_PROVENANCE.md .agent/TEMPLATES/RESEARCH_CLAIM.md .agent/STANDARDS.md .agent/PROMPTS.md
git commit -m "Add AI and research lifecycle guidance"
```

---

## Task 8: Systems, Accelerators, and Performance Overlays

**Files:**
- Create: `.agent/DOMAINS/SYSTEMS_KERNELS.md`
- Create: `.agent/DOMAINS/ACCELERATORS.md`
- Create: `.agent/TEMPLATES/HARDWARE_BENCHMARK.md`
- Modify: `.agent/TEMPLATES/BENCHMARK_NOTE.md`
- Modify: `.agent/STANDARDS.md`
- Modify: `.agent/PROMPTS.md`

- [x] **Step 1: Create `.agent/DOMAINS/SYSTEMS_KERNELS.md`**

Include:

- OS/kernel/driver/firmware applicability,
- ABI/API compatibility,
- unsafe code and undefined behavior,
- concurrency and interrupt/preemption concerns,
- memory ordering and synchronization,
- resource lifetime,
- fault injection,
- fuzzing/static/dynamic analysis,
- cross-platform and architecture-specific validation,
- rollback and boot/recovery considerations.

- [x] **Step 2: Create `.agent/DOMAINS/ACCELERATORS.md`**

Include:

- heterogeneous CPU/GPU/TPU/NPU/FPGA applicability,
- hardware topology,
- runtime/compiler stack,
- profiling-first workflow,
- numerical equivalence and tolerances,
- precision/quantization,
- deterministic vs nondeterministic kernels,
- memory transfers and bandwidth,
- occupancy/throughput/latency,
- power/energy when relevant,
- multi-device and distributed behavior,
- correctness before speed.

- [x] **Step 3: Expand benchmark templates**

Update `.agent/TEMPLATES/BENCHMARK_NOTE.md` and create `.agent/TEMPLATES/HARDWARE_BENCHMARK.md` with fields:

```text
Hardware:
Topology:
Firmware/driver/runtime:
Compiler flags:
Dataset/workload:
Precision:
Batch/concurrency:
Warmup:
Runs:
Variance:
Power/energy:
Correctness checks:
Baseline:
After:
Regression threshold:
Artifacts:
```

- [x] **Step 4: Integrate standards and prompts**

Add short pointers in `.agent/STANDARDS.md`.

Add prompts for:

- kernel/unsafe review,
- accelerator performance review,
- hardware benchmark note,
- profiling-first optimization.

- [x] **Step 5: Validate systems/performance coverage**

Run:

```bash
rg -n "undefined behavior|ABI|memory ordering|fuzz|hardware topology|driver|runtime|precision|quantization|warmup|variance|power|energy" .agent/DOMAINS/SYSTEMS_KERNELS.md .agent/DOMAINS/ACCELERATORS.md .agent/TEMPLATES/BENCHMARK_NOTE.md .agent/TEMPLATES/HARDWARE_BENCHMARK.md .agent/STANDARDS.md .agent/PROMPTS.md
git diff --check
```

Expected:

- Benchmark templates require enough metadata for expert review.

- [x] **Step 6: Commit**

```bash
git add .agent/DOMAINS/SYSTEMS_KERNELS.md .agent/DOMAINS/ACCELERATORS.md .agent/TEMPLATES/BENCHMARK_NOTE.md .agent/TEMPLATES/HARDWARE_BENCHMARK.md .agent/STANDARDS.md .agent/PROMPTS.md
git commit -m "Add systems and accelerator guidance"
```

---

## Task 9: Compilers, Quantum, and Formal Verification Overlays

**Files:**
- Create: `.agent/DOMAINS/COMPILERS.md`
- Create: `.agent/DOMAINS/QUANTUM.md`
- Create: `.agent/DOMAINS/FORMAL_VERIFICATION.md`
- Create: `.agent/TEMPLATES/FORMAL_PROOF_NOTE.md`
- Create: `.agent/TEMPLATES/INTERFACE_CONTRACT.md`
- Modify: `.agent/STANDARDS.md`
- Modify: `.agent/PROMPTS.md`

- [x] **Step 1: Create `.agent/DOMAINS/COMPILERS.md`**

Include:

- language and IR source-of-truth,
- parser/lowering/typechecker/optimizer/codegen boundaries,
- semantic preservation,
- diagnostics and error messages,
- compatibility and migration,
- golden tests and negative tests,
- differential testing,
- fuzzing,
- performance impact,
- release notes for user-facing language changes.

- [x] **Step 2: Create `.agent/DOMAINS/QUANTUM.md`**

Include:

- circuit model and target backend,
- OpenQASM/QIR compatibility,
- simulator vs hardware behavior,
- noise/error model,
- gate set and topology constraints,
- timing/calibration assumptions,
- measurement and randomness,
- reproducibility,
- numerical tolerances,
- hardware availability limits.

- [x] **Step 3: Create `.agent/DOMAINS/FORMAL_VERIFICATION.md`**

Include:

- proof assistant/model checker/source-of-truth,
- definitions and theorem statements,
- assumptions and axioms,
- proof status: informal, checked, partial, admitted, failed,
- trusted computing base,
- extraction/codegen concerns,
- regression proofs,
- proof review by specialist,
- migration notes for Lean/Rocq/tool versions.

- [x] **Step 4: Create templates**

`FORMAL_PROOF_NOTE.md` fields:

```text
Claim/theorem:
Formal system:
Definitions:
Assumptions/axioms:
Proof status:
Trusted computing base:
Commands:
Artifacts:
Known gaps:
Reviewer:
```

`INTERFACE_CONTRACT.md` fields:

```text
Interface:
Consumers:
Compatibility promises:
Inputs:
Outputs:
Errors:
Versioning:
Security/privacy:
Performance:
Tests:
Migration:
```

- [x] **Step 5: Integrate standards and prompts**

Add short pointers in `.agent/STANDARDS.md`.

Add prompts for:

- compiler change review,
- quantum change review,
- formal proof review,
- interface contract review.

- [x] **Step 6: Validate coverage**

Run:

```bash
rg -n "IR|semantic preservation|differential|OpenQASM|QIR|noise|theorem|axiom|trusted computing base|proof status|interface contract" .agent/DOMAINS/COMPILERS.md .agent/DOMAINS/QUANTUM.md .agent/DOMAINS/FORMAL_VERIFICATION.md .agent/TEMPLATES/FORMAL_PROOF_NOTE.md .agent/TEMPLATES/INTERFACE_CONTRACT.md .agent/STANDARDS.md .agent/PROMPTS.md
git diff --check
```

Expected:

- Formal and semantic claims require explicit assumptions and evidence.

- [x] **Step 7: Commit**

```bash
git add .agent/DOMAINS/COMPILERS.md .agent/DOMAINS/QUANTUM.md .agent/DOMAINS/FORMAL_VERIFICATION.md .agent/TEMPLATES/FORMAL_PROOF_NOTE.md .agent/TEMPLATES/INTERFACE_CONTRACT.md .agent/STANDARDS.md .agent/PROMPTS.md
git commit -m "Add compiler quantum and formal guidance"
```

---

## Task 10: Robotics, Autonomy, and Frontend Overlays

**Files:**
- Create: `.agent/DOMAINS/ROBOTICS_AUTONOMY.md`
- Create: `.agent/DOMAINS/FRONTENDS.md`
- Create: `.agent/TEMPLATES/SAFETY_CASE.md`
- Modify: `.agent/STANDARDS.md`
- Modify: `.agent/PROMPTS.md`

- [x] **Step 1: Create `.agent/DOMAINS/ROBOTICS_AUTONOMY.md`**

Include:

- simulation vs hardware evidence,
- safety boundaries,
- actuation gating,
- operator override,
- ROS 2 QoS/security where applicable,
- sensor calibration,
- time synchronization,
- fault handling,
- logs/traces,
- field-test admission,
- no unapproved physical-world actions.

- [x] **Step 2: Create `.agent/DOMAINS/FRONTENDS.md`**

Include:

- product intent and user workflow,
- accessibility,
- visual regression,
- responsive behavior,
- browser/device coverage,
- state/data contracts,
- error and loading states,
- performance and Core Web Vitals when relevant,
- privacy-sensitive UI,
- screenshots or browser evidence for visual changes.

- [x] **Step 3: Create `.agent/TEMPLATES/SAFETY_CASE.md`**

Include:

```text
System/change:
Hazards:
Assumptions:
Controls:
Human override:
Simulation evidence:
Hardware/field evidence:
Logs/traces:
Residual risk:
Approval needed:
Rollback/recovery:
```

- [x] **Step 4: Integrate standards and prompts**

Add short pointers in `.agent/STANDARDS.md`.

Add prompts for:

- robotics safety review,
- autonomy field-test admission,
- frontend workflow review,
- visual verification review.

- [x] **Step 5: Validate coverage**

Run:

```bash
rg -n "simulation|hardware|actuation|operator override|QoS|security enclave|accessibility|visual regression|responsive|Core Web Vitals|safety case" .agent/DOMAINS/ROBOTICS_AUTONOMY.md .agent/DOMAINS/FRONTENDS.md .agent/TEMPLATES/SAFETY_CASE.md .agent/STANDARDS.md .agent/PROMPTS.md
git diff --check
```

Expected:

- Physical-world and user-facing changes require explicit evidence and review.

- [x] **Step 6: Commit**

```bash
git add .agent/DOMAINS/ROBOTICS_AUTONOMY.md .agent/DOMAINS/FRONTENDS.md .agent/TEMPLATES/SAFETY_CASE.md .agent/STANDARDS.md .agent/PROMPTS.md
git commit -m "Add robotics and frontend guidance"
```

---

## Task 11: Cross-Document Consistency Pass

**Files:**
- Modify as needed: all markdown files touched in v0.2.

- [x] **Step 1: Check terminology**

Run:

```bash
rg -n "agentic|specialist|subagent|quality bar|overlay|adapter|source-of-truth|source of truth|validation|evidence|risk" README.md ADOPTION.md AGENTS.md .agent
```

Expected:

- Terminology is consistent.
- Use `source-of-truth` consistently unless in prose where `source of truth` reads better.
- Use `specialist review` as the broad concept and `subagent review` only when the reviewer is actually another agent.

- [x] **Step 2: Check for prohibited expansion**

Run:

```bash
find . -path ./.git -prune -o -type f -print | sort
find . -path ./.git -prune -o -type f -perm -111 -print
find . -path ./.git -prune -o \( -name package.json -o -name pyproject.toml -o -name Cargo.toml -o -name go.mod -o -name Makefile -o -name justfile -o -name "*.lock" -o -path "./.github/*" \) -print
```

Expected:

- The executable-file command prints nothing.
- The package/build/CI/tooling command prints nothing.
- Only markdown, `VERSION`, `.gitignore`, and `LICENSE` are present.

- [x] **Step 3: Check adapter restraint**

Run:

```bash
find . -path ./.git -prune -o \( -name CLAUDE.md -o -name GEMINI.md -o -path "./.github/*" -o -path "./.claude/*" -o -path "./.gemini/*" \) -print
```

Expected:

- The command prints nothing except `.gitignore` entries are not files.
- Adapter guidance exists in `.agent/ADAPTERS.md`; vendor files are not added by default.

- [x] **Step 4: Placeholder scan**

Run:

```bash
rg -n "TBD|TODO|FIXME|<fill in>|<summary>|<command>|<goal>|<path>|<question>|lorem|placeholder" README.md ADOPTION.md AGENTS.md .agent
```

Expected:

- Existing templates may intentionally contain bracket placeholders.
- New guidance files should not contain accidental placeholders.
- If this output includes new non-template guidance files, replace placeholders with concrete guidance.

- [x] **Step 5: Line count sanity**

Run:

```bash
wc -l AGENTS.md README.md ADOPTION.md .agent/*.md .agent/DOMAINS/*.md .agent/TEMPLATES/*.md
```

Expected:

- `AGENTS.md` remains compact enough to skim quickly.
- Long detail lives in `.agent/` modules and templates.

- [x] **Step 6: Final commit for consistency edits**

```bash
git add README.md ADOPTION.md AGENTS.md .agent CHANGELOG.md VERSION .gitignore
git commit -m "Polish v0.2 guidance consistency"
```

Skip this commit if there are no consistency edits after Task 10.

---

## Task 12: Final Validation, Merge, and Push

**Files:**
- No content edits expected.

- [x] **Step 1: Run final validation**

Run:

```bash
git status --short --branch
find . -path ./.git -prune -o -type f -print | sort
find . -path ./.git -prune -o -type f -perm -111 -print
find . -path ./.git -prune -o \( -name package.json -o -name pyproject.toml -o -name Cargo.toml -o -name go.mod -o -name Makefile -o -name justfile -o -name "*.lock" -o -path "./.github/*" \) -print
rg -n "0\\.2\\.0" VERSION CHANGELOG.md
git diff --check HEAD
```

Expected:

- Working tree is clean.
- No executable files outside `.git`.
- No package/build/CI/tooling files.
- Version and changelog show `0.2.0`.
- `git diff --check HEAD` exits 0.

- [x] **Step 2: Review final tree manually**

Confirm final tree includes:

```text
README.md
ADOPTION.md
AGENTS.md
CHANGELOG.md
VERSION
LICENSE
.gitignore
.agent/ADAPTERS.md
.agent/DONE.md
.agent/LOCAL_CONTEXT.example.md
.agent/NESTED_GUIDANCE.md
.agent/PROMPTS.md
.agent/QUALITY_BAR.md
.agent/REVIEW_PROTOCOL.md
.agent/SECURITY.md
.agent/STANDARDS.md
.agent/WORKFLOW.md
.agent/DOMAINS/*.md
.agent/TEMPLATES/*.md
```

- [x] **Step 3: Merge locally**

From the feature branch:

```bash
git switch main
git pull --ff-only
git merge --ff-only agent-seed-v0.2
```

Expected:

- Fast-forward merge succeeds.

- [x] **Step 4: Re-run final validation on `main`**

Run the full command set from Step 1 again.

Expected:

- Same successful result on `main`.

- [x] **Step 5: Push and confirm**

```bash
git push origin main
git status --short --branch
git ls-remote origin refs/heads/main
git log -1 --oneline --decorate
```

Expected:

- `main` is clean and aligned with `origin/main`.
- Remote `refs/heads/main` points to the v0.2 commit.

- [x] **Step 6: Cleanup merged feature branch**

```bash
git branch -d agent-seed-v0.2
```

Expected:

- Local feature branch deletes cleanly.

---

## Execution Evidence

The v0.2 plan was executed and merged before later corrective releases.

- Historical v0.2 implementation tip from Git history: `db2593e5b97169534d7b8d53bb6b1e4a2ec4371f`.
- Remote branch checked during backfill: `origin/main`.
- Local feature branch state during backfill: no `agent-seed-v0.2` branch is present.
- Hosted CI check during backfill: `gh run list --limit 3 --json databaseId,status,conclusion,headSha,workflowName` returned `[]`, so no hosted GitHub Actions workflows existed for this repository.
- Backfill validation evidence: clean `main`, `git diff --check HEAD` passed, executable/prohibited-file scans were empty, stale MCP scans were empty, unresolved-text scans for active artifacts were empty.

## Acceptance Criteria

v0.2 is complete when:

- `VERSION` is `0.2.0`.
- `CHANGELOG.md` documents v0.2 additions.
- Root `AGENTS.md` remains compact and points to deeper guidance.
- `.agent/QUALITY_BAR.md` captures the elite engineering/scientific bar.
- `.agent/SECURITY.md` covers current agentic AI, tool, MCP, context, memory, and supply-chain risks.
- `.agent/ADAPTERS.md` explains ecosystem adaptation without adding vendor files by default.
- `.agent/NESTED_GUIDANCE.md` covers monorepo and nested instruction precedence.
- `.agent/REVIEW_PROTOCOL.md` defines self-review, specialist review, subagent review, adversarial review, integration review, and disagreement handling.
- `.agent/DOMAINS/` contains optional overlays for AI/ML, systems/kernels, accelerators, compilers, quantum, formal verification, robotics/autonomy, frontends, and autonomous research.
- Templates cover threat models, specialist reviews, domain overlay adoption, model cards, dataset cards, eval reports, experiment logs, training runs, inference deployment, data provenance, research claims, formal proof notes, hardware benchmarks, interface contracts, and safety cases.
- Benchmark templates include enough hardware/runtime/statistical metadata for serious performance work.
- Adoption docs explain high-rigor adoption and license handling.
- No executable installer, package manifest, dependency lockfile, build config, CI config, generated docs, vendored content, or model-specific root config is added.
- Final validation commands pass on merged `main`.

## Execution Recommendation

Use subagent-driven implementation for Tasks 2 through 10 if available, with disjoint ownership:

- Agent A: quality, done, workflow integration.
- Agent B: security and threat model.
- Agent C: adapters and nested guidance.
- Agent D: review protocol and review templates.
- Agent E: AI/ML and autonomous research overlays/templates.
- Agent F: systems, accelerators, and benchmark templates.
- Agent G: compilers, quantum, and formal overlays/templates.
- Agent H: robotics, frontend, and safety templates.

The parent/integrating agent should own:

- root file consistency,
- final terminology pass,
- final validation,
- merge/push/cleanup,
- resolving cross-domain conflicts.

Do not let subagents make destructive git operations, push to remote, change licensing, or decide accepted risk without parent/maintainer approval.
