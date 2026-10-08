---
generated: '2026-10-07'
method: generated
name: octen-ai-broad-search-research
description: "Decompose one question into concurrent sub-queries with Broad Search, then read the top sources in full with Extract."
api: openapi/octen-ai-openapi.yml
operations: [broad-search, extract]
source: >-
  Grounded in openapi/octen-ai-openapi.yml operationIds and the docs pages docs.octen.ai/resources/rate-limits, error-codes, overview/pricing; provider-published skills saved verbatim under skills/_provider/.
---

# Research a question from multiple angles

Decompose one question into concurrent sub-queries with Broad Search, then read the top sources in full with Extract.

## Steps
1. Call `broad-search` (POST /broad-search) with `query` and `max_queries` (1-30, default 5). Results come back grouped per generated sub-query.
2. Pick the URLs worth reading in full and call `extract` (POST /extract) with 1-20 `urls`; pass `query` to get `highlights` instead of `full_content`.
3. Failed URLs in an Extract response carry `status: "failed"` and `error_message` and are not billed; the request itself still returns 200.

## Rules
- Auth: `x-api-key: <key>` or `Authorization: Bearer <key>`; a payment method is required (authentication/octen-ai-authentication.yml).
- Rate limits: Broad Search shares the tier QPS with Web/News/Business Search (Free 10, Base 20, Builder 50, Pro 200, Max 500); Extract is 2,000/500/200 URLs per minute by mode. A 429 carries `msg` (rate-limits/octen-ai-rate-limits.yml).
- Every call is billed; there is no idempotency key, so do not retry blindly (conventions/octen-ai-conventions.yml).
- Errors use `{code, msg, request_id}`; quote `request_id` to support@octen.ai (errors/octen-ai-problem-types.yml).
