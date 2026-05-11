# Robotics And Autonomy Overlay

Use this overlay for robotics, drones, vehicles, lab automation, embodied agents, autonomous planners, ROS 2 systems, safety-critical control, or physical-world actuation.

## Simulation Versus Hardware Evidence

Separate:

- unit tests,
- simulation,
- hardware-in-the-loop,
- bench tests,
- field tests,
- production evidence.

Do not treat simulation as proof of field safety unless limitations are explicit.

## Safety Boundaries

Identify:

- hazards,
- safety constraints,
- actuation limits,
- forbidden actions,
- safe state,
- emergency stop,
- operator override,
- rollback or recovery.

Use `.agent/TEMPLATES/SAFETY_CASE.md`.

## Actuation Gating

Physical-world actions require explicit approval and admission criteria.

Agents should not perform unapproved actuation, hardware operation, lab action, or field-test action.

## ROS 2 And Middleware

For ROS 2 systems, consider:

- QoS settings,
- node graph,
- topic/service/action contracts,
- transforms,
- time synchronization,
- lifecycle nodes,
- security enclave configuration,
- authentication and encryption,
- replay and bag files.

## Sensors And Calibration

Record:

- sensor model,
- calibration,
- coordinate frames,
- time sync,
- uncertainty,
- failure modes,
- stale or missing data behavior.

## Fault Handling

Consider:

- degraded sensors,
- actuator faults,
- communication loss,
- planner failure,
- localization failure,
- power constraints,
- watchdogs,
- safe stop behavior.

## Logs And Traces

Preserve:

- commands,
- simulation configs,
- bag files,
- traces,
- telemetry,
- operator notes,
- safety approvals,
- incident reports.

## Field-Test Admission

Before field or hardware tests, confirm:

- simulation evidence,
- risk assessment,
- environment constraints,
- operator override,
- emergency stop,
- logs/traces,
- approval,
- rollback or recovery.

## Specialist Review

Request robotics/autonomy/safety review for planning, control, perception, actuation, safety cases, field admission, middleware security, or hardware operation.
