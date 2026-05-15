# M001: Crawleo OpenClaw Skill

**Gathered:** 2026-05-13
**Status:** Ready for planning

## Project Description

Build a complete OpenClaw skill for Crawleo that connects OpenClaw to Crawleo's documented web intelligence features: Bing-powered web search, Google Search, Google Maps place search, URL crawling/content extraction, and Headful Browser crawling for protected or heavily dynamic sites.

The deliverable must use only Crawleo branding, include every Crawleo-documented endpoint/tool, and avoid invented undocumented fields. If Crawleo docs are ambiguous, the skill documentation must say “not specified in Crawleo docs.”

## Why This Milestone

The repo currently has no working OpenClaw skill package. This milestone creates the full Crawleo skill from the ground up so OpenClaw users and agents can use Crawleo for live search and crawling workflows with clear setup, safe authentication handling, endpoint coverage proof, and verification.

## User-Visible Outcome

### When this milestone is complete, the user can:

- Install or inspect a self-contained OpenClaw Crawleo skill package in this repo.
- Configure `CRAWLEO_API_KEY` and use Crawleo REST-backed helpers for every documented Crawleo capability.
- Read the README and endpoint coverage checklist to confirm all Crawleo-documented endpoints/tools are included.
- Run offline tests/examples without a Crawleo API key or credit usage.
- Optionally run live tests with `CRAWLEO_API_KEY` when explicitly enabled.

### Entry point / environment

- Entry point: OpenClaw skill package files, README examples, and local test/example commands.
- Environment: local development repository.
- Live dependencies involved: Crawleo REST API at `https://api.crawleo.dev`; optional Crawleo MCP endpoint at `https://api.crawleo.dev/mcp`; Crawleo docs as source of truth.

## Completion Class

- Contract complete means: every Crawleo-documented endpoint/tool has a documented contract, implementation wrapper, example, and test/fixture coverage.
- Integration complete means: the package wires Crawleo authentication, request construction, validation, and error normalization into a coherent OpenClaw-facing skill package.
- Operational complete means: missing secrets, invalid parameters, quota/rate/concurrency errors, and Crawleo API failures are visible and actionable; default tests do not require secrets or consume credits.

## Final Integrated Acceptance

To call this milestone complete, we must prove:

- The endpoint coverage checklist includes `/search`, `/google-search`, `/google-maps`, `/crawl`, `/headful-browser`, and MCP tool mappings `search_web`, `google_search`, `google_maps`, `crawl_web`, `headful_browser`.
- The skill package contains implementation, README, setup instructions, examples, tests, and coverage documentation.
- Offline verification passes for every endpoint wrapper, including parameter validation and error fixture behavior.
- No non-Crawleo brand references or undocumented Crawleo endpoints/parameters appear in deliverables.
- Live Crawleo behavior is not simulated as default proof; optional live tests must be explicitly gated by `CRAWLEO_API_KEY`.

## Architectural Decisions

### Self-Contained OpenClaw Skill Package

**Decision:** Build a self-contained OpenClaw Crawleo skill package in this repo rather than waiting for an external loader convention.

**Rationale:** The repo is greenfield and does not contain an existing OpenClaw manifest/runtime contract. A self-contained package with explicit README, implementation, examples, and tests is the most useful deliverable available from current evidence.

**Alternatives Considered:**
- Wait for an exact OpenClaw specification — not chosen because the user confirmed the self-contained package direction and wants production-ready files now.
- Produce docs only — not chosen because the user required working code, tests, and setup.

### REST Primary, MCP Documented as Companion

**Decision:** Implement Crawleo REST endpoint wrappers as the primary execution path and document Crawleo MCP setup as optional companion context.

**Rationale:** Crawleo endpoint-specific docs provide concrete parameters, response shapes, costs, and errors for REST endpoints. REST wrappers can be tested offline and optionally live-tested without depending on an authenticated remote MCP server during planning.

**Alternatives Considered:**
- MCP primary — not chosen because the deliverable is an OpenClaw skill package, and the locally configured authenticated Crawleo API MCP server rejected discovery during discussion.
- Both REST and MCP as first-class execution paths — deferred because it would duplicate scope; M001 must first establish complete REST-backed skill coverage.

### Endpoint-Specific Crawleo Docs Drive Coverage

**Decision:** Use Crawleo endpoint-specific docs, docs index, public docs MCP descriptor, and OpenAPI as evidence, preferring endpoint-specific docs where sources conflict.

**Rationale:** Crawleo's docs index and endpoint pages list five capabilities, while the OpenAPI snapshot retrieved during discussion listed fewer paths. Endpoint pages are more complete for the requested coverage.

**Alternatives Considered:**
- Use OpenAPI only — not chosen because it would omit documented Crawleo capabilities.

## Error Handling Strategy

The skill should fail fast when `CRAWLEO_API_KEY` is missing and must never print API key values. It should validate documented required parameters, enums, and limits before calling Crawleo. It should normalize Crawleo JSON error bodies into actionable errors with HTTP status, Crawleo error code where present, and a suggested next action.

`402` should be treated as insufficient credits where documented. `429` should be treated as rate limit, credits exhausted, or concurrent request limit depending on Crawleo's returned message. `500` should be treated as Crawleo-side/service failure. Headful Browser docs note failed requests cost 0 credits; documentation and errors should preserve that nuance.

Default examples and tests should avoid accidental credit usage. Use lower-cost Crawleo paths first, such as `/crawl` before `/headful-browser`, and keep costly parameters like `max_pages`, rendering, and screenshots explicit.

