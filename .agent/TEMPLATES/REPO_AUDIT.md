# Repository Audit

Use this template to inspect a repository before major agent-assisted work or before adopting `agent-seed`.

Do not edit files during the audit unless explicitly asked.

## 1. Repository Summary

```text
Project purpose: <summary>
Primary language(s): <languages>
Main framework/tooling: <frameworks/tools>
Maturity: <prototype | internal | production | research | unknown>
Quality bar: <minimal | standard | high-rigor | safety-critical | unknown>
```

## 2. Repository Map

```text
<path>: <purpose>
<path>: <purpose>
<path>: <purpose>
```

## 3. Canonical Commands Discovered

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
Security checks:   <command or not found>
Formal checks:     <command or not found>
Hardware checks:   <command or not found>
```

## 4. Existing Quality Gates

```text
Tests: <summary>
Formatting: <summary>
Linting: <summary>
Type checking: <summary>
CI: <summary>
Docs checks: <summary>
Benchmarks: <summary>
Security/dependency checks: <summary>
Review requirements: <summary>
```

## 5. Existing Agent Guidance

```text
AGENTS.md: <present/missing and summary>
.agent/: <present/missing and summary>
Adapter files: <CLAUDE/GEMINI/Copilot/Cursor/Aider/other>
Nested guidance: <present/missing and scope>
Other guidance files: <summary>
```

## 6. Agentic Security Readiness

```text
Agent/tool/MCP usage: <summary>
Tool permissions: <summary>
Secrets/privacy handling: <summary>
Prompt-injection risk: <summary>
Context/memory poisoning risk: <summary>
Supply-chain risk: <summary>
Approval boundaries: <summary>
Auditability: <summary>
```

## 7. Local Conventions

```text
Code style: <summary>
Testing style: <summary>
Error handling: <summary>
Documentation style: <summary>
Dependency style: <summary>
Release style: <summary>
```

## 8. Important Modules Or Flows

```text
<module or flow>: <responsibility and notes>
<module or flow>: <responsibility and notes>
```

## 9. Risky Areas

```text
<area>: <reason>
<area>: <reason>
```

## 10. Domain Overlay Assessment

```text
AI/ML: <applies/does not apply/unknown>
Autonomous research: <applies/does not apply/unknown>
Systems/kernels: <applies/does not apply/unknown>
Accelerators: <applies/does not apply/unknown>
Compilers: <applies/does not apply/unknown>
Quantum: <applies/does not apply/unknown>
Formal verification: <applies/does not apply/unknown>
Robotics/autonomy: <applies/does not apply/unknown>
Frontends: <applies/does not apply/unknown>
```

## 11. Review Readiness

```text
Self-review guidance: <rating>
Specialist review lanes: <rating>
Adversarial review triggers: <rating>
Integration review guidance: <rating>
Source-of-truth drift handling: <rating>
```

## 12. Missing Or Unclear Information

```text
<missing information>
<missing information>
```

## 13. Agent-Readiness Assessment

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
Agentic security: <rating>
Adapter guidance: <rating>
Nested guidance: <rating>
Domain overlays: <rating>
current-source refresh guidance: <rating>
Review protocol: <rating>
```

## 14. Recommended Improvements

List the smallest useful improvements first.

```text
1. <recommendation>
2. <recommendation>
3. <recommendation>
```

## 15. Suggested Seed Adoption

```text
Recommended adoption mode: <minimal | standard | reference-only | high-rigor>
Files to copy or update: <files>
Local customizations needed: <customizations>
Domain overlays to adopt: <overlays>
Adapter files to create: <adapter files or none>
Nested guidance to add: <paths or none>
current-source refresh needs: <sources or none>
```
