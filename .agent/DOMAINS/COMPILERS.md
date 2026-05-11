# Compilers, Languages, And Runtimes Overlay

Use this overlay for parsers, languages, IRs, type systems, lowering, optimizers, code generation, runtimes, diagnostics, or compatibility-sensitive tooling.

## Source Of Truth

Identify:

- language specification,
- grammar,
- IR definition,
- type rules,
- lowering rules,
- runtime semantics,
- compatibility policy,
- diagnostics conventions.

## Pipeline Boundaries

Know which stage is changing:

- parser,
- resolver,
- typechecker,
- lowering,
- optimizer,
- scheduler,
- codegen,
- linker,
- runtime,
- diagnostics,
- tooling.

## Semantic Preservation

Optimization and lowering changes should state:

- source semantics,
- target semantics,
- invariants,
- assumptions,
- unsupported cases,
- tests proving preservation.

## Diagnostics

User-facing diagnostics should be:

- accurate,
- actionable,
- stable where compatibility matters,
- tested with positive and negative cases.

## Compatibility And Migration

Consider:

- language compatibility,
- IR compatibility,
- ABI/API compatibility,
- serialized artifact compatibility,
- feature flags,
- deprecation,
- migration notes,
- release notes.

## Validation

Consider:

- golden tests,
- negative tests,
- parser round-trip tests,
- differential testing,
- fuzzing,
- property tests,
- conformance suites,
- performance benchmarks,
- cross-backend tests.

## Specialist Review

Request compiler/language/runtime review for semantic changes, optimizer changes, IR changes, diagnostics policy, compatibility changes, or runtime behavior.
