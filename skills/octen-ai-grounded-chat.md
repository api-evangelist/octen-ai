---
generated: '2026-10-07'
method: generated
name: octen-ai-grounded-chat
description: "Call frontier models through Octen's OpenAI-compatible chat completions with live search grounding."
api: openapi/octen-ai-openapi.yml
operations: [chat-completions, messages]
source: >-
  Grounded in openapi/octen-ai-openapi.yml operationIds and the docs pages docs.octen.ai/resources/rate-limits, error-codes, overview/pricing; provider-published skills saved verbatim under skills/_provider/.
---

# Chat with built-in web search through the Model Gateway

Call frontier models through Octen's OpenAI-compatible chat completions with live search grounding.

## Steps
1. Call `chat-completions` (POST /v1/chat/completions) with an OpenAI-shaped body (`model` such as `openai/gpt-5.5` or `anthropic/claude-sonnet-4.6`, `messages`); the gateway adds live web search where the model supports it.
2. Anthropic-shaped clients call `messages` (POST /v1/messages) instead.
3. Model Gateway errors arrive in the native OpenAI or Anthropic format without `request_id` in the body; read the `x-request-id` response header.

## Rules
- Limits: 300 RPM and 2,000,000 TPM, counted per model (rate-limits/octen-ai-rate-limits.yml).
- Per-model token prices are on https://docs.octen.ai/overview/pricing (plans/octen-ai-plans-pricing.yml).
- No idempotency key: a retried completion is billed again.
