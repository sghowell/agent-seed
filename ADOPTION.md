# Adopting agent-seed

This document explains how to add `agent-seed` to a new or existing repository.

The goal is not to impose a heavy process. The goal is to give coding agents a clear, local operating model so they can work more safely with less repeated prompting.

## Adoption modes

There are three practical adoption modes.

## Mode 1: Minimal adoption

Use this when the repository is small, experimental, or early-stage.

Copy only:

```text
AGENTS.md
.agent/WORKFLOW.md
.agent/DONE.md
.agent/LOCAL_CONTEXT.example.md
```

Then rename:

```text
.agent/LOCAL_CONTEXT.example.md -> .agent/LOCAL_CONTEXT.md
```

Customize `AGENTS.md` and `.agent/LOCAL_CONTEXT.md` with the repository's real commands and constraints.

This mode is enough to establish basic agent behavior.

## Mode 2: Standard adoption

Use this for most repositories.

Copy:

```text
AGENTS.md
.agent/
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

This mode gives agents the full lightweight seed: workflow, standards, prompts, templates, and local context.

## Mode 3: Reference-only adoption

Use this when the target repository should not receive new files yet.

Keep `agent-seed` separate and tell the agent:

```text
Use the guidance in the agent-seed repository as operating context for this task. First audit the target repository and recommend which seed files should be copied or adapted. Do not edit the target repository yet.
```

This is useful when evaluating whether the seed fits a repository.

## Step-by-step standard adoption

### 1. Copy the files

From the `agent-seed` repository:

```bash
cp AGENTS.md /path/to/target-repo/AGENTS.md
cp -R .agent /path/to/target-repo/.agent
cp .agent/LOCAL_CONTEXT.example.md /path/to/target-repo/.agent/LOCAL_CONTEXT.md
```

### 2. Edit `AGENTS.md`

Replace generic placeholders with target-repository facts.

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

Do not invent commands for the sake of completeness. It is better to say “not currently defined” than to give an agent a fake command.

### 3. Create local context

Edit:

```text
.agent/LOCAL_CONTEXT.md
```

Fill in:

- project purpose,
- repository structure,
- main modules,
- data flow,
- important dependencies,
- style conventions,
- test conventions,
- deployment constraints,
- performance-sensitive areas,
- security-sensitive areas,
- known pitfalls.

This is the most important customization file. Generic standards are useful, but local facts guide safe changes.

### 4. Customize standards

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

### 5. Customize done criteria

Edit:

```text
.agent/DONE.md
```

Make the definition of done match the repository's real lifecycle.

For example:

- prototype repositories may require basic tests and explicit caveats,
- production repositories may require CI, release notes, migrations, monitoring, and rollback notes,
- research repositories may require reproducibility notes and experiment metadata.

### 6. Use the prompts

Use `.agent/PROMPTS.md` to start common tasks.

Examples:

```text
Use AGENTS.md and .agent/WORKFLOW.md. Audit this repository using .agent/TEMPLATES/REPO_AUDIT.md. Do not edit files yet.
```

```text
Use the repo guidance. Implement this feature as the smallest safe change. Add or update tests and report validation honestly.
```

```text
Review the current diff using .agent/TEMPLATES/REVIEW.md. List the highest-priority issues first.
```

## What to customize first

Prioritize these fields:

1. Canonical commands.
2. Repository structure.
3. Testing expectations.
4. Planning triggers.
5. Known risky areas.
6. Performance-sensitive areas.
7. Security-sensitive areas.
8. Documentation expectations.
9. Final response format.

## What not to customize too early

Do not over-specify:

- style preferences that are not enforced,
- workflows nobody will use,
- commands that do not exist,
- theoretical standards without validation mechanisms,
- language-specific policies that do not apply.

The seed should make agent work safer, not slower.

## Recommended first prompt after adoption

After copying and lightly customizing the seed, give a coding agent this prompt:

```text
Read AGENTS.md and the files in .agent/. Then audit this repository for agent-readiness using .agent/TEMPLATES/REPO_AUDIT.md. Do not edit files yet. Identify the canonical commands, missing local context, unclear standards, risky areas, and the smallest improvements that would make future agent work safer.
```

## Signs the adoption is working

The seed is working when agents:

- inspect relevant files before editing,
- produce narrower diffs,
- follow existing patterns,
- add or update tests more consistently,
- stop inventing validation,
- state risks clearly,
- ask fewer avoidable questions,
- and summarize changes in a reviewable way.

## Signs the adoption needs adjustment

Revise the seed in the target repository when agents:

- run the wrong commands,
- miss important local conventions,
- over-plan small changes,
- under-plan large changes,
- repeatedly touch risky areas carelessly,
- skip important tests,
- make broad unrelated changes,
- or produce final summaries without useful validation evidence.

## Keeping the seed lightweight

Do not let the target repository's `AGENTS.md` become a giant manual.

Use this split:

- `AGENTS.md`: compact operating agreement and command index.
- `.agent/LOCAL_CONTEXT.md`: repo-specific facts.
- `.agent/WORKFLOW.md`: process for substantial work.
- `.agent/STANDARDS.md`: engineering standards.
- `.agent/DONE.md`: completion criteria.
- `.agent/TEMPLATES/`: reusable structured artifacts.

When `AGENTS.md` grows too large, move details into `.agent/` and keep only a pointer in `AGENTS.md`.
