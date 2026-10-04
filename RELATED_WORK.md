# Related work

Boundry was developed independently, from practical need, and arrived at an architecture that overlaps with several active research directions. Read against the work below, it is best understood as **a working example of one layer that many of these frameworks call for**, not as a replacement for any of them. Each of these works has strengths Boundry lacks.

## Layered runtime guardrails

**Shamsujjoha, Lu, Zhao, Zhu (CSIRO Data61).** *Swiss Cheese Model for AI Safety: A Taxonomy and Reference Architecture for Multi-Layered Guardrails of Foundation Model Based Agents.* arXiv:2408.02205.
A taxonomy and reference architecture for layered runtime guardrails (ICSA 2025). In its terms, Boundry is a rule-based, fail-closed guardrail at the tool-execution and action stage, with a verifiable record of its own decisions.

## Enforcement outside the model

- **Debenedetti et al.** *Defeating Prompt Injections by Design* (CaMeL). arXiv:2503.18813.
  A custom interpreter enforces data-flow policies on a model-written program. CaMeL tracks the origin of values, which Boundry does not. Boundry adds a sealed record checked by an independent verifier.
- **Shi et al.** *Progent: Securing AI Agents with Privilege Control.* arXiv:2504.11703.
  Deterministic privilege policies for tool calls, among the closest designs. Boundry differs in executing from the checked bytes and in producing an independently verifiable record of each admission and refusal.
- **Wang, Poskitt, Sun.** *AgentSpec: Customizable Runtime Enforcement for Safe and Reliable LLM Agents.* ICSE 2026; arXiv:2503.18666.
  Trigger, check and enforce rules with low overhead. AgentSpec rules fire on matching triggers; Boundry refuses anything not declared.
- **Costa et al. (Microsoft).** *Securing AI Agents with Information-Flow Control* (FIDES). arXiv:2505.23643.
- **Beurer-Kellner et al.** *Design Patterns for Securing LLM Agents against Prompt Injections.* arXiv:2506.08837.

## AI control

- **Greenblatt, Shlegeris, Sachan, Roger (Redwood Research).** *AI Control: Improving Safety Despite Intentional Subversion.* ICML 2024; arXiv:2312.06942.
  Safety protocols that hold even against an adversarial model. Boundry is a trusted (model-free) permission and record layer of the kind such protocols can sit on. It is not itself a control protocol, and it has not been evaluated against an attack policy.

## Verifiable audit of agent actions

**Ghosh.** *Tracekit: Tamper-Evident Intent-Reasoning-Action Auditing for Autonomous Coding Agents.* arXiv:2609.35659.
Gates a coding agent's tool calls with a pre-execution policy and records intent, reasoning and action in a tamper-evident, externally anchorable ledger. The closest work on the evidence side. Boundry differs in model-free admission limited to declared operations, execution from the sealed bytes that were admitted, and verification by an implementation independent of the producer.

## Multi-agent risk

**Reid, O'Callaghan, Venini, Carroll, Caetano.** *Risks and Controls for Multi-Agent Systems: An Analytical Framework for Deployment of AI Agents across Organisational Boundaries.* Published by the Australian AI Safety Institute, Aug 2026; arXiv:2608.26626.
Analyses risks and controls for agents deployed across organisational boundaries. Boundry has been exercised only within one organisation.

## Rules as code

- **Merigoux, Chataing, Protzenko.** *Catala: A Programming Language for the Law.* ICFP 2021; arXiv:2103.03198.
- **Yadamsuren, Platt, Diaz.** *LLM-Assisted Formalization Enables Deterministic Detection of Statutory Inconsistency in the Internal Revenue Code.* arXiv:2511.11954.

Both treat human-declared legal rules as the deterministic authority. Catala computes from the rules. Boundry governs who may propose an action under them, and records each decision verifiably.

## Proof assistants (lineage)

The general pattern of a small trusted kernel checking untrusted proposals follows the LCF tradition (Milner, 1970s), as used in Lean and Coq. See [Essay 01](essays/01-a-proof-assistant-kernel-for-actions.md).

## Concurrent work on pre-action authorisation and attestation (2026)

- **Uchibeke.** *Before the Tool Call: Deterministic Pre-Action Authorization for Autonomous AI Agents* (Open Agent Passport). arXiv:2603.20953.
  Fails closed, signs every decision including denials, and reports a live adversarial testbed.
- **Salfeld-Nebgen.** *Governing Actions, Not Agents: Institutional Attestation as a Governance Model for Autonomous AI Systems.* arXiv:2606.26298.
  The agent holds no execution authority over designated actions. These run only on independently signed, intent-bound evidence under a deny-by-default policy.
- **He, Yu.** *Sovereign Assurance Boundary* (arXiv:2606.11632) and *Sovereign Execution Broker* (arXiv:2606.20520).
  Separates proposal, admission and execution for cloud mutations, with signed decision records. A prototype is evaluated on AWS and Kubernetes.
- **Qu, Xu, Wang, Zhai, Zhang, Song.** *Securing LLM Agents Need Intent-to-Execution Integrity.* arXiv:2605.16976.
  A position paper defining end-to-end integrity properties.

Boundry was developed independently of these works, and they share its central move: the agent proposes, and something deterministic outside it decides.

## Capability comparison

Cells are filled from the full text of each paper, read in October 2026.
- "--" means the capability is **not described in the reviewed material**, which is not the same as absent.
- Boundry's cells carry its stage labels: B = demonstrated on the bench, K = in the public kit, L = live use.
- Corrections are welcome at verify@boundry.tech.

