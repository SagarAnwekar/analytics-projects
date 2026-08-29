# Architecture Notes

## Design goal

Keep business analytics trustworthy by separating request handling, metric context, tool execution, and evidence generation.

## Boundaries

1. API — validates request shape and authentication context.
2. Orchestrator — selects deterministic steps and records state.
3. Metric context — resolves definitions such as revenue, margin, period, and business dimensions.
4. SQL boundary — limits schemas, validates generated SQL, and prevents unrestricted writes.
5. RAG boundary — retrieves glossary/policy content with source references.
6. MCP boundary — exposes governed external capabilities as explicit tools.
7. Evidence layer — captures query, rows/aggregates used, assumptions, and validation results.
8. Insight layer — turns evidence into an executive answer without silently inventing facts.

## Key trade-offs

### SQL + RAG instead of RAG alone
RAG is appropriate for definitions, policies, and contextual documents. Numeric answers should come from structured data and executable queries.

### Explicit validation layer
An LLM can produce syntactically valid but semantically wrong SQL. Validation gives the system a place to enforce read-only rules, approved tables, row limits, and known metric definitions.

## Future deployment shape

```text
Client -> API Gateway -> FastAPI
                     -> Agent Runtime
                     -> PostgreSQL
                     -> Vector Store
                     -> MCP Servers
                     -> Observability / Evaluation
```
