# Requirements

This file is the explicit capability and coverage contract for the project.

Use it to track what is actively in scope, what has been validated by completed work, what is intentionally deferred, and what is explicitly out of scope.

Guidelines:
- Keep requirements capability-oriented, not a giant feature wishlist.
- Requirements should be atomic, testable, and stated in plain language.
- Every **Active** requirement should be mapped to a slice, deferred, blocked with reason, or moved out of scope.
- Each requirement should have one accountable primary owner and may have supporting slices.
- Research may suggest requirements, but research does not silently make them binding.
- Validation means the requirement was actually proven by completed work and verification, not just discussed.

## Active

### R001 — Complete Crawleo Endpoint Coverage
- Class: core-capability
- Status: active
- Description: The skill must include every Crawleo-documented endpoint/tool found in Crawleo docs: `/search`, `/google-search`, `/google-maps`, `/crawl`, `/headful-browser`, plus the documented MCP tool mapping names `search_web`, `google_search`, `google_maps`, `crawl_web`, and `headful_browser`.
- Why it matters: The user explicitly asked for full Crawleo coverage and no skipped endpoints; incomplete coverage would make the skill unreliable for OpenClaw users.
- Source: user + research
- Primary owning slice: M001/S01
- Supporting slices: M001/S03, M001/S04, M001/S06
- Validation: mapped
- Notes: Crawleo endpoint-specific docs are authoritative where the OpenAPI snapshot is narrower.

### R002 — OpenClaw-Compatible Crawleo Skill Package
- Class: launchability
- Status: active
- Description: The repository must contain a self-contained OpenClaw skill package with clear skill instructions, implementation files, examples, tests, and documentation.
- Why it matters: OpenClaw users need a ready-to-use package rather than a loose outline or research note.
- Source: user
- Primary owning slice: M001/S02
- Supporting slices: M001/S04, M001/S06
- Validation: mapped
- Notes: Exact OpenClaw loader conventions are not present in the repo; the package must be practical, explicit, and self-contained.

### R003 — Crawleo Authentication Setup
- Class: integration
- Status: active
- Description: The skill must document and implement Crawleo API key authentication using `CRAWLEO_API_KEY`, sending requests with Crawleo's documented `x-api-key` header by default and noting `Authorization: Bearer` support.
- Why it matters: Crawleo endpoints require authentication and the skill must avoid exposing secrets.
- Source: research
- Primary owning slice: M001/S03
- Supporting slices: M001/S04, M001/S05
- Validation: mapped
- Notes: API keys must never be logged or echoed.

### R004 — Endpoint Parameter and Response Documentation
- Class: core-capability
- Status: active
- Description: Each Crawleo capability must document name, description, required parameters, optional parameters, parameter types, defaults, limits, enums, validation rules where documented, example usage, and expected response shape.
- Why it matters: OpenClaw and its users need enough information to choose and call the right Crawleo capability correctly.
- Source: user + research
- Primary owning slice: M001/S01
- Supporting slices: M001/S04
- Validation: mapped
- Notes: Missing or ambiguous fields must be marked “not specified in Crawleo docs.”

### R005 — Crawleo REST Execution Wrappers
- Class: core-capability
- Status: active
- Description: The skill must provide working wrappers/helpers for Crawleo REST endpoints that construct requests, validate documented parameters, and return usable results.
- Why it matters: The deliverable must be production-ready code, not only documentation.
- Source: user
- Primary owning slice: M001/S03
- Supporting slices: M001/S05, M001/S06
- Validation: mapped
- Notes: REST is the primary integration path; Crawleo MCP setup is documented as optional companion context.

### R006 — Actionable Error Handling
- Class: failure-visibility
- Status: active
- Description: The implementation must provide clear errors for missing API key, invalid parameters, Crawleo API errors, insufficient credits, rate limits, concurrent request limits, and Crawleo service errors.
- Why it matters: Agents need actionable failures to recover or explain the next step instead of surfacing raw HTTP noise.
- Source: user + research
- Primary owning slice: M001/S03
- Supporting slices: M001/S05
- Validation: mapped
- Notes: Normalize Crawleo error objects and include HTTP status/code/message where available without exposing secrets.

### R007 — Offline Tests and Examples for Every Endpoint
- Class: quality-attribute
- Status: active
- Description: The package must include default offline tests/examples covering every Crawleo endpoint, parameter validation, URL/query construction, missing API key behavior, and error normalization fixtures.
- Why it matters: Verification should not require spending Crawleo credits or a live API key by default.
- Source: user
- Primary owning slice: M001/S05
- Supporting slices: M001/S06
- Validation: mapped
- Notes: Offline tests are the default verification path.

### R008 — Optional Live Tests Gated by API Key
- Class: operability
- Status: active
- Description: The package must include optional live test examples that run only when explicitly enabled and `CRAWLEO_API_KEY` is present.
- Why it matters: Live verification is useful but should not accidentally consume Crawleo credits.
- Source: user
- Primary owning slice: M001/S05
- Supporting slices: M001/S06
- Validation: mapped
- Notes: Live tests should use minimal-cost examples and clearly warn about credit usage.

