# Decisions Register

<!-- Append-only. Never edit or remove existing rows.
     To reverse a decision, add a new row that supersedes it.
     Read this file at the start of any planning or research phase. -->

| # | When | Scope | Decision | Choice | Rationale | Revisable? | Made By |
|---|------|-------|----------|--------|-----------|------------|---------|
| D001 | M001 planning | architecture | OpenClaw skill package shape | Build a self-contained Crawleo OpenClaw skill package in this repo. | The repo has no existing OpenClaw loader files or manifest convention, and the user confirmed a self-contained package is the preferred delivery shape. | Yes | collaborative |
| D002 | M001 planning | architecture | Crawleo connection strategy | Use Crawleo REST endpoint wrappers as the primary execution path and document Crawleo MCP setup as optional companion context. | Endpoint-specific Crawleo docs provide concrete parameters, response shapes, costs, and errors that can be tested offline. The user chose REST primary, and the authenticated local Crawleo API MCP endpoint was not reliable during planning. | Yes | collaborative |
| D003 | M001 planning | documentation | Crawleo documentation precedence | Prefer Crawleo endpoint-specific docs over narrower OpenAPI when sources conflict, and mark unresolved ambiguity as “not specified in Crawleo docs.” | Crawleo endpoint pages and docs index list the full five-capability surface, while the retrieved OpenAPI snapshot was narrower. Endpoint-specific docs better satisfy the full coverage requirement. | Yes | agent |
