# M001: Crawleo OpenClaw Skill

**Vision:** Build a complete OpenClaw skill package that connects OpenClaw to Crawleo's documented web intelligence capabilities: search, crawling/content extraction, Google Search, Google Maps, and Headful Browser. The package uses Crawleo branding only, covers every Crawleo-documented endpoint/tool, includes REST-backed helpers, setup docs, endpoint examples, error handling, and offline verification with optional live tests gated by CRAWLEO_API_KEY.

## Success Criteria

- Every Crawleo-documented REST endpoint is represented: /search, /google-search, /google-maps, /crawl, and /headful-browser.
- The corresponding Crawleo MCP tool names are documented: search_web, google_search, google_maps, crawl_web, and headful_browser.
- Every endpoint has documented parameters, types, defaults, limits/enums where documented, examples, expected response shape, and source links.
- The package contains working REST wrappers/helpers, README, setup instructions, examples, tests, and endpoint coverage checklist.
- Default verification runs offline without Crawleo API calls or credit usage; optional live tests are gated by explicit enablement and CRAWLEO_API_KEY.
- Deliverables use Crawleo branding only and do not invent undocumented endpoints or parameters.

## Slices

- [ ] **S01: Crawleo endpoint contract inventory** `risk:high` `depends:[]`
  > After this: A generated/curated endpoint contract file lists every Crawleo-documented REST endpoint and MCP tool with parameters, defaults, limits, examples, response shapes, source links, and ambiguity notes.

- [ ] **S02: OpenClaw skill package scaffold** `risk:high` `depends:[S01]`
  > After this: The repo has a self-contained Crawleo OpenClaw skill package structure with README skeleton, manifest/instructions, examples, tests, and package metadata ready for endpoint wiring.

- [ ] **S03: Crawleo REST client and endpoint wrappers** `risk:high` `depends:[S01,S02]`
  > After this: OpenClaw-facing helpers can construct validated Crawleo requests for all five endpoints and normalize Crawleo auth/API/rate/quota errors without exposing secrets.

- [ ] **S04: Skill documentation, examples, and coverage checklist** `risk:medium` `depends:[S03]`
  > After this: A user can read the README and coverage checklist to install the skill, configure CRAWLEO_API_KEY, understand every Crawleo capability, and copy examples for each endpoint.

- [ ] **S05: Offline and optional live verification suite** `risk:medium` `depends:[S03,S04]`
  > After this: Offline tests validate every endpoint wrapper, parameter rule, URL construction path, and error fixture; optional live tests are gated behind CRAWLEO_API_KEY.

- [ ] **S06: Final OpenClaw integration proof** `risk:medium` `depends:[S05]`
  > After this: The assembled skill is checked end-to-end as a package: all files exist, no non-Crawleo references appear, coverage matches Crawleo docs, and verification commands pass.

## Boundary Map

### S01 → S02

Produces:
- Crawleo endpoint contract inventory with endpoint/tool names, parameter schemas, examples, response shapes, source URLs, and ambiguity notes.

Consumes:
- Crawleo docs index, endpoint docs, public docs MCP descriptor, and OpenAPI evidence.

### S01 + S02 → S03

Produces:
- Stable package layout and contract data for all Crawleo capabilities.

Consumes:
- Endpoint names, parameter rules, auth requirements, documented costs, and response/error shapes.

### S03 → S04

Produces:
- Implemented REST wrappers, validation behavior, and error normalization semantics.

Consumes:
- Contract inventory and package scaffold.

### S03 + S04 → S05

Produces:
- User-facing examples, docs, and implementation surfaces that tests can exercise.

Consumes:
- Endpoint wrappers and documented expected behavior.

### S05 → S06

Produces:
- Passing offline test suite and optional live test path.

Consumes:
- Full package artifacts, docs, tests, and coverage checklist for integrated verification.
