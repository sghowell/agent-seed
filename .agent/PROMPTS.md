# Reusable Prompt Snippets

These prompts help users start common coding-agent tasks with less repeated instruction.

They are starting points. Adjust them to the target repository and task.

## 1. Bootstrap Repository Understanding

```text
Read AGENTS.md and the files in .agent/. Then inspect this repository enough to understand its structure, commands, tests, conventions, active domain overlays, and risks. Do not edit files yet. Produce a concise repo map, identify the canonical commands, summarize the main risks, and recommend small updates that would make the repository easier for coding agents to work in safely.
```

## 2. Audit For Agent-Readiness

```text
Use AGENTS.md and .agent/TEMPLATES/REPO_AUDIT.md to audit this repository for agent-readiness. Do not edit files yet. Focus on whether an agent can quickly understand the project, find canonical commands, run relevant checks, modify code safely, use active domain overlays, and know what "done" means. Recommend the smallest useful improvements.
```

## 3. Create Local Context

```text
Read the repository and create .agent/LOCAL_CONTEXT.md from .agent/LOCAL_CONTEXT.example.md. Fill in only facts supported by repository files. Do not invent commands or conventions. Mark unknowns clearly.
```

## 4. Start A Small Feature

```text
Use the repo guidance in AGENTS.md. First inspect the relevant files and tests. Implement the smallest safe change for this feature. Add or update tests where appropriate. Run relevant checks where possible. In the final response, summarize the change, validation, and remaining risks.
```

## 5. Start A Substantial Feature

```text
Use AGENTS.md and .agent/WORKFLOW.md. Before editing, create a concise execution plan using .agent/TEMPLATES/EXEC_PLAN.md. Include goals, non-goals, affected files, implementation steps, active domain overlays, validation strategy, specialist review plan, risks, and open questions. After the plan, implement only the approved or clearly safe next steps.
```

## 6. Review Current Diff

```text
Review the current diff using .agent/TEMPLATES/REVIEW.md and .agent/REVIEW_PROTOCOL.md. Act as a strict senior engineer. Focus on correctness, missing tests, unnecessary churn, docs drift, dependency risk, performance risk, security risk, specialist-review needs, and whether the change solves the requested task. List highest-priority findings first.
```

## 7. Debug A Bug

```text
Use AGENTS.md and .agent/TEMPLATES/BUG_REPORT.md. First characterize or reproduce the bug from the available information. Identify likely root cause, propose the smallest fix, add regression coverage where practical, and report validation honestly.
```

## 8. Refactor Safely

```text
Use AGENTS.md and .agent/WORKFLOW.md. Treat this as a behavior-preserving refactor. First identify the existing behavior and tests that protect it. Create a brief plan. Keep the diff narrow, avoid unrelated cleanup, and run relevant tests before finalizing.
```

## 9. Improve Tests

```text
Use AGENTS.md and .agent/STANDARDS.md. Inspect the current tests for the target area. Identify important untested behavior, edge cases, and regression risks. Add focused tests without changing production behavior unless required to improve testability. Run relevant checks and summarize coverage added.
```

## 10. Improve Documentation

```text
Use AGENTS.md and .agent/TEMPLATES/DOCS_UPDATE.md. Inspect the relevant code and existing docs. Update documentation so it accurately reflects current behavior. Keep the update concise and discoverable. Do not invent features or commands.
```

## 11. Performance-Sensitive Change

```text
Use AGENTS.md, .agent/STANDARDS.md, and .agent/TEMPLATES/BENCHMARK_NOTE.md. Treat this as performance-sensitive work. Identify the hot path, baseline behavior, proposed change, measurement method, workload, environment, variance, correctness checks, and validation limits. Avoid claiming improvement without measurement unless measurement is not practical and that limitation is stated.
```

## 12. Hardware Or Accelerator Benchmark

```text
Use .agent/DOMAINS/ACCELERATORS.md and .agent/TEMPLATES/HARDWARE_BENCHMARK.md. Record hardware topology, firmware, driver, runtime, compiler flags, precision, workload, warmup, runs, variance, power or energy if relevant, correctness checks, baseline, after result, artifacts, and regression threshold.
```

## 13. Dependency Review

```text
Review the proposed dependency change. Explain why the dependency is needed, whether existing code or dependencies could avoid it, what transitive, license, security, provenance, and maintenance risks it adds, and how it affects performance. Do not add the dependency unless the benefit is clear.
```

## 14. Agentic AI Threat Model

```text
Use .agent/SECURITY.md and .agent/TEMPLATES/THREAT_MODEL.md. Threat-model this agentic system or change. Focus on prompt injection, goal hijack, tool misuse, excessive permissions, identity abuse, memory or context poisoning, data exfiltration, unsafe code execution, supply-chain risk, autonomy boundaries, approval gates, auditability, and residual risk.
```

## 15. MCP Or Tool Review

