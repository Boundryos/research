# Claims and evidence

Every claim below is listed with its evidence and current status. "In production" means running on real records in live systems. "Proven in testing" means demonstrated on a test bench with synthetic data. "Built" means implemented and awaiting enablement. "Specified" means designed, with implementation under way.

| # | Claim | Evidence | Status |
|---|---|---|---|
| 1 | A sealed, signed, hash-chained record layer can run in ordinary business software | Runs in two Australian financial applications (bookkeeping and financial reconciliation). An automated daily check confirms that application records and the chain agree, and any mismatch blocks approvals until a person resolves it | **In production** |
| 2 | A proposal outside the declared set of operations is refused, with no model involved | Admission and typed refusal exercised end to end on the test bench; each refusal is a named, signed, recorded outcome tied to the stage that raised it. A refused run is in the public kit | **Proven in testing** |
| 3 | An admitted action is executed from exactly the bytes that were checked | Execution reads the sealed proposal; the record binds the proposal, the decision and the result | **Proven in testing** |
| 4 | Tampering is detected and named | Altering a single byte in a sealed record causes verification to refuse it, naming the altered record | **Proven in testing** |
| 5 | State can be rebuilt from the record alone | Full rebuild from the ledger compared identical to the original | **Proven in testing** |
| 6 | Verification does not depend on the producer's code | The kernel's own verifier and the separate offline verifier agree on 144 of 144 bundles. A further verifier written in Go from the specification agrees with the Python verifier on 148 of 148 vectors (internal, not published) | **Proven in testing** |
| 7 | The system is reproducible across machines | The software was rebuilt on a second, different machine from sealed bundles and matched the first byte for byte | **Proven in testing** |
| 8 | Anyone can check a record offline | Public verifier and sample records at verify.boundry.tech | **Public** |
| 9 | Checkpoints can be time-stamped by an independent authority (RFC 3161) | Mechanism built; scheduled for enablement on production checkpoints | **Built** |
| 10 | Rules can gate actions by recorded authority, with a verdict recorded before the effect | Specified. Today's public kit shows the refusal side; authority-based gating will be added | **Specified** |

## What "proven in testing" does and does not mean

These results come from a controlled bench with synthetic data. They show that the mechanisms work as designed. They are not formal proofs. Independent evaluation and adversarial red-teaming are the next steps, and we welcome researchers who want to take them on.
