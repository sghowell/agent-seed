# Autonomous Research Overlay

Use this overlay for repositories that support autonomous literature review, hypothesis generation, experiment planning, simulation, theorem search, lab automation, scientific discovery, or claim synthesis.

## Literature Source-Of-Truth

Track:

- papers, datasets, code, and artifacts used,
- retrieval query or search method,
- publication dates,
- versions,
- citations,
- access dates when needed,
- source quality and limitations.

Do not let a generated summary become the only record of evidence.

## Claim Inventory

Maintain a claim graph or claim inventory for research conclusions.

Each claim should record:

- statement,
- evidence,
- counterevidence,
- assumptions,
- uncertainty,
- replication status,
- next evidence needed.

Use `.agent/TEMPLATES/RESEARCH_CLAIM.md`.

## Hypothesis And Experiment Separation

Separate:

- hypotheses,
- planned experiments,
- executed experiments,
- results,
- interpretation,
- follow-up decisions.

Use `.agent/TEMPLATES/EXPERIMENT_LOG.md`.

## Autonomous Agent Boundaries

Autonomous research agents need explicit boundaries:

- allowed sources,
- allowed tools,
- allowed compute,
- data access,
- publication boundaries,
- lab or hardware boundaries,
- human approval gates,
- stop conditions.

## Replication Requirements

Before treating a result as strong evidence, record:

- commands,
- environment,
- data and artifact versions,
- seeds,
- hardware,
- runtime,
- limitations,
- whether the result was replicated.

## Negative Results

Negative and inconclusive results are evidence.

Do not delete or bury them when they affect future search, benchmark claims, theorem attempts, experiment planning, or research conclusions.

## Artifact Retention

Preserve enough artifacts to audit:

- prompts,
- queries,
- notes,
- configs,
- logs,
- generated hypotheses,
- experiment outputs,
- datasets,
- plots,
- proofs,
- code changes.

When raw artifacts cannot be retained, record hashes, paths, summaries, and reasons.

## Human Review Gates

Require human review before:

- external publication,
- high-impact scientific claims,
- expensive compute runs,
- physical lab actions,
- clinical, safety, legal, or policy recommendations,
- changes to research records that erase prior evidence.
