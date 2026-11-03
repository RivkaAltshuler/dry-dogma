# dry-dogma
> **Escaping the DRY Dogma: Reactive Runtimes as Error-Correcting Protocols**
> 
> *"Redundancy is a feature, not a bug — in noisy, agent-based (and human) communication."*


## Motivation: From Agent Hallucinations to the Human-Machine Friction

The emergence of AI agents—systems that "think" in natural language and attempt to emit rigid, formal representations without error—sheds fresh light on a longstanding challenge in computer science: the inherent friction and frustration between human cognition and rigid software interfaces.

When an LLM agent hallucinates, emits contradictory constraints, or fails to satisfy strict schema requirements, it is not merely demonstrating an AI flaw. It is mirroring a fundamental cognitive reality: **natural communication relies on multiple, interchangeable, and often overlapping perspectives to convey intent**.

This dynamic exposes a fundamental divide between software engineering dogmas and natural communication practices:

* **Classical Software Dogma (DRY & SSOT):** For decades, foundational programming paradigms have treated redundancy as an architectural sin. Single Source of Truth (SSOT) and Don’t Repeat Yourself (DRY) dictate that every concept must have an isolated, non-overlapping representation. Overlapping declarations are treated as bugs, race conditions, or illegal states.
* **Natural & Human Practices:** In human collaboration—as well as in probabilistic agent reasoning—**redundancy is essential**. We naturally restate requirements from different angles, cross-reference figures, and verify mutual understanding through repetition and parity checks.

When formal software rejects redundancy, it forces the entire burden of precision and error prevention onto the human or the agent before execution even begins. If an agent or human introduces a slight cognitive misalignment, traditional runtimes either silently overwrite state or crash unpredictably.

**dry-dogma** challenges this convention: rather than forcing noisy, multi-perspective agents and humans into the mold of rigid, non-redundant state machines, we reframe the runtime itself as an **error-correcting channel** that treats intentional redundancy as a first-class reliability mechanism.

## Our Approach: From Historical Constraints to Error-Correcting Channels

### 1. DRY and Low Coupling as Tooling-Imposed Constraints
Principles such as DRY (*Don't Repeat Yourself*), code reuse, and loose coupling have long been treated as universal virtues. In practice, they originated as practical heuristics to address a human limitation: the difficulty of maintaining manual consistency across codebases. 

Developers minimize duplication primarily to ensure that modifications can be made safely in a single location without manual synchronization errors. In the absence of runtime mechanisms capable of synchronizing overlapping representations automatically, eliminating redundancy was the only viable strategy. When runtime tooling can maintain semantic consistency across representations, redundancy ceases to be a liability.

### 2. Human/Agent-Software Interaction as a Noisy Channel
Communication between natural-language systems (whether humans or generative AI agents) and formal software interfaces constitutes a **noisy communication channel** in the classic information-theoretic sense. 

In information theory, reliable transmission across a noisy medium requires intentional redundancy (such as parity bits and checksums) paired with an error-correcting protocol. Applying this principle to software architecture, intentional redundancy provides the overlapping signals necessary to detect misunderstandings, trace semantic drift, and guide automated recovery.

### 3. Intentional Redundancy as a Runtime Protocol
Instead of treating redundancy as duplicate data to be eliminated, we approach it as a first-class architectural protocol. By designing runtimes that can accept multiple, simultaneous declarations of state, we turn overlapping inputs into continuous parity checks. 

This shifts the responsibility of consistency from manual developer discipline or rigid user inputs to an automated runtime protocol—one capable of propagation, validation, and structured conflict resolution without crashing the execution environment.

## Enabling the Protocol: The RIVar Computational Model

To operationalize an error-correcting runtime without falling into the pitfalls of existing paradigms, we build upon the **RIVar** computational model:

* **Why not traditional Reactive Programming (FRP)?**  
  Conventional dataflow engines enforce strict Directed Acyclic Graphs (DAGs) and single-source updates[cite: 1]. Circular dependencies or competing inputs cause infinite loops or stream crashes. RIVar introduces *constructive assignment*, natively supporting cyclic, multi-directional dependencies and resolving them deterministically.
* **Why not classical Constraint Solvers?**  
  Traditional constraint satisfaction systems operate as monolithic, batch solvers that take over execution and obscure local state transitions. In contrast, RIVar operates over decentralized, event-driven streams, allowing flexible **merge policies** that negotiate conflicts directly with the user or agent in real time.

### The Three Operational Modes
When overlapping inputs are introduced through this model, the runtime behaves across three deterministic states[cite: 2]:
1. **Propagation (Partial Input):** Deriving missing state automatically[cite: 2].
2. **Parity Check (Consistent Redundancy):** Confirming mutual agreement across overlapping constraints[cite: 2].
3. **Structured Rejection (Conflict Isolation):** Trapping contradictions and returning actionable diagnostic feedback without breaking the active stream[cite: 2].

## Foundations

* **Published Research:** *Escaping the DAG Dogma: Toward Modular Reactive Architectures* (Rivka Altshuler & David H. Lorenz) — **ACM SIGPLAN SPLASH / Onward! 2026**.

  📄 [Paper on ACM Digital Library](https://doi.org/10.1145/3840586.3843206)

* **Core Engine Repositories:** [RIVarX Organization](https://github.com/RIVarX) (implementations in C#, TypeScript, and JavaScript).

