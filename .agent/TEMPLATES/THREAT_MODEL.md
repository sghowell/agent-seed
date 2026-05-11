# Threat Model

Use this template for security-sensitive, agentic, tool/MCP, data, model, identity, production, privacy, or safety-related changes.

## System Or Change

```text
<system or change>
```

## Current-Source Refresh

Use this section when security, tool, MCP, agent, model, dataset, benchmark, hardware, API, legal, or standards facts may have drifted.

```text
Sources checked:
- <source title and URL or local path>
Date checked:
Version or publication date:
Decision depending on source:
Drift risk:
```

## Assets

```text
<asset>: <why it matters>
<asset>: <why it matters>
```

## Trust Boundaries

```text
<boundary>: <what crosses it>
<boundary>: <what crosses it>
```

## Actors And Identities

```text
Human users: <summary>
Agents/subagents: <summary>
Services/tools: <summary>
External actors: <summary>
Credentials used: <summary>
```

## Agentic AI Risk Taxonomy

```text
Privilege risks:
Design and configuration risks:
Behavior risks:
Structural risks:
Accountability risks:
Lifecycle stage: <designing | developing | managing third-party components | deploying | operating | not applicable>
```

## Tools And Permissions

```text
Tool or MCP server: <scope and permissions>
Tool or MCP server: <scope and permissions>
```

## MCP Authorization

```text
HTTP-based MCP involved: <yes/no>
MCP authorization spec version checked: <version/date or not applicable>
Transport credential model: <HTTP authorization | STDIO environment credentials | other approved mechanism | not applicable>
Protected resource metadata discovery: <WWW-Authenticate resource_metadata | well-known URI | both | not applicable>
Protected resource metadata authorization_servers: <present with one server | present with multiple servers and selection policy | absent and rejected | not applicable>
Authorization server discovery: <OAuth metadata | OpenID Connect discovery | both | not applicable>
Authorization server endpoint security: <HTTPS endpoints | non-HTTPS endpoint rejected | not applicable>
Client registration approach: <pre-registered | Client ID Metadata Document | Dynamic Client Registration | user-provided | not applicable>
Client ID Metadata Document validation: <validation plan or not applicable>
Requested scopes: <scopes and least-privilege rationale or not applicable>
Scope challenge and step-up handling: <handling plan or not applicable>
Resource indicator: <canonical MCP server resource or not applicable>
Token transport: <Authorization header every request | not applicable>
Token audience validation: <validation plan or not applicable>
Token passthrough prevented: <yes/no/not applicable>
Authorization error handling: <401/403/insufficient_scope handling or not applicable>
PKCE support discovery: <code_challenge_methods_supported metadata source, S256 advertisement, and refusal behavior or not applicable>
PKCE method: <S256 | other with justification | not applicable>
Authorization state binding: <state generation, storage, verification, and mismatch handling or not applicable>
Redirect URI policy: <exact registered redirect URI policy, HTTPS/localhost constraints, and open-redirect prevention or not applicable>
Localhost redirect risk controls: <development-only constraint, warning, attestation, or not applicable>
Trust policy: <trusted authorization servers, clients, metadata documents, redirect URIs, redirect destinations, scopes>
Token storage and logging controls: <controls>
```

## Data Sources

```text
<source>: <trusted/untrusted, sensitivity, provenance>
```

## Memory And Context Sources

```text
<source>: <risk and mitigation>
```

## External Content Sources

```text
<source>: <prompt-injection or data risk>
```

## Prompt-Injection Risks

```text
<risk>: <mitigation>
```

## Goal-Hijack Risks

```text
<risk>: <mitigation>
```

## Tool-Misuse Risks

```text
<risk>: <mitigation>
```

## Secrets And Privacy Risks

```text
<risk>: <mitigation>
```

## Supply-Chain Risks

```text
<risk>: <mitigation>
```

## Autonomy And Approval Boundaries

```text
Allowed without approval: <actions>
Requires approval: <actions>
Denied: <actions>
```

## Failure Modes

```text
<failure mode>: <impact>
```

## Mitigations

```text
<mitigation>: <risk addressed>
```

## Validation

```text
Checks: <commands or evidence>
Adversarial cases: <cases>
Audit evidence: <logs/artifacts>
```

## Residual Risk

```text
<residual risk>
```

## Reviewer

```text
Reviewer:
Review date:
Open questions:
```
