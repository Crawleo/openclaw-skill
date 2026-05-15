# Project

## What This Is

This project is a self-contained OpenClaw skill package for Crawleo. It connects OpenClaw to Crawleo's documented web intelligence capabilities: Bing-powered web search, Google Search, Google Maps place search, URL crawling/content extraction, and Headful Browser crawling for protected or heavily dynamic sites.

## Core Value

OpenClaw can use Crawleo's full documented search and crawling surface through a clear, Crawleo-branded skill with complete endpoint coverage, actionable errors, and examples/tests for every capability.

## Project Shape

- **Complexity:** complex
- **Why:** The work is greenfield but must preserve complete endpoint coverage, reconcile Crawleo docs/OpenAPI ambiguity, handle authentication and quota failures safely, and produce a package useful to agents rather than only static documentation.

## Current State

The repository started essentially empty aside from GSD scaffolding. No OpenClaw skill files, implementation code, tests, or README exist yet. Crawleo docs research confirmed the relevant REST endpoints and MCP tool names, but implementation still needs to be created.

## Architecture / Key Patterns

The skill will be a self-contained package in this repo. The primary integration path is Crawleo REST API calls to `https://api.crawleo.dev`, authenticated with `CRAWLEO_API_KEY` using Crawleo's documented `x-api-key` header by default. Crawleo's remote MCP endpoint at `https://api.crawleo.dev/mcp` is documented as an optional companion configuration, not the primary execution path for this package.

Endpoint definitions are grounded in Crawleo endpoint-specific docs, the Crawleo docs index, the public docs MCP descriptor, and OpenAPI where it agrees. Where Crawleo docs are ambiguous or inconsistent, fields must say “not specified in Crawleo docs” instead of inventing behavior.

## Capability Contract

See `.gsd/REQUIREMENTS.md` for the explicit capability contract, requirement status, and coverage mapping.

## Milestone Sequence

- [ ] M001: Crawleo OpenClaw Skill — Build a production-ready OpenClaw skill package covering all Crawleo-documented search and crawling capabilities with docs, examples, error handling, and verification.
