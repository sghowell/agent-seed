# Nested Guidance

Use nested guidance when a repository contains subtrees with materially different commands, ownership, risks, languages, build systems, deployment paths, or domain overlays.

## When To Add Nested `AGENTS.md`

Add a nested `AGENTS.md` when a subtree has:

- different setup, test, build, or validation commands,
- different deployment or release ownership,
- security, safety, or performance constraints not shared by the whole repository,
- active domain overlays not used elsewhere,
- generated or vendored files requiring special handling,
- package-specific compatibility promises,
- separate frontend, backend, kernel, model, hardware, or research workflows.

Do not add nested files just to repeat the root policy.

## Precedence

Use this rule:

- direct user instructions for the current task override repository guidance,
- the nearest applicable `AGENTS.md` governs files in its scope,
- root `AGENTS.md` remains the general policy when nested files are silent,
- `.agent/LOCAL_CONTEXT.md` provides facts, not a way to bypass policy,
- safety, security, privacy, legal, and credential constraints should be treated as hard gates unless an authorized maintainer explicitly changes them.

## Monorepo Examples

Useful nested locations include:

```text
apps/web/AGENTS.md
apps/mobile/AGENTS.md
services/api/AGENTS.md
crates/runtime/AGENTS.md
kernels/gpu/AGENTS.md
models/AGENTS.md
docs/AGENTS.md
experiments/AGENTS.md
hardware/AGENTS.md
```

Each nested file should describe what is different about that subtree.

## Required Nested Sections

Nested files should usually include:

- scope and ownership,
- local commands,
- local tests and validation,
- local risky files or operations,
- generated, vendored, or external artifacts,
- active domain overlays,
- local review requirements,
- local done criteria,
- compatibility or migration constraints.

## Avoid Duplication

Nested files should not copy the full root policy. They should say:

```markdown
Follow the root `AGENTS.md`. This file adds guidance for this subtree.
```

Then add only local facts.

## Conflict Handling

When nested and root guidance conflict:

1. Check whether the nested file is intentionally more specific.
2. Prefer the safer or more specific instruction for the scoped files.
3. Preserve root policy for areas not mentioned locally.
4. Ask the maintainer before weakening security, safety, privacy, compatibility, or validation requirements.
5. Update stale guidance rather than silently ignoring it.

## Review

Review nested guidance when:

- packages move,
- commands change,
- ownership changes,
- new tools or adapters are introduced,
- domain overlays become active or inactive,
- CI or validation gates change,
- production, safety, security, or release paths change.
