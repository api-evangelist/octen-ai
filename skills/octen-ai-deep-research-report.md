---
generated: '2026-10-07'
method: generated
name: octen-ai-deep-research-report
description: "Launch an autonomous multi-step research run and read the multimodal report it returns."
api: openapi/octen-ai-openapi.yml
operations: [deep-research, answer]
source: >-
  Grounded in openapi/octen-ai-openapi.yml operationIds and the docs pages docs.octen.ai/resources/rate-limits, error-codes, overview/pricing; provider-published skills saved verbatim under skills/_provider/.
---

# Run a Deep Research job

Launch an autonomous multi-step research run and read the multimodal report it returns.

## Steps
1. Call `deep-research` (POST /v1/research) with the research question. Only a single concurrent Deep Research request is supported per account (rate-limits page), so serialise jobs.
2. The report can include text, images and videos (changelog, July 2026).
3. For a grounded conversational answer instead of a full report, call `answer` (POST /answer); it is also subject to the Model Gateway RPM/TPM limits.

## Rules
- Same `x-api-key` auth; Deep Research is a billed operation with no idempotency key.
- A 429 means the single-concurrency limit or tier QPS was hit; back off rather than looping.
