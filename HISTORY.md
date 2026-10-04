# Development history

Boundry was not designed from the research literature. It grew out of practical work, and its ideas changed considerably along the way. This page records how they developed, so that readers can see where the current design came from.

The earlier documents named below were internal or limited-circulation working papers. They are superseded by the [preprint](paper/Boundry_preprint_v1.0.2.pdf), and some of their claims were stated more strongly than the current evidence supports. Researchers who would like to see them for historical interest can ask at verify@boundry.tech.

## Background

The problem predates AI. I have built software for regulated accounting work since 2005, including one of the early cloud accounting products. The recurring difficulty was the same each time: every figure must be traceable and defensible, and the decision logic that produces it tends to end up scattered through code that only its author understands. When AI arrived in that work, the difficulty became sharper. A model is a capable but unpredictable author, and "the AI did it" is not an answer a regulator will accept.

## Stages

| When | Stage | What changed |
|---|---|---|
| Jan 2026 | First provisional patent application | An AI governance architecture in which a central orchestrator is the only route by which agents act, and agents cannot bypass it. Governance is still AI-mediated at this stage; determinism comes next. |
| May 2026 | **Determinism first** (internal whitepaper; second provisional) | The new thesis: determinism is the precondition for compliance. A model acts as a compiler of intent at design time, and a deterministic runtime does the work. Developed against accounting workloads. |
| May 2026 | **"Boundry OS": a deterministic spine** (whitepaper v1.0.1) | The name appears, and so does a discipline that has stayed since: each claim labelled with its status, and an explicit "what is not claimed" section. |
| May 2026 | **From accounting to a general substrate** (whitepaper v2.0) | The design stops being accounting-specific and becomes a domain-neutral verification substrate: intent, then contract, then execution, with signed records and independent replay. |
| May 2026 | **The declared language** (BCL working draft) | The small declared language in which every request is expressed first appears, framed initially for safety-critical and supervisory control. |
| Jun–Sep 2026 | **Refusal-driven build** | The kernel is built by AI agents working under the substrate's own checks; refused proposals drive the design. See [Essay 02](essays/02-refusal-driven-development.md). |
| Sep 2026 | **Kernel V1 and clean-room reproduction** | The governing core is completed and rebuilt byte for byte on a second machine from sealed bundles. Explanations shift deliberately to "tamper-evident, not tamper-proof". |
| Sep 2026 | **Independent verifier published** | [Boundry Verify](https://github.com/Boundryos/boundry-verify) and its evaluation kit go public at [verify.boundry.tech](https://verify.boundry.tech). |
| Sep–Oct 2026 | **Record layer in production** | Sealing runs on real records in a bookkeeping application and, from October, in a financial reconciliation application, which checks daily that its records match the chain. |
| Oct 2026 | **Preprint v1.0 (revised to v1.0.2)** | The work is set out for researchers, with a threat model, evaluation and deployment stages. Related work is reviewed for the first time, and the design turns out to converge with several active research directions. |

## What carried through, and what changed

- **Carried through:** the separation of authoring from execution; determinism as the foundation; refusal as an outcome rather than an error; labelling every claim with its status.
- **Changed:** the scope (from one domain to any untrusted author of actions); the emphasis (from correctness of outputs to evidence that anyone can check independently); and the language of assurance (from "guarantees" to tamper-evidence, stated scope and stated stages).
