# 04 · Small, portable and offline: where governed execution could go

*Ben Mueller · October 2026 · discussion essay (draft)*

[Essay 03](03-execution-governance-beyond-ai.md) asked whether governed execution applies to computation generally. This essay follows its physical properties. It is small and deterministic. Its record verifies without a network. And the model, when there is one, is needed only to *propose*, never to *execute*.

Each direction below carries one of three labels:

- **Measured:** an element has been demonstrated, as reported in the [preprint](../paper/Boundry_preprint_v1.0.2.pdf) or the [claims table](../CLAIMS_AND_EVIDENCE.md).
- **Plausible:** follows from the design, but not yet tried.
- **Speculative:** promising, with significant open questions.

## 1. Small enough to trust · Approximate

There is a long engineering tradition behind keeping the trusted part small. Saltzer and Schroeder called it *economy of mechanism*. seL4 showed that an operating-system kernel of about 10,000 lines can be formally verified.[^sel4]

Boundry's approximate sizes:

| Component | Approximate size |
|---|---|
| Governing core | about 32,000 lines of code (about 1.7 MB) |
| Offline verifier package | about 0.35 MB, Python standard library only |

The governing core needs a standard Python runtime and its dependencies, so it is small software, not microcontroller firmware. It has not been formally verified to seL4's standard. That remains an aspiration, but the core is small enough for it to be a realistic one.

## 2. Moving work out of the model · Plausible, with supporting evidence

In Boundry, the model is needed only to *write* the proposal. Everything after that is deterministic, so a mistake by the model becomes a problem at proposal time rather than at run time.

The research literature already shows that planning once and then executing deterministically is cheaper and faster than asking a model to drive each step:

- Plan-then-execute approaches report up to 3.7× lower latency and 6.7× lower cost.[^llmcompiler]
- They also report about 5× fewer tokens.[^rewoo]
- Delegating computation from a model to an interpreter improves accuracy as well.[^pot]

Governed execution adds what those systems lack: an admission decision and a record anyone can verify.

There is a second saving. A sealed plan's identity is a fingerprint of its inputs, the same way build systems such as Bazel and Nix identify a computation.[^bazel] So identical plans can be compared, replayed or reused, and checking a result means comparing fingerprints, not running the work again.

To be clear about the limits: governance itself adds some work. It does not make processors faster. The saving comes from doing less model inference, and from not repeating work that has already been verified.

## 3. Portable records and portable environments · Measured (parts), Plausible (whole)

Boundry is not an operating system, but two things about it travel:

- **The record travels.** A sealed record can be carried on removable media and verified anywhere, offline, without the system that produced it. This mirrors how signed software bundles can be checked on an air-gapped machine.[^sigstore] The difference is that Boundry verifies *decisions and executions*, not just artefacts.
- **The software travels.** The whole system was rebuilt on a second machine from sealed bundles and an offline package cache, with the network blocked, and matched the original byte for byte. This is the reproducible-builds discipline applied to the governing core.[^rb]

Together these suggest a governed environment on a stick: sealed software, its record and a verifier, carried on removable media, rebuilt and checked anywhere. Running governed execution from removable media has not yet been tried.

## 4. The record as the database; the cloud as replication · Speculative

A design principle from Boundry's development is that **the signed chain is the source of truth**, and conventional databases are caches that can be rebuilt from it. Rebuilding state from the record alone has been measured on the bench: the rebuilt state matched the original exactly.

If authority lives in a record that verifies on any machine, the cloud's role can shift from *being the authority* to *replicating verifiable records*. Git hosting has the same relationship to Git, and this is the aim of the local-first software movement.[^localfirst]

Hash-linked updates between parties that don't trust each other have recent precedent in Byzantine-tolerant CRDTs.[^bftcrdt] Boundry adds something those systems don't record: what was *refused*, and why.

Open questions:

- How records from several devices are merged and ordered, given that Boundry today serialises decisions through one kernel.
- How keys are held on each device.
- How conflicts between devices are resolved.

## 5. Robotics, transport and safety-critical settings · Plausible as a supervisory layer

Aviation and robotics already accept that you cannot certify the clever part, only the thing that bounds it. The *Simplex* architecture runs a complex, unverified controller beside a small, trusted safety controller that takes over at the boundary.[^simplex] The pattern is standardised for aircraft as run-time assurance (ASTM F3269).[^astm] *Shielding* applies the same idea to learned controllers.[^shield]