### R009 — README, Setup, and Usage Examples
- Class: launchability
- Status: active
- Description: The package must include a README explaining what the skill does, installation/setup instructions, authentication setup, endpoint usage examples, and optional Crawleo MCP configuration notes.
- Why it matters: A future user or agent must be able to install and use the skill without this planning conversation.
- Source: user
- Primary owning slice: M001/S04
- Supporting slices: M001/S06
- Validation: mapped
- Notes: Use only Crawleo branding.

### R010 — Endpoint Coverage Checklist
- Class: failure-visibility
- Status: active
- Description: The deliverable must include a checklist confirming every Crawleo-documented endpoint/tool was included and identifying the source docs used for each.
- Why it matters: The user's strongest requirement is not skipping endpoints; a checklist provides auditable proof.
- Source: user
- Primary owning slice: M001/S04
- Supporting slices: M001/S05, M001/S06
- Validation: mapped
- Notes: Checklist must cover REST endpoint names and corresponding MCP tool names.

## Validated

None yet.

## Deferred

### R011 — Exact OpenClaw Runtime Loader Conformance
- Class: integration
- Status: deferred
- Description: Validate the package against an official OpenClaw runtime/loader specification if one becomes available.
- Why it matters: The current repo does not provide an OpenClaw loader contract, so strict conformance cannot be proven during initial planning.
- Source: inferred
- Primary owning slice: none
- Supporting slices: none
- Validation: unmapped
- Notes: The first milestone will still produce a practical self-contained OpenClaw skill package.

### R012 — First-Class Crawleo MCP Execution Path
- Class: integration
- Status: deferred
- Description: Make Crawleo's remote MCP endpoint a first-class execution path in addition to REST wrappers.
- Why it matters: Crawleo supports MCP, but the confirmed architecture is REST primary with MCP setup documented as a companion.
- Source: user decision
- Primary owning slice: none
- Supporting slices: none
- Validation: unmapped
- Notes: Optional MCP setup should still be documented in M001.

## Out of Scope

### R013 — Non-Crawleo Brand References
- Class: anti-feature
- Status: out-of-scope
- Description: The deliverable must not mention or reference non-Crawleo competitor brands or clone-source terminology.
- Why it matters: The user explicitly required Crawleo-only branding and no competitor references.
- Source: user
- Primary owning slice: none
- Supporting slices: none
- Validation: n/a
- Notes: Final verification must scan deliverables for prohibited terminology.

### R014 — Undocumented Crawleo Endpoints or Parameters
- Class: anti-feature
- Status: out-of-scope
- Description: The skill must not invent Crawleo endpoints, parameters, defaults, limits, or response fields that are not documented.
- Why it matters: Invented behavior would mislead OpenClaw and users.
- Source: user
- Primary owning slice: none
- Supporting slices: none
- Validation: n/a
- Notes: Ambiguity must be labeled “not specified in Crawleo docs.”

### R015 — Live Crawleo Calls During Default Test Run
- Class: constraint
- Status: out-of-scope
- Description: Default tests must not call live Crawleo endpoints or consume credits.
- Why it matters: Verification should be safe by default and not depend on quota, network, or secrets.
- Source: user
- Primary owning slice: none
- Supporting slices: none
- Validation: n/a
- Notes: Optional live tests are allowed when explicitly enabled.

## Traceability

| ID | Class | Status | Primary owner | Supporting | Proof |
|---|---|---|---|---|---|
| R001 | core-capability | active | M001/S01 | M001/S03, M001/S04, M001/S06 | mapped |
| R002 | launchability | active | M001/S02 | M001/S04, M001/S06 | mapped |
| R003 | integration | active | M001/S03 | M001/S04, M001/S05 | mapped |
| R004 | core-capability | active | M001/S01 | M001/S04 | mapped |
| R005 | core-capability | active | M001/S03 | M001/S05, M001/S06 | mapped |
| R006 | failure-visibility | active | M001/S03 | M001/S05 | mapped |
| R007 | quality-attribute | active | M001/S05 | M001/S06 | mapped |
| R008 | operability | active | M001/S05 | M001/S06 | mapped |
| R009 | launchability | active | M001/S04 | M001/S06 | mapped |
| R010 | failure-visibility | active | M001/S04 | M001/S05, M001/S06 | mapped |
| R011 | integration | deferred | none | none | unmapped |
| R012 | integration | deferred | none | none | unmapped |
| R013 | anti-feature | out-of-scope | none | none | n/a |
| R014 | anti-feature | out-of-scope | none | none | n/a |
| R015 | constraint | out-of-scope | none | none | n/a |

## Coverage Summary

- Active requirements: 10
- Mapped to slices: 10
- Validated: 0
- Unmapped active requirements: 0
