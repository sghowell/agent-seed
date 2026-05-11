# Domain Overlays

Domain overlays are optional guidance modules for repositories where generic software standards are not enough.

Copy or activate only the overlays that match real repository work.

## Rules

- Overlays are optional.
- Target repositories should copy only relevant overlays.
- `.agent/LOCAL_CONTEXT.md` should list active overlays.
- Overlays do not override local source-of-truth facts.
- Overlays can require stronger validation than generic guidance.
- If overlays conflict, the more safety-critical or specific rule governs until maintainers decide.
- If an overlay is copied but not used, remove it or mark it deferred.

## Available Overlays

```text
AI_ML.md                    Models, data, training, inference, evals, safety, and reproducibility.
AUTONOMOUS_RESEARCH.md      Literature, claims, experiments, replication, and autonomous research boundaries.
SYSTEMS_KERNELS.md          OS, kernels, drivers, firmware, unsafe code, ABI, and recovery.
ACCELERATORS.md             GPU/TPU/NPU/FPGA and heterogeneous performance work.
COMPILERS.md                Language, IR, lowering, optimization, codegen, diagnostics, and semantic preservation.
QUANTUM.md                  Circuits, OpenQASM, QIR, simulation, hardware constraints, and error models.
FORMAL_VERIFICATION.md      Proof assistants, SMT, model checking, theorem status, assumptions, and proof artifacts.
ROBOTICS_AUTONOMY.md        ROS 2, actuation, simulation, hardware tests, field admission, and safety cases.
FRONTENDS.md                Product workflows, accessibility, browser evidence, responsive behavior, and visual verification.
```

## Adoption

Use `.agent/TEMPLATES/DOMAIN_OVERLAY_ADOPTION.md` to record:

- active overlays,
- why each overlay applies,
- files/modules covered,
- commands and checks,
- specialist review lanes,
- domain-specific risks,
- evidence requirements,
- deferred overlays.

## Review

Revisit overlays when:

- repository scope changes,
- new hardware, models, or runtime targets are added,
- public interfaces change,
- safety/security posture changes,
- domain-specific tests or benchmarks change,
- ownership changes,
- or agents repeatedly miss domain-specific risks.
