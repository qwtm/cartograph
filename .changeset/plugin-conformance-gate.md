---
'cartograph': minor
---

Conformance gate for WASM adapter plugins (#200): a durable `plugin-gate` job
proves the SPI contract under the standard bounds, the plugin's own golden
corpus (expected facts pinned with the host identity), and double-run
determinism. The verdict persists per (plugin id, content hash) — replaced
bytes are ungated again — and Settings shows a per-artifact gate chip with the
failing check named, plus a run-gate action. A failed or ungated plugin stays
proposed and never joins extraction.
