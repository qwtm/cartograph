---
'cartograph': minor
---

Kotlin joins the deterministic tier (#212): a new compiled-in
`adapters-lang-kotlin` crate recovers Confirmed T0 facts from `.kt`/`.kts`
sources — classes, interfaces, objects, data classes, enums, and functions
(top-level, member, and extension) with exact evidence spans; import-proven
cross-file calls (type/object receivers and imported top-level functions)
joined repo-wide with declared-package misses failing closed to explicit
Gaps; and Spring Web endpoints proven per annotation package with
class+method path composition. Preflight and Settings now report Kotlin as
installed (`t0.adapter-kotlin`) instead of a requestable planned adapter,
the ingest summary reports a Kotlin layer row, and live recovery progress
narrates Kotlin file reads. Ktor routing is a follow-on.
