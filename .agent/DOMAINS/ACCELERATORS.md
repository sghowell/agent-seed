# Accelerators And Heterogeneous Hardware Overlay

Use this overlay for GPU, TPU, NPU, FPGA, DSP, accelerator, heterogeneous CPU/device, distributed training, inference kernels, runtime, or hardware performance work.

## Applicability

This overlay applies when work touches:

- kernels,
- device memory,
- runtime dispatch,
- profiling,
- compiler flags,
- distributed compute,
- quantization,
- mixed precision,
- hardware-specific paths,
- performance claims.

## Hardware Topology

Record:

- host CPU and memory,
- accelerator model,
- interconnect,
- NUMA placement,
- device placement,
- topology,
- driver,
- firmware,
- runtime,
- libraries.

## Profiling-First Workflow

Optimization should start from evidence:

1. Identify the hot path.
2. Establish baseline.
3. Profile.
4. Make a narrow change.
5. Validate correctness.
6. Measure after.
7. Document variance and limitations.

## Numerical Correctness

Accelerator changes must preserve correctness.

Define:

- reference implementation,
- tolerance,
- precision,
- quantization,
- determinism requirements,
- acceptable nondeterminism,
- failure cases.

## Performance Dimensions

Consider:

- latency,
- throughput,
- occupancy,
- memory bandwidth,
- host/device transfer,
- kernel launch overhead,
- batching,
- concurrency,
- cache behavior,
- communication overhead,
- power/energy,
- cost.

## Multi-Device And Distributed Behavior

Review:

- device placement,
- collective operations,
- synchronization,
- failure recovery,
- deterministic reduction behavior,
- topology-sensitive performance,
- cross-device data movement.

## Evidence

Use `.agent/TEMPLATES/BENCHMARK_NOTE.md` or `.agent/TEMPLATES/HARDWARE_BENCHMARK.md`.

Benchmark records should include warmup, runs, variance, hardware, topology, firmware/driver/runtime, compiler flags, precision, batch/concurrency, correctness checks, baseline, after result, regression threshold, and artifacts.

## Specialist Review

Request accelerator/performance review for kernel changes, performance claims, precision changes, quantization, runtime dispatch, multi-device behavior, or expensive benchmark conclusions.
