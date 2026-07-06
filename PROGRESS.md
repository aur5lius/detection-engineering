# PROGRESS

- 2026-07-05 — Session 1: started first detection (PowerShell encoded-command, T1059.001). Wrote `rule.kql` with inline reasoning, the switch-prefix dead end, and the Base64-length discriminator. 5 of 6 DoD items remain.
- 2026-07-06 — Session 2: rebuilt the detection logic blind from the technique; rediscovered the -e prefix quirk by testing and independently arrived at the same Base64-shape regex. Lowered threshold {20,}→{15,} with measured justification (whoami blob = 16 chars, policy words ≤ 12).
