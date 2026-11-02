# Focused repair record — 03.06

reproduction: Baseline 78429f59. Support input 0 displays Not loaded.
expected: 0 -> 0; positive counts keep their value; null -> Not loaded.
patch: One display assignment plus the zero regression test. Other fields and files preserved.
evidence: Before: 5 pass, 1 fail. After: 15 tests pass; typecheck 0; preview and queue link checked.
limits: Synthetic local preview. No database, external service, or production deployment claim.
