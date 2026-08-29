# ADR 0001 — Explicit Agent Boundaries

## Status
Accepted

## Context

Generative AI systems can become difficult to test and secure when the model directly controls every capability.

## Decision

The copilot will use explicit tool boundaries. The model chooses among constrained capabilities; each capability validates inputs and returns structured results.

## Consequences

Positive: easier testing, auditing, smaller blast radius, clearer interview story.

Negative: more interface design and less flexibility than unconstrained tool execution.

## Evidence needed later

- golden evaluation set
- tool rejection tests
- audit log examples
