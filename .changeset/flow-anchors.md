---
'cartograph': minor
---

Flow Inspector now traces real targets beyond web apps: extension contexts (popup, background, content scripts) and manifest keyboard commands anchor their own flows, walking from the manifest entry into the entry file's symbols and across message channels. When zero flows trace, the Inspector names every anchor kind recovery looked for and what it found instead of a generic hint.