```text
Review this MCP server, tool, skill, hook, plugin, or agent adapter as executable supply chain. Inspect requested permissions, credential handling, tool descriptions, external inputs, network/file access, logging, installation path, version/provenance, and approval boundaries. Identify blocking security risks first.
```

## 16. Secrets And Privacy Review

```text
Review this change for secrets and privacy risk. Identify sensitive files, tokens, personal data, logs, URLs, screenshots, artifacts, model prompts, model outputs, and data flows. Confirm secrets are not printed or persisted and that private data stays within approved boundaries.
```

## 17. Supply-Chain Review

```text
Review this dependency, model, dataset, binary, container, prompt pack, skill, hook, or generated artifact for supply-chain risk. Check provenance, license, version pinning, integrity, maintenance status, transitive dependencies, known vulnerabilities, and whether a safer local or existing option exists.
```

## 18. Adversarial Security Review

```text
Use .agent/SECURITY.md and .agent/REVIEW_PROTOCOL.md. Perform an adversarial review of this change. Try to find prompt-injection paths, data exfiltration paths, privilege escalation, confused-deputy behavior, unsafe tool chains, missing approval gates, weak audit evidence, and residual risk. Findings first, ordered by severity.
```

## 19. Specialist Review

```text
Use .agent/REVIEW_PROTOCOL.md and .agent/TEMPLATES/SPECIALIST_REVIEW.md. Perform a specialist review for the requested lane. Inspect source-of-truth files, the diff or artifacts, validation evidence, and known risks. Return findings first, blocking issues, non-blocking issues, evidence gaps, final recommendation, and reviewer uncertainty.
```

## 20. Integration Review

```text
Use .agent/REVIEW_PROTOCOL.md. Review this multi-file or multi-domain change for integration risk. Check that source-of-truth docs agree, templates and guidance reference each other correctly, validation covers the whole change, no incompatible assumptions remain, and final accountability is clear.
```

## 21. Resolve Review Disagreement

```text
Use .agent/REVIEW_PROTOCOL.md. Two reviewers disagree. Preserve both positions, identify the evidence behind each, identify what evidence would resolve the disagreement, apply the stricter safety/security/correctness position until a maintainer decides, and record any accepted risk.
```

## 22. Create Adapter Guidance

```text
Use .agent/ADAPTERS.md. Audit which agent ecosystems this repository actually uses. Recommend minimal bridge files for Codex/OpenAI, Claude Code, Gemini CLI, GitHub Copilot, Cursor, Aider, or generic agents. Keep AGENTS.md and .agent/ as the source of truth and avoid duplicating long policy blocks.
```

## 23. Audit Nested Instruction Coverage

```text
Use .agent/NESTED_GUIDANCE.md. Audit this monorepo for subtrees that need nested AGENTS.md files. Identify package-specific commands, tests, risks, active overlays, ownership, and done criteria. Do not add nested files unless the benefit is clear.
```

## 24. Convert Existing Agent Instructions

```text
Convert existing CLAUDE.md, GEMINI.md, Copilot instructions, Cursor rules, or Aider guidance into AGENTS.md and .agent/ without losing local facts. Keep vendor-specific files as thin adapters that point back to the source-of-truth guidance.
```

## 25. Adopt Domain Overlays

```text
Use .agent/DOMAINS/README.md and .agent/TEMPLATES/DOMAIN_OVERLAY_ADOPTION.md. Identify which overlays apply to this repository, why they apply, which files/modules they cover, what commands and checks prove them, which specialist review lanes are active, and which overlays are intentionally deferred.
```

## 26. Audit Missing Overlays

```text
Audit this repository for missing domain overlays. Consider AI/ML, autonomous research, systems/kernels, accelerators, compilers, quantum, formal verification, robotics/autonomy, and frontends. Recommend only overlays justified by actual repository work.
```

## 27. Prune Irrelevant Overlays

```text
Review active .agent/DOMAINS/* overlays and identify any that do not apply. Recommend removing or deferring irrelevant overlays to keep guidance focused.
```

## 28. Model Card Creation

```text
Use .agent/DOMAINS/AI_ML.md and .agent/TEMPLATES/MODEL_CARD.md. Create or update a model card from source-of-truth code, training config, data records, eval reports, safety notes, license, and artifact provenance. Mark unknowns explicitly.
```

## 29. Dataset Card Creation

```text
Use .agent/DOMAINS/AI_ML.md and .agent/TEMPLATES/DATASET_CARD.md. Create or update a dataset card covering source, license, collection process, consent/privacy, schema, splits, bias, restrictions, transformations, and known limitations.
```

## 30. Evaluation Report

```text
Use .agent/TEMPLATES/EVAL_REPORT.md. Produce an evaluation report for this model or system. Include system under test, metrics, datasets, baselines, statistical treatment, failure cases, safety/security observations, limitations, and reproducibility commands.
```

## 31. Experiment Log

