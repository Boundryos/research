# Boundry: research notes

**A small, deterministic kernel that admits or refuses AI-proposed actions, and leaves a record anyone can check.**

This repository collects the research notes, essays and evidence behind Boundry. It is written for researchers and practitioners working on AI safety, agent governance, verifiable computation and rules as code.

> **Status:** active research and development. Parts are in production; the full governing core is proven in testing. See [Claims and evidence](CLAIMS_AND_EVIDENCE.md) and [Limitations](LIMITATIONS.md).

---

## The idea in one paragraph

Most approaches to AI safety try to make the model behave. Boundry takes a different position: the harms we fear from AI agents are harms of **action** (records changed, money moved, systems operated), and the safety of an action does not have to live inside the model. In Boundry, an AI, a person or a program can only **propose** an action in a small declared language. A deterministic kernel, containing no model, **admits or refuses** each proposal against rules set by people. Anything not declared is refused, and the refusal is recorded with its reason. An admitted action is carried out from **exactly the same sealed bytes that were checked**, and every decision is sealed into a signed, hash-chained record that can be **verified offline by an independent verifier** sharing no code with the kernel.

## A familiar shape

The architecture follows a pattern with a long history: **a small, trusted kernel that checks untrusted proposals.** Proof assistants such as Lean and Coq work this way, in the tradition of Robin Milner's LCF approach from the 1970s. Anyone, including an AI, may propose a proof; a small kernel accepts or rejects it. Boundry applies that pattern to **actions, records and rules** rather than proofs. See [A proof-assistant kernel for actions](essays/01-a-proof-assistant-kernel-for-actions.md).

## Try it yourself

A read-only, offline verifier and sample records are public at **https://verify.boundry.tech**. The verifier re-derives every fingerprint and re-checks every seal and chain link on your own machine. It cannot execute, sign or write.

## Contents

| | |
|---|---|
| [Claims and evidence](CLAIMS_AND_EVIDENCE.md) | Each claim, the evidence behind it, and its status |
| [Limitations](LIMITATIONS.md) | What Boundry does not do, and what is not yet established |
| [Related work](RELATED_WORK.md) | How Boundry relates to current research on agent guardrails, AI control and rules as code |
| [Essays](essays/) | Short pieces on the design ideas and the development method |
| [About](ABOUT.md) | Who is behind this, and how to get in touch |
| [Technical brief (PDF)](docs/Boundry_Technical_Brief_Oct2026.pdf) | Two-page overview |

## Citing this work

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.23129908.svg)](https://doi.org/10.5281/zenodo.23129908)

Mueller, B. (2026). *Boundry: research notes on deterministic, verifiable governance of AI actions* (v0.1). Zenodo. https://doi.org/10.5281/zenodo.23129908

See also [`CITATION.cff`](CITATION.cff).

## Intellectual property

The written material in this repository is shared under [CC BY 4.0](LICENSE). The Boundry software is proprietary. The methods described are the subject of Australian provisional patent applications (patent pending), and no patent licence is granted by this repository.

## Contact

Ben Mueller · verify@boundry.tech
