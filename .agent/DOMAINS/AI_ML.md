# AI/ML Overlay

Use this overlay for repositories involving machine learning models, datasets, training, fine-tuning, inference, evaluation, agents, embeddings, retrieval, ranking, safety, or model-serving infrastructure.

## Source Of Truth

Identify source-of-truth records for:

- model architecture and version,
- training configuration,
- datasets and splits,
- data provenance and licensing,
- checkpoints and artifacts,
- eval harnesses and metrics,
- inference runtime and deployment configuration,
- safety and misuse analysis.

Do not rely on informal summaries when configs, manifests, logs, or artifacts exist.

## Data Provenance And Licensing

Track:

- data origin,
- license and attribution,
- collection method,
- consent or privacy basis,
- transformations,
- filtering,
- retention,
- downstream consumers.

Use `.agent/TEMPLATES/DATA_PROVENANCE.md` and `.agent/TEMPLATES/DATASET_CARD.md`.

## Contamination And Leakage

For training or evaluation work, consider:

- train/eval/test split contamination,
- benchmark leakage,
- deduplication,
- prompt or answer leakage,
- retrieval corpus overlap,
- user data leakage,
- temporal leakage,
- label leakage.

Report checks performed and residual risk.

## Reproducibility

Record:

- code version,
- configs,
- dependency versions,
- hardware,
- runtime,
- seeds,
- distributed setup,
- checkpoints,
- data versions,
- environment variables,
- nondeterminism.

## Evaluation

Evaluation should include:

- baselines,
- metrics,
- datasets,
- confidence intervals or variance where practical,
- failure slices,
- calibration or robustness checks where relevant,
- safety/security observations,
- limitations.

Use `.agent/TEMPLATES/EVAL_REPORT.md`.

## Training

Training records should include:

- optimizer,
- schedule,
- batch size,
- precision,
- checkpointing,
- resume behavior,
- distributed failures,
- cost,
- metrics,
- artifacts.

Use `.agent/TEMPLATES/TRAINING_RUN.md`.

## Inference

Inference work should consider:

- latency,
- throughput,
- memory,
- precision,
- quantization,
- batching,
- caching,
- fallback behavior,
- monitoring,
- rollback,
- safety filters,
- prompt-injection and data-exfiltration risks.

Use `.agent/TEMPLATES/INFERENCE_DEPLOYMENT.md`.

## Model Documentation

Use `.agent/TEMPLATES/MODEL_CARD.md` for models that may be reused, deployed, published, evaluated, or audited.

Model cards should cover intended use, limitations, training data, evals, safety, license, provenance, and version.

## Specialist Review

Request AI/ML and evaluation review for:

- benchmark claims,
- model releases,
- training pipeline changes,
- eval harness changes,
- data filtering changes,
- safety-sensitive inference behavior,
- privacy-sensitive datasets,
- production model rollouts.