```text
Use .agent/TEMPLATES/EXPERIMENT_LOG.md. Record the hypothesis, setup, commands, environment, artifacts, results, interpretation, limitations, negative results, and next step for this experiment.
```

## 32. Autonomous Research Audit

```text
Use .agent/DOMAINS/AUTONOMOUS_RESEARCH.md. Audit this autonomous research workflow for literature source-of-truth, claim tracking, hypothesis/experiment separation, agent boundaries, replication requirements, negative result handling, artifact retention, and human review gates.
```

## 33. Kernel Or Unsafe Review

```text
Use .agent/DOMAINS/SYSTEMS_KERNELS.md. Review this systems, kernel, driver, firmware, unsafe-code, or low-level runtime change for ABI/API compatibility, undefined behavior, memory ordering, synchronization, resource lifetime, fault handling, fuzz/static/dynamic analysis, cross-platform validation, and rollback or recovery.
```

## 34. Accelerator Performance Review

```text
Use .agent/DOMAINS/ACCELERATORS.md. Review this accelerator change for hardware topology, runtime/compiler stack, profiling evidence, numerical equivalence, precision, quantization, determinism, memory transfers, occupancy, throughput, latency, energy, multi-device behavior, and correctness before speed.
```

## 35. Profiling-First Optimization

```text
Treat this as profiling-first optimization. Identify the hot path from evidence, define a baseline, make the smallest change, measure before and after, preserve correctness checks, and document limitations.
```

## 36. Compiler Change Review

```text
Use .agent/DOMAINS/COMPILERS.md. Review this compiler/language/runtime change for source-of-truth semantics, parser/lowering/typechecker/optimizer/codegen boundaries, semantic preservation, diagnostics, compatibility, golden and negative tests, differential testing, fuzzing, and release notes.
```

## 37. Quantum Change Review

```text
Use .agent/DOMAINS/QUANTUM.md. Review this quantum change for circuit model, target backend, OpenQASM/QIR compatibility, simulator versus hardware behavior, noise/error model, gate set, topology constraints, timing/calibration assumptions, measurement randomness, reproducibility, and tolerances.
```

## 38. Formal Proof Review

```text
Use .agent/DOMAINS/FORMAL_VERIFICATION.md and .agent/TEMPLATES/FORMAL_PROOF_NOTE.md. Review theorem statements, definitions, assumptions, axioms, proof status, trusted computing base, commands, artifacts, known gaps, and whether the proof is checked, partial, admitted, failed, or informal.
```

## 39. Interface Contract Review

```text
Use .agent/TEMPLATES/INTERFACE_CONTRACT.md. Review this API, CLI, schema, protocol, UI contract, file format, or model artifact interface for consumers, compatibility promises, inputs, outputs, errors, versioning, security/privacy, performance, tests, and migration.
```

## 40. Robotics Safety Review

```text
Use .agent/DOMAINS/ROBOTICS_AUTONOMY.md and .agent/TEMPLATES/SAFETY_CASE.md. Review hazards, assumptions, controls, actuation gating, operator override, simulation evidence, hardware or field evidence, logs/traces, residual risk, approval needed, and rollback or recovery.
```

## 41. Autonomy Field-Test Admission

```text
Before any hardware or field test, verify simulation evidence, safety boundaries, actuation gating, operator override, logs/traces, emergency stop behavior, environment assumptions, approval, and rollback or recovery. Do not perform unapproved physical-world actions.
```

## 42. Frontend Workflow Review

```text
Use .agent/DOMAINS/FRONTENDS.md. Review this frontend change for product intent, user workflow, accessibility, responsive behavior, browser/device coverage, state/data contracts, loading and error states, performance, privacy-sensitive UI, and visual evidence.
```

## 43. Visual Verification Review

```text
For this visual change, run or inspect browser evidence such as screenshots, visual regression output, or manual viewport checks. Confirm text fits, controls are accessible, layouts do not overlap, responsive states work, and the UI matches the intended workflow.
```

## 44. Final Pre-Submit Review

```text
Before finalizing, reread AGENTS.md, .agent/DONE.md, and any active domain overlays. Review the diff for correctness, tests, docs, unnecessary churn, dependency risk, performance risk, security risk, source-of-truth drift, specialist-review requirements, and remaining uncertainty. Then provide a final response with Summary, Validation, and Notes.
```

## 45. Create An Execution Plan Only

```text
Create an execution plan using .agent/TEMPLATES/EXEC_PLAN.md. Do not edit code yet. The plan should be concrete enough for another agent or engineer to implement. Include assumptions, affected files, active overlays, validation strategy, review strategy, risks, and open questions.
```

## 46. Convert A Vague Request Into A Safe Plan

```text
The request is broad or ambiguous. Use AGENTS.md and .agent/WORKFLOW.md to narrow it into a safe implementation plan. Identify what can be done now, what assumptions are required, what should not be changed, what validation would prove success, and what review is needed. Do not edit files yet.
```
