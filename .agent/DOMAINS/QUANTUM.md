# Quantum Computing Overlay

Use this overlay for quantum circuits, algorithms, simulators, compilers, OpenQASM, QIR, hardware backends, error models, or quantum-control-adjacent tooling.

## Circuit And Backend Model

Identify:

- circuit model,
- target backend,
- simulator or hardware execution,
- supported gate set,
- topology constraints,
- measurement model,
- randomness model,
- classical control behavior.

## OpenQASM And QIR Compatibility

When using interchange formats, record:

- OpenQASM version,
- QIR profile or assumptions,
- supported subset,
- unsupported features,
- translation boundaries,
- round-trip or conformance tests.

## Simulator Versus Hardware

Distinguish:

- noiseless simulation,
- noisy simulation,
- hardware execution,
- calibration assumptions,
- timing assumptions,
- shot count,
- queue and availability limits.

## Error And Noise Model

Record:

- error model,
- noise parameters,
- decoherence assumptions,
- readout errors,
- crosstalk assumptions,
- mitigation techniques.

## Reproducibility

Record:

- random seeds,
- shot count,
- backend version,
- calibration timestamp,
- simulator version,
- hardware availability limits,
- numerical tolerances.

## Validation

Consider:

- small analytic circuits,
- simulator cross-checks,
- hardware/simulator comparisons,
- tolerance checks,
- format conformance tests,
- differential tests across backends.

## Specialist Review

Request quantum review for circuit semantics, OpenQASM/QIR translation, simulator correctness, hardware assumptions, error models, or quantum performance claims.
