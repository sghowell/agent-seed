# Threat Model

Use this template for security-sensitive, agentic, tool/MCP, data, model, identity, production, privacy, or safety-related changes.

## System Or Change

```text
<system or change>
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
Authorization spec version: <version/date or not applicable>
Resource indicator: <intended MCP server resource or not applicable>
Token audience validation: <validation plan or not applicable>
Token passthrough prevented: <yes/no/not applicable>
PKCE required: <yes/no/not applicable>
Redirect URI policy: <exact HTTPS/localhost policy or not applicable>
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
