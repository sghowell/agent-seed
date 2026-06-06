# Adopting agent-seed

This document explains how to add `agent-seed` to a new or existing repository.

The goal is not to impose a heavy process. The goal is to give coding agents a clear, local operating model so they can work more safely with less repeated prompting.

## Adoption Modes

There are four practical adoption modes.

## Mode 1: Minimal Adoption

Use this when the repository is small, experimental, or early-stage.

Copy only:

```text
AGENTS.md
.agent/WORKFLOW.md
.agent/DONE.md
.agent/GIT_AND_MR_WORKFLOW.md
.agent/LOCAL_CONTEXT.example.md
```

Then rename:

```text
.agent/LOCAL_CONTEXT.example.md -> .agent/LOCAL_CONTEXT.md
```

Customize `AGENTS.md` and `.agent/LOCAL_CONTEXT.md` with the repository's real commands and constraints.

This mode is enough to establish basic agent behavior.

## Mode 2: Standard Adoption

Use this for most repositories.

Copy:

```text
AGENTS.md
.agent/WORKFLOW.md
.agent/STANDARDS.md
.agent/DONE.md
.agent/GIT_AND_MR_WORKFLOW.md
.agent/PROMPTS.md
.agent/LOCAL_CONTEXT.example.md
.agent/TEMPLATES/
```

Then rename:

```text
.agent/LOCAL_CONTEXT.example.md -> .agent/LOCAL_CONTEXT.md
```

Customize:

```text
AGENTS.md
.agent/LOCAL_CONTEXT.md
.agent/STANDARDS.md
.agent/DONE.md
```

This mode gives agents the full lightweight seed: workflow, standards, prompts, templates, and local context. It does not copy domain overlays by default.

## Mode 3: Reference-Only Adoption

Use this when the target repository should not receive new files yet.

Keep `agent-seed` separate and tell the agent:

```text
Use the guidance in the agent-seed repository as operating context for this task. First audit the target repository and recommend which seed files should be copied or adapted. Do not edit the target repository yet.
```

This is useful when evaluating whether the seed fits a repository.

## Mode 4: High-Rigor Adoption

Use this for repositories where the quality bar is closer to principal or distinguished engineer/scientist work, or where mistakes can affect security, safety, scientific validity, public APIs, performance-critical systems, expensive experiments, or production operations.

Copy:

```text
AGENTS.md
.agent/WORKFLOW.md
.agent/STANDARDS.md
.agent/DONE.md
.agent/GIT_AND_MR_WORKFLOW.md
.agent/QUALITY_BAR.md
.agent/SECURITY.md
.agent/REVIEW_PROTOCOL.md
.agent/ADAPTERS.md
.agent/NESTED_GUIDANCE.md
.agent/LOCAL_CONTEXT.example.md
.agent/TEMPLATES/
selected .agent/DOMAINS/
```

Then rename:

```text
.agent/LOCAL_CONTEXT.example.md -> .agent/LOCAL_CONTEXT.md
```

Use `.agent/TEMPLATES/DOMAIN_OVERLAY_ADOPTION.md` to record which overlays apply and which modules they govern.

High-rigor adoption is appropriate for projects involving AI/ML, systems software, kernels, drivers, accelerators, compilers, quantum computing, formal verification, robotics, autonomous research, safety-sensitive automation, regulated data, or production infrastructure.

## Step-By-Step Standard Adoption

### 1. Copy The Files

From the `agent-seed` repository:

```bash
mkdir -p /path/to/target-repo/.agent
cp AGENTS.md /path/to/target-repo/AGENTS.md
cp .agent/WORKFLOW.md /path/to/target-repo/.agent/WORKFLOW.md
cp .agent/STANDARDS.md /path/to/target-repo/.agent/STANDARDS.md
cp .agent/DONE.md /path/to/target-repo/.agent/DONE.md
cp .agent/GIT_AND_MR_WORKFLOW.md /path/to/target-repo/.agent/GIT_AND_MR_WORKFLOW.md
cp .agent/PROMPTS.md /path/to/target-repo/.agent/PROMPTS.md
cp .agent/LOCAL_CONTEXT.example.md /path/to/target-repo/.agent/LOCAL_CONTEXT.md
cp -R .agent/TEMPLATES /path/to/target-repo/.agent/TEMPLATES
```

For high-rigor adoption, copy high-rigor core files and only the relevant overlays:

```bash
cp .agent/QUALITY_BAR.md /path/to/target-repo/.agent/QUALITY_BAR.md
cp .agent/SECURITY.md /path/to/target-repo/.agent/SECURITY.md
cp .agent/GIT_AND_MR_WORKFLOW.md /path/to/target-repo/.agent/GIT_AND_MR_WORKFLOW.md
cp .agent/REVIEW_PROTOCOL.md /path/to/target-repo/.agent/REVIEW_PROTOCOL.md
cp .agent/ADAPTERS.md /path/to/target-repo/.agent/ADAPTERS.md
cp .agent/NESTED_GUIDANCE.md /path/to/target-repo/.agent/NESTED_GUIDANCE.md
mkdir -p /path/to/target-repo/.agent/DOMAINS
cp .agent/DOMAINS/README.md /path/to/target-repo/.agent/DOMAINS/README.md
cp .agent/DOMAINS/AI_ML.md /path/to/target-repo/.agent/DOMAINS/AI_ML.md
```

