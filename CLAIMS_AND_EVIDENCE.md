# Claims and evidence

Every claim below is listed with its evidence and current status. "In production" means running on real records in live systems. "Proven in testing" means demonstrated on a test bench with synthetic data. "Designed" means specified but not yet in operation.

| # | Claim | Evidence | Status |
|---|---|---|---|
| 1 | A sealed, signed, hash-chained record layer can run in ordinary business software | Runs in two Australian financial applications (bookkeeping and financial reconciliation). An automated daily check confirms that application records and the chain agree, and any mismatch blocks approvals until a person resolves it | **In production** |
| 2 | Every proposal is admitted or refused by declared rules, with no model involved | Admission and typed refusal exercised end to end on the test bench; each refusal is a named, recorded outcome tied to the stage that raised it | **Proven in testing** |
| 3 | An admitted action is executed from exactly the bytes that were checked | Execution reads the sealed proposal; the record binds the proposal, the decision and the result | **Proven in testing** |
| 4 | Tampering is detected and named | Altering a single byte in a sealed record causes verification to refuse it, naming the altered record | **Proven in testing** |
| 5 | State can be rebuilt from the record alone | Full rebuild from the ledger compared identical to the original | **Proven in testing** |
| 6 | Verification does not depend on the producer's code | Two independent implementations, the kernel's own verifier and a separate offline verifier, agree at shared test vectors | **Proven in testing** |
| 7 | The system is reproducible across machines | The software was rebuilt on a second, different machine from sealed bundles and matched the first byte for byte | **Proven in testing** |
| 8 | Anyone can check a record offline | Public verifier and sample records at verify.boundry.tech | **Public** |
| 9 | Checkpoints can be time-stamped by an independent authority (RFC 3161) | Mechanism built; daily time-stamping of production checkpoints scheduled | **Scheduled (Oct 2026)** |
| 10 | Rules can gate actions by recorded authority and a verdict recorded before the effect | Specified | **Designed** |

## What "proven in testing" does and does not mean

These results come from a controlled bench with synthetic data. They show that the mechanisms work as designed. They are not formal proofs, and the system has not yet been evaluated by an independent party or red-teamed by an adversarial team. Independent evaluation is a stated next step.
