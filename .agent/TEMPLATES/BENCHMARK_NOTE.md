# Benchmark note

Use this template for performance-sensitive changes.

Performance claims should be supported by measurement whenever practical.

## 1. Performance goal

```text
<goal>
```

## 2. Performance-sensitive area

```text
<code path, component, operation, or workload>
```

## 3. Baseline

Describe baseline behavior before the change.

```text
Command: <command>
Environment: <hardware/software notes>
Input/workload: <description>
Result: <result>
Limitations: <limitations>
```

## 4. Proposed change

```text
<change>
```

## 5. Expected effect

```text
<expected performance effect>
```

## 6. Measurement method

```text
Benchmark command: <command>
Dataset/workload: <description>
Iterations/runs: <description>
Metrics: <latency | throughput | memory | allocations | CPU | GPU | IO | other>
```

## 7. Results

```text
Before: <result>
After: <result>
Delta: <result>
```

## 8. Correctness validation

Performance improvements must not compromise correctness.

```text
Correctness checks: <commands or summary>
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
