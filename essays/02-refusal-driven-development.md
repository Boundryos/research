# 02 · Refusal-driven development: building a system by challenging it

*Ben Mueller · October 2026 · an experience report*

## How Boundry was built

Boundry was not designed from a body of prior research. I came to the literature afterwards, and found that much of it converges on the same ideas. Instead, the design emerged from a working method: AI agents proposed changes, and a deterministic substrate with fixed rules either admitted them or refused them with a stated reason.

In practice, the development was organised as a set of AI agent roles: an architect, a governance role, a build role and an operations role. They were coordinated by me and constrained by written rules. Proposed changes had to pass the substrate's own checks: canonical forms, invariants, reproducibility gates and test suites, with thousands of tests and rehearsals run before a change was admitted. Changes that failed were refused, and the refusal was recorded.

## What the refusals did

The most useful moments came when a proposal *failed*. A refused change exposes an assumption that turned out to be wrong: an ambiguous byte format, an undeclared dependency on the machine's environment, a value that could be rendered two ways, or a claim that the record could not support. Each refusal became a design decision, and many of the system's primitives exist because some earlier proposal was refused for lacking them.

The checks applied to the AI agents' own statements as well as their code. On one occasion a governance statement made by one of the AI roles about the system's history was refused, because the record did not support it, and it was corrected on the record. The rules applied equally to everyone, including the agents building the system.

## Reproducibility as the hardest test

The clearest example is reproducibility. A system that claims to be deterministic should produce identical results on a different machine. Getting there meant repeatedly proposing that the build was reproducible, having the check refuse it, finding the hidden source of variation (environment, ordering, encoding), declaring it, and trying again. The end result was that the software was rebuilt on a second, different machine from sealed bundles and matched the first **byte for byte**.

## What I think this shows, and what it doesn't

**What it shows:** a deterministic referee that records every proposal, including refusals, is a productive partner for AI-assisted engineering. The AI supplies breadth and speed. The referee supplies discipline and a reliable memory of what was tried and why it failed. The pattern is the proof-assistant one described in [Essay 01](01-a-proof-assistant-kernel-for-actions.md), applied to building the system itself.

**What it doesn't show:**
- that the method is better than conventional engineering in general;
- that the resulting system is free of defects;
- that this one programme generalises.

It is one experience report, from one builder. It does suggest a hypothesis worth testing more widely: **that refusal-driven development with a deterministic, recording referee could serve as a research tool**, for building systems and for running AI-agent experiments whose every step must be reproducible and tamper-evident.

I'd welcome researchers who want to test that hypothesis.
