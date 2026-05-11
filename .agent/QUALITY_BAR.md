# Quality Bar

This repository expects agent-assisted work to meet a principal or distinguished engineer/scientist standard when risk, scope, or domain complexity warrants it.

## Core Expectation

Work should be precise, evidence-driven, reviewable, reversible where practical, and honest about uncertainty.

Generic guidance is a floor, not a ceiling. When a repository activates this file, agents should raise the level of rigor until it matches the consequence of being wrong.

## Engineering Standard

Agents should:

- prefer source-of-truth evidence over summaries,
- preserve compatibility unless the task explicitly changes it,
- make narrow changes that solve the actual problem,
- use existing abstractions before inventing new ones,
- identify failure modes before changing high-risk paths,
- prove behavior with tests, checks, benchmarks, traces, formal arguments, or specialist review appropriate to the risk,
- keep rollback or recovery practical for high-risk changes,
- and avoid trading correctness, security, maintainability, reproducibility, or safety for speed without explicit approval.

## Scientific Standard

Agents should:

- separate claims from evidence,
- state assumptions, units, tolerances, datasets, hardware, seeds, and environment,
- preserve enough metadata for another expert to reproduce or challenge the result,
- treat negative results as evidence when they are measured carefully,
- distinguish exploratory work from validated results,
- and avoid overstating conclusions from weak, narrow, or non-representative measurements.

## Evidence Ladder

Evidence strength, from weakest to strongest:

1. Reasoned inspection.
2. Targeted manual reproduction.
3. Targeted automated tests.
4. Broad automated checks.
5. Benchmarks with environment, workload, variance, and limitations.
6. Cross-platform, cross-backend, or independent implementation validation.
7. Independent specialist review.
8. Formal proof, mechanically checked invariant, or model-checked property.
9. Production, field, or operational evidence with monitoring and rollback.

Use the strongest practical evidence for the risk level. This evidence ladder is intentionally cumulative: a low-risk documentation edit may only need inspection, while a kernel, autonomy, security, ML-evaluation, or formal-methods change may need several layers.

## Review Posture

- Review your own diff before asking others to trust it.
- Invite specialist review for areas outside ordinary application code.
- Treat unresolved reviewer disagreement as a risk, not as noise.
- Label unvalidated claims as assumptions.
- Record accepted risk in the final notes, design record, or release evidence.
- Final accountability stays with the integrating agent or maintainer.

## Risk Calibration

Raise the evidence bar when work affects:

- security, identity, secrets, privacy, or authorization,
- data or model provenance,
- training, evaluation, or inference behavior,
- numerical, scientific, or statistical claims,
- kernels, drivers, unsafe code, firmware, or hardware interaction,
- accelerators, compilers, runtimes, or language semantics,
- formal proofs, theorem statements, or verified artifacts,
- robotics, actuation, autonomy, or safety cases,
- public APIs, schemas, protocols, or persisted data,
- production operations, release processes, or external users.

## What Fails This Bar

Work does not meet this bar when it:

- relies on unsourced claims where evidence is available,
- hides uncertainty,
- reports checks that were not run,
- changes public behavior without compatibility analysis,
- treats benchmarks as proof without workload and environment detail,
- treats tests as proof while ignoring untested critical paths,
- accepts external content, tools, or model artifacts without provenance,
- weakens safety or security gates for convenience,
- or delegates high-impact decisions without preserving accountability.
