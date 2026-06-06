# Git And Merge Request Workflow

This workflow defines how agents should handle branch, commit, review, pull request, merge request, merge, push, and cleanup work.

Apply it proportionally. A tiny documentation fix may need one commit and inspection; high-risk work may need a branch, plan, tests, review, CI evidence, and explicit maintainer approval before merge.

## Terms

Use the host platform's native name:

- GitHub: pull request or PR.
- GitLab and some other hosts: merge request or MR.

This document uses `PR/MR` for both.

## Core Rules

- Work on a short-lived feature branch for non-trivial changes.
- Do not work directly on `main`, `master`, or another default branch unless the maintainer explicitly asks for that or the repository's local guidance allows it.
- Keep changes narrow and reviewable.
- Preserve existing user changes. Never discard, overwrite, or revert unrelated work without explicit maintainer instruction.
- Stage only the files that belong to the intended change.
- Commit in sensible chunks with concise, descriptive messages.
- Run relevant local validation before publishing.
- Do not claim checks passed unless they were actually run and passed.
- Do not merge or push to a protected/default branch unless the maintainer explicitly requested that closeout path or the repository's local process allows it.
- Confirm remote CI or hosted checks when they exist and are relevant to the requested closeout.

## 1. Start From A Clean Understanding

Before changing files or staging work:

1. Run `git status --short --branch`.
2. Inspect the existing diff with `git diff` and, when staged changes exist, `git diff --cached`.
3. Identify which files are in scope.
4. Identify unrelated dirty files and leave them untouched.
5. Check the current branch and upstream state.

If the worktree is mixed and the user has not confirmed that all dirty files are in scope, ask before staging broad changes.

If the user explicitly says all unstaged or uncommitted work should be captured, inspect the full diff, preserve it, and include it in the branch/commit plan.

## 2. Branch

For non-trivial work, create or reuse a feature branch.

Recommended branch shape:

```text
codex/<short-description>
```

Examples:

```text
codex/git-and-mr-workflow
codex/readiness-audit-docs
codex/fix-parser-empty-input
```

When local guidance defines a branch helper or naming convention, use that instead.

If uncommitted work already exists on the default branch, preserve it by creating a feature branch from the current state before editing or committing.

## 3. Commit

Commit only intentional work.

Before each commit:

1. Run `git status --short`.
2. Review `git diff`.
3. Stage explicit paths when the worktree is mixed.
4. Use `git add -A` only when the whole worktree is confirmed in scope.
5. Review `git diff --cached`.
6. Commit with a concise, descriptive message.

Commit message guidance:

```text
Add git and merge request workflow guidance
Fix release adapter adoption notes
Document local validation commands
```

Avoid vague messages such as:

```text
updates
fix stuff
wip
misc
```

Use multiple commits when the changes represent separable ideas. Use one commit when the change is a single coherent documentation or implementation slice.

## 4. Validate Before Publishing

Run the most relevant checks available for the changed files.

Validation may include:

- targeted tests,
- full tests,
- format checks,
- lint checks,
- type checks,
- docs checks,
- examples,
- benchmarks,
- security checks,
- inspection for markdown-only repositories with no defined commands.

When commands are not documented, inspect the repository for likely commands before asking the user.

If no relevant command exists, validate by inspection and state that no repository command is defined.

## 5. Self-Review

Before pushing or opening a PR/MR, review the final diff as if reviewing another engineer's work.

Check for:

- accidental file changes,
- unrelated churn,
- missing tests or validation,
- documentation drift,
- weakened checks,
- public behavior changes,
- compatibility issues,
- security or privacy issues,
- performance concerns,
- incomplete cleanup,
- unresolved review comments,
- and untracked files that should either be committed or intentionally left out.

Use `.agent/TEMPLATES/REVIEW.md` for structured review and `.agent/REVIEW_PROTOCOL.md` for specialist, adversarial, subagent, or integration review.

## 6. Publish A Branch

Push the branch when the work is committed and local validation is complete or explicitly reported as unavailable.

Typical command:

```bash
git push -u origin <branch>
```

After pushing, verify that the remote branch exists.

Do not force-push unless the maintainer requested it or the repository explicitly allows it for the branch. If force-push is required for a reviewed branch, prefer `--force-with-lease` and state why.

## 7. Open Or Update A PR/MR

Use a PR/MR when review is expected, the repository requires it, or the change is non-trivial.

The PR/MR should include:

- what changed,
- why it changed,
- validation run,
- review performed or required,
- risks or limitations,
- related issues, plans, or docs,
- and any checks that were not run.

Default to a draft PR/MR unless the maintainer explicitly asks for ready-for-review.

If the maintainer asks for a direct merge and push, a PR/MR may be skipped only when local guidance and branch protection permit that path.

## 8. Respond To Review

When review comments exist:

1. Read all comments before editing.
2. Separate blocking issues from suggestions.
3. Fix blocking issues in focused commits.
4. Preserve reviewer uncertainty and unresolved disagreements.
5. Rerun relevant checks.
6. Update the PR/MR with what changed and what validation was rerun.

Do not dismiss review findings without evidence. When reviewers disagree, use `.agent/REVIEW_PROTOCOL.md`.

## 9. Merge

Merge only when the repository's policy allows it and required checks or reviews are satisfied.

Before merging:

1. Confirm the target branch.
2. Confirm the branch is up to date or intentionally mergeable.
3. Confirm relevant local checks passed or were explicitly deferred.
4. Confirm required hosted checks passed when they exist.
5. Confirm blocking review findings are resolved.

Use the repository's merge strategy:

- fast-forward,
- merge commit,
- squash merge,
- rebase and fast-forward,
- or platform-managed PR/MR merge.

Do not change merge strategy just for convenience.

## 10. Post-Merge Closeout

After merge:

1. Switch to the target branch.
2. Pull or update the target branch if needed.
3. Rerun relevant validation on the merged result when practical.
4. Push the merged target branch if the merge was local.
5. Confirm hosted checks or CI are green when they exist.
6. Delete the local topic branch after the merged result is verified.
7. Delete the remote topic branch when repository policy allows it.
8. Report commit SHA, branch, validation, CI or hosted check status, and cleanup performed.

Do not stop at commit, branch push, or PR/MR creation when the user asked for full closeout.

## 11. Failure Handling

When validation, push, CI, or merge fails:

1. Read the failure carefully.
2. Determine whether it is caused by the change.
3. Fix in scope when practical.
4. Rerun the relevant check.
5. Report any remaining failure honestly.

Do not weaken tests, checks, or review gates to finish a closeout.

If the failure is unrelated to the change, preserve evidence and ask the maintainer how to proceed unless local policy defines the path.

## 12. Final Response

After git, PR/MR, or merge work, final responses should include:

```text
Summary:
- What changed and why.
- Branch and commit SHA.

Validation:
- Exact checks run and results.
- Hosted CI/check status when relevant.

Notes:
- PR/MR link if created.
- Merge/push/cleanup status.
- Risks, limitations, or checks not run.
```
