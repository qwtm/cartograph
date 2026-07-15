---
'cartograph': minor
---

IndexedDB data model (US-0016, #99): explicit `createObjectStore`
declarations and repository operations (`tx.objectStore(X).put(…)`, bound
store handles, `.index(…)` chains) become cited `DataEntity` nodes with
symbol-attributed READS/WRITES relations. Store identities resolve through
string literals or repo-wide const-string maps; runtime-computed identities
stay explicit Gaps.
