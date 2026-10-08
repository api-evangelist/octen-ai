---
generated: '2026-10-07'
method: generated
name: octen-ai-web-search-with-content
description: "Run a focused Web Search with filters and pull full content or highlights for the ranked pages."
api: openapi/octen-ai-openapi.yml
operations: [search, news-search]
source: >-
  Grounded in openapi/octen-ai-openapi.yml operationIds and the docs pages docs.octen.ai/resources/rate-limits, error-codes, overview/pricing; provider-published skills saved verbatim under skills/_provider/.
---

# Search the web and read the results

Run a focused Web Search with filters and pull full content or highlights for the ranked pages.

## Steps
1. Call `search` (POST /search) with `query`; narrow with `include_domains` / `exclude_domains`, `include_text` / `exclude_text`, `time_range` or `start_time` / `end_time`, and `language`.
2. Ask for `highlight` snippets for cheap context, or `full_content` when the agent must read the page. The first 10 results' full content is free; beyond that full content is billed per 1k results.
3. Use `news-search` (POST /news-search) instead when the question is about current events.

## Rules
- Auth and billing as in authentication/octen-ai-authentication.yml; `count` is 1-100 per call.
- Search QPS is per account by tier and shared across Broad/Web/News/Business Search; optional per-key caps apply, the lower wins.
- No pagination: one call returns one ranked page of `count` results.
