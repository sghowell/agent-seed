# Review template

Use this template to review a diff, pull request, patch, or proposed change.

Review as a strict but constructive senior engineer.

## 1. Summary judgment

```text
Safe to proceed | Needs changes | Risky | Insufficient information
```

## 2. What changed

```text
<brief summary>
```

## 3. Correctness review

Check whether the change solves the intended problem without introducing regressions.

```text
Issues:
- <issue or none found>

Notes:
- <note>
```

## 4. Test review

Check whether the change has appropriate test coverage.

```text
Existing tests affected: <summary>
New tests added: <summary>
Missing tests: <summary>
Tests weakened or removed: <summary>
```

## 5. Validation review

```text
Checks run: <summary>
Checks not run: <summary>
Validation gaps: <summary>
```

## 6. Documentation review

```text
Docs updated: <yes/no/not needed>
Docs gaps: <summary>
```

## 7. Maintainability review

Check for readability, unnecessary churn, naming, complexity, and consistency with local patterns.

```text
Issues:
- <issue or none found>
```

## 8. Dependency review

```text
New dependencies: <summary>
Dependency risks: <summary>
Lockfile changes: <summary>
```

## 9. Performance review

```text
Performance-sensitive: <yes/no>
Measurement provided: <yes/no/not needed>
Performance risks: <summary>
```

## 10. Security review

```text
Security-sensitive: <yes/no>
Security risks: <summary>
```

## 11. Compatibility review

```text
Public API impact: <summary>
Config/schema/data impact: <summary>
Migration needed: <summary>
```

## 12. Highest-priority issues

List only the issues that should be fixed before the change is accepted.

```text
1. <issue>
2. <issue>
3. <issue>
```

## 13. Suggested fixes

```text
<fix recommendation>
<fix recommendation>
```

## 14. Final recommendation

```text
<recommendation>
```