The `AI_ML.md` command is an example. Select the overlays that match actual repository work.

### 2. Preserve Licensing

`agent-seed` is MIT licensed.

Target repositories should keep their own project license. Do not overwrite, delete, or replace an existing target repository license while copying seed files. If the target organization requires attribution for copied guidance, preserve attribution in the repository's normal notice, third-party, or documentation location.

If the target repository has no license, do not infer one from `agent-seed`. Ask the maintainer to choose a project license.

### 3. Edit `AGENTS.md`

Replace generic command entries with target-repository facts.

At minimum, fill in:

- setup command,
- test command,
- formatting command,
- linting command,
- type-checking command,
- documentation command,
- benchmark command,
- known risky areas,
- planning thresholds.

Delete commands that do not exist.

Do not invent commands for the sake of completeness. It is better to say "not currently defined" than to give an agent a fake command.

### 4. Create Local Context

Edit:

```text
.agent/LOCAL_CONTEXT.md
```

Fill in:

- project purpose,
- repository structure,
- main modules,
- data flow,
- active domain overlays,
- specialist review lanes,
- important dependencies,
- style conventions,
- test conventions,
- deployment constraints,
- performance-sensitive areas,
- security-sensitive areas,
- safety-sensitive operations,
- hardware/runtime environments,
- known pitfalls.

This is the most important customization file. Generic standards are useful, but local facts guide safe changes.

### 5. Select Domain Overlays

Use `.agent/DOMAINS/README.md` and `.agent/TEMPLATES/DOMAIN_OVERLAY_ADOPTION.md`.

Select only overlays that match real repository work:

- `AI_ML.md` for models, datasets, training, inference, evaluation, and ML safety.
- `AUTONOMOUS_RESEARCH.md` for agentic literature review, experiment planning, claim tracking, and replication.
- `SYSTEMS_KERNELS.md` for OS, kernel, driver, firmware, low-level runtime, and unsafe code.
- `ACCELERATORS.md` for GPU, TPU, NPU, FPGA, heterogeneous hardware, and performance kernels.
- `COMPILERS.md` for language, IR, lowering, optimization, codegen, diagnostics, and runtime semantics.
- `QUANTUM.md` for circuits, simulation, OpenQASM, QIR, hardware constraints, and error models.
- `FORMAL_VERIFICATION.md` for proof assistants, SMT, model checking, theorem status, and assumptions.
- `ROBOTICS_AUTONOMY.md` for ROS 2, actuation, field tests, simulation, hardware evidence, and safety cases.
- `FRONTENDS.md` for user workflows, accessibility, responsive behavior, browser evidence, and state/data contracts.

If an overlay does not apply, do not copy it just because it exists.

### 6. Select Relevant Agent Surfaces

Use `.agent/ADAPTERS.md` to decide which instruction surfaces the target repository actually needs.

Start from the maintainers' real workflows, not from a checklist of every available agent. Record the primary/default agent, second-priority agents, and any significantly lower-priority active ecosystems in `.agent/LOCAL_CONTEXT.md`, then add only the shared or bridge files those ecosystems need. If broad compatibility conflicts with the primary/default agent's effectiveness, prefer the primary/default agent and document the tradeoff.

Keep `AGENTS.md` and nested `AGENTS.md` files as the source-of-truth instructions for AGENTS-compatible agents. This is the default path for Codex/OpenAI agents, Hermes Agent, Pi, OpenCode, and other agents that directly load `AGENTS.md`.

Add ecosystem-specific bridge files only when maintainers use that ecosystem and can keep the bridge synchronized. Common surfaces include:

- `AGENTS.md` and nested `AGENTS.md` files for Codex/OpenAI agents, Hermes Agent, Pi, OpenCode, and other AGENTS-compatible agents,
- `CLAUDE.md` for Claude Code bridge guidance, usually importing or pointing back to `AGENTS.md`,
- `GEMINI.md` for Gemini CLI bridge guidance, when Gemini CLI is used,
- `.github/copilot-instructions.md` for Copilot-specific repository-wide instructions, when Copilot is used,
- `.github/instructions/*.instructions.md` for Copilot path-specific instructions, when Copilot is used and nested `AGENTS.md` is not enough,
- Cursor project rules, when Cursor is used,
- `.aider.conf.yml` for shared Aider read-file configuration, when Aider is used.

Do not add Copilot, Gemini, Cursor, Aider, or other vendor-specific files just to appear comprehensive. Unused ecosystems should be left absent or explicitly marked deferred in `.agent/LOCAL_CONTEXT.md`.

Vendor-specific bridge files should point back to `AGENTS.md` and `.agent/`, not fork policy into inconsistent copies.

### 7. Add Nested Guidance For Monorepos

