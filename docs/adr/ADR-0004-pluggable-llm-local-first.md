# ADR-0004 — Pluggable LLM, local-first, per-tier cloud opt-in

- **Status:** Accepted
- **Date:** 2026-06-21
- **Deciders:** Chris Kane

## Context
Semantic (T2) and agentic (T3) tiers need models, but the app is local-first and
privacy-sensitive. Provider choice must be swappable.

## Decision
A `LlmProvider` trait abstracts all model access (`locality` = Local | Cloud).
**Ollama is the default** for embeddings and agent completions. Cloud providers
(Claude/Grok/GPT/Gemini) are **opt-in per tier and per action**, gated by an egress
consent dialog that shows the exact span-level payload. A Local-only policy makes
cloud calls **hard-fail closed** (no silent egress). Secrets are redacted from payloads.

Completion requests are constructed only inside the `llm` egress firewall. It
redacts the structured system/prompt/span payload first, hashes that exact
provider+tier+action payload, and accepts a cloud call only when a one-action
consent grant matches the hash. A changed outbound payload requires new consent.

The `agents` broker accepts only explicit Gap slots, bounded evidence spans, and
a closed existing-node candidate set. It returns data-only Agentic/InferredWeak
proposals with citations from both sides and has no graph-store dependency.
Human accept/reject decisions live in a SQLite/WAL decision log keyed by proposal
content hash and the task's evidence/candidate basis hash; unchanged bases reapply
after re-ingest, while changed evidence returns to undecided.

## Consequences
- Privacy by default; provider independence; clean test seams.
- Local model quality bounds T2/T3 unless the user opts into cloud.
- Consent cannot be replayed for a different provider, tier, action, or outbound payload.
- T3 curation survives graph replacement without giving the agent a confirmed-fact write path.

## Alternatives (≤3)
- **Cloud-default** — better quality, unacceptable default egress.
- **Single hard-wired local model** — simpler, no provider independence.
