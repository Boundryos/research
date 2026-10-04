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