Use `.agent/NESTED_GUIDANCE.md` when the target repository has multiple packages, applications, services, hardware backends, research tracks, or documentation systems.

Nested `AGENTS.md` files should add local facts:

- package-specific commands,
- local ownership,
- local tests,
- local risks,
- local done criteria,
- active overlays for that subtree.

They should not repeat the full root policy.

### 8. Customize Standards

Edit:

```text
.agent/STANDARDS.md
```

Remove sections that do not apply. Tighten sections where the repository already has tooling or review expectations.

Examples:

- A Rust project may add `cargo fmt`, `cargo clippy`, and `cargo test` expectations.
- A Python project may add formatter, linter, type checker, and test runner commands.
- A performance-sensitive project may define benchmark commands and regression thresholds.
- A scientific project may define reproducibility and artifact expectations.
- An AI/ML project may require model cards, dataset cards, eval reports, and data provenance records.
- A formal methods project may require checked proof status and explicit assumptions.

### 9. Customize Done Criteria

Edit:

```text
.agent/DONE.md
```

Make the definition of done match the repository's real lifecycle.

For example:

- prototype repositories may require basic tests and explicit caveats,
- production repositories may require CI, release notes, migrations, monitoring, and rollback notes,
- research repositories may require reproducibility notes and experiment metadata,
- safety-sensitive repositories may require safety cases, specialist review, and explicit approval gates.

### 10. Use The Prompts

Use `.agent/PROMPTS.md` to start common tasks.

Examples:

```text
Use AGENTS.md and .agent/WORKFLOW.md. Audit this repository using .agent/TEMPLATES/REPO_AUDIT.md. Do not edit files yet.
```

```text
Use the repo guidance. Implement this feature as the smallest safe change. Add or update tests and report validation honestly.
```

```text
Review the current diff using .agent/TEMPLATES/REVIEW.md and .agent/REVIEW_PROTOCOL.md. List the highest-priority issues first.
```

## What To Customize First

Prioritize these fields:

1. Canonical commands.
2. Repository structure.
3. Testing expectations.
4. Git, PR/MR, merge, push, and cleanup workflow.
5. Planning triggers.
6. Known risky areas.
7. Performance-sensitive areas.
8. Security-sensitive areas.
9. Active domain overlays.
10. Specialist review lanes.
11. Documentation expectations.
12. Final response format.

## What Not To Customize Too Early

Do not over-specify:

- style preferences that are not enforced,
- workflows nobody will use,
- commands that do not exist,
- theoretical standards without validation mechanisms,
- language-specific policies that do not apply,
- domain overlays that do not match the target repository,
- vendor-specific adapter files for tools the team does not use.

The seed should make agent work safer, not slower.

## Recommended First Prompt After Adoption

After copying and lightly customizing the seed, give a coding agent this prompt:

```text
Read AGENTS.md and the files in .agent/. Then audit this repository for agent-readiness using .agent/TEMPLATES/REPO_AUDIT.md. Do not edit files yet. Identify the canonical commands, missing local context, unclear standards, risky areas, active domain overlays, adapter needs, and the smallest improvements that would make future agent work safer.
```

## Signs The Adoption Is Working

The seed is working when agents:

- inspect relevant files before editing,
- produce narrower diffs,
- follow existing patterns,
- add or update tests more consistently,
- stop inventing validation,
- identify security and performance risks early,
- request specialist review when appropriate,
- state risks clearly,
- ask fewer avoidable questions,
- and summarize changes in a reviewable way.

## Signs The Adoption Needs Adjustment

Revise the seed in the target repository when agents:

- run the wrong commands,
- miss important local conventions,
- over-plan small changes,
- under-plan large changes,
- repeatedly touch risky areas carelessly,
- skip important tests,
- miss relevant domain overlays,
- duplicate conflicting adapter instructions,
- make broad unrelated changes,
- or produce final summaries without useful validation evidence.

## Keeping The Seed Lightweight

Do not let the target repository's `AGENTS.md` become a giant manual.

Use this split:

- `AGENTS.md`: compact operating agreement and command index.
- `.agent/LOCAL_CONTEXT.md`: repo-specific facts.
- `.agent/WORKFLOW.md`: process for substantial work.
- `.agent/STANDARDS.md`: engineering standards.
- `.agent/DONE.md`: completion criteria.
- `.agent/GIT_AND_MR_WORKFLOW.md`: branch, commit, PR/MR, merge, push, and cleanup workflow.
- `.agent/QUALITY_BAR.md`: high-rigor expectations.
- `.agent/SECURITY.md`: agentic AI and tool security.
- `.agent/REVIEW_PROTOCOL.md`: review layers and specialist lanes.
- `.agent/ADAPTERS.md`: ecosystem-specific bridge guidance.
- `.agent/NESTED_GUIDANCE.md`: monorepo and nested instruction rules.
- `.agent/DOMAINS/`: optional domain-specific overlays.
- `.agent/TEMPLATES/`: reusable structured artifacts.

When `AGENTS.md` grows too large, move details into `.agent/` and keep only a pointer in `AGENTS.md`.