Governed execution is the same bargain applied to *discrete actions*, plus a receipt. It suggests two roles:

- **Supervisory admission of high-consequence commands.** A route change, a movement outside a declared working envelope or a dispatch is admitted or refused on the device, with no model and no network involved. The design goal, set out in earlier design work, is that an unsafe state is unreachable *by construction*, because no admissible plan leads to it.
- **A command recorder that anyone can check.** We already put recorders in aircraft and cars.[^edr] Those devices rely on physical tamper *resistance*. A signed, hash-chained record of what was commanded, admitted and refused offers tamper *evidence* that an independent party can verify.

**This is not real-time control.** Fast control loops stay where they are. Latency on embedded hardware, integration with certified safety systems (IEC 61508, ISO 26262, DO-178C) and qualification of tools are all open. Nothing has been tested on a robot or a vehicle.

## 6. Mobile, modest hardware and offline AI · Plausible

The governed runs in the public kit were executed on macOS and on Linux on 64-bit ARM, the processor family used in most phones and single-board computers. Two things follow:

- **Checking a record on a phone or a small device is a short step,** because verification needs only the record and a verifying key.
- **An on-device model can propose while a local kernel admits,** with no cloud in the decision. Governance then goes wherever the model goes, including places with poor or no connectivity.

Running the governing core on phones has not been tried.

## 7. Other directions

- **Reproducible research.** Agent experiments in which every step and every refusal is recorded, so another lab can re-check them.
- **Regulatory record-keeping.** The EU AI Act requires high-risk systems to keep automatic logs,[^aiact] and regulated pharmaceutical systems require audit trails that do not obscure earlier entries.[^part11] A record that a regulator can verify independently could go beyond both requirements.
- **Evidence that outlives the vendor.** Records stay verifiable after the system that made them, or the company behind it, is gone.
- **Governed device updates.** An update is admitted only if it matches a declared, sealed specification.

## What would test these

Cheapest first:

1. Run the verifier on a phone and on a single-board computer.
2. Carry a sealed environment on removable media to a clean machine, then rebuild and verify it there.
3. Measure per-request latency and memory for governed execution on 64-bit ARM.
4. Replace a model-driven multi-step task with a model-proposed, governed plan, and measure tokens, latency and cost.
5. Prototype synchronising verifiable records between several devices.

I would welcome collaborators on any of these.

---

[^sel4]: G. Klein et al., "seL4: Formal Verification of an OS Kernel," SOSP 2009. doi:10.1145/1629575.1629596
[^llmcompiler]: S. Kim et al., "An LLM Compiler for Parallel Function Calling," ICML 2024. arXiv:2312.04511
[^rewoo]: B. Xu et al., "ReWOO: Decoupling Reasoning from Observations for Efficient Augmented Language Models," 2023. arXiv:2305.18323
[^pot]: W. Chen et al., "Program of Thoughts Prompting," TMLR 2023. arXiv:2211.12588
[^bazel]: A. Mokhov, N. Mitchell, S. Peyton Jones, "Build Systems à la Carte," ICFP 2018; E. Dolstra et al., "Nix: A Safe and Policy-Free System for Software Deployment," LISA 2004.
[^sigstore]: Sigstore cosign, offline bundle verification. https://github.com/sigstore/cosign
[^rb]: C. Lamb and S. Zacchiroli, "Reproducible Builds," IEEE Software 39(2), 2022. doi:10.1109/MS.2021.3073045
[^localfirst]: M. Kleppmann et al., "Local-first software: you own your data, in spite of the cloud," Onward! 2019. doi:10.1145/3359591.3359737
[^bftcrdt]: M. Kleppmann, "Making CRDTs Byzantine Fault Tolerant," PaPoC 2022. doi:10.1145/3517209.3524042
[^simplex]: L. Sha, "Using Simplicity to Control Complexity," IEEE Software 18(4), 2001. doi:10.1109/MS.2001.936213
[^astm]: ASTM F3269-21, run-time assurance for aircraft systems containing complex functions.
[^shield]: M. Alshiekh et al., "Safe Reinforcement Learning via Shielding," AAAI 2018.
[^edr]: EUROCAE ED-112A (flight recorders); US 49 CFR Part 563 (vehicle event data recorders).
[^aiact]: Regulation (EU) 2024/1689 (AI Act), Article 12.
[^part11]: US 21 CFR Part 11, §11.10(e).
