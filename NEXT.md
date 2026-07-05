# NEXT

**Single next action:** Get test evidence for the PowerShell encoded-command rule — find one specific public sample (OTRF Security-Datasets or EVTX-ATTACK-SAMPLES) that contains an `-EncodedCommand` execution, run the rule logic against it, and save the matching event(s) into `detections/powershell-encoded-command/test-evidence/`.

Detection in flight: `detections/powershell-encoded-command/` — `rule.kql` done. Still needed for Definition of Done: test evidence (next), `rule.sigma.yml`, ATT&CK coverage notes, FP analysis, `README.md`.
