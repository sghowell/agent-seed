# Reusable prompt snippets

These prompts help users start common coding-agent tasks with less repeated instruction.

They are starting points. Adjust them to the target repository and task.

## 1. Bootstrap repository understanding

```text
Read AGENTS.md and the files in .agent/. Then inspect this repository enough to understand its structure, commands, tests, and conventions. Do not edit files yet. Produce a concise repo map, identify the canonical commands, summarize the main risks, and recommend any small updates that would make the repository easier for coding agents to work in safely.
```

## 2. Audit for agent-readiness

```text
Use AGENTS.md and .agent/TEMPLATES/REPO_AUDIT.md to audit this repository for agent-readiness. Do not edit files yet. Focus on whether an agent can quickly understand the project, find canonical commands, run relevant checks, modify code safely, and know what “done” means. Recommend the smallest useful improvements.
```

## 3. Create local context

```text
Read the repository and create .agent/LOCAL_CONTEXT.md from .agent/LOCAL_CONTEXT.example.md. Fill in only facts supported by repository files. Do not invent commands or conventions. Mark unknowns clearly.
```

## 4. Start a small feature

```text
Use the repo guidance in AGENTS.md. First inspect the relevant files and tests. Implement the smallest safe change for this feature. Add or update tests where appropriate. Run relevant checks where possible. In the final response, summarize the change, validation, and remaining risks.
```

## 5. Start a substantial feature

```text
Use AGENTS.md and .agent/WORKFLOW.md. Before editing, create a concise execution plan using .agent/TEMPLATES/EXEC_PLAN.md. Include goals, non-goals, affected files, implementation steps, validation strategy, risks, and open questions. After the plan, implement only the approved or clearly safe next steps.
```

## 6. Review current diff

```text
Review the current diff using .agent/TEMPLATES/REVIEW.md. Act as a strict senior engineer. Focus on correctness, missing tests, unnecessary churn, docs drift, dependency risk, performance risk, security risk, and whether the change solves the requested task. List highest-priority issues first.
```

## 7. Debug a bug

```text
Use AGENTS.md and .agent/TEMPLATES/BUG_REPORT.md. First characterize or reproduce the bug from the available information. Identify likely root cause, propose the smallest fix, add regression coverage where practical, and report validation honestly.
```

## 8. Refactor safely

```text
Use AGENTS.md and .agent/WORKFLOW.md. Treat this as a behavior-preserving refactor. First identify the existing behavior and tests that protect it. Create a brief plan. Keep the diff narrow, avoid unrelated cleanup, and run relevant tests before finalizing.
```

## 9. Improve tests

```text
Use AGENTS.md and .agent/STANDARDS.md. Inspect the current tests for the target area. Identify important untested behavior, edge cases, and regression risks. Add focused tests without changing production behavior unless required to improve testability. Run relevant checks and summarize coverage added.
```

## 10. Improve documentation

```text
Use AGENTS.md and .agent/TEMPLATES/DOCS_UPDATE.md. Inspect the relevant code and existing docs. Update documentation so it accurately reflects current behavior. Keep the update concise and discoverable. Do not invent features or commands.
```

## 11. Performance-sensitive change

```text
Use AGENTS.md and .agent/TEMPLATES/BENCHMARK_NOTE.md. Treat this as performance-sensitive work. Identify the hot path, baseline behavior, proposed change, measurement method, and validation limits. Avoid claiming improvement without measurement unless measurement is not practical and that limitation is stated.
```

## 12. Dependency review

```text
Review the proposed dependency change. Explain why the dependency is needed, whether existing code or dependencies could avoid it, what transitive or security risks it adds, and how it affects maintenance. Do not add the dependency unless the benefit is clear.
```

## 13. Final pre-submit review

```text
Before finalizing, reread AGENTS.md and .agent/DONE.md. Review the diff for correctness, tests, docs, unnecessary churn, dependency risk, performance risk, and security risk. Then provide a final response with Summary, Validation, and Notes.
```

## 14. Create an execution plan only

```text
Create an execution plan using .agent/TEMPLATES/EXEC_PLAN.md. Do not edit code yet. The plan should be concrete enough for another agent or engineer to implement. Include assumptions, affected files, validation strategy, risks, and open questions.
```

## 15. Convert a vague request into a safe plan

```text
The request is broad or ambiguous. Use AGENTS.md and .agent/WORKFLOW.md to narrow it into a safe implementation plan. Identify what can be done now, what assumptions are required, what should not be changed, and what validation would prove success. Do not edit files yet.
```
