# Formal Verification And Mathematics Overlay

Use this overlay for theorem proving, proof assistants, SMT, model checking, verified extraction, formal specifications, mathematical libraries, or proof-carrying artifacts.

## Source Of Truth

Identify:

- proof assistant,
- solver,
- model checker,
- specification language,
- theorem statements,
- definitions,
- libraries,
- tool versions.

## Definitions And Theorems

State:

- definitions,
- theorem or property statement,
- scope,
- preconditions,
- postconditions,
- assumptions,
- expected consumers.

## Assumptions And Axioms

Record all:

- axioms,
- admitted lemmas,
- trusted external facts,
- solver assumptions,
- extraction assumptions,
- runtime assumptions.

Use `.agent/TEMPLATES/FORMAL_PROOF_NOTE.md`.

## Proof Status

Use explicit proof status:

```text
Informal
Checked
Partial
Admitted
Failed
Unknown
```

Do not describe admitted or partial proof as proven without qualification.

## Trusted Computing Base

Identify the trusted computing base:

- proof assistant kernel,
- solver,
- code generator,
- extracted runtime,
- libraries,
- axioms,
- imported artifacts.

## Regression Proofs

When changing definitions, statements, or implementations:

- run proof checks,
- update dependent proofs deliberately,
- record migration notes,
- preserve theorem names when compatibility matters,
- document changed assumptions.

## Specialist Review

Request formal verification/math review for theorem statements, proof status, assumptions, axioms, extraction, solver trust, or mathematical claims.