| Capability | CaMeL | Progent | AgentSpec | FIDES | Tracekit | OAP | IA | SAB/SEB | Boundry |
|---|---|---|---|---|---|---|---|---|---|
| ***Architecture*** | | | | | | | | | |
| Enforcement outside the model | Y | Y | Y | Y | Y | Y | Y | Y | Y (B) |
| Fail-closed by default | P | Y | -- | N | N | Y | Y | Y | Y (B, K) |
| Bounded declared plan language | P | N | N | N | N | N | P | P | Y (B) |
| Executes the admitted representation | P | P | P | P | P | P | P | P | Y (B) |
| ***Evidence*** | | | | | | | | | |
| Signed refusal records | N | -- | -- | -- | N | Y | P | P | Y (K) |
| Tamper-evident decision log | -- | -- | -- | -- | Y | Y | P | P | Y (L) |
| Separately implemented offline verifier | N | N | N | N | P | N | P | N | Y (K) |
| Cross-platform determinism measured | -- | -- | -- | -- | -- | -- | -- | -- | Y (K) |
| Adversarial evaluation | Y | Y | P | Y | P | Y | N | P | N |
| Overhead measured | Y | -- | Y | Y | Y | Y | N | Y | P |
| ***Scope and maturity*** | | | | | | | | | |
| Information-flow tracking | Y | N | P | Y | N | N | P | N | N |
| Peer-reviewed | -- | N | Y | N | N | N | N | N | N |
| Public implementation artefact | Y | Y | Y | Y | Y | Y | Y | N | P |
| Live deployment reported | N | P | N | N | N | P | N | N | P (L) |

### Where each cell comes from

**Rows (same order as the table):** enforcement · fail-closed · plan language · executes checked · signed refusal · tamper-evident log · offline verifier · determinism · information flow · adversarial evaluation · overhead · peer review · code · deployment.

- **CaMeL** (2503.18813v2)
  - interpreter enforces policies at tool calls (§5.2–5.4)
  - only exposed tools are callable; default for un-policied tools not described
  - restricted Python, which is general-purpose (§5.4)
  - per-call checks (§5.2)
  - denial returned to the user (§5.2)
  - not described
  - none
  - not described
  - capabilities track provenance (§5.3)
  - AgentDojo (§6)
  - 2.7–2.8× tokens (§6.5)
  - no venue listed on arXiv
  - Apache-2.0
  - research prototype
- **Progent** (2504.11703v3)
  - "deterministically allows or blocks" (§2.2)
  - "calls that match no rule are blocked by default" (§2.2)
  - symbolic rules over tool calls (§4.1)
  - per call
  - not described
  - not described
  - none
  - not described
  - no taint tracking
  - AgentDojo ASR 39.9%→1.0%; ASB 70.3%→3.9% (§8)
  - not described
  - preprint
  - MIT
  - integration demos only
- **AgentSpec** (2503.18666v3)
  - intercepts execution stages (§1)
  - rules fire on matched triggers (§3.2); default not stated
  - trigger/predicate/enforce rules (Fig. 3)
  - per action
  - not described
  - not described
  - none
  - not described
  - untrusted-source predicate (Fig. 5)
  - safety benchmarks, not injection
  - ms-level (§5.5)
  - ICSE 2026
  - public repo, no licence file
  - none
- **FIDES** (2505.23643v2)
  - policy engine in the planner loop (§4)
  - default label requirement is permissive (§4)
  - per-step tool calls
  - per call
  - not described
  - not described
  - none
  - not described
  - confidentiality/integrity labels (§4)
  - AgentDojo (§1)
  - 2–3× tokens (appendix)
  - preprint
  - MIT
  - none
- **Tracekit** (2609.35659v1)
  - PreToolUse hook (§4.3)
  - fail-open unless configured (Alg. 1)
  - none
  - per call
  - hash-chained but unsigned denials
  - SHA-256 chain with anchors (§4.2)
  - browser re-hasher, same author (§4.5)
  - not described
  - none
  - 18/44 harmful calls blocked; tamper mutations (§5)
  - 23.9 ms median per hook (§5.2)
  - preprint
  - MIT
  - experimental runs
- **OAP** (2603.20953v1)
  - framework-layer interception (Table 1)
  - unknown capability gives DENY (§3)
  - policy packs over tool calls (§3)
  - per call
  - "signed denial + reason" (§3.2)
  - write-once SHA-256 log (Table 10)
  - spec claim only
  - not described
  - none
  - live testbed: 0/879 under a restrictive policy (§6.1)
  - 53 ms median
  - preprint
  - Apache-2.0 spec
  - live testbed, self-reported by the vendor
- **IA** (2606.26298v1)
  - agent "holds no execution authority" (abstract)
  - "The default posture is deny" (§3.1)
  - declared intent plus skill contracts (§3.5)
  - hub executes or issues a token (§3.1)
  - signed receipts; signing of denials not explicit (§3.4)
  - hash chain or Merkle tree, described (§3.4)
  - third-party re-verification described, not separately implemented (§3.4)
  - not described
  - provenance of signed evidence only
  - none
  - qualitative only (§5)
  - preprint
  - MIT
  - proof of concept
- **SAB/SEB** (2606.11632v1, 2606.20520v2)
  - broker alone holds mutation credentials
  - every check must pass; revocation outage leads to rejection (SEB Eq. 5)
  - typed per-call execution contract
  - request matched against the contract, not the contract executed (SEB §9.1)
  - signed DecisionRecord at the broker only (SEB §4.4)
  - signed rows in PostgreSQL, no chain described
  - in-system replay service only (SAB §4.5)
  - not described
  - provenance freshness predicate only
  - injected fault and attack suites (SEB Table 10)
  - 28–137 ms p50 (SEB)
  - preprints
  - code "will be released"
  - research prototype on a test cluster
- **Boundry:** see [Claims and evidence](CLAIMS_AND_EVIDENCE.md) and the preprint, §5–§6.
