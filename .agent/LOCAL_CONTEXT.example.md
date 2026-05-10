# Local repository context

Copy this file to:

```text
.agent/LOCAL_CONTEXT.md
```

Then replace the placeholders with facts about the target repository.

Do not invent commands or conventions. Mark unknowns clearly.

## Project summary

```text
Project name: <fill in>
Purpose: <fill in>
Primary users: <fill in>
Current maturity: <prototype | internal tool | production | research | unknown>
```

## Repository structure

Describe the major directories and files.

```text
<directory or file>: <purpose>
<directory or file>: <purpose>
<directory or file>: <purpose>
```

## Canonical commands

Use real commands only.

```text
Setup:             <command or not defined>
Run locally:       <command or not defined>
Format:            <command or not defined>
Lint:              <command or not defined>
Type check:        <command or not defined>
Unit tests:        <command or not defined>
Integration tests: <command or not defined>
All tests:         <command or not defined>
All checks:        <command or not defined>
Docs:              <command or not defined>
Benchmarks:        <command or not defined>
Build/package:     <command or not defined>
```

## Main modules

```text
<module>: <responsibility>
<module>: <responsibility>
<module>: <responsibility>
```

## Architecture notes

Summarize important architecture facts.

```text
<fill in>
```

## Data flow

Describe important data flow, request flow, or execution flow.

```text
<fill in>
```

## Public interfaces

List interfaces that require compatibility care.

```text
APIs: <fill in or none known>
CLIs: <fill in or none known>
Config files: <fill in or none known>
Schemas: <fill in or none known>
File formats: <fill in or none known>
Environment variables: <fill in or none known>
External integrations: <fill in or none known>
```

## Testing conventions

Describe how tests are organized and what kinds of tests are expected.

```text
<fill in>
```

## Documentation conventions

Describe documentation locations and expectations.

```text
<fill in>
```

## Style conventions

Describe naming, formatting, error handling, logging, and other local style expectations.

```text
<fill in>
```

## Dependency conventions

Describe dependency policy.

```text
<fill in>
```

## Risky areas

List files, modules, or behaviors that require extra care.

```text
<area>: <reason>
<area>: <reason>
<area>: <reason>
```

## Performance-sensitive areas

```text
<area>: <reason and relevant benchmark, if known>
<area>: <reason and relevant benchmark, if known>
```

## Security-sensitive areas

```text
<area>: <reason>
<area>: <reason>
```

## Generated, vendored, or external files

List files that agents should avoid editing directly.

```text
<path>: <how it is generated or maintained>
<path>: <how it is generated or maintained>
```

## Release or deployment notes

```text
<fill in>
```

## Known pitfalls

```text
<pitfall>: <how to avoid it>
<pitfall>: <how to avoid it>
```

## Open questions

Track missing local context that should be filled in later.

```text
<question>
<question>
<question>
```
