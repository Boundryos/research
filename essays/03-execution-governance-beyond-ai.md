# 03 · Beyond AI: governed computation

*Ben Mueller · October 2026 · discussion essay*

## The question

The [preprint](../paper/Boundry_preprint_v1.0.2.pdf) is about AI. A model proposes an action; a deterministic kernel that contains no model admits or refuses it; an admitted proposal runs from the sealed bytes that were checked; and anyone can verify the record afterwards.

Nothing in that arrangement needs the author to be a model. So the broader question is this: **if separating authorship from execution helps govern AI, should it apply to computation generally?**

## The untrusted author is older than AI

Every system that does consequential work acts on instructions from authors it cannot fully trust:

| Author | Typical failure |
|---|---|
| A person at a screen | Mistakes, overreach, a shared login |
| A script or scheduled job | Written for last year's assumptions |
| An integration from another system | Malformed input, a changed contract |
| An AI model | All of the above, at speed, with confident prose |

AI is the most capable and least predictable author so far. A mechanism built for the extreme case should, in principle, handle the ordinary ones too.

## Where the decision logic lives today

In a conventional backend, the logic that decides whether work may proceed is written by hand and scattered through the code:

> **Conventional:** request → validation logic → authorisation logic → business rules → audit logic → effect

The consequences are well documented:

- **It breaks often.** Broken access control is first in the OWASP Top 10 (2021), the category with the most occurrences in the applications contributors tested.[^owasp]
- **It is hard to recover.** Reconstructing the business rules buried in large legacy systems is a research field of its own.[^sneed]
- **It is hard to audit.** "Why was this allowed?" is answered by reading code and logs that the operator controls.

The industry has started to respond by pulling authorisation out of application code into small policy languages that a machine can analyse. Examples are Amazon's Cedar, built and checked with formal methods,[^cedar] and automated reasoning over AWS access policies, which is used in production at AWS.[^zelkova] Their lesson is that *rules are safer when they leave the code and become small, declared and checkable.*

## Moving the decision logic

Governed execution takes that lesson further, from individual permission checks to whole actions:

> **Governed:** request → admission → governed execution → record → effect

A system built this way could **move the decision logic of a conventional backend** into a small declared set that the kernel checks and records. That logic covers request validation, authorisation and tenant separation, business rules and the audit trail. Interfaces, integrations and storage stay ordinary code.

In large systems, decision logic is often where much of the complexity lives: rules engines, permission systems, workflow code and audit layers that have grown over years. If a substantial part of it can move into a small, declared, checked set, the gain is not marginal. There is less bespoke code to understand, test and secure, and every decision leaves a record. That is the proposition worth testing.

**How it differs from policy languages.** A policy language answers one question: may this principal do this action on this resource? Governed execution goes further:

- It admits a *whole plan*.
- It executes exactly the bytes it admitted.
- It records the decision, including refusals, in a form a stranger can verify.

A Cedar-style policy could be one of the rules the kernel applies.

## What would change, if it works

- **The audit trail exists by construction.** It is produced by the same path that made the decision, not added afterwards.
- **"Why was this allowed?" has a recorded answer.** The answer binds together the rule, who requested the action and the proposal.
- **"Why was this refused?" has one too.** Most systems record what happened and discard what was stopped.
- **Rules become artefacts.** They can be inspected and attributed to the people who wrote them.
- **Results can be compared by hash.** A record can be checked without re-running the system or trusting its operator.

## What is not yet established

- **How much code it removes.** How much real governing logic can move, and how much code that removes, has not been measured. This is the most important experiment.
- **Overhead.** The overhead in high-volume workloads has not been measured.
- **Where the boundary sits.** The declared language is deliberately bounded to finite, loop-free plans over registered operations, and someone must write and register each operation. Where that boundary sits for general business logic is still open.
- **Live use so far.** Boundry's live uses so far are of its record layer, in a bookkeeping application and a financial reconciliation application. The full governed-execution path has been demonstrated on a test bench.

## Neighbours

- **Database integrity constraints and stored procedures:** declared rules enforced at the point of change.
- **Workflow engines:** declared processes with execution histories.
- **Event sourcing:** state rebuilt from an append-only log of events.[^fowler]
- **Smart contracts:** deterministic execution with a verifiable record, agreed by consensus among many parties.
- **Rules as code (Catala) and policy as code (Cedar, Rego):** declared rules as the authority.
- **Reference monitors:** complete mediation of access.[^saltzer]

The proposition here is the *combination*: a declared proposal, a deterministic admission that can refuse, execution of exactly what was admitted, and a record that a stranger can verify offline. It applies whoever the author is.

## An invitation

The simplest test is to take a real backend's governing logic, re-express it as declared, governed execution, and measure what changes: lines of code, defect classes, audit effort and latency. I would gladly run that study with a research partner.

*See also [Research directions](../RESEARCH_DIRECTIONS.md).*

---

[^owasp]: OWASP Top 10:2021, A01 Broken Access Control. https://owasp.org/Top10/A01_2021-Broken_Access_Control/
[^sneed]: H. M. Sneed and C. Verhoef, "From COBOL to Business Rules — Extracting Business Rules from Legacy Code," Springer, 2020. doi:10.1007/978-3-030-26574-8_14
[^cedar]: J. W. Cutler et al., "Cedar: A New Language for Expressive, Fast, Safe, and Analyzable Authorization," OOPSLA 2024. arXiv:2403.04651
[^zelkova]: J. Backes et al., "Semantic-based Automated Reasoning for AWS Access Policies using SMT," FMCAD 2018. doi:10.23919/FMCAD.2018.8602994
[^fowler]: M. Fowler, "Event Sourcing," 2005. https://martinfowler.com/eaaDev/EventSourcing.html
[^saltzer]: J. H. Saltzer and M. D. Schroeder, "The Protection of Information in Computer Systems," Proc. IEEE 63(9), 1975.