## Risks and Unknowns

- Exact OpenClaw skill loader convention is not present in the repo — package must be self-contained and explicit enough to be useful without assuming hidden runtime behavior.
- Crawleo docs sources are not perfectly aligned — endpoint-specific docs must drive coverage, and ambiguity must be marked instead of invented.
- Live tests consume Crawleo credits — default verification must be offline, with live tests opt-in only.
- The authenticated local Crawleo API MCP server rejected discovery during planning — M001 should not depend on that path for implementation proof.

## Existing Codebase / Prior Art

- Repository root — greenfield integration directory with no OpenClaw skill implementation yet.
- Crawleo docs index `https://docs.crawleo.dev/llms.txt` — lists available docs pages and OpenAPI spec.
- Crawleo public docs MCP descriptor `https://docs.crawleo.dev/mcp` — describes docs search/filesystem tools for Crawleo documentation.
- Crawleo API docs `https://docs.crawleo.dev/api-reference/endpoint/*` — endpoint-specific source of truth for parameters, examples, response shapes, costs, and errors.
- Crawleo OpenAPI `https://docs.crawleo.dev/openapi.json` — useful but narrower than endpoint-specific docs for complete coverage.

## Relevant Requirements

- R001 — M001 establishes complete Crawleo endpoint/tool coverage.
- R002 — M001 creates the OpenClaw skill package.
- R003 — M001 implements and documents Crawleo API key authentication.
- R004 — M001 documents endpoint parameters and responses.
- R005 — M001 implements Crawleo REST execution wrappers.
- R006 — M001 adds actionable error handling.
- R007 — M001 adds offline tests/examples for every endpoint.
- R008 — M001 adds optional live tests gated by API key.
- R009 — M001 adds README, setup, and usage examples.
- R010 — M001 adds endpoint coverage checklist.

## Scope

### In Scope

- Crawleo-only OpenClaw skill package.
- REST wrappers for `/search`, `/google-search`, `/google-maps`, `/crawl`, and `/headful-browser`.
- Documentation of corresponding Crawleo MCP tool names: `search_web`, `google_search`, `google_maps`, `crawl_web`, `headful_browser`.
- Authentication setup via `CRAWLEO_API_KEY`.
- Endpoint contract inventory with source links and ambiguity notes.
- README, installation/setup, usage examples, endpoint coverage checklist.
- Offline tests/examples and optional live tests gated by API key.
- Error handling for missing key, invalid parameters, Crawleo API errors, rate limits, quota, concurrent limits, and service failures.

### Out of Scope / Non-Goals

- Non-Crawleo brand references or clone-source terminology.
- Undocumented Crawleo endpoints, parameters, defaults, limits, or response fields.
- Default live API calls that consume Crawleo credits.
- First-class execution through Crawleo MCP endpoint beyond optional setup documentation.
- Proving strict conformance to an official OpenClaw runtime loader not present in the repo.

## Technical Constraints

- Use only Crawleo website/docs/OpenAPI as endpoint source of truth.
- Preserve exact Crawleo terminology for endpoints, parameters, response fields, costs, and documented limits.
- Mark ambiguous fields as “not specified in Crawleo docs.”
- Do not log secrets.
- Default tests must run without `CRAWLEO_API_KEY` and without network access.
- Optional live tests must be clearly gated and credit-aware.

## Integration Points

- Crawleo REST API — all primary endpoint wrappers call `https://api.crawleo.dev`.
- Crawleo authentication — API key via `CRAWLEO_API_KEY`, sent as `x-api-key` by default.
- Crawleo MCP endpoint — optional setup note for `https://api.crawleo.dev/mcp`.
- OpenClaw skill consumer — package must be organized and documented for OpenClaw use despite missing exact loader files in the current repo.

## Testing Requirements

Default tests should be offline and should validate each endpoint wrapper's parameter validation, query construction, authentication preflight, and error normalization. Fixtures should cover Crawleo error shapes for `400`, `401`, `402`, `403`, `429`, and `500` where documented. Optional live tests should require explicit enablement and `CRAWLEO_API_KEY`, should warn about credit usage, and should use minimal-cost examples.

## Acceptance Criteria

- S01 acceptance: endpoint contract inventory covers every Crawleo-documented endpoint/tool with source links, parameters, defaults/limits/enums where documented, examples, response shapes, and ambiguity notes.
- S02 acceptance: self-contained package scaffold exists with clear OpenClaw skill entry documentation, source layout, examples, tests, and README placeholders ready for wiring.
- S03 acceptance: REST wrappers construct validated requests for all five endpoints, handle `CRAWLEO_API_KEY`, and normalize Crawleo errors without logging secrets.
- S04 acceptance: README, setup instructions, usage examples, optional MCP setup notes, and endpoint coverage checklist are complete and Crawleo-only.
- S05 acceptance: offline tests pass for every endpoint and optional live test path is gated behind explicit opt-in plus `CRAWLEO_API_KEY`.
- S06 acceptance: final package verification passes, coverage checklist matches docs, no non-Crawleo references are present, and all deliverable files exist.

## Open Questions

- Exact OpenClaw loader/manifest convention — current thinking: use a self-contained package with practical manifest/instructions and executable helpers unless repo evidence appears during implementation.
- Crawleo docs conflicts — current thinking: prefer endpoint-specific docs over narrower OpenAPI and mark unresolved fields as “not specified in Crawleo docs.”
