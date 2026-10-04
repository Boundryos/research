# Research directions

The preprint is about governing AI-proposed actions. These are the questions we think come next, and most of them reach beyond AI.

Each is stated as a question with a measurement that would answer it. We are looking for research partners on any of them: verify@boundry.tech.

### 1. How much backend logic can move?
**Question:** if a real application's request validation, authorisation, business rules and audit logic are re-expressed as declared rules that a deterministic kernel checks and records, how much bespoke code goes away? What happens to defect rates and audit effort?

**Measurement:** a migration study on a real codebase, measuring lines of code, defect classes, audit effort and latency.

### 2. What does governed execution cost?
**Question:** what is the per-request overhead in realistic workloads, and how does it compare with the cost of having a model carry out the same steps?

**Measurement:** a benchmark across request types and hardware, against model-driven execution of the same tasks.

### 3. How small can the verifying side be?
**Question:** can records be verified on phones, single-board computers and other modest hardware?

**Measurement:** run the public verifier on those devices and report time and memory.

### 4. Can governed systems work offline?
**Question:** what does governed execution look like where connectivity cannot be assumed?

**Measurement:** to be defined with partners in the relevant domains.

### 5. Supervisory control of physical systems
**Question:** fields such as aviation and robotics already bound complex controllers with simple, trusted monitors. Could the properties reported in the preprint be useful in supervisory control of physical systems?

**Measurement:** a study with partners in safety-critical domains.

### 6. Reproducible AI-agent research
**Question:** can agent experiments be run so that every step and every refusal is recorded and can be re-checked by another lab?

**Measurement:** a pilot replication between two groups.
