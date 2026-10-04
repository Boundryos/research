# Boundry: research notes

**A small, deterministic kernel that admits or refuses AI-proposed actions, and leaves a record anyone can check.**

This repository collects the research notes, essays and evidence behind Boundry. It is written for researchers and practitioners working on AI safety, agent governance, verifiable computation and rules as code.

> **Status:** being rolled out in stages. The record layer is in live use; the full governing core is demonstrated end to end in testing. See [Claims and evidence](CLAIMS_AND_EVIDENCE.md) and [Design boundaries and next stages](LIMITATIONS.md).

---

## The idea in one paragraph

Most approaches to AI safety try to make the model behave. Boundry takes a different position: the harms we fear from AI agents are harms of **action** (records changed, money moved, systems operated), and the safety of an action does not have to live inside the model. In Boundry, an AI, a person or a program can only **propose** an action in a small declared language. A deterministic kernel, containing no model, **admits or refuses** each proposal against rules set by people. Anything not declared is refused, and the refusal is recorded with its reason. An admitted action is carried out from **exactly the same sealed bytes that were checked**, and every decision is sealed into a signed, hash-chained record that can be **verified offline by a separately implemented verifier** whose verification core imports no kernel code.

## A familiar shape

The architecture follows a pattern with a long history: **a small, trusted kernel that checks untrusted proposals.** Proof assistants such as Lean and Coq work this way, in the tradition of Robin Milner's LCF approach from the 1970s. Anyone, including an AI, may propose a proof; a small kernel accepts or rejects it. Boundry applies that pattern to **actions, records and rules** rather than proofs. See [A proof-assistant kernel for actions](essays/01-a-proof-assistant-kernel-for-actions.md).

## Try it yourself

A read-only, offline verifier and an evaluation kit are public at **https://verify.boundry.tech** (source: [Boundryos/boundry-verify](https://github.com/Boundryos/boundry-verify)). The verifier re-derives every fingerprint and re-checks every seal and chain link on your own machine. It cannot execute, sign or write.

## Contents

| | |
|---|---|
| [**Preprint (PDF)**](paper/Boundry_preprint_v1.0.2.pdf) | *Boundry: Model-Free Admission and Independently Verifiable Records for AI-Proposed Actions* (v1.0.2, Oct 2026). LaTeX source in [`paper/`](paper/) |
| [Claims and evidence](CLAIMS_AND_EVIDENCE.md) | Each claim, the evidence behind it, and its status |
| [Design boundaries and next stages](LIMITATIONS.md) | What the design leaves to other layers, and where each capability is in the rollout |
| [Related work](RELATED_WORK.md) | How Boundry relates to current research on agent guardrails, AI control and rules as code |
| [Development history](HISTORY.md) | How the ideas developed, from an accounting tool to a general substrate |
| [Essays](essays/) | Short pieces on the design ideas and the development method |
| [About](ABOUT.md) | Who is behind this, and how to get in touch |
| [Technical brief (PDF)](docs/Boundry_Technical_Brief_Oct2026.pdf) | Two-page overview |

## Citing this work

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.23129907.svg)](https://doi.org/10.5281/zenodo.23129907)

Mueller, B. (2026). *Boundry: Model-Free Admission and Independently Verifiable Records for AI-Proposed Actions*. Preprint v1.0.2. Zenodo. https://doi.org/10.5281/zenodo.23129907

This DOI always resolves to the latest version. See also [`CITATION.cff`](CITATION.cff).

## Intellectual property

The written material in this repository is shared under [CC BY 4.0](LICENSE). The Boundry software is proprietary. The methods described are the subject of Australian provisional patent applications (patent pending), and no patent licence is granted by this repository.

## Contact

Ben Mueller · verify@boundry.tech
