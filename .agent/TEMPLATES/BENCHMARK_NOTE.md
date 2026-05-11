# Benchmark Note

Use this template for performance-sensitive changes.

Performance claims should be supported by measurement whenever practical. Benchmark notes should include enough metadata for another expert to reproduce, challenge, or reinterpret the result.

## 1. Performance Goal

```text
<goal>
```

## 2. Performance-Sensitive Area

```text
<code path, component, operation, or workload>
```

## 3. Baseline

Describe baseline behavior before the change.

```text
Command: <command>
Environment: <hardware/software notes>
Hardware: <CPU/GPU/accelerator/memory/storage/network>
Topology: <NUMA, device placement, interconnect, or not relevant>
Firmware/driver/runtime: <versions or not relevant>
Compiler flags: <flags or not relevant>
Dataset/workload: <description>
Precision: <precision, tolerance, quantization, or not relevant>
Batch/concurrency: <shape>
Warmup: <warmup policy>
Runs: <iterations/repetitions>
Result: <result>
Variance: <variance/confidence interval/outliers>
Limitations: <limitations>
```

## 4. Proposed Change

```text
<change>
```

## 5. Expected Effect

```text
<expected performance effect>
```

## 6. Measurement Method

```text
Benchmark command: <command>
Dataset/workload: <description>
Iterations/runs: <description>
Metrics: <latency | throughput | memory | allocations | CPU | GPU | IO | power | energy | other>
Isolation: <machine load, pinning, clocks, containers, or not controlled>
Regression threshold: <threshold>
Artifacts: <logs/profiles/traces/raw data>
```

## 7. Results

```text
Before: <result>
After: <result>
Delta: <result>
Variance: <summary>
Power/energy: <result or not measured>
```

## 8. Correctness Validation

Performance improvements must not compromise correctness.

```text
Correctness checks: <commands or summary>
Tolerance: <tolerance if numerical>
Reference implementation: <reference or not applicable>
```

## 9. Tradeoffs

```text
<tradeoff>
<tradeoff>
```

## 10. Limitations

```text
<limitation>
<limitation>
```

## 11. Recommendation

```text
<recommendation>
```
