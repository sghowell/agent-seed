# Review Template

Use this template to review a diff, pull request, patch, or proposed change.

Review as a strict but constructive senior engineer. For high-risk work, pair this template with `.agent/REVIEW_PROTOCOL.md` and `.agent/TEMPLATES/SPECIALIST_REVIEW.md`.

## 1. Summary Judgment

```text
Safe to proceed | Needs changes | Risky | Block | Insufficient information
```

## 2. Review Lane

```text
General | Security and agentic AI | AI/ML and evaluation | Systems/kernel/unsafe/firmware | Accelerators/performance | Compilers/language/runtime | Quantum | Formal verification/math | Robotics/autonomy/safety | Frontend/product/accessibility | Documentation/source-of-truth
```

## 3. Specialist Or Adversarial Review Required

```text
Specialist review required: <yes/no and lane>
Adversarial review required: <yes/no and why>
Integration review required: <yes/no and why>
```

## 4. What Changed

```text
<brief summary>
```

## 5. Evidence Inspected

```text
Source-of-truth files: <files>
Diff/artifacts: <diff/artifacts>
Validation evidence: <commands/results/artifacts>
```

## 6. Correctness Review

Check whether the change solves the intended problem without introducing regressions.

```text
Issues:
- <issue or none found>

Notes:
- <note>
```

## 7. Test Review

Check whether the change has appropriate test coverage.

```text
Existing tests affected: <summary>
New tests added: <summary>
Missing tests: <summary>
Tests weakened or removed: <summary>
```

## 8. Validation Review

```text
Checks run: <summary>
Checks not run: <summary>
Validation gaps: <summary>
Evidence strength: <inspection | targeted test | broad checks | benchmark | cross-backend | specialist review | formal proof | operational evidence>
```

## 9. Documentation And Source-Of-Truth Review

```text
Docs updated: <yes/no/not needed>
Docs gaps: <summary>
Source-of-truth drift: <summary>
```

## 10. Maintainability Review

Check for readability, unnecessary churn, naming, complexity, and consistency with local patterns.

```text
Issues:
- <issue or none found>
```

## 11. Dependency And Supply-Chain Review

```text
New dependencies: <summary>
Dependency risks: <summary>
Lockfile changes: <summary>
Model/data/binary/prompt/tool provenance: <summary>
```

## 12. Performance Review

```text
Performance-sensitive: <yes/no>
Measurement provided: <yes/no/not needed>
Performance risks: <summary>
```

## 13. Security Review

```text
Security-sensitive: <yes/no>
Agent/tool/MCP/autonomy impact: <summary>
Secrets/privacy impact: <summary>
Security risks: <summary>
```

## 14. Compatibility Review

```text
Public API impact: <summary>
Config/schema/data impact: <summary>
Model/artifact/interface impact: <summary>
Migration needed: <summary>
```

## 15. Highest-Priority Findings

List only the issues that should be fixed before the change is accepted.

```text
1. <issue>
2. <issue>
3. <issue>
```

## 16. Suggested Fixes

```text
<fix recommendation>
<fix recommendation>
```

## 17. Final Accountability

```text
Integrating owner:
Accepted risks:
Deferred review:
```

## 18. Final Recommendation

```text
<recommendation>
```
