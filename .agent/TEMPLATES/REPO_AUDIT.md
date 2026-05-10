# Repository audit

Use this template to inspect a repository before major agent-assisted work or before adopting `agent-seed`.

Do not edit files during the audit unless explicitly asked.

## 1. Repository summary

```text
Project purpose: <summary>
Primary language(s): <languages>
Main framework/tooling: <frameworks/tools>
Maturity: <prototype | internal | production | research | unknown>
```

## 2. Repository map

```text
<path>: <purpose>
<path>: <purpose>
<path>: <purpose>
```

## 3. Canonical commands discovered

Use only commands supported by repository files or documentation.

```text
Setup:             <command or not found>
Run locally:       <command or not found>
Format:            <command or not found>
Lint:              <command or not found>
Type check:        <command or not found>
Unit tests:        <command or not found>
Integration tests: <command or not found>
All checks:        <command or not found>
Docs:              <command or not found>
Benchmarks:        <command or not found>
Build/package:     <command or not found>
```

## 4. Existing quality gates

```text
Tests: <summary>
Formatting: <summary>
Linting: <summary>
Type checking: <summary>
CI: <summary>
Docs checks: <summary>
Benchmarks: <summary>
Security/dependency checks: <summary>
```

## 5. Existing agent guidance

```text
AGENTS.md: <present/missing and summary>
.agent/: <present/missing and summary>
Other guidance files: <summary>
```

## 6. Local conventions

```text
Code style: <summary>
Testing style: <summary>
Error handling: <summary>
Documentation style: <summary>
Dependency style: <summary>
```

## 7. Important modules or flows

```text
<module or flow>: <responsibility and notes>
<module or flow>: <responsibility and notes>
```

## 8. Risky areas

```text
<area>: <reason>
<area>: <reason>
```

## 9. Missing or unclear information

```text
<missing information>
<missing information>
```

## 10. Agent-readiness assessment

Rate each area as `good`, `partial`, `missing`, or `unknown`.

```text
Repo map: <rating>
Canonical commands: <rating>
Testing guidance: <rating>
Validation guidance: <rating>
Local context: <rating>
Documentation: <rating>
Risk identification: <rating>
Definition of done: <rating>
```

## 11. Recommended improvements

List the smallest useful improvements first.

```text
1. <recommendation>
2. <recommendation>
3. <recommendation>
```

## 12. Suggested seed adoption

```text
Recommended adoption mode: <minimal | standard | reference-only>
Files to copy or update: <files>
Local customizations needed: <customizations>
```
