# 01 · A proof-assistant kernel for actions

*Ben Mueller · October 2026*

## A pattern mathematics already trusts

When a mathematician uses a proof assistant such as Lean or Coq, the trust does not rest on the person, or the tool, that produced the proof. Anyone can propose a proof: a student, an expert, a heuristic search, or today an AI model. What makes the result trustworthy is a small, deterministic **kernel** that checks every step against a fixed set of rules. It accepts the proof or rejects it, and a rejection says where and why.

The idea goes back to Robin Milner's LCF system in the 1970s. Its key insight was that a large, complicated, untrusted process can still produce trustworthy results, provided every result passes through a small trusted core that cannot be argued with. The kernel is not intelligent, and that is its strength: it cannot be persuaded, flattered or confused. It applies the rules.

This is also how AI is increasingly used in mathematics. The model proposes freely and creatively, often wrongly, and the kernel decides. Nobody asks the model to be trustworthy, only to be useful. The trust lives elsewhere.

## The same pattern, applied to actions

Boundry applies that architecture to a different object. Instead of proofs, it checks **actions**: changing a record, sending a message, moving money. Instead of logical inference rules, it checks against **rules set by people**: who may do what, to which data, under which conditions.

| | Proof assistant | Boundry |
|---|---|---|
| Who proposes | A person, a search, an AI | A person, a program, an AI |
| What is proposed | A proof | An action, in a small declared language |
| Who decides | A small deterministic kernel | A small deterministic kernel, with no model in it |
| Basis of the decision | The rules of logic | Rules declared by the people who run it |
| On failure | Rejection, with the reason | Refusal, with the reason, recorded |
| Result | A checked proof | A sealed, signed record that can be verified offline |

Two properties go beyond a typical proof checker, because actions have consequences that proofs do not:

1. **The action runs from the bytes that were checked.** There is no gap between what was approved and what was done.
2. **Every decision is recorded,** refusals included, in a tamper-evident chain that an independent verifier can re-check without trusting the operator.

## Why this framing matters for AI safety

Much AI-safety work asks how to make the model trustworthy. The proof-assistant tradition suggests a complementary question: **where should trust live?** For actions with real consequences, one answer is "in a small, inspectable kernel that the model cannot reach or persuade." The model can then be as creative as it likes, because nothing it proposes takes effect until a deterministic check admits it.

The trade-off is the same one proof assistants face. The kernel can only check what it has rules for. In Boundry, anything without a declared rule is refused rather than allowed. That is safe, but it means somebody has to write good rules. A kernel moves the trust problem to the rules, where it can be inspected and attributed to the people who wrote them. It does not make the problem disappear.

## Limits of the analogy

A proof kernel checks logical validity, which is absolute. Boundry checks conformance to declared rules, which are only as good as the people who wrote them. Lean's kernel is also far more mature and more heavily scrutinised. The analogy is about architecture, not about equal assurance.
