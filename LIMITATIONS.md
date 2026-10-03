# Limitations

Stating the limits is part of the claim.

## What Boundry does not do

- **It does not make a model smarter or safer in itself.** It governs how a model's proposals are acted on and recorded.
- **It does not judge whether rules are good.** It applies the rules it is given and makes them attributable. A bad rule remains a bad rule.
- **It does not check that inputs are true.** It checks that the declared process was followed.
- **It governs only what passes through it.** Protection is only as complete as the rule that Boundry is the sole path to an action.
- **It admits wrong-but-permitted proposals.** If a model misunderstands a request but proposes something the rules allow, it is admitted. Consequential actions should still have human confirmation.
- **It is tamper-evident, not tamper-proof.** An edit is not prevented. It cannot pass unnoticed at the next check.
- **It is not a general-purpose computer.** The request language is deliberately bounded: requests are finite, loop-free plans. This is a design choice, not a proved theorem.
- **It does not track the origin of every value through a computation** (information-flow control), as some research systems do.
- **It does not reason about multi-step trajectories.** It judges each proposal against declared rules.

## What is not yet established

- The full governing core in production use with real-world effects.
- Independent evaluation or adversarial red-teaming.
- Formal proofs of the properties described.
- Per-request latency at scale. It is expected to be small, but has not been measured.
- Operation across organisational boundaries.

## Document provenance

Documents may be transformed in transit, for example by email gateways or social-media re-encoding. Boundry's binding is byte-exact by default, so a re-encoded copy returns "cannot be confirmed", never "false". Canonicalisation handles some structural rewrites, but not lossy re-encoding.
