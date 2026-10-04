# Design boundaries and next stages

Being precise about scope is part of the claim. This page separates what the design deliberately leaves to other layers from what is simply further along the rollout.

## Design boundaries

- **It does not make a model smarter or safer in itself.** It governs how a model's proposals are acted on and recorded.
- **It does not judge whether rules are good.** It applies the rules it is given and makes them attributable. A bad rule remains a bad rule.
- **It does not check that inputs are true.** It checks that the declared process was followed.
- **It governs only what passes through it.** Protection is only as complete as the rule that Boundry is the sole path to an action.
- **Permitted is not the same as intended.** If a model misunderstands a request but proposes something the rules allow, it is admitted. Consequential actions should include human confirmation.
- **It is tamper-evident, not tamper-proof.** An edit is not prevented. It cannot pass unnoticed at the next check.
- **It is bounded by design.** Requests are finite, loop-free plans over registered operations, which keeps every request checkable before it runs. New capability is added by registering operations.
- **It complements information-flow control and trajectory analysis.** Each proposal is judged against declared rules; value-level provenance tracking and multi-step analysis, as in some research systems, can sit alongside it.

## Deployment stages and next steps

| Capability | Stage | Next step |
|---|---|---|
| Signed, hash-chained record layer | In production | Report volume and reconciliation statistics |
| Admission, refusal, execution from sealed bytes | Demonstrated | Production deployment in a first selected product |
| Independent time-stamping of checkpoints (RFC 3161) | Built | Enable on production checkpoints, so the absence of rewriting is independently checkable rather than resting on the single operator key |
| Gating by recorded authority | Specified | Implement and add to the public kit (today's kit shows the refusal side) |
| Per-request overhead | Planned | Measure in realistic agent workloads |
| Adversarial and independent evaluation | Planned | Prompt-injection benchmark; invite external red-teaming |
| Cross-organisation operation | Planned | After single-organisation deployments mature |
| Formal proofs of core properties | Planned | Mechanise key invariants |

## Document provenance

Documents may be transformed in transit, for example by email gateways or social-media re-encoding. Boundry's binding is byte-exact by default, so a re-encoded copy returns "cannot be confirmed", never "false". Canonicalisation handles some structural rewrites, but not lossy re-encoding.
